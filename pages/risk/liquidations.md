# Liquidations

| Field | Value |
|-------|--------|
| Shelf | Risk and operations (`pages/risk/`) |
| Scope | When liquidation starts, book attempt versus backstop, isolated versus cross effects. Not auto-deleveraging. Not portfolio-margin liquidations. Not the margin-tier table. |
| Status | Accepted |
| Page `as-of` | 2026-09-16 |
| Rank | All claims below are Rank 1 |

This page does not cover auto-deleveraging, portfolio-margin or borrow liquidation, or the per-asset max-leverage table. How collateral is shared or fenced lives on [Margin modes](margin-modes.md). That page is not retold here.

---

## When liquidation starts

Official Liquidations page: a liquidation event occurs when account equity falls below the maintenance margin.

Official maintenance margin on that page: **half of the initial margin at max leverage**. Official range of max leverage named there: **3x to 40x**. Official maintenance-margin range that follows: **1.25%** (40x max-leverage assets) to **16.7%** (3x max-leverage assets), depending on the asset.

Official Margining page, same check date, states the trigger in these words:

- Cross: the account value, including unrealized PnL, is less than the maintenance margin times the total open notional position.
- Isolated: the same maintenance-margin logic, with inputs limited to the isolated margin and the notional value of that isolated position.

This page records both official wordings. It does not invent a third formula that merges them.

Sources: [Liquidations](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/liquidations.md); [Margining](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/margining.md) — checked 2026-09-16.

---

## Book attempt

Official Liquidations page: when equity is below maintenance margin, positions are first attempted to be **entirely closed by sending market orders to the book**. The orders are for the **full size** of the position, except under the partial-liquidation rule below. The book close may be full or partial.

If positions are closed enough that maintenance-margin requirements are met, **any remaining collateral remains with the trader**.

Official motivation on that page: most liquidations are sent to the book so users compete for the flow and the liquidated user can keep remaining margin. Official comparison named there: unlike CEXs, there is **no clearance fee** on liquidations.

Source: [Liquidations](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/liquidations.md) — checked 2026-09-16.

---

## Partial liquidations

Official Liquidations page, dated 2026-09-16:

- For liquidatable positions larger than **100k USDC** (**10k USDC on testnet**), only **20%** of the position is sent as a market liquidation order to the book.
- After a block in which any position of a user is partially liquidated, there is a **30-second cooldown**.
- During that cooldown, all market liquidation orders for that user are for the **entire position**.

Source: [Liquidations](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/liquidations.md) — checked 2026-09-16.

---

## Backstop

Official Liquidations page: if account equity drops below **2/3 of the maintenance margin** without a successful book liquidation, a **backstop liquidation** happens through the **liquidator vault**.

Official vault description on that page: the liquidator vault is a component strategy of **HLP**. Positions below 2/3 of maintenance margin can be taken over by that vault. Official claim: on average, backstop liquidations are profitable for the liquidator, and that PnL stream goes to the community through HLP.

Official buffer: during backstop liquidation, **maintenance margin is not returned to the user**. Official reason named there: the vault needs a buffer so backstop liquidations are profitable on average. Official user-side note on that page: to avoid losing the maintenance margin, traders can place stop-loss orders or exit before mark price reaches the liquidation price. That note is not trading advice on this page; it is the official wording of the buffer.

Source: [Liquidations](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/liquidations.md) — checked 2026-09-16.

---

## Isolated versus cross effects

Official Liquidations page:

- **Cross, backstop:** the trader's cross positions and cross margin are all transferred to the liquidator. If the trader has no isolated positions, the trader ends with **zero account equity**.
- **Isolated, backstop:** that isolated position and isolated margin are transferred to the liquidator. The user's cross margin and cross positions are untouched.

Official Margining page, same fence already recorded on [Margin modes](margin-modes.md): liquidations in an isolated asset do not affect other isolated positions or cross positions, and the reverse is also official.

Source: [Liquidations](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/liquidations.md); [Margining](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/margining.md) — checked 2026-09-16.

---

## Mark price

Official Liquidations page: liquidations use the **mark price**, which combines external CEX prices with Hyperliquid's book state. Official note on that page: in high volatility or on highly leveraged positions, mark price may differ significantly from book price.

Source: [Liquidations](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/liquidations.md) — checked 2026-09-16.

---

## Published liquidation price

Official Liquidations page:

- An estimated liquidation price is shown when entering a trade. Official limit: that estimate may be inaccurate versus the position's estimated liquidation price because book liquidity changes.
- Once a position is open, a liquidation price is shown. Official certainty: it has the entry price. Official remaining limits: funding payments, or changes in unrealized PnL in other positions for cross margin, can still move the actual liquidation price.
- Actual liquidation price for **cross** does not depend on the leverage set. A lower-leverage cross position simply uses more collateral.
- Actual liquidation price for **isolated** does depend on leverage set, because isolated margin allocated depends on the initial margin set.
- When there is insufficient margin to make the trade, the estimate assumes the account is topped up to the initial margin requirement.

Official formula on 2026-09-16:

`liq_price = price - side * margin_available / position_size / (1 - l * side)`

where

- `l = 1 / MAINTENANCE_LEVERAGE`
- For assets with margin tiers, maintenance leverage depends on the unique margin tier corresponding to the position value **at the liquidation price**
- `side = 1` for long and `-1` for short
- `margin_available` (cross) = `account_value - maintenance_margin_required`
- `margin_available` (isolated) = `isolated_margin - maintenance_margin_required`

The margin-tier table itself is out of scope.

Source: [Liquidations](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/liquidations.md) — checked 2026-09-16.

---

## Gaps inside this scope

- How HIP-3 DEX liquidations differ from the Liquidations page above: **unknown here**. That official page does not name HIP-3.
- How book-attempt market orders interact with a multi-position cross book when only some contracts are liquidatable: **unknown here** beyond the official plural wording that "the positions" are sent to the book.
- Auto-deleveraging after account or isolated value goes negative: **unknown here** by scope.
- Portfolio-margin and borrow liquidation, including the official note that those liquidations skip the market-book phase: **unknown here** by scope.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/liquidations.md | 1 | 2026-09-16 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/margining.md | 1 | 2026-09-16 |
