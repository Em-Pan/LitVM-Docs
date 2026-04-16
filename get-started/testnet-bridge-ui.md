# Testnet Bridge UI

{% hint style="success" %}
✅ **Live Now**

Bridge assets between Litecoin and LitVM.
{% endhint %}

## Bridge UI

The LitVM Bridge enables trustless bridging of LTC from the Litecoin mainchain to zkLTC on LitVM using BitcoinOS's Grail bridge infrastructure.

**URL:** [https://liteforge.hub.caldera.xyz](https://liteforge.hub.caldera.xyz)

### Supported Assets

| Asset | Network | Description |
|-------|---------|-------------|
| **LTC** | Litecoin Mainchain | Native Litecoin |
| **zkLTC** | LitVM | Wrapped LTC on LitVM |

### How to Bridge

{% stepper %}
{% step %}
### Visit the Bridge

Go to [https://liteforge.hub.caldera.xyz](https://liteforge.hub.caldera.xyz)
{% endstep %}

{% step %}
### Connect Wallets

* Connect your **Litecoin wallet** (for LTC)
* Connect your **EVM wallet** (for zkLTC on LitVM)
{% endstep %}

{% step %}
### Select Direction

* **LTC → zkLTC:** Deposit LTC to receive zkLTC on LitVM
* **zkLTC → LTC:** Burn zkLTC to receive LTC on Litecoin
{% endstep %}

{% step %}
### Enter Amount

* Enter the amount you want to bridge
* Review fees and estimated time
* Confirm the transaction
{% endstep %}

{% step %}
### Wait for Confirmation

* LTC → zkLTC: Typically ~10-30 minutes
* zkLTC → LTC: Typically ~10-30 minutes
* Track progress on the [Block Explorer](https://liteforge.explorer.caldera.xyz)
{% endstep %}
{% endstepper %}

### Bridge Fees

* **Network Fees:** Variable based on Litecoin and LitVM gas prices
* **Bridge Fee:** Small percentage for protocol operation
* **Minimum Bridge Amount:** Check the UI for current minimums

### Security

The LitVM Bridge uses **BitcoinOS Grail** infrastructure for trustless bridging:

* No centralized custodians
* Cryptographic proofs ensure asset backing
* Decentralized validator set

### Need Help?

Join our community for support:

* **Telegram:** [https://t.me/litecoinvm](https://t.me/litecoinvm)
* **Twitter:** [https://twitter.com/LitecoinVM](https://twitter.com/LitecoinVM)