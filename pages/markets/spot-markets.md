# Spot markets

| Field | Value |
|-------|--------|
| Shelf | Markets (`pages/markets/`) |
| Scope | What a spot market is on HyperCore. Not the listing auction. Not HIP-2 internals. Not fees. |
| Status | Accepted |
| Page `as-of` | 2026-09-16 |
| Rank | All claims below are Rank 1 |

This page does not cover how HyperCore runs as an execution component, how tokens are listed in the Dutch auction, HIP-2 seeding math, fee schedules, order-type behaviour, or Core↔EVM linking. Perpetual products live on [Perpetual markets](perpetual-markets.md).

---

## HIP-1 tokens and onchain spot books

Official HIP-1 page: HIP-1 is a capped-supply fungible token standard. It also features **onchain spot order books between pairs of HIP-1 tokens**.

Official About page: HyperCore includes fully onchain perpetual futures and **spot order books**. That sentence is product location, not a retelling of HyperCore as a component.

Sources:

- [HIP-1: Native token standard](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-1-native-token-standard.md) — checked 2026-09-16
- [About Hyperliquid](https://hyperliquid.gitbook.io/hyperliquid-docs/about-hyperliquid.md) — checked 2026-09-16

---

## Spot USDC as published quote

Official HIP-1 USDC section: USDC is currently used for all perps margining. With HIP-1, USDC also becomes a spot token with an **atomic transfer between perps and spot wallet USDC**. This page names that transfer. It does not write account mechanics.

Official published decimals for spot USDC on 2026-09-16: `szDecimals = weiDecimals = 8`. Official reason on that page: to allow a wide range of HIP-1 token prices.

Source: [HIP-1: Native token standard](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-1-native-token-standard.md) — checked 2026-09-16.

---

## Books: base, quote, native USDC book

Official HIP-1 spot-trading section: HIP-1 tokens trade on order books parametrized by `base` and `quote` tokens.

Any HIP-1 token is initialized with a **native spot order book** whose quote token is **spot USDC**. Official sentence on the same page: trading of **arbitrary pairs** of native tokens can be enabled in the future. Whether that later state is live on this `as-of` is **unknown here** beyond that sentence.

Source: [HIP-1: Native token standard](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-1-native-token-standard.md) — checked 2026-09-16.

---

## Name, decimals, lot size

Official HIP-1 genesis fields that define the tradable token (auction and deploy steps are out of scope):

| Field | Official published rule on 2026-09-16 |
|-------|--------------------------------------|
| `name` | Human readable. Maximum **6 characters**. No uniqueness constraints. |
| `weiDecimals` | Conversion from the minimal integer unit to a human-interpretable float. Official examples on that page: ETH-style `18`, BTC-style `8`. |
| `szDecimals` | Minimum tradable number of decimals on spot order books. |
| Lot size | `10 ** (weiDecimals - szDecimals)` on all spot order books. |
| Constraint | `szDecimals + 5 <= weiDecimals`. |

6, 5, and the example decimal values 18 and 8 are official published figures on 2026-09-16.

Source: [HIP-1: Native token standard](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-1-native-token-standard.md) — checked 2026-09-16.

---

## Limit-order exchange identity

Official HIP-1 spot-trading section, as market structure not as an API body: a limit order is a commitment to exchange

`sz * 10 ** (weiDecimalsBase - szDecimalsBase)` units of the base token

for

`px * sz * 10 ** (weiDecimalsQuote - szDecimalsQuote)` units of the quote token.

How an order is posted, cancelled, or matched is the order-types-and-book page, not this one.

Source: [HIP-1: Native token standard](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-1-native-token-standard.md) — checked 2026-09-16.

---

## Other official spot names (not specified here)

Official docs also name:

- **HIP-2 hyperliquidity**, published as currently available only on spot pairs against USDC
- **permissionless spot quote assets**
- **aligned quote assets**

This page does not specify those products.

Sources for the pointers only:

- [HIP-2: Hyperliquidity](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-2-hyperliquidity.md) — checked 2026-09-16
- [Permissionless spot quote assets](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/permissionless-spot-quote-assets.md) — named, not specified
- [Aligned quote assets](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/aligned-quote-assets.md) — named, not specified

---

## Gaps inside this scope

- Whether arbitrary HIP-1 pairs beyond the native spot-USDC book are enabled on this `as-of`: **unknown here**. Official HIP-1 text says they can be enabled in the future.
- Live list of HIP-1 tickers and books: **not on this page**.
- How the atomic perps↔spot USDC transfer is initiated as a user action: **unknown here** by scope.
- Quote-asset rules beyond spot USDC as the native book quote: **unknown here**; official pages exist and are not specified on this page.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-1-native-token-standard.md | 1 | 2026-09-16 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/about-hyperliquid.md | 1 | 2026-09-16 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-2-hyperliquidity.md | 1 | 2026-09-16 |
