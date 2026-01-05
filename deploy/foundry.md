# Foundry

[Foundry](https://book.getfoundry.sh/) is a blazing-fast, portable, and modular toolkit for Ethereum application development. This guide shows you how to deploy smart contracts to LitVM using Foundry.

## Prerequisites

* [Foundry installed](https://book.getfoundry.sh/getting-started/installation)
* A wallet with testnet zkLTC (see Add to Your Wallet)
* Basic familiarity with Solidity

***

## Install Foundry

If you haven't installed Foundry yet:

```bash
# Install foundryup
curl -L https://foundry.paradigm.xyz | bash

# Install Foundry
foundryup
```

Verify installation:

```bash
forge --version
```

***

## Create a New Project

```bash
# Create new project
forge init my-litvm-project

# Navigate to project
cd my-litvm-project
```

This creates a project structure:

```
my-litvm-project/
├── lib/ # Dependencies
├── script/ # Deployment scripts
├── src/ # Contracts
├── test/ # Tests
└── foundry.toml  # Configuration
```

***

## Write Your Contract

Create a simple contract in `src/Counter.sol`:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.19;

contract Counter {
    uint256 public count;
    event CountChanged(uint256 newCount);

    function increment() public {
        count += 1;
        emit CountChanged(count);
    }

    function decrement() public {
        require(count > 0, "Count cannot go below zero");
        count -= 1;
        emit CountChanged(count);
    }

    function setCount(uint256 _count) public {
        count = _count;
        emit CountChanged(count);
    }
}
```

***

## Configure for LitVM

Update `foundry.toml` to include LitVM network:

```toml
[profile.default]
src = "src"
out = "out"
libs = ["lib"]
solc = "0.8.19"

[rpc_endpoints]
litvm_testnet = "RPC_URL"
litvm_mainnet = "RPC_URL"

[explorer]
litvm_testnet = { key = "${LITVM_EXPLORER_API_KEY}", url = "EXPLORER_URL/api"}
```

***

## Set Up Environment

Create a `.env` file (add to `.gitignore`!):

```bash
# .env
PRIVATE_KEY=your_private_key_here
LITVM_RPC_URL=RPC_URL
```

Load environment variables:

```bash
source .env
```

***

## Compile

```bash
forge build
```

Expected output:

```
[⠊] Compiling...
[⠒] Compiling 1 files with 0.8.19
[⠑] Solc 0.8.19 finished in 1.23s
Compiler run successful!
```

***

## Test

Run tests before deploying:

```bash
forge test
```

Add a test in `test/Counter.t.sol`:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.19;
import {Test, console} from "forge-std/Test.sol";
import {Counter} from "../src/Counter.sol";

contract CounterTest is Test {
    Counter public counter;

    function setUp() public {
        counter = new Counter();
    }

    function test_Increment() public {
        counter.increment();
        assertEq(counter.count(), 1);
    }

    function test_Decrement() public {
        counter.increment();
        counter.decrement();
        assertEq(counter.count(), 0);
    }

    function test_SetCount() public {
        counter.setCount(100);
        assertEq(counter.count(), 100);
    }

    function testFail_DecrementBelowZero() public {
        counter.decrement(); // Should fail
    }
}
```

Run with verbosity:

```bash
forge test -vvv
```

***

## Deploy

{% stepper %}
{% step %}
#### Direct deploy

Use forge create with your RPC and private key:

```bash
forge create --rpc-url $LITVM_RPC_URL \
  --private-key $PRIVATE_KEY \
  src/Counter.sol:Counter
```
{% endstep %}

{% step %}
#### Deploy script (Recommended)

Create `script/Deploy.s.sol`:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.19;
import {Script, console} from "forge-std/Script.sol";
import {Counter} from "../src/Counter.sol";

contract DeployCounter is Script {
    function run() public {
        uint256 deployerPrivateKey = vm.envUint("PRIVATE_KEY");
        vm.startBroadcast(deployerPrivateKey);
        Counter counter = new Counter();
        console.log("Counter deployed to:", address(counter));
        vm.stopBroadcast();
    }
}
```

Run the script:

```bash
forge script script/Deploy.s.sol:DeployCounter \
  --rpc-url $LITVM_RPC_URL \
  --broadcast
```
{% endstep %}
{% endstepper %}

***

## Verify Contract

Verify on LitVM Explorer:

```bash
forge verify-contract \
  --chain-id [LITVM_CHAIN_ID] \
  --compiler-version v0.8.19 \
  --watch \
  [DEPLOYED_CONTRACT_ADDRESS] \
  src/Counter.sol:Counter \
  --explorer-api-key $LITVM_EXPLORER_API_KEY \
  --verifier-url EXPLORER_URL
```

***

## Interact with Contract

### Using cast

```bash
# Read count
cast call [CONTRACT_ADDRESS] "count()" --rpc-url $LITVM_RPC_URL

# Increment
cast send [CONTRACT_ADDRESS] "increment()" \
  --rpc-url $LITVM_RPC_URL \
  --private-key $PRIVATE_KEY

# Set count to 42
cast send [CONTRACT_ADDRESS] "setCount(uint256)" 42 \
  --rpc-url $LITVM_RPC_URL \
  --private-key $PRIVATE_KEY
```

### Using Forge Script

Create `script/Interact.s.sol`:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.19;
import {Script, console} from "forge-std/Script.sol";
import {Counter} from "../src/Counter.sol";

contract InteractCounter is Script {
    function run() public {
        uint256 deployerPrivateKey = vm.envUint("PRIVATE_KEY");
        address counterAddress = vm.envAddress("COUNTER_ADDRESS");
        Counter counter = Counter(counterAddress);
        vm.startBroadcast(deployerPrivateKey);
        // Increment 3 times
        counter.increment();
        counter.increment();
        counter.increment();
        console.log("New count:", counter.count());
        vm.stopBroadcast();
    }
}
```

***

## Gas Estimation

Check gas costs before deploying:

```bash
# Estimate deployment gas
forge create --rpc-url $LITVM_RPC_URL \
  src/Counter.sol:Counter \
  --estimate
```

***

## Common Issues

<details>

<summary>"Insufficient funds"</summary>

Ensure your wallet has testnet zkLTC. Visit the faucet.

</details>

<details>

<summary>"Nonce too low"</summary>

Reset nonce or wait for pending transactions to confirm:

```bash
cast nonce [YOUR_ADDRESS] --rpc-url $LITVM_RPC_URL
```

</details>

<details>

<summary>"RPC error"</summary>

* Check RPC URL is correct
* Verify network connectivity
* Try alternative RPC endpoints

</details>

***

## Next Steps

* Deploy more complex contracts (ERC-20, ERC-721, etc.)
* Set up Hardhat for alternative tooling
* Explore LitVM ecosystem dApps

***

## Resources

* [Foundry Book](https://book.getfoundry.sh/)
* [Foundry GitHub](https://github.com/foundry-rs/foundry)
* LitVM Block Explorer (coming soon)
