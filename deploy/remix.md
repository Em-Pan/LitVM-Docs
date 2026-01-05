# remix

[Remix IDE](https://remix.ethereum.org/) is a browser-based development environment that requires no setup. It's perfect for quick prototyping, learning, and deploying simple contracts to LitVM.

## Prerequisites

* A modern web browser (Chrome, Firefox, Brave)
* MetaMask or another Web3 wallet installed
* Testnet zkLTC in your wallet (see Add to Your Wallet)

***

## Access Remix

{% stepper %}
{% step %}
Open Remix

1. Open [remix.ethereum.org](https://remix.ethereum.org/) in your browser
2. You'll see the Remix IDE with a default workspace
{% endstep %}
{% endstepper %}

***

## Create Your Contract

{% stepper %}
{% step %}
Create a New File

* In the File Explorer panel (left sidebar), click the 📄 icon to create a new file
* Name it Counter.sol
{% endstep %}

{% step %}
Write the Contract

Paste this code into Counter.sol:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.19;
contract Counter {
uint256 public count;
event CountChanged(uint256 new Count);
constructor(uint256_initialCount){
count = _initialCount;
}
function increment() public {
count += 1;
emit CountChanged(count);
}
function decrement() public {
require(count > 0, "Count cannot go below zero");
count -= 1;
emit CountChanged(count);
}
functiongetCount() publicviewreturns(uint256){
returncount;
}
}

```
{% endstep %}
{% endstepper %}

***

## Compile the Contract

{% stepper %}
{% step %}
Open Compiler

* Click the **Solidity Compiler** icon in the left sidebar (looks like "S")
{% endstep %}

{% step %}
Configure Compiler

* **Compiler Version** : Select 0.8.19 (or match your pragma)
* **EVM Version** : Leave as default or select shanghai
* Enable **Auto compile** for convenience
{% endstep %}

{% step %}
Compile

1. Click **Compile Counter.sol**
2. A green checkmark appears when successful
3. You'll see "Counter" in the CONTRACT dropdown
{% endstep %}
{% endstepper %}

***

## Connect to LitVM

{% stepper %}
{% step %}
Configure MetaMask

Ensure LitVM Testnet is added to your wallet:

| **Setting**     | **Value**                                                                                                     |
| --------------- | ------------------------------------------------------------------------------------------------------------- |
| Network Name    | LitVM Testnet                                                                                                 |
| RPC URL         | ⚠️ **⚠️ TBA — This value will be published closer to launch** — This value will be published closer to launch |
| Chain ID        | ⚠️ **⚠️ TBA — This value will be published closer to launch** — This value will be published closer to launch |
| Currency Symbol | zkLTC                                                                                                         |
{% endstep %}

{% step %}
Select Network in Remix

1. Click the **Deploy & Run** icon in the left sidebar (arrow icon)
2. In the **ENVIRONMENT** dropdown, select **Injected Provider - MetaMask**
3. MetaMask will popup—select **LitVM Testnet** and connect
{% endstep %}

{% step %}
Verify Connection

* You should see your wallet address under **ACCOUNT**
* Your zkLTC balance will be displayed
* The network should show the LitVM Chain ID
{% endstep %}
{% endstepper %}

***

## Deploy the Contract

{% stepper %}
{% step %}
Configure Deployment

1. In the **CONTRACT** dropdown, select Counter
2. In the field next to **Deploy**, enter the initial count (e.g., 0)
{% endstep %}

{% step %}
Deploy

1. Click **Deploy**
2. MetaMask will popup with the transaction
3. Review gas fees (paid in zkLTC)
4. Click **Confirm**
{% endstep %}

{% step %}
Wait for Confirmation

* Watch the Remix terminal for deployment status
* Once confirmed, your contract appears under **Deployed Contracts**
{% endstep %}
{% endstepper %}

***

## Interact with Your Contract

### Read Functions (Free)

Under **Deployed Contracts**, expand your contract to see available functions:

* **count** : Click to read the current count value
* **getCount** : Alternative read function

### Write Functions (Costs Gas)

* **increment** : Click to add 1 to the count
* **decrement** : Click to subtract 1 from the count

Each write function triggers a MetaMask transaction popup.

### Example Interaction

{% stepper %}
{% step %}
1. Click "count" → Shows: 0
{% endstep %}

{% step %}
2. Click "increment" → Confirm in MetaMask
{% endstep %}

{% step %}
3. Click "count" → Shows: 1
{% endstep %}

{% step %}
4. Click "increment" → Confirm in MetaMask
{% endstep %}

{% step %}
5. Click "count" → Shows: 2
{% endstep %}
{% endstepper %}

***

## View on Block Explorer

1. After deploying, copy the contract address from **Deployed Contracts**
2. Visit LitVM Explorer (Coming Soon)
3. Paste your contract address in the search bar
4. View transactions, events, and contract code

***

## Verify Your Contract

{% stepper %}
{% step %}
Open Verification Plugin

1. In Remix, go to **Plugin Manager** (plug icon in left sidebar)
2. Search for "Contract Verification"
3. Click **Activate**
{% endstep %}

{% step %}
Verify

1. Open the verification plugin
2. Select **LitVM Testnet** as the chain
3. Enter your contract address
4. Select the contract file and compiler version
5. Enter constructor arguments (e.g., 0)
6. Click **Verify**
{% endstep %}
{% endstepper %}

***

## Deploy an ERC-20 Token

{% stepper %}
{% step %}
Install OpenZeppelin

1. In Remix, go to **Plugin Manager**
2. Search for and activate **DGIT** or **Remixd** for GitHub imports
{% endstep %}

{% step %}
Create Token Contract

Create MyToken.sol:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.19;
import"@openzeppelin/contracts/token/ERC20/ERC20.sol";
contractMyTokenisERC20{
constructor(uint256initialSupply)ERC20("MyToken","MTK"){
_mint(msg.sender, initialSupply*10**decimals());
}
}
```
{% endstep %}

{% step %}
Compile and Deploy

1. Compile with Solidity 0.8.19
2. Deploy with initial supply (e.g., 1000000 for 1M tokens)
3. Your wallet will receive all tokens
{% endstep %}
{% endstepper %}

***

## Tips for Using Remix

### Save Your Work

* Remix stores files in browser storage
* For important work, use **GitHub** integration or download files

### Use Workspaces

* Create separate workspaces for different projects
* Click the hamburger menu in File Explorer → **Create Workspace**

### Debug Transactions

1. Go to **Debugger** plugin
2. Enter a transaction hash
3. Step through execution to find issues

### Gas Estimation

* Before deploying, Remix shows estimated gas
* Ensure you have enough zkLTC

***

## Common Issues

<details>

<summary>"Transaction reverted"</summary>

* Check error message in Remix console
* Ensure you're passing correct parameters
* Verify you have sufficient zkLTC

</details>

<details>

<summary>"MetaMask not connecting"</summary>

* Refresh the page
* Ensure you're on LitVM Testnet in MetaMask
* Try disconnecting and reconnecting

</details>

<details>

<summary>"Contract not verified"</summary>

* Ensure compiler version matches exactly
* Check constructor arguments are correct
* Try flattening your contract first

</details>

<details>

<summary>"Invalid opcode"</summary>

* Your EVM version might not match
* Try selecting a different EVM version in compiler

</details>

***

## Deploy to Mainnet

When LitVM mainnet launches:

1. Switch MetaMask to **LitVM Mainnet**
2. Ensure you have mainnet zkLTC
3. Follow the same deployment process
4. Be extra careful—mainnet deployments are permanent!

***

## Next Steps

* Try deploying an NFT contract
* Learn Foundry for local development
* Set up Hardhat for larger projects
* Explore verified contracts on LitVM Explorer

***

## Resources

* [Remix Documentation](https://remix-ide.readthedocs.io/)
* [Remix GitHub](https://github.com/ethereum/remix-project)
* [OpenZeppelin Wizard](https://wizard.openzeppelin.com/) - Generate token contracts
* [Solidity Documentation](https://docs.soliditylang.org/)
