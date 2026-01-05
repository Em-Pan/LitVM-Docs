# add to wallet

Connect your Web3 wallet to the LitVM network to start interacting with dApps, bridging assets, and deploying smart contracts.

## Supported Wallets

LitVM is EVM-compatible and works with any Ethereum wallet:

* **MetaMask**
* **Rabby Wallet**
* **Coinbase Wallet**
* **Trust Wallet**
* **Rainbow**
* **OKX Wallet**
* **Any WalletConnect-compatible wallet**

***

## Quick Add (Recommended)

The easiest way to add LitVM is through our network configuration page:

{% stepper %}
{% step %}
### One-Click Add

* Visit the LitVM Network Hub (coming soon)
* Click **"Add to Wallet"**
* Approve the network addition in your wallet
* Done! You're connected to LitVM
{% endstep %}

{% step %}
### ChainList

* Go to [ChainList.org](https://chainlist.org/)
* Search for "LitVM"
* Click **"Add to MetaMask"** (or your wallet)
* Approve the network addition
{% endstep %}
{% endstepper %}

***

## Manual Configuration

If automatic methods don't work, add the network manually using these parameters:

### LitVM Testnet

| **Parameter**          | **Value**                                                                                                     |
| ---------------------- | ------------------------------------------------------------------------------------------------------------- |
| **Network Name**       | LitVM Testnet                                                                                                 |
| **RPC URL**            | ⚠️ **⚠️ TBA — This value will be published closer to launch** — This value will be published closer to launch |
| **Chain ID**           | ⚠️ **⚠️ TBA — This value will be published closer to launch** — This value will be published closer to launch |
| **Currency Symbol**    | zkLTC                                                                                                         |
| **Block Explorer URL** | ⚠️ **⚠️ TBA — This value will be published closer to launch** — This value will be published closer to launch |

⚠️ **Note**: Testnet parameters will be confirmed at launch (Q1 2026). Check our official channels for the latest details.

### LitVM Mainnet(Coming Soon)

| **Parameter**          | **Value**                                                                                                     |
| ---------------------- | ------------------------------------------------------------------------------------------------------------- |
| **Network Name**       | LitVM                                                                                                         |
| **RPC URL**            | ⚠️ **⚠️ TBA — This value will be published closer to launch** — This value will be published closer to launch |
| **Chain ID**           | ⚠️ **⚠️ TBA — This value will be published closer to launch** — This value will be published closer to launch |
| **Currency Symbol**    | zkLTC                                                                                                         |
| **Block Explorer URL** | ⚠️ **⚠️ TBA — This value will be published closer to launch** — This value will be published closer to launch |

***

## MetaMask

### Adding the Network

{% stepper %}
{% step %}
### Open MetaMask

* Open MetaMask and click the network dropdown at the top
{% endstep %}

{% step %}
### Add Network

* Click **"Add Network"** at the bottom of the list
* Select **"Add a network manually"**
{% endstep %}

{% step %}
### Enter Network Details

Enter the network details:

* Network Name: LitVM Testnet
* New RPC URL: ⚠️ **⚠️ TBA — This value will be published closer to launch** — This value will be published closer to launch
* Chain ID: ⚠️ **⚠️ TBA — This value will be published closer to launch** — This value will be published closer to launch
* Currency Symbol: zkLTC
* Block Explorer URL: ⚠️ **⚠️ TBA — This value will be published closer to launch** — This value will be published closer to launch
{% endstep %}

{% step %}
### Save and Switch

* Click **"Save"**
* Switch to the network by selecting **LitVM Testnet** from the dropdown
{% endstep %}
{% endstepper %}

### Verifying Connection

Once connected, you should see:

* "LitVM Testnet" in your network dropdown
* "zkLTC" as your native currency
* Your balance displayed (0 zkLTC initially)

***

## Rabby Wallet

{% stepper %}
{% step %}
### Open Rabby

* Open Rabby and go to Settings
{% endstep %}

{% step %}
### Add Custom Network

* Click **"Custom Networks"** → **"Add Network"**
{% endstep %}

{% step %}
### Enter Network Details

* Enter the LitVM network details (same as in Manual Configuration)
{% endstep %}

{% step %}
### Save and Switch

* Save and switch to the LitVM network
{% endstep %}
{% endstepper %}

***

## Mobile Wallets

### Trust Wallet

{% stepper %}
{% step %}
Open Trust Wallet and tap the **Settings** icon
{% endstep %}

{% step %}
Select **Network** → **Add Custom Network**, enter LitVM network parameters, then tap **Save**
{% endstep %}
{% endstepper %}

### Coinbase Wallet

{% stepper %}
{% step %}
Open Coinbase Wallet and go to **Settings** → **Networks**
{% endstep %}

{% step %}
Tap **Add Network**, enter LitVM network parameters, then tap **Add**
{% endstep %}
{% endstepper %}

***

## Getting Testnet zkLTC

After connecting your wallet, you'll need testnet zkLTC for gas:

{% stepper %}
{% step %}
### Testnet Faucet

* Visit the LitVM Testnet Faucet (coming soon)
* Connect your wallet
* Request testnet zkLTC
* Tokens will arrive in \~30 seconds
{% endstep %}

{% step %}
### Bridge from Testnet LTC

* Acquire testnet LTC from a Litecoin testnet faucet
* Use the LitVM Bridge to convert to zkLTC
* zkLTC will appear in your wallet
{% endstep %}
{% endstepper %}

***

## Troubleshooting

<details>

<summary>"Network not found" Error</summary>

* Double-check all network parameters (especially Chain ID)
* Ensure there are no extra spaces in URLs
* Try clearing your wallet cache and re-adding

</details>

<details>

<summary>Transaction Stuck</summary>

* LitVM uses zkLTC for gas—ensure you have a balance
* Try increasing the gas limit
* Reset your wallet's transaction nonce if needed

</details>

<details>

<summary>Wrong Network</summary>

* Check that you're on "LitVM Testnet" not mainnet (or vice versa)
* Verify the Chain ID matches your intended network

</details>

<details>

<summary>RPC Connection Issues</summary>

* Try an alternative RPC endpoint
* Some corporate firewalls block RPC connections
* VPN may help in certain regions

</details>

***

## Security Tips

1. **Verify URLs** : Always double-check RPC and explorer URLs match official sources
2. **Test First** : Send a small amount before large transfers
3. **Bookmark Official Sites** : Avoid phishing by bookmarking litvm.com
4. **Never Share Keys** : No one from LitVM will ever ask for your private key

***

## Community

For the latest network parameters and support:

* **Twitter** : [@LitecoinVM](https://twitter.com/LitecoinVM)
* **Telegram** : [t.me/LitecoinVM](https://t.me/litecoinvm)

***

## Next Steps

Now that your wallet is connected:

1. **Get Testnet zkLTC** — Fund your wallet for testing
2. **Bridge Assets** — Move LTC to LitVM
3. **Deploy a Contract** — Start building on LitVM
