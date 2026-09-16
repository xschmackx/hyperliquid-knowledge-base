# Auto-deleveraging

| Field | Value |
|-------|--------|
| Shelf | Risk and operations (`pages/risk/`) |
| Scope | Official auto-deleveraging behaviour as published. Not the liquidation catalog. Not a margin-modes catalog. Not an API catalog. |
| Status | Accepted |
| Page `as-of` | 2026-09-17 |
| Rank | Claims below are Rank 1 unless tagged |

This page does not retell book attempt, partial liquidation, or the liquidator vault. Those stay on [Liquidations](liquidations.md). Isolated versus cross as a collateral fence stays on [Margin modes](margin-modes.md). This page is not a second liquidation page.

---

## What auto-deleveraging is for

Official Auto-deleveraging page:

- Auto-deleveraging strictly ensures that the platform stays solvent.
- Auto-deleveraging is an important final safeguard on the solvency of the platform.
- Close against the underwater user is published as ensuring that the platform has no bad debt.

Official invariant on the same page: there is a strict invariant that under all operations, a user who has no open positions will not socialize any losses of the platform.

The official page title is Auto-deleveraging. That page also writes “ADL queue logic.” This page uses both names that way.

Source: [Auto-deleveraging](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/auto-deleveraging.md) — checked 2026-09-17.

---

## Official grouping relative to liquidation

Official docs list Liquidations and Auto-deleveraging as two sibling leaves under `trading/`. They are not one page.

On this check:

- The Liquidations page does not name auto-deleveraging. Book attempt, partial-liquidation rule, and backstop through the liquidator vault stay on [Liquidations](liquidations.md).
- The Auto-deleveraging page does not retell book versus backstop. It starts when a user's account value or isolated position value becomes negative. It names backstop-liquidated positions once: they have no special treatment in the ADL queue logic.

Official texts do not draw an arrow such as “ADL always follows backstop.” This page does not invent that sequence.

Official Margining and Portfolio margin pages, on this check, do not name ADL. This page does not infer a portfolio-margin-specific ADL rule. What “isolated” versus account value names as a fence stays on [Margin modes](margin-modes.md).

Sources: [Auto-deleveraging](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/auto-deleveraging.md); [Liquidations](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/liquidations.md); [llms.txt](https://hyperliquid.gitbook.io/hyperliquid-docs/llms.txt) — checked 2026-09-17.

---

## Published behaviour

Official Auto-deleveraging page, checked 2026-09-17. Quoted as published. Not tidied into a third formula.

**Trigger.** If a user's account value or isolated position value becomes negative.

**Who is selected.** Users on the opposite side of the position are ranked by unrealized pnl and leverage used.

**Sorting index** (official string, published to determine the affected users in profit):

`(mark_price / entry_price) * (notional_position / account_value)`

**What happens.** Those traders' positions are closed at the previous mark price against the now underwater user.

**Queue versus backstop.** Backstop liquidated positions have no special treatment in the ADL queue logic.

No other official threshold, percent, cooldown, or size cap is published on that page on this check. Liquidation figures already recorded on [Liquidations](liquidations.md) are not imported here as ADL parameters.

“Previous mark price” is official and undefined beyond those three words on that page. This page does not gloss it as last-trade or oracle.

The sorting index uses `account_value`. How that term applies when the trigger was isolated position value is **unknown** on Rank 1.

Source: [Auto-deleveraging](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/auto-deleveraging.md) — checked 2026-09-17.

---

## Gaps inside this scope

- Exact walk of the ranked opposite-side queue (how much is closed, in what slices): **unknown here**. Official text does not say how far down the ranked list is taken, whether closes are partial, or how isolated opposite positions are sized.
- Meaning of `account_value` in the sorting index when the trigger was isolated position value: **unknown here**.
- Meaning of “previous mark price” beyond the official three words: **unknown here**.
- Whether ADL differs under portfolio margin or on HIP-3 DEXs: **unknown here**. Those official pages do not name ADL on this check.
- Historical frequency, UI warnings, and any API field for ADL rank: **unknown here**.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/auto-deleveraging.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/liquidations.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/llms.txt | 1 | 2026-09-17 |
