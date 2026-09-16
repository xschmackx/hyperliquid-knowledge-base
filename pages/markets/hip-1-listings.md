# Listings and HIP-1

| Field | Value |
|-------|--------|
| Shelf | Markets (`pages/markets/`) |
| Scope | Official listings and HIP-1 as published: how spot assets are listed, including the official Dutch auction. Not the spot-product catalog. Not HIP-3. Not HIP-2 internals. Not a live listings dump. Not an API catalog. Not a fee table. |
| Status | Accepted |
| Page `as-of` | 2026-09-17 |
| Rank | Claims below are Rank 1 unless tagged |

This page does not retell token fields, lot size, the native USDC book, or limit-order exchange identity. Those stay on [Spot markets](spot-markets.md). Additional HIP-3 assets that share this auction stay on [HIP-3 builder-deployed perps](hip-3-markets.md). Validator-operated perp specs stay on [Perpetual markets](perpetual-markets.md). Book matching stays on [Order types and the book](order-types-and-the-book.md). Dust conversion is official on the HIP-1 page and is **not specified here** (post-listing book operations).

---

## What HIP-1 listing is for

Official HIP-1 page:

- HIP-1 is a **capped supply fungible token standard**.
- It also features **onchain spot order books between pairs of HIP-1 tokens**.

What that token is as a traded spot product stays on [Spot markets](spot-markets.md). This page records **how a spot asset gets listed**, including the official Dutch auction that sets deployment gas.

Official: the deployment transaction generates a **globally unique hash** by which execution logic indexes the token.

Source: [HIP-1: Native token standard](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-1-native-token-standard.md) — checked 2026-09-17.

---

## Official grouping vs other markets pages

- **Spot product.** `name`, `weiDecimals`, `szDecimals`, lot size, native USDC book: [Spot markets](spot-markets.md).
- **HIP-3 product.** Additional HIP-3 assets share this auction’s frequency and minimum price. First-three-free and the HIP-3 reserve formula stay on [HIP-3 builder-deployed perps](hip-3-markets.md).
- **HIP-2.** Official HIP-1 genesis field 7 is `hyperliquidityInit`. Official HIP-2 page: Hyperliquidity is currently only on spot pairs against USDC. Seeding math stays off this page. Official HIP-2 URL: [HIP-2: Hyperliquidity](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-2-hyperliquidity.md).
- **Delisting.** Official Delisting page is validator-operated perps. It does not name HIP-1 spot. Whether a listed HIP-1 token is delisted by that vote is **unknown here**.

Source: [HIP-1: Native token standard](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-1-native-token-standard.md) — checked 2026-09-17.

---

## Genesis fields specified at listing

Official numbered list on the HIP-1 page. Fields 1–3 (`name`, `weiDecimals`, `szDecimals`) are already on [Spot markets](spot-markets.md). Listing extras:

4. `maxSupply` — maximum and **initial** supply. Supply may decrease over time due to spot order-book fees or future burn mechanisms.
5. `initialWei` — optional genesis balances (official examples: multisig treasury, initial bridge mint).
6. `anchorTokenWei` — existing HIP-1 tokens to proportionally receive genesis balances.
7. `hyperliquidityInit` — parameters for initializing Hyperliquidity on the USDC spot pair. See official HIP-2 page. Not specified here.

Source: [HIP-1: Native token standard](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-1-native-token-standard.md) — checked 2026-09-17.

---

## Auction / deployment gas

Official HIP-1 “Gas cost for deployment,” checked 2026-09-17:

- Gas is paid in the native Hyperliquid token. Official current unit: **HYPE**.
- Gas cost of deployment is decided through a **Dutch auction with duration 31 hours**.
- In that period, deployment gas **decreases linearly** from `initial_price` to **500 HYPE**.
- `initial_price` is **500 HYPE** if the last auction **failed to complete**, otherwise **2 times the last gas price**.

31 hours is duration of one auction, not a cadence between auctions. Whether auctions chain immediately is **unknown here** beyond the initial-price rule that reads the last auction.

These are the official frequency-adjacent and minimum-price figures that [HIP-3 builder-deployed perps](hip-3-markets.md) left unknown there. This Issue does not edit that page.

Source: [HIP-1: Native token standard](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-1-native-token-standard.md) — checked 2026-09-17.

---

## Anchor-token genesis cutoff

Official, same gas section: genesis to existing anchor-token holders is proportional to `balance - 1e-6 * anchorTokenMaxSupply` at the deployed token’s genesis. If negative, no genesis tokens. Official meaning: genesis holders must hold at least **0.0001%** of the anchor token’s max supply at genesis.

Official potential workaround for that cutoff: a small initial USDC gas fee (**value TBD**) for the initial state update of each `(address, token)` pair. TBD stays TBD.

Source: [HIP-1: Native token standard](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-1-native-token-standard.md) — checked 2026-09-17.

---

## Time-sensitive first step and stuck deployments

Official IMPORTANT: the only time-sensitive step is the **first** step of deploying the token, where the deployer specifies `name`, `szDecimals`, and `weiDecimals`. That is when gas is charged and the token is locked in. Official: no time limit once gas is paid. Official: take time after that step to reduce errors.

Official: deployment is a complex multi-stage process; it is possible to get stuck (example: Hyperliquidity and total supply incompatible). Official: deployer responsibility to try the exact deployment on testnet first (`https://app.hyperliquid-testnet.xyz/deploySpot`). Official: gas cannot be refunded if the deployment is stuck.

The multi-stage `spotDeploy` enum stays off this page.

Source: [HIP-1: Native token standard](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-1-native-token-standard.md) — checked 2026-09-17.

---

## Existing or bridged assets as a listing pattern

Official HIP-1 page: a common pattern is HyperCore onchain spot books for an asset that exists externally (bridged assets, tokenized RWAs / stablecoins). Official: those deployers often mint on HyperEVM. Official: they still pay the same permissionless HIP-1 Dutch auction gas on HyperCore; that gas pays for order-book and HyperCore token state. Official: ticker is a unique onchain identifier; frontends may display a different name. Official: simplest genesis can put max supply (or `2^64-1`) in the system address. Official: bridged-asset deployers often elect **not** to use Hyperliquidity (`noHyperliquidity`).

Linking Core↔EVM transfers is not this page. This page is not a bridge how-to.

Source: [HIP-1: Native token standard](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-1-native-token-standard.md) — checked 2026-09-17.

---

## Pair listing after the token exists

Official HIP-1 spot-trading section: any HIP-1 token is initialized with a native spot book quoted in spot USDC. Arbitrary pairs of native tokens can be enabled in the future.

Official API deploy page (Rank 1, API-shaped): deployments between pairs of existing assets follow an **independent Dutch auction**. That *independent pair auction* is recorded here as a listing fact. The Info request catalog stays off this page. Whether that pair auction uses the same 31-hour / 500 HYPE curve is **unknown** on the HIP-1 product page.

Sources: [HIP-1: Native token standard](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-1-native-token-standard.md); [Deploying HIP-1 and HIP-2 assets](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/deploying-hip-1-and-hip-2-assets.md) — checked 2026-09-17.

---

## Deployer fee share as a listing setting

Official HIP-1 page: base-token deployer fee share defaults to **100%** and can only be lowered after (legacy one-time increase from zero). This page is not a volume fee schedule.

Source: [HIP-1: Native token standard](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-1-native-token-standard.md) — checked 2026-09-17.

---

## Gaps inside this scope

- Live list of HIP-1 tickers: **unknown here** by scope.
- Cadence between successive deployment auctions beyond the initial-price rule: **unknown here**.
- Whether the independent pair auction uses the same 31-hour / 500 HYPE curve: **unknown** on the HIP-1 product page.
- USDC gas-fee workaround value: official **TBD**.
- Whether a listed HIP-1 spot token can be delisted by the validator Delisting page: **unknown here**. That page names validator-operated perps only.
- HIP-2 seeding math: **unknown here** by scope.
- Exact multi-stage action order: **unknown here** by scope.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-1-native-token-standard.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-2-hyperliquidity.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/deploying-hip-1-and-hip-2-assets.md | 1 | 2026-09-17 |
