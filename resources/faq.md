# FAQ

Find answers to common questions about LitVM, its technology, and how to get started.

***

### General

<details>

<summary>What is LitVM?</summary>

LitVM is an EVM-compatible Arbitrum Orbit chain using Ethereum settlement. It connects Litecoin assets with EVM applications through Charms Protocol and Arbitrum infrastructure. Litecoin secures native LTC ownership; Ethereum provides settlement for the LitVM chain.

</details>

<details>

<summary>Is LitVM endorsed by the Litecoin Foundation?</summary>

Yes. LitVM is officially endorsed by the Litecoin Foundation, making it the first EVM Litecoin rollup with official community backing.

</details>

<details>

<summary>When will LitVM launch?</summary>

Use the [LitVM Testnet Hub](https://testnet.litvm.com) for testnet access. Refer to [Network Status](network-status.md) and official announcements for mainnet availability, token launch information, and V2 integration updates.

</details>

***

### Technology

<details>

<summary>How does LitVM work?</summary>

LitVM uses Arbitrum Orbit and Nitro for EVM-compatible execution and Ethereum for settlement. Charms provides the Litecoin interoperability layer. The intended asset route is **Litecoin → Charms / zkLTC → Ethereum → Arbitrum → LitVM**. Succinct and Espresso provide the proving and sequencing components of the architecture. See [Architecture](../overview/architecture.md).

</details>

<details>

<summary>Is LitVM a zkRollup or Optimistic Rollup?</summary>

LitVM is built on Arbitrum Orbit and Nitro. Its architecture includes Succinct technology for proving. The execution framework, execution proving, and Charms asset validation are separate components; the presence of ZK technology alone does not establish the operating mode of the deployed rollup. See [Architecture](../overview/architecture.md) and [Network Status](network-status.md) for component roles and availability.

</details>

<details>

<summary>How does Charms validate asset movement?</summary>

Charms uses client-side validation and zero-knowledge proofs to establish the validity of asset state and transitions. The intended LitVM route combines the Charms integration between Litecoin and Ethereum with Arbitrum infrastructure between Ethereum and LitVM. Security and operational conditions of the complete route depend on those integrations. See [Charms Protocol](../overview/charms.md).

</details>

<details>

<summary>How do I bridge assets from Ethereum?</summary>

Arbitrum infrastructure provides the Ethereum ↔ LitVM connection in the V2 architecture, including the movement of zkLTC. Use the released LitVM Bridge instructions for the relevant network and asset. Refer to [Network Status](network-status.md) for availability information.

</details>

<details>

<summary>Does LitVM require changes to Litecoin?</summary>

No. LitVM works with Litecoin's existing protocol. No soft forks, hard forks, or upgrades to Litecoin are required.

</details>

<details>

<summary>Are there any EVM differences I should know about?</summary>

Yes, a few minor ones. Most notably, `block.number` returns the approximate Ethereum L1 block number, not the LitVM block number. See our [EVM Differences guide](../deploy-on-testnet/evm-differences.md) for details.

</details>

<details>

<summary>What's the difference between zkLTC and wrapped LTC?</summary>

zkLTC is designed to represent LTC on EVM through the Charms integration, using cryptographic validation of asset state and transitions. A conventional custodial wrapped asset depends on an issuer or custodian. The complete zkLTC route also uses Ethereum and Arbitrum infrastructure; backing, issuance, and redemption conditions must be established by the integration documentation. See [zkLTC](../overview/usdlitvm-and-usdzkltc.md).

</details>



***

### Tokens

<details>

<summary>What is zkLTC?</summary>

zkLTC is designed to represent native LTC in the EVM ecosystem. In the V2 architecture, it exists as an ERC-20-compatible asset on Ethereum and moves into LitVM through Arbitrum infrastructure. Within LitVM, it is intended to serve as the native gas asset and an asset used by applications. Testnet zkLTC is separate from native LTC interoperability; see [Network Status](network-status.md).

</details>

<details>

<summary>What is $LITVM?</summary>

$LITVM is the governance and utility token of the LitVM ecosystem. It provides:

* Voting rights in the Litecoin DAO
* Share of protocol revenue (sequencer fees)
* Ecosystem access and benefits

</details>

<details>

<summary>How can I get $LITVM?</summary>

$LITVM will be available after the Token Generation Event (TGE). Ways to participate:

* Follow [@LitecoinVM](https://twitter.com/LitecoinVM) for early access programs
* Participate in testnet activities
* Join community campaigns

</details>

***

### Using LitVM

<details>

<summary>How do I add LitVM to my wallet?</summary>

See our Add to Your Wallet guide. You can:

1. Use the one-click add on the [LitVM Testnet Hub](https://testnet.litvm.com)
2. Add manually using RPC details
3. Use ChainList.org

</details>

<details>

<summary>How do I get testnet zkLTC?</summary>

Add the testnet to your wallet, then visit the [LitVM Testnet Hub](https://testnet.litvm.com) and select **Get zkLTC**. Follow the faucet instructions. Testnet tokens are for testing and do not represent a deposit through the V2 interoperability route.

</details>

<details>

<summary>Which wallets work with LitVM?</summary>

Any EVM-compatible wallet works:

* MetaMask
* Rabby
* Coinbase Wallet
* Trust Wallet
* Rainbow
* WalletConnect-compatible wallets

</details>

<details>

<summary>Can I deploy smart contracts?</summary>

Yes. LitVM is fully EVM-compatible. You can deploy using:

* Foundry
* Hardhat
* Remix

Use Solidity, Vyper, or any EVM-compatible language.

</details>

<details>

<summary>What are gas fees like?</summary>

Fees depend on transaction execution and L1 data posting costs. Use your wallet or developer tooling to estimate the current fee before submitting a transaction. The intended gas asset within LitVM is zkLTC. See [Gas and Fees](../deploy-on-testnet/evm-differences.md#gas-and-fees).

</details>

***

### Security

<details>

<summary>Is LitVM safe?</summary>

The architecture has several security boundaries: Litecoin secures native LTC, Charms validates programmable asset state and transitions, Arbitrum infrastructure connects Ethereum and LitVM, and Ethereum provides LitVM settlement. Evaluate the deployed integrations, their operating conditions, and integration-specific audit information. No component description establishes a guarantee for the complete route.

</details>

<details>

<summary>Has LitVM been audited?</summary>

Use published LitVM security announcements and audit reports to assess the relevant deployment. An audit of an underlying technology is distinct from an audit of its LitVM integration. See [Network Status](network-status.md) and [Official Channels](connect.md).

</details>

<details>

<summary>What happens if the sequencer goes down?</summary>

A sequencing interruption can affect transaction inclusion and confirmation. Recovery and any L1 inclusion or withdrawal mechanisms depend on the deployed chain configuration. Check official network updates and the released operating instructions for the relevant network.

</details>

<details>

<summary>Are my funds safe if LitVM has issues?</summary>

Cross-chain access and redemption depend on the affected infrastructure layer and the integration’s operating conditions. Check official network updates and use the released bridge and support instructions. The presence of cryptographic proofs alone does not establish uninterrupted access or redemption.

</details>

***

### Developers

<details>

<summary>Is LitVM EVM-compatible?</summary>

Yes, fully EVM-equivalent. Deploy the same contracts you'd deploy on Ethereum, Arbitrum, or any EVM chain. Standard tooling works:

* Solidity/Vyper
* Hardhat/Foundry/Remix
* Ethers.js/Web3.js
* All standard ERC standards

</details>

<details>

<summary>Where can I find the RPC endpoints?</summary>

See [Network Configuration](../get-started/network-configuration.md) for published testnet RPC, WebSocket, explorer, and faucet details. Existing Caldera-hosted endpoints remain documented during the migration to Zeeve. Mainnet connection details will be added when confirmed.

</details>

<details>

<summary>Are there developer grants?</summary>

51% of the total $LITVM token supply is reserved for community and ecosystem via the Litecoin DAO. This will include grants and bootstrapping capital for ecosystem applications.

</details>

<details>

<summary>How do I get developer support?</summary>

1. **Telegram:** Fastest response for quick questions
2. **GitHub:** File issues for bugs
3. **Documentation:** Check these docs first!
4. **Twitter:** Tag [@LitecoinVM](https://x.com/litecoinvm) for visibility

</details>

***

### Ecosystem

<details>

<summary>What can I do on LitVM?</summary>

* **Yield:** Earn yield on LTC with on-chain DeFi and institutional-grade vaults
* **DeFi:** Trade, lend, borrow, provide liquidity
* **RWAs:** Tokenized real-world assets
* **AI:** AI agents and AI-integrated applications
* **Payments:** Fast, cheap and programmable Litecoin transactions
* **NFTs:** Mint, trade, and use Litecoin-native NFTs
* **Gaming:** On-chain games and rewards

</details>

<details>

<summary>Will stablecoins be available?</summary>

The architecture supports an Ethereum ↔ LitVM connection through Arbitrum infrastructure. Availability of particular stablecoins or other assets depends on the deployed integrations and announced asset support. Use the released asset list and bridge instructions for the relevant network.

</details>

<details>

<summary>Can I bridge assets other than LTC?</summary>

The V2 architecture distinguishes Charms-based Litecoin interoperability from the Arbitrum connection between Ethereum and LitVM. Availability of ETH, ERC-20 tokens, or particular Litecoin-native assets depends on the released integrations. Use the announced asset list rather than assuming that every asset supported by an underlying protocol is available through LitVM.

</details>

***

### Token & Economics

<details>

<summary>What is the total supply of $LITVM?</summary>

The full tokenomics details can be found [here](https://www.litvm.com/blog/litvm-token). Key points:

* 51% community allocation via the Litecoin DAO
* Revenue sharing from sequencer fees
* Governance rights

</details>

<details>

<summary>How does revenue sharing work?</summary>

$LITVM holders and/or stakers receive a share of sequencer fees—the fees generated from transaction ordering and batching on the network. This creates sustainable value tied to actual network usage.

</details>

<details>

<summary>Why does LitVM have two tokens?</summary>

zkLTC is intended as the gas and application asset, connecting LitVM with LTC as the underlying asset through the Charms integration. $LITVM serves governance and utility purposes. See [$LITVM & $zkLTC](../overview/usdlitvm-and-usdzkltc.md).

</details>

***

### Troubleshooting

<details>

<summary>My transaction is stuck</summary>

1. Check you have enough zkLTC for gas
2. Try increasing gas limit
3. Reset your wallet's nonce
4. Wait for network congestion to clear

</details>

<details>

<summary>I can't connect to the network</summary>

1. Verify RPC URL is correct
2. Check Chain ID matches
3. Try an alternative RPC endpoint
4. Clear wallet cache and reconnect

</details>

<details>

<summary>Bridge transaction not completing</summary>

Check which part of the route is affected: Litecoin ↔ Ethereum through the Charms integration, or Ethereum ↔ LitVM through Arbitrum infrastructure. Record the source and destination networks, transaction hashes, and the status shown by the bridge. Follow the released instructions for the relevant network and contact [official support](connect.md) if the issue persists. Never share private keys or recovery phrases.

</details>

***

### Still Have Questions?

* Telegram: [t.me/litecoinvm](http://t.me/litecoinvm)
* Twitter: [@LitecoinVM](https://twitter.com/LitecoinVM)
* Email: [hello@litvm.com](mailto:hello@litvm.com)

Can't find your question? Submit feedback via our [Feedback Form](https://forms.gle/Geo4ojvZ4egLE9od6) and we'll add it.
