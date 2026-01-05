# hardhat

[Hardhat](https://hardhat.org/) is a popular Ethereum development environment that provides a flexible and extensible framework for building smart contracts. This guide shows you how to deploy to LitVM using Hardhat.

## Prerequisites

* [Node.js](https://nodejs.org/) v18 or later
* npm or yarn
* A wallet with testnet zkLTC (see Add to Your Wallet)
* Basic familiarity with JavaScript/TypeScript and Solidity

***

## Create a New Project

```bash
# Create project directory
mkdir my-litvm-hardhat
cd my-litvm-hardhat

# Initialize npm
npm init -y

# Install Hardhat
npm install --save-dev hardhat

# Create Hardhat project
npx hardhat init
```

Select "Create a JavaScript project" (or TypeScript) and follow the prompts.

***

## Install Dependencies

```bash
npm install --save-dev @nomicfoundation/hardhat-toolbox dotenv
```

***

## Configure for LitVM

Update hardhat.config.js:

```javascript
require("@nomicfoundation/hardhat-toolbox");
require("dotenv").config();
const PRIVATE_KEY = process.env.PRIVATE_KEY || "";
/** @type import('hardhat/config').HardhatUserConfig */
module.exports = {
  solidity: {
    version: "0.8.19",
    settings: {
      optimizer: {
        enabled: true,
        runs: 200,
      },
    },
  },
  networks: {
    litvm_testnet: {
      url: "RPC_URL",
      chainId: 0, // Replace with actual Chain ID when available
      accounts: PRIVATE_KEY ? [PRIVATE_KEY] : [],
      gasPrice: "auto",
    },
    litvm_mainnet: {
      url: "RPC_URL",
      chainId: 0, // Replace with actual Chain ID when available
      accounts: PRIVATE_KEY ? [PRIVATE_KEY] : [],
      gasPrice: "auto",
    },
  },
  etherscan: {
    apiKey: {
      litvm_testnet: process.env.LITVM_EXPLORER_API_KEY || "",
    },
    customChains: [
      {
        network: "litvm_testnet",
        chainId: 0, // Replace with actual Chain ID
        urls: {
          apiURL: "EXPLORER_URL/api",
          browserURL: "EXPLORER_URL",
        },
      },
    ],
  },
};
```

***

## Set Up Environment

Create a .env file (add to .gitignore!):

```bash
# .env
PRIVATE_KEY=your_private_key_here
LITVM_EXPLORER_API_KEY=your_api_key_here
```

***

## Write Your Contract

Create contracts/Counter.sol:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.19;

contract Counter {
    uint256 public count;
    address public owner;

    event CountChanged(uint256 newCount, address changedBy);
    event OwnershipTransferred(address indexed previousOwner, address indexed newOwner);

    modifier onlyOwner() {
        require(msg.sender == owner, "Not the owner");
        _;
    }

    constructor(uint256 _initialCount) {
        count = _initialCount;
        owner = msg.sender;
    }

    function increment() public {
        count += 1;
        emit CountChanged(count, msg.sender);
    }

    function decrement() public {
        require(count > 0, "Count cannot go below zero");
        count -= 1;
        emit CountChanged(count, msg.sender);
    }

    function setCount(uint256 _count) public onlyOwner {
        count = _count;
        emit CountChanged(count, msg.sender);
    }

    function transferOwnership(address newOwner) public onlyOwner {
        require(newOwner != address(0), "Invalid address");
        emit OwnershipTransferred(owner, newOwner);
        owner = newOwner;
    }
}
```

***

## Compile

```bash
npx hardhat compile
```

Expected output:

```
Compiled 1 Solidity file successfully
```

***

## Test

Create test/Counter.js:

```javascript
const { expect } = require("chai");
const { ethers } = require("hardhat");

describe("Counter", function () {
  let counter;
  let owner;
  let addr1;

  beforeEach(async function () {
    [owner, addr1] = await ethers.getSigners();
    const Counter = await ethers.getContractFactory("Counter");
    counter = await Counter.deploy(0);
    await counter.waitForDeployment();
  });

  describe("Deployment", function () {
    it("Should set the initial count", async function () {
      expect(await counter.count()).to.equal(0);
    });

    it("Should set the owner", async function () {
      expect(await counter.owner()).to.equal(owner.address);
    });
  });

  describe("Increment", function () {
    it("Should increment the count", async function () {
      await counter.increment();
      expect(await counter.count()).to.equal(1);
    });

    it("Should emit CountChanged event", async function () {
      await expect(counter.increment())
        .to.emit(counter, "CountChanged")
        .withArgs(1, owner.address);
    });
  });

  describe("Decrement", function () {
    it("Should decrement the count", async function () {
      await counter.increment();
      await counter.decrement();
      expect(await counter.count()).to.equal(0);
    });

    it("Should revert when count is zero", async function () {
      await expect(counter.decrement()).to.be.revertedWith(
        "Count cannot go below zero"
      );
    });
  });

  describe("SetCount", function () {
    it("Should allow owner to set count", async function () {
      await counter.setCount(100);
      expect(await counter.count()).to.equal(100);
    });

    it("Should revert when non-owner tries to set count", async function () {
      await expect(counter.connect(addr1).setCount(100)).to.be.revertedWith(
        "Not the owner"
      );
    });
  });
});
```

Run tests:

```bash
npx hardhat test
```

***

## Deploy

Create scripts/deploy.js:

```javascript
const hre = require("hardhat");

async function main() {
  const initialCount = 0;
  console.log("Deploying Counter contract...");
  const Counter = await hre.ethers.getContractFactory("Counter");
  const counter = await Counter.deploy(initialCount);
  await counter.waitForDeployment();
  const address = await counter.getAddress();
  console.log(`Counter deployed to: ${address}`);
  console.log(`Initial count: ${initialCount}`);
  console.log(`Network: ${hre.network.name}`);
  // Wait for a few block confirmations
  console.log("Waiting for block confirmations...");
  await counter.deploymentTransaction().wait(5);
  console.log("Confirmed!");
  return address;
}

main()
  .then(() => process.exit(0))
  .catch((error) => {
    console.error(error);
    process.exit(1);
  });
```

Deploy to LitVM testnet:

```bash
npx hardhat run scripts/deploy.js --network litvm_testnet
```

***

## Verify Contract

```bash
npx hardhat verify --network litvm_testnet [CONTRACT_ADDRESS] 0
```

The final `0` is the constructor argument (initial count).

***

## Interact with Contract

Create scripts/interact.js:

```javascript
const hre = require("hardhat");

async function main() {
  // Replace with your deployed contract address
  const contractAddress = "0x...";
  const Counter = await hre.ethers.getContractFactory("Counter");
  const counter = Counter.attach(contractAddress);

  // Read current count
  const currentCount = await counter.count();
  console.log(`Current count: ${currentCount}`);

  // Increment
  console.log("Incrementing...");
  const tx = await counter.increment();
  await tx.wait();

  // Read new count
  const newCount = await counter.count();
  console.log(`New count: ${newCount}`);
}

main()
  .then(() => process.exit(0))
  .catch((error) => {
    console.error(error);
    process.exit(1);
  });
```

Run:

```bash
npx hardhat run scripts/interact.js --network litvm_testnet
```

***

## Using Hardhat Console

Interactive testing:

```bash
npx hardhat console --network litvm_testnet
```

Then in the console:

```javascript
> const Counter = await ethers.getContractFactory("Counter")
> const counter = Counter.attach("0x...")
> await counter.count()
> await counter.increment()
> await counter.count()
```

***

## Gas Reporting

Install gas reporter:

```bash
npm install --save-dev hardhat-gas-reporter
```

Add to hardhat.config.js:

```javascript
require("hardhat-gas-reporter");
module.exports = {
  // ... other config
  gasReporter: {
    enabled: true,
    currency: "USD",
  },
};
```

Run tests to see gas usage:

```bash
REPORT_GAS=true npx hardhat test
```

***

## Common Issues

<details>

<summary>"Insufficient funds for gas"</summary>

Get testnet zkLTC from the faucet.

</details>

<details>

<summary>"Network not configured"</summary>

Ensure litvm\_testnet is in your hardhat.config.js networks.

</details>

<details>

<summary>"Invalid chainId"</summary>

Update the chainId in config once official values are released.

</details>

<details>

<summary>"Nonce too high"</summary>

Reset your account nonce in MetaMask or wait for pending transactions.

</details>

***

## TypeScript Support

For TypeScript projects, create hardhat.config.ts:

```typescript
import { HardhatUserConfig } from "hardhat/config";
import "@nomicfoundation/hardhat-toolbox";
import * as dotenv from "dotenv";
dotenv.config();

const config: HardhatUserConfig = {
  solidity: "0.8.19",
  networks: {
    litvm_testnet: {
      url: "RPC_URL",
      accounts: process.env.PRIVATE_KEY ? [process.env.PRIVATE_KEY] : [],
    },
  },
};

export default config;
```

***

## Next Steps

* Deploy ERC-20 or ERC-721 tokens
* Set up Foundry for faster compilation
* Try Remix for browser-based development
* Explore the LitVM ecosystem

***

## Resources

* [Hardhat Documentation](https://hardhat.org/docs)
* [Hardhat GitHub](https://github.com/NomicFoundation/hardhat)
* [OpenZeppelin Contracts](https://docs.openzeppelin.com/contracts)
