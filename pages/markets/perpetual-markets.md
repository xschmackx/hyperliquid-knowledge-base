# Perpetual markets

| Field | Value |
|-------|--------|
| Shelf | Markets (`pages/markets/`) |
| Scope | What a perpetual market is on HyperCore, and the published contract-spec skeleton. Not the HyperCore component. Not funding internals. Not liquidation math. |
| Status | Accepted |
| Page `as-of` | 2026-09-16 |
| Rank | All claims below are Rank 1 |

This page does not cover how HyperCore runs as an execution component, how funding is computed, how marks or oracles are computed, order types, the book, fees, or liquidations. Official docs also describe other perp-shaped products named below; those products are not specified here.

---

## What a Hyperliquid perpetual is

Official Contract specifications page: Hyperliquid perpetuals are derivatives products **without expiration date**. Instead they rely on **funding payments** so the contract converges to the underlying spot price over time. Official docs name that mechanism on the Funding page. This page does not write the funding formula.

Official instrument type on the spec table: **linear perpetual**. Official contract size: **1 unit of the underlying spot asset**. Official underlying: the Hyperliquid oracle index of that underlying spot asset.

Official Perpetual assets page: max leverage varies by asset, ranging from **3x to 40x** (published range on 2026-09-16). That page also lists individual assets; this page does not copy that catalogue.

Sources:

- [Contract specifications](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/contract-specifications.md) — checked 2026-09-16
- [Perpetual assets](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/perpetual-assets.md) — checked 2026-09-16

---

## Collateral and denomination

Official Contract specifications page: the main style of margining is **USDC margining, USDT-denominated linear contracts**. The oracle price is denominated in USDT; the collateral is USDC. Official note on that page: no conversions with the USDC/USDT exchange rate are applied, so these contracts are technically **quanto** contracts where USDT PnL is denominated in USDC.

When the spot asset's primary source of liquidity is USDC-denominated, the oracle price is denominated in USDC. Official text on 2026-09-16: the only USDC-denominated perpetual contracts are **PURR-USD** and **HYPE-USD**, where the most liquid spot oracle source is Hyperliquid spot. Treat those two names as the official published exceptions on this `as-of`, not a live scan.

Source: [Contract specifications](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/contract-specifications.md) — checked 2026-09-16.

---

## Published spec-table fields (dated)

Official Contract specifications table, checked 2026-09-16. Figures can change. They are official published values on that date, not measurements made by this desk.

| Field | Official published value on 2026-09-16 |
|-------|----------------------------------------|
| Initial margin fraction (IMF) | 1 / (leverage set by the user) |
| Maintenance margin fraction (MMF) | Half of maximum initial margin fraction |
| Delivery / expiration | N/A (funding payments every hour) |
| Position limit | N/A |
| Account type | Per-wallet cross or isolated margin |
| Funding impact notional | 20000 USDC for BTC and ETH; 6000 USDC for all other assets |
| Maximum market order value | $30,000,000 if max leverage ≥ 25; $5,000,000 if max leverage in [20, 25); $2,000,000 if max leverage in [10, 20); otherwise $500,000 |
| Maximum limit order value | 10 × maximum market order value |

Official spec table also points mark price at a separate Robust price indices page. That formula is out of scope.

Cross versus isolated appears here only as that official account-type line. How those modes share or fence collateral is risk, not this page.

Source: [Contract specifications](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/contract-specifications.md) — checked 2026-09-16.

---

## Other official perp names (not specified here)

Official docs also name **hyperps**, **index perpetual contracts**, and **HIP-3** (builder-deployed perpetuals). This page does not specify those products.

The same Contract specifications page also describes **recurring outcomes**. Those are not specified here.

---

## Gaps inside this scope

- Live list of listed perpetual tickers: **not on this page**. Official Perpetual assets page exists; it is a catalogue, not copied here.
- Whether PURR-USD and HYPE-USD remain the only USDC-denominated perps after this `as-of`: **unknown here** until the spec page is re-checked.
- Funding formula, premium index, and mark/oracle construction: **unknown here** by scope.
- What “maximum initial margin fraction” equals for each asset, beyond MMF = half of that fraction: **unknown here** except the 3x–40x max-leverage range on Perpetual assets.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/contract-specifications.md | 1 | 2026-09-16 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/perpetual-assets.md | 1 | 2026-09-16 |
