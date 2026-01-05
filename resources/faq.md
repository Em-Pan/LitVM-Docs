# faq

Find answers to common questions about LitVM, its technology, and how to get started.

***

### General

<details>

<summary>What is LitVM?</summary>

LitVM (Litecoin Virtual Machine) is Litecoin's first trustless EVM rollup. It's an EVM-compatible smart contract platform built on Arbitrum Orbit and powered by BitcoinOS technology, enabling Web3 functionality such as Litecoin yield markets, RWA platforms, DeFi, NFTs, and programmable applications while inheriting Litecoin's proof-of-work security.

</details>

<details>

<summary>Is LitVM endorsed by the Litecoin Foundation?</summary>

Yes. LitVM is officially endorsed by the Litecoin Foundation, making it the first EVM Litecoin rollup with official community backing.

</details>

<details>

<summary>When will LitVM launch?</summary>

* Testnet: Q1 2026
* Token Generation Event (TGE): Following testnet
* Mainnet: After TGE and security audits

</details>

***

### Technology

<details>

<summary>How does LitVM work?</summary>

Executes smart contracts (Arbitrum Nitro)LitVM executes smart contracts using Arbitrum Nitro (EVM-compatible).Generates zk validity proofs (Succinct zkVM)Uses Succinct zkVM to generate validity proofs.Trustless LTC bridging (BitcoinOS Grail bridge)Bridges LTC trustlessly via BitcoinOS Grail bridge.EVM asset bridging (Arbitrum Bridge)Bridges ETH and ERC-20s via the Arbitrum Bridge.Decentralized sequencing (Espresso)Decentralizes sequencing through Espresso shared sequencer.Settlement migrationInitially settles on Ethereum, then migrates to Litecoin mainchain.

</details>

<details>

<summary>Is LitVM a zkRollup or Optimistic Rollup?</summary>

LitVM is a hybrid rollup that combines both:

* Optimistic execution for fast transaction processing
* ZK validity proofs for cryptographic security guarantees

This gives the speed of optimistic rollups with the security of zkRollups.

</details>

<details>

<summary>What makes the LTC bridge trustless?</summary>

Unlike traditional bridges that rely on multisig custodians, LitVM uses BitcoinOS's Grail bridge which:

* Uses ZK-SNARK proofs to verify locked LTC
* Requires only 1 honest validator (vs. majority consensus)
* Never places funds in third-party custody
* Provides mathematical guarantees, not trust assumptions

</details>

<details>

<summary>How do I bridge assets from Ethereum?</summary>

LitVM supports the standard Arbitrum Bridge for EVM-native assets like ETH, USDC, and other ERC-20 tokens. This provides a familiar bridging experience for Ethereum users and access to deep EVM liquidity.

</details>

<details>

<summary>Does LitVM require changes to Litecoin?</summary>

No. LitVM works with Litecoin's existing protocol. No soft forks, hard forks, or upgrades to Litecoin are required.

</details>

<details>

<summary>What's the difference between zkLTC and wrapped LTC?</summary>

| zkLTC                        | Wrapped LTC (Traditional)      |
| ---------------------------- | ------------------------------ |
| Trustless ZK-verified        | Custodian-dependent            |
| Non-custodial                | Third-party custody            |
| 1/n security (1 honest node) | m-of-n trust (honest majority) |
| On-chain verification        | Off-chain attestation          |

</details>

***

### Tokens

<details>

<summary>What is zkLTC?</summary>

zkLTC is a 1:1 representation of LTC on LitVM. When you bridge LTC to LitVM via the BitcoinOS Grail bridge, you receive zkLTC which is used for:

* Gas fees (transaction costs)
* DeFi protocols (trading, lending, etc.)
* The primary base asset on LitVM

Every zkLTC is backed by LTC locked on the Litecoin mainchain.

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
* Join community campaigns (like LitVM’s ongoing [Xeet campaign](https://www.xeet.ai/signals/litvm))

</details>

***

### Using LitVM

<details>

<summary>How do I add LitVM to my wallet?</summary>

One-click (when available)Use the one-click add on the LitVM Network Hub (Coming Soon).Manual RPCAdd manually using RPC details.ChainListUse ChainList.org.

</details>

<details>

<summary>How do I get testnet zkLTC?</summary>

Add testnetAdd LitVM Testnet to your wallet.Visit faucetVisit the Testnet Faucet.Connect walletConnect your wallet and request zkLTC.Receive tokensTokens arrive in \~30 seconds.

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

LitVM targets sub-cent transaction fees, with typical costs:

* Simple transfer: \~$0.001
* DEX swap: \~$0.01-0.02
* Contract deployment: \~$0.05-0.50

Fees are paid in zkLTC.

</details>

***

### Security

<details>

<summary>Is LitVM safe?</summary>

LitVM inherits security from multiple layers:

1. Litecoin: 14+ years of uninterrupted PoW security
2. Ethereum: World's most decentralized smart contract platform (Phase 1 settlement)
3. ZK Proofs: Mathematical guarantees of execution correctness
4. Espresso: Decentralized sequencing prevents censorship
5. BitcoinOS Grail: Non-custodial bridging with 1/n security
6. Arbitrum Bridge: Battle-tested rollup bridge for EVM assets

</details>

<details>

<summary>Has LitVM been audited?</summary>

Audits are in progress. Results will be published publicly. Component technologies (Arbitrum Nitro, BitcoinOS, SP1) have undergone separate audits.

</details>

<details>

<summary>What happens if the sequencer goes down?</summary>

Espresso's shared sequencer provides redundancy. If primary sequencers fail:

* Other sequencers in the network continue operation
* Users can force-include transactions via L1
* Funds are never at risk—you can always withdraw via the bridge

</details>

<details>

<summary>Are my funds safe if LitVM has issues?</summary>

Yes. Because zkLTC is backed 1:1 by LTC on Litecoin mainchain:

* You can always bridge back to native LTC
* Proofs are verified on-chain
* No single entity can steal funds

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

**Testnet:**

```
RPCURL:⚠️ **⚠️ **TBA** — This value will be published closer to launch** — This value will be published closer to launch
ChainID:⚠️ **⚠️ **TBA** — This value will be published closer to launch** — This value will be published closer to launch
Explorer:⚠️ **⚠️ **TBA** — This value will be published closer to launch** — This value will be published closer to launch
```

**Mainnet:** Coming after TGE

</details>

<details>

<summary>Are there developer grants?</summary>

```
51% of the total $LITVM token supply is reserved for community and ecosystem via the Litecoin DAO. This will include grants and bootstrapping capital for ecosystem applications.
```

</details>

<details>

<summary>How do I get developer support?</summary>

TelegramFastest response for quick questions.GitHubFile issues for bugs.DocumentationCheck these docs first!TwitterTag @LitecoinVM for visibility.

</details>

***

### Ecosystem

<details>

<summary>What can I do on LitVM?</summary>

* Yield: Earn yield on LTC with on-chain DeFi and institutional-grade vaults
* DeFi: Trade, lend, borrow, provide liquidity
* RWAs: Tokenized real-world assets
* AI: AI agents and AI-integrated applications
* Payments: Fast, cheap and programmable Litecoin transactions
* NFTs: Mint, trade, and use Litecoin-native NFTs
* Gaming: On-chain games and rewards

</details>

<details>

<summary>Will stablecoins be available?</summary>

Yes. USDC, USDT and other stablecoins can also be bridged from Ethereum via the Arbitrum Bridge. We also expect Litecoin-based stablecoins to make an appearance on LitVM.

</details>

<details>

<summary>Can I bridge assets other than LTC?</summary>

Yes! LitVM has a dual bridge architecture:

From Litecoin (BitcoinOS Grail Bridge):

* LTC → zkLTC

From Ethereum (Arbitrum Bridge):

* ETH
* USDC, USDT, and other stablecoins
* ERC-20 tokens

Future support planned for Litecoin-native assets:

* Litecoin Ordinals
* Litecoin Runes
* LTC-20 tokens
* BitcoinOS Charms

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

zkLTC serves as the gas token (1:1 backed by LTC), while $LITVM is the governance and utility token. This separation preserves Litecoin's sound money properties for transactions while enabling community coordination and revenue sharing through a dedicated governance token.

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

For LTC bridging (BitcoinOS Grail):

1. Ensure you have enough LTC for fees on mainchain
2. Wait for sufficient confirmations (may take several blocks)
3. Check bridge UI for status

For ETH/ERC-20 bridging (Arbitrum Bridge):

1. Ensure transaction confirmed on Ethereum
2. Wait for the standard confirmation period
3. Check Arbitrum Bridge UI for status

Contact support in Discord if issues persist >1 hour.

</details>

***

### Still Have Questions?

* Telegram: [t.me/litecoinvm](http://t.me/litecoinvm)
* Twitter: [@LitecoinVM](https://twitter.com/LitecoinVM)
* Email: [\[email protected\]](file:///cdn-cgi/l/email-protection)

Can't find your question? Submit feedback via our Feedback Form and we'll add it.
