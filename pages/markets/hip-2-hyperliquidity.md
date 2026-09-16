# HIP-2 Hyperliquidity

| Field | Value |
|-------|--------|
| Shelf | Markets (`pages/markets/`) |
| Scope | Official HIP-2 Hyperliquidity as published: the liquidity product on spot pairs. Not the HIP-1 listing auction. Not the spot-product catalog. Not an HLP catalog. Not a live pair dump. Not an API catalog. |
| Status | Accepted |
| Page `as-of` | 2026-09-17 |
| Rank | Claims below are Rank 1 unless tagged |

This page does not retell the listing auction, genesis fields 1–6, `noHyperliquidity`, or stuck-deploy. Those stay on [Listings and HIP-1](hip-1-listings.md). Token fields, lot size, and the native USDC book stay on [Spot markets](spot-markets.md). ALO rejection and matching stay on [Order types and the book](order-types-and-the-book.md).

---

## What Hyperliquidity is

Official HIP-2 page:

- HIP-1 is sufficient as a permissionless token standard; in practice it is often crucial to **bootstrap liquidity**.
- Official design principle named there: liquidity should be democratized.
- For perps, **HLP** can quote from CEX perp and spot prices; official: a **new model** is needed for HIP-1 tokens in early price discovery.
- Hyperliquidity is inspired by Uniswap, while interoperating with a **native onchain order book** so end users can add book liquidity.
- HIP-2 is a **fully decentralized onchain strategy** that is part of Hyperliquid’s **block transition logic**. Official: **no operators**. Strategy logic is secured by the same consensus that operates the order book.
- Official constraint: Hyperliquidity is **currently only available on spot pairs against USDC**.

HLP is named only as that contrast. HLP as a protocol vault product is not this page. “Part of block transition logic” is official product grouping, not a HyperCore component page.

Source: [HIP-2: Hyperliquidity](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-2-hyperliquidity.md) — checked 2026-09-17.

---

## Official grouping vs other markets pages

- **HIP-1 listing.** Auction, genesis fields 1–6, `noHyperliquidity`, and the stuck-deploy warning stay on [Listings and HIP-1](hip-1-listings.md). This page starts at what Hyperliquidity does on the book after those params exist.
- **Spot product.** Token / lot / native USDC book stay on [Spot markets](spot-markets.md).
- **Order types.** ALO stays on [Order types and the book](order-types-and-the-book.md).

Source: [HIP-2: Hyperliquidity](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-2-hyperliquidity.md) — checked 2026-09-17.

---

## Published parameters

Official HIP-2 numbered list, checked 2026-09-17:

1. `spot` — a spot order-book asset with USDC quote returned by a HIP-1 deployment.
2. `startPx` — the initial price of the range.
3. `nOrders` — the number of orders in the range.
4. `orderSz` — the size of a full order in the range.
5. `nSeededLevels` — the number of levels that begin as **bids instead of asks**. Official: for each additional bid level from incrementing `nSeededLevels`, the deployer funds Hyperliquidity with `px * sz` worth of USDC. Official: for fixed `nOrders`, increasing seeded levels **decreases total supply** because it reduces the genesis supply of Hyperliquidity.

Which `px` is used in `px * sz` when seeding several bid levels is **unknown** beyond that official short string.

Source: [HIP-2: Hyperliquidity](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-2-hyperliquidity.md) — checked 2026-09-17.

---

## Price range and cadence

Official recursive string on that page. Quoted as published. Not tidied into a third spread identity.

`px_0 = startPx`

`px_i = round(px_{i-1} * 1.003)`

`round` is official and undefined beyond that word. This page does not specify tick rounding.

Official update cadence: the strategy updates on every block where the block time is at least **3 seconds** since the previous update block.

Source: [HIP-2: Hyperliquidity](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-2-hyperliquidity.md) — checked 2026-09-17.

---

## After each update

Official numbered list on that page:

1. Strategy targets `nFull = floor(balance / orderSz)` full ask orders and a `balance % orderSz` partial ask order if the partial is nonzero. Official: to the extent that **ALO** orders are not rejected, these orders are ensured.
2. Each fully filled tranche is modified to an order of size `orderSz` on the side with available balance, except the single partial order from (1) if it exists.

Official published guarantee: the resulting strategy guarantees a **0.3% spread every 3 seconds**.

1.003 and 0.3% are the same official step. This page does not invent a third spread identity.

ALO rejection stays on [Order types and the book](order-types-and-the-book.md).

Source: [HIP-2: Hyperliquidity](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-2-hyperliquidity.md) — checked 2026-09-17.

---

## Maintenance

Official HIP-2 page: like smart-contract pools on general-purpose chains, Hyperliquidity requires **no maintenance in the form of user transactions**. Official improvement: it participates in a general-purpose order book; active LPs can join alongside it at any time.

Source: [HIP-2: Hyperliquidity](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-2-hyperliquidity.md) — checked 2026-09-17.

---

## Gaps inside this scope

- Live list of pairs that have Hyperliquidity enabled: **unknown here** by scope.
- Which `px` is used in `px * sz` when seeding several bid levels: **unknown here** beyond the official short string.
- Meaning of `round` versus book tick size: **unknown** on the HIP-2 page.
- Whether Hyperliquidity can exist on a non-USDC quote pair: official text says **currently only** USDC quote.
- Interaction with dust conversion: **unknown here**.
- HLP internals: **unknown here** by scope.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-2-hyperliquidity.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-1-native-token-standard.md | 1 | 2026-09-17 |
