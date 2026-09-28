# Initial and maintenance margin

| Field | Value |
|-------|--------|
| Shelf | Risk and operations (`pages/risk/`) |
| Scope | What official docs call initial margin versus maintenance margin, and how each is used as risk. Not the margin-tier tables. Not portfolio margin. Not HIP-3 margin across DEXs. Not auto-deleveraging. Not the liquidation engine. Not an API catalog. |
| Status | Accepted |
| Page `as-of` | 2026-09-28 |
| Rank | All claims below are Rank 1 |

This page does not retell how collateral is shared or fenced. That stays on [Margin modes](margin-modes.md). Book attempt, partial liquidation, backstop, and the liquidation-price formula stay on [Liquidations](liquidations.md). Tier tables and the continuous maintenance-margin formula stay on [Margin tiers](margin-tiers.md). Portfolio maintenance and PMR stay on [Portfolio margin](portfolio-margin.md). HIP-3 cross-DEX share and no-cross stay on [HIP-3 margin](hip-3-margin.md) and [Margin modes](margin-modes.md). Auto-deleveraging stays on [Auto-deleveraging](auto-deleveraging.md).

---

## Official names

Official docs use two pairs of names for the same split.

Contract specifications table, checked 2026-09-28:

- **Initial margin fraction** = `1 / (leverage set by user)`.
- **Maintenance margin fraction** = **half of maximum initial margin fraction**.

Margining and Liquidations use **initial margin** and **maintenance margin** for the same split. This page uses those official names. It does not invent IMR or MMR. The tiers page’s `maintenance_margin_rate` is a tiers-page name; that formula stays on [Margin tiers](margin-tiers.md).

Sources: [Contract specifications](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/contract-specifications.md); [Margining](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/margining.md) — checked 2026-09-28.

---

## Initial margin: open or increase

Official Margining page: the margin required to open a position is `position_size * mark_price / leverage`.

That leverage is the user’s. Official contract specifications: initial margin fraction is `1 / (leverage set by user)`. Official Margining page: leverage can be any integer from 1 to the max leverage. Max leverage depends on the asset. How max leverage changes with position notional is the tier table on [Margin tiers](margin-tiers.md). This page does not ingest that table.

Official check is on open, not continuous:

- The leverage of an existing position can be increased without closing the position.
- Leverage is only checked upon opening a position.
- After that, monitoring usage is the user’s responsibility. Official Margining page states that. This page does not claim a continuous initial-margin check.

How initial margin attaches after open, as official Margining states it (the mode catalog stays on [Margin modes](margin-modes.md)):

- Cross: the initial margin used by the position cannot be withdrawn.
- Isolated: adding and removing margin after opening is supported. Strict isolated cannot remove margin except proportionally on close. Which assets are strict isolated is unknown here.
- Unrealized PnL on cross is automatically available as initial margin for new positions. Unrealized PnL on isolated is applied as additional margin for the open position.

The transfer floor is not maintenance margin. Official Margining page: unrealized PnL can be withdrawn from isolated positions or the cross account only if remaining margin meets both the initial margin requirement and 10% of the total notional position value of all open positions.

`transfer_margin_required = max(initial_margin_required, 0.1 * total_position_value)`

Official meaning of “transferring” on that page: any action that removes margin from a position other than trading. Examples named there: withdrawals, transfer to spot wallet, isolated margin transfers. The floor is already recorded on [Margin modes](margin-modes.md). This page does not catalog transfers.

Sources: [Margining](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/margining.md); [Contract specifications](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/contract-specifications.md) — checked 2026-09-28.

---

## Maintenance margin: when liquidation risk starts

Maintenance margin fraction is not half of the user’s initial margin fraction. Official contract specifications: it is half of the **maximum** initial margin fraction. Official Margining, Liquidations, and Perpetual assets pages say the same rule in these words: maintenance margin is half of the initial margin at max leverage.

A user at 2x on an asset whose max leverage is 20x still has maintenance margin at the 20x-max rate, not at half of 2x. That follows from the official rule above. It is not a separate published worked example. Official example on Perpetual assets, checked 2026-09-28: if max leverage is 20x, the maintenance margin is 2.5%. The same 20x → 2.5% example is on the Margin tiers page as `maintenance_margin_rate`. How that rate is applied per tier, including the deduction that keeps total maintenance margin continuous, stays on [Margin tiers](margin-tiers.md). This page does not paste tier tables.

Published range on the Liquidations page, checked 2026-09-28: max leverage named there is 3x to 40x, and maintenance margin is between 1.25% (40x max-leverage assets) and 16.7% (3x max-leverage assets), depending on the asset. These percents are the official page on this `as-of`. They are not a live `meta` snapshot.

Two official trigger wordings exist. This page records both. It does not invent a merged formula. Both are already on [Liquidations](liquidations.md).

- Liquidations page: a liquidation event occurs when account equity falls below the maintenance margin.
- Margining page: cross positions are liquidated when the account value (including unrealized PnL) is less than the maintenance margin times the total open notional position. Isolated positions use the same maintenance-margin logic, with inputs limited to the isolated margin and the notional value of that isolated position.

What happens after that threshold — book attempt, partials, backstop at 2/3 of maintenance margin, liquidation price — stays on [Liquidations](liquidations.md). Mark price is what that page says liquidations use. How the mark is built stays on [Oracles and marks](../markets/oracles-and-marks.md). This page does not retell either.

Portfolio-margin liquidation is not this maintenance-margin sentence. Official portfolio margin uses a separate portfolio maintenance margin and a PMR trigger. That stays on [Portfolio margin](portfolio-margin.md).

HIP-3: initial and maintenance margin still apply to the position that is open. How margin is shared across HIP-3 DEXs, and no-cross, stay on [HIP-3 margin](hip-3-margin.md) and [Margin modes](margin-modes.md). Whether every HIP-3 perp uses the same initial-margin-fraction / maintenance-margin-fraction sentence as the main contract-specifications table is unknown here.

Auto-deleveraging is not initial margin and not maintenance margin. It stays on [Auto-deleveraging](auto-deleveraging.md).

Sources: [Contract specifications](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/contract-specifications.md); [Margining](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/margining.md); [Liquidations](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/liquidations.md); [Perpetual assets](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/perpetual-assets.md); [Margin tiers](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/margin-tiers.md) — checked 2026-09-28.

---

## Gaps inside this scope

- Whether every HIP-3 perp uses the same initial-margin-fraction and maintenance-margin-fraction sentence as the main contract-specifications table: **unknown here**.
- Live `meta` versus this docs snapshot on a later day: **unknown here**. Live `meta` was not walked on this check.
- Which assets are strict isolated: **unknown here**. Official Margining names the mode; it does not list the assets on that page.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/margining.md | 1 | 2026-09-28 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/liquidations.md | 1 | 2026-09-28 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/contract-specifications.md | 1 | 2026-09-28 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/perpetual-assets.md | 1 | 2026-09-28 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/margin-tiers.md | 1 | 2026-09-28 |
