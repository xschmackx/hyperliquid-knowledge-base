# Spot deploy sequence

| Field | Value |
|-------|--------|
| Shelf | Markets (`pages/markets/`) |
| Scope | Official published sequence for deploying a spot market on Hyperliquid when HIP-2 is not used and when the asset is bridged. Not HIP-1 auction or listing rules. Not HIP-2 Hyperliquidity mechanism. Not a live catalog. Not an API catalog. |
| Status | Accepted |
| Page `as-of` | 2026-11-09 |
| Rank | Claims below are Rank 1 unless tagged |

This page does not retell the Dutch auction, genesis fields 1–6, or listing rules. Those stay on [Listings and HIP-1](hip-1-listings.md). What Hyperliquidity is stays on [HIP-2 Hyperliquidity](hip-2-hyperliquidity.md). Token fields, lot size, and the native USDC book stay on [Spot markets](spot-markets.md). Aligned quote assets stay on [Aligned quote assets](aligned-quote-assets.md).

---

## Official five-step SpotDeployAction sequence

Official API page: the API for deploying HIP-1 and HIP-2 assets is a five-step process which involves sending the first 5 variants (the remaining variants are optional) of the enum in the order below.

The ordered variants are:

1. `registerToken2`
2. `userGenesis`
3. `genesis`
4. `registerSpot`
5. `registerHyperliquidity`

Official names as published: `SpotDeployAction`, `registerToken2`, `userGenesis`, `genesis`, `registerSpot`, `registerHyperliquidity`.

Source: [Deploying HIP-1 and HIP-2 assets](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/deploying-hip-1-and-hip-2-assets.md) — checked 2026-11-09.

---

## No-HIP-2 case

Official `Genesis` type: optional `noHyperliquidity` sets hyperliquidity balance to 0.

Official `RegisterHyperliquidity` comment: if `"noHyperliquidity"` was set to True, then `nOrders` must be 0.

The five-step sequence still requires the `registerHyperliquidity` variant. Official text specifies the constraint only on `nOrders`.

What HIP-2 Hyperliquidity is stays on [HIP-2 Hyperliquidity](hip-2-hyperliquidity.md). Do not rewrite that page.

Source: [Deploying HIP-1 and HIP-2 assets](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/deploying-hip-1-and-hip-2-assets.md) — checked 2026-11-09.

---

## Bridged or existing assets

Official HIP-1 page, “Deploying existing assets” section:

One common deployment pattern is to use HyperCore's onchain spot order books for trading an asset that exists externally. For example, this includes assets bridged from other chains or tokenized RWAs like stablecoins.

These deployers often use the HyperEVM for minting in order to leverage battle-tested multichain bridging, including the following options (listed as examples; whether the list is exhaustive is **unknown here**).

To deploy a HyperEVM minted ERC-20 token for trading on HyperCore, the deployer must pay the deployment gas cost in the permissionless HIP-1 Dutch auction on HyperCore. The gas cost pays for order book and HyperCore token states, which are charged to the deployer instead of future users.

For the simplest setup, during the genesis step, the deployer can put the max supply (or `2^64-1` for maximum flexibility) in the system address. See official transfers docs for how the system address is determined based on the HyperCore token index.

Usually deployers of bridged assets elect not to use Hyperliquidity, which can be configured with the `noHyperliquidity` field.

Once the HyperCore token and HyperEVM ERC-20 address are linked, transfers to the system address on the HyperEVM will reflect in the sender's HyperCore balance, and vice versa.

Auction and gas details stay on [Listings and HIP-1](hip-1-listings.md). Linking mechanics stay on the official system-addresses page.

Source: [HIP-1: Native token standard](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-1-native-token-standard.md) — checked 2026-11-09.

---

## Time-sensitive step and stuck deployments

Official IMPORTANT GAS DETAILS on the HIP-1 page: the only time-sensitive step is the first step of deploying the token, where the deployer specifies `name`, `szDecimals`, and `weiDecimals`. That is when gas is charged and the token is locked in. There is no time limit once the gas is paid. Take time after that step to reduce errors.

Official: deployment is a complex multi-stage process, and it is possible to get in a state where your deployment is stuck. For example, Hyperliquidity and total supply may be incompatible. It is the deployer's responsibility to try the exact deployment on testnet first (`https://app.hyperliquid-testnet.xyz/deploySpot`). Gas cannot be refunded if the deployment is stuck.

Mainnet deploy UI: `https://app.hyperliquid.xyz/deploySpot`.

Source: [HIP-1: Native token standard](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-1-native-token-standard.md) — checked 2026-11-09.

---

## Pair deployments between existing tokens

Official `RegisterSpot`: this is also the action used to deploy pairs between an existing base and existing quote asset. Deployments between pairs of existing assets follow an independent Dutch auction. This auction's status is available from the `spotPairDeployAuctionStatus` info request.

Auction details stay on [Listings and HIP-1](hip-1-listings.md). Info endpoint catalogs stay off this page.

Source: [Deploying HIP-1 and HIP-2 assets](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/deploying-hip-1-and-hip-2-assets.md) — checked 2026-11-09.

---

## Gaps inside this scope

- Exact frontend validation rules beyond published: **unknown here**.
- Full list of supported bridges: **unknown here**; the listed bridges on the HIP-1 page are examples only.
- Any post-link steps not published in the official docs: **unknown here**.
- Whether `orderSz` must also be 0 when `noHyperliquidity` is true: official text specifies only that `nOrders` must be 0.
- Live status of any specific deployment or auction: **unknown here** by scope.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/deploying-hip-1-and-hip-2-assets.md | 1 | 2026-11-09 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-1-native-token-standard.md | 1 | 2026-11-09 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-2-hyperliquidity.md | 1 | 2026-11-09 |
| https://app.hyperliquid.xyz/deploySpot | 1 | 2026-11-09 |
| https://app.hyperliquid-testnet.xyz/deploySpot | 1 | 2026-11-09 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm/hypercore-less-than-greater-than-hyperevm-transfers#system-addresses | 1 | 2026-11-09 |
