# Network Configuration

Use these published details to configure access to the LitVM LiteForge testnet. Wallet setup is covered in [Add to Your Wallet](add-to-wallet.md).

## LiteForge testnet

| Parameter | Value |
| --- | --- |
| Network name | LitVM LiteForge |
| Chain ID | 4441 |
| Currency symbol | zkLTC |
| RPC URL (HTTP) | https://rpc.testnet.liteforge.zeeve.net/ |
| Block explorer | https://explorer.testnet.liteforge.zeeve.net |
| Explorer API | https://explorer.testnet.liteforge.zeeve.net/api |
| Faucet | https://faucet.testnet.liteforge.zeeve.net/ |
| LitVM Testnet Hub | https://testnet.litvm.com |

## Infrastructure

**Zeeve** is LitVM’s Rollup-as-a-Service infrastructure provider, supporting chain deployment and network operations. LitVM’s LiteForge testnet infrastructure has migrated from Caldera to Zeeve.

The HTTP RPC, explorer, explorer API, and faucet above use the Zeeve services also listed by the LitVM Testnet Hub. Use the HTTP RPC for new connections. The Caldera WebSocket endpoint is no longer active. Use the HTTP RPC; a replacement WebSocket endpoint will be listed only after it is confirmed operational.

{% hint style="info" %}
**Already connected to LiteForge?** If your wallet or application still uses the old Caldera HTTP RPC, update it to https://rpc.testnet.liteforge.zeeve.net/. The network name, Chain ID (**4441**), and gas currency (**zkLTC**) remain unchanged. Update saved explorer and faucet links to the Zeeve services listed above. A replacement WebSocket endpoint has not been published here; use the HTTP RPC.
{% endhint %}

Testnet zkLTC is used to exercise the network. Its availability does not establish that the V2 native LTC interoperability route is available.

## Mainnet

Mainnet connection details will be published when confirmed. Do not use testnet endpoints or assume a mainnet chain ID from the testnet configuration.

See [Network Status](../resources/network-status.md) for availability notes and follow [LitVM’s official announcements](https://x.com/LitecoinVM) for network updates.
