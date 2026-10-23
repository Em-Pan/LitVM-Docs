# Network Status

This page separates operational availability from the component roles described in [Architecture](../overview/architecture.md).

## Testnet

LiteForge is LitVM’s testnet. Start at the [LitVM Testnet Hub](https://testnet.litvm.com) and use the published [Network Configuration](../get-started/network-configuration.md) for wallet and developer setup.

Testnet zkLTC supports testing on the network. Receiving testnet tokens is separate from bringing native LTC through the V2 interoperability route.

## Charms integration

LitVM is co-developing Litecoin and Ethereum support with Charms. The V2 design represents LTC on Ethereum as zkLTC and routes it into LitVM through Arbitrum infrastructure.

Availability of that complete route, supported assets, and issuance and redemption conditions will be described in release documentation. Use the release documentation for the relevant network when accessing the route.

## Infrastructure migration

Zeeve is replacing Caldera as LitVM’s Rollup-as-a-Service provider. The migration is not yet complete. The existing Caldera-hosted RPC, WebSocket, explorer, and faucet URLs remain in the documentation until replacements are confirmed.

## Proving and sequencing

Succinct and Espresso remain components of the architecture. Network-specific activation details and measured proving or finality performance require release information for the relevant integration; this documentation does not assume them from the technology providers’ general capabilities.

## Mainnet and security information

Mainnet availability, connection details, and integration-specific security or audit information will be communicated through [LitVM’s official channels](connect.md). An audit of an underlying technology is distinct from an audit of its LitVM integration.
