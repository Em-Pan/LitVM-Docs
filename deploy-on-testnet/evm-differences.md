# EVM Differences

LitVM is built on Arbitrum Orbit and is designed to be as compatible with Ethereum as possible. Developers experienced with Ethereum will find that little to no new knowledge is required to build on LitVM.

However, there are some important differences in how certain EVM operations behave on LitVM compared to Ethereum mainnet. This page documents these differences to help developers avoid unexpected behavior.

***

### Quick Summary

| Area          | Key Difference                                                        |
| ------------- | --------------------------------------------------------------------- |
| Block Numbers | `block.number` returns approximate Ethereum L1 block, not LitVM block |
| Block Time    | Variable; blocks produced on-demand, not at fixed intervals           |
| Gas Limit     | Displayed limit appears very high, but effective cap is 32M           |
| Randomness    | `blockhash()` is NOT cryptographically secure                         |
| Timestamps    | Set by sequencer clock, not linked to Ethereum                        |

***

### Solidity Differences

When deploying Solidity contracts on LitVM, most code works identically to Ethereum. However, the following operations return different results:

| Operation          | Behavior on LitVM                                                                                                                                      |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `blockhash(x)`     | Returns a cryptographically insecure, pseudo-random hash for `x` within the range `block.number - 256 <= x < block.number.` Do not use for randomness. |
| `block.coinbase`   | Returns the sequencer's designated address if the transaction was sequenced normally.                                                                  |
| `block.difficulty` | Returns the constant 1.                                                                                                                                |
| `block.prevrandao` | Returns the constant 1.                                                                                                                                |
| `block.number`     | Returns an approximate Ethereum L1 block number, NOT the LitVM block number. See details below.                                                        |
| `msg.sender`       | Works normally for L2-to-L2 transactions. For cross-chain messages from L1, returns an aliased address.                                                |

#### Important: Randomness

⚠️ LitVM's block hashes should NOT be relied on as a secure source of randomness.

If your contract requires secure randomness, use a dedicated oracle service rather than `blockhash()`.

***

### Block Numbers

Block numbers on LitVM work differently than on Ethereum.

#### `block.number` in Solidity

When you access `block.number` in a smart contract, it returns a value close to (but not exactly) the Ethereum L1 block number at which the sequencer received the transaction.

solidity

> // In a LitVM contract:
>
> block.number // => Returns approximate Ethereum L1 block number, NOT LitVM block

This means:

* The value may lag behind the actual Ethereum block by a small amount
* It does NOT return the LitVM-specific block number
* Multiple LitVM blocks can exist within a single Ethereum block

#### Getting the Actual LitVM Block Number

LitVM has its own block numbers that start at 0 at genesis and increment sequentially. To access these:

Via ArbSys Precompile (in Solidity):

solidity

> interface ArbSys {
>
> &#x20;    function arbBlockNumber() external view returns (uint256);
>
> }
>
> \
> // Usage:
>
> uint256 litvmBlockNumber = ArbSys(address(100)).arbBlockNumber();

Via RPC Response:

javascript

const receipt = await provider.getTransactionReceipt('0x...');

// receipt.blockNumber => LitVM block number

// receipt.l1BlockNumber => Ethereum L1 block number (approximate)

#### Timing Assumptions

As a general rule:

* **Long-term timing (hours+):** Block numbers and timestamps are generally reliable
* **Short-term timing (minutes):** Unreliable—don't depend on precise block timing

This is similar guidance to Ethereum itself, but more pronounced on L2s.

***

### Block Timestamps

Block timestamps on LitVM are **not directly linked** to Ethereum block timestamps:

1. **Set by the sequencer:** Timestamps are based on the sequencer's clock
2. **Monotonically increasing:** Each block's timestamp must be ≥ the previous block
3. **Bounded:** Timestamps must be within 24 hours in the past or 1 hour in the future

For force-included transactions (bypassing the sequencer), the timestamp is the greater of:

* The L1 timestamp when the transaction was submitted
* The previous L2 block's timestamp

***

### Block Time

Unlike Ethereum's \~12 second block time, LitVM block production is **variable:**

* Blocks are produced **on-demand** when there are transactions to sequence
* Multiple LitVM blocks can fit within a single Ethereum block
* In active periods, blocks may be produced very frequently
* In quiet periods, block production may be sporadic

**Key implication:** Don't assume fixed block intervals for time-sensitive logic.

***

### Gas and Fees

#### Two-Dimensional Fee Structure

LitVM transactions pay for two components:

1. **L2 execution cost:** Gas for executing the transaction on LitVM
2. **L1 data posting cost:** Cost of posting transaction data to Ethereum

This means gas limits and costs may appear different than expected.

#### Block Gas Limit

When querying a block's gas limit, you may see an artificially high value `(1,125,899,906,842,624)`. This accommodates the variable L1 posting costs.

**The effective execution gas limit is 32 million per block.**

To see actual gas used for execution, check the `gasUsed` field rather than `gasLimit`.

#### Gas Estimation

* `eth_estimateGas` works normally and accounts for both L2 and L1 costs
* Estimates may vary over time due to L1 gas price fluctuations
* The gas limit shown for a transaction includes a buffer for L1 posting costs

***

### Precompiles

LitVM supports all standard Ethereum precompiles, plus additional Arbitrum-specific precompiles:

| Precompile        | Address      | Purpose                                    |
| ----------------- | ------------ | ------------------------------------------ |
| `ArbSys`          | `0x64` (100) | System info (block number, chain ID, etc.) |
| `ArbInfo`         | `0x65` (101) | Account info                               |
| `ArbAddressTable` | `0x66` (102) | Address compression for calldata savings   |
| `ArbGasInfo`      | `0x6c` (108) | Gas pricing info                           |
| `ArbRetryableTx`  | `0x6e` (110) | Retryable ticket management                |
| `ArbStatistics`   | `0x6f` (111) | Chain statistics                           |

#### Using ArbSys

The ArbSys precompile is particularly useful:

> solidity
>
> interface ArbSys {
>
> &#x20;   function arbBlockNumber() external view returns (uint256);
>
> &#x20;   function arbBlockHash(uint256 blockNumber) external view returns (bytes32);
>
> &#x20;   function arbChainID() external view returns (uint256);
>
> }

<br>

> contract MyContract {
>
> &#x20;   function getLitVMBlockNumber() public view returns (uint256)&#x20;
>
> &#x20;   {
>
> &#x20;       return ArbSys(address(100)).arbBlockNumber();
>
> &#x20;   }
>
> }

***

### RPC Differences

Most Ethereum RPC methods work identically. Key differences:

#### Additional Block Fields

When calling `eth_getBlockByHash` or `eth_getBlockByNumber`:

| Field           | Description                                   |
| --------------- | --------------------------------------------- |
| `l1BlockNumber` | Approximate L1 block number for this L2 block |
| `sendCount`     | Number of L2-to-L1 messages since genesis     |
| `sendRoot`      | Merkle root of the outbox tree                |

#### Additional Transaction Types

LitVM supports standard Ethereum transaction types plus Arbitrum-specific types:

| Type             | Code  | Description                            |
| ---------------- | ----- | -------------------------------------- |
| Deposit          | `100` | ETH deposit from L1 via bridge         |
| Unsigned         | `101` | L1 user calling L2 contract via bridge |
| Contract         | `102` | L1 contract calling L2 contract        |
| Retry            | `104` | Retryable ticket redemption            |
| Submit Retryable | `105` | Retryable ticket submission            |
| Internal         | `106` | ArbOS internal transaction             |

***

### Cross-Chain Messaging

When sending messages from Ethereum L1 to LitVM:

#### Address Aliasing

The `msg.sender` for L1→L2 messages is not the original L1 address. It's an "aliased" address calculated as:

> L2\_Alias = L1\_Contract\_Address + 0x1111000000000000000000000000000000001111

This prevents address collision attacks. If your contract receives cross-chain messages, account for this aliasing.

***

### Best Practices

#### ✅ Do

* Use `ArbSys.arbBlockNumber()` when you need the actual LitVM block number
* Use oracles for secure randomness
* Account for variable block times in time-sensitive logic
* Test gas estimates under different L1 gas conditions
* Use `gasUsed` rather than `gasLimit` when analyzing blocks

#### ❌ Don't

* Don't use `blockhash()` for randomness or security
* Don't assume fixed block intervals
* Don't assume `block.number` returns the L2 block number
* Don't rely on precise short-term timing (< 1 hour)

***

### Further Reading

* [Arbitrum vs Ethereum: Full Documentation](https://docs.arbitrum.io/build-decentralized-apps/arbitrum-vs-ethereum/comparison-overview)
* [Arbitrum Block Numbers and Time](https://docs.arbitrum.io/build-decentralized-apps/arbitrum-vs-ethereum/block-numbers-and-time)
* [Arbitrum Solidity Support](https://docs.arbitrum.io/build-decentralized-apps/arbitrum-vs-ethereum/solidity-support)
* [Arbitrum Gas and Fees](https://docs.arbitrum.io/how-arbitrum-works/gas-fees)

***

Have questions about EVM compatibility? Join our [Telegram](https://t.me/litecoinvm) for developer support.
