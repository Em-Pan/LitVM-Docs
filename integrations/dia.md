# DIA (Oracle)

> dApps built on LitVM can leverage DIA oracles to access up-to-date asset price information.

DIA is a cross-chain, trustless oracle network delivering verifiable price feeds for [LitVM](https://litvm.com/). DIA sources raw trade data directly from primary markets and computes it onchain, ensuring transparency and data integrity.

### Key Features

* Complete verifiability from source to destination smart contract.
* Direct data sourcing from 100+ primary markets eliminating intermediary risk.
* Support for 20,000+ assets across all major asset classes.
* Custom oracle configuration with tailored sources and methodologies.

### Oracle Contracts

| Chain         | Contract Address |
| ------------- | --------------- |
| LitVM Testnet | [0xE7F65d4bAdcfABc4eA57B8F66bBa044363D89eec](https://liteforge.explorer.caldera.xyz/address/0xE7F65d4bAdcfABc4eA57B8F66bBa044363D89eec) |

### Oracle Configuration

| Parameter         | Value                                     |
| ----------------- | ----------------------------------------- |
| **Deviation (%)** | 0.5% for stablecoins, 1% for other assets |
| **Heartbeat**     | 1h                                        |

### Available Asset Feeds

| Chain         | Price Feed | Type   | Adapter Address (AggregatorV3Interface) |
| :------------ | :--------- | :----- | :-------------------------------------- |
| LitVM Testnet | USDC       | Market | [0x4f91a950ed73c8B6F28dFE460f9444ed8866894f](https://liteforge.explorer.caldera.xyz/address/0x4f91a950ed73c8B6F28dFE460f9444ed8866894f) |
| LitVM Testnet | USDT       | Market | [0xd7ff0A3DdE1FdC2137Ff4CaAde5396f009739645](https://liteforge.explorer.caldera.xyz/address/0xd7ff0A3DdE1FdC2137Ff4CaAde5396f009739645) |
| LitVM Testnet | ETH        | Market | [0xc760B46beF9eD3F9A3d2b825164324D6703F0185](https://liteforge.explorer.caldera.xyz/address/0xc760B46beF9eD3F9A3d2b825164324D6703F0185) |
| LitVM Testnet | BTC        | Market | [0x7d0445782E383223c7B4B660bb96b87213e9b605](https://liteforge.explorer.caldera.xyz/address/0x7d0445782E383223c7B4B660bb96b87213e9b605) |
| LitVM Testnet | LTC/USD    | Market | [TBD](https://liteforge.explorer.caldera.xyz/) |
| LitVM Testnet | XAU/USD    | Market | [TBD](https://liteforge.explorer.caldera.xyz/) |
| LitVM Testnet | XAG/USD    | Market | [TBD](https://liteforge.explorer.caldera.xyz/) |
| LitVM Testnet | WTI/USD    | Market | [TBD](https://liteforge.explorer.caldera.xyz/) |
| LitVM Testnet | XBR/USD    | Market | [TBD](https://liteforge.explorer.caldera.xyz/) |

## How to Access Data

### Adapter Contracts

To consume price data from the oracle, use the [adapter smart contract](#available-asset-feeds) for the asset you want to query on LitVM Testnet. This will allow you to access the same methods on the AggregatorV3Interface such as `getRoundData` & `latestRoundData`.

Below is an example of a contract consuming `$USDC` from the oracle using the `DiaAssetSpecificCallingConvention` interface. It will return the most recent price of `USDC` in `USD` with 18 decimal places (e.g. `999799952400000000` is $0.9997999524) along with the Unix timestamp of the last price update.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.13;

interface DiaAssetSpecificCallingConvention {
    function latestRoundData() external view returns (
        uint80 roundId,
        int256 answer,
        uint256 startedAt,
        uint256 updatedAt,
        uint80 answeredInRound
    );
}

contract DIAOracleSample {
    address usdcAdapter = 0x4f91a950ed73c8B6F28dFE460f9444ed8866894f;

    function getUSDCLatestPrice() external view returns (
        uint128 latestPrice,
        uint128 timestampOflatestPrice
    ) {
        // Call the Chainlink adapter's latestRoundData function
        (, int256 answer, , uint256 updatedAt, ) =
        DiaAssetSpecificCallingConvention(usdcAdapter).latestRoundData();

        latestPrice = uint128(uint256(answer));
        timestampOflatestPrice = uint128(updatedAt);

        return (latestPrice, timestampOflatestPrice);
    }
}
```

***

## Request a Custom Oracle

DIA offers highly customizable oracles that are individually tailored to each dApp's needs. Each oracle can be customized in the following ways:

* Data Sources & Asset Feeds
* Pricing Methodologies
* Update Triggers (Frequency, Deviation, Heartbeat, etc.)

[Request a Custom Oracle →](https://www.diadata.org/docs/guides/how-to-guides/request-a-custom-oracle)

## Support

For developer assistance, connect with the DIA team directly on [Discord](https://discord.gg/ZvGjVY5uvs) or [Telegram](https://t.me/diadata_org).
