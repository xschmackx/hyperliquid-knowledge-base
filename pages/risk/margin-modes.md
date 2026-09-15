# Margin modes

| Field | Value |
|-------|--------|
| Shelf | Risk and operations (`pages/risk/`) |
| Scope | How collateral is shared or fenced. Not the liquidation engine. Not portfolio-margin risk math. |
| Status | Accepted |
| Page `as-of` | 2026-09-16 |
| Rank | All claims below are Rank 1 |

This page does not cover when liquidation starts, book versus backstop, ADL, the margin-tier leverage table, PMR, LTV, or borrow caps. How unified, standard, and portfolio-margin modes share collateral across DEXs lives on [Account types](../accounts/account-types.md). That table is not retold here.

---

## Cross and isolated

Official Margining page: a margin mode is selected when opening a position.

- **Cross margin** is the default. It shares collateral between all other cross-margin positions.
- **Isolated margin** constrains an asset's collateral to that asset. Official fence: liquidations in that asset do not affect other isolated positions or cross positions. Cross liquidations or other isolated liquidations do not affect the original isolated position.

This page records that fence. It does not specify the liquidation engine.

Source: [Margining](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/margining.md) — checked 2026-09-16.

---

## Strict isolated

Official Margining page: some assets are **strict isolated**. Same as isolated, with the extra constraint that **margin cannot be removed**. Margin is removed **proportionally as the position is closed**.

Which assets are strict isolated on this `as-of` is **unknown here**. Official text names the mode; it does not list the assets on that page.

Source: [Margining](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/margining.md) — checked 2026-09-16.

---

## HIP-3 no-cross

Official Margining page: HIP-3 DEXs also support **no cross** margin mode. Official definition: isolated margin with margin removal enabled, but **no cross**.

How unified versus standard accounts share same-collateral DEX margin is on [Account types](../accounts/account-types.md).

Source: [Margining](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/margining.md) — checked 2026-09-16.

---

## Leverage, IMF, MMF

Official Margining page, dated 2026-09-16:

- Leverage can be set to any **integer between 1 and the max leverage**. Max leverage depends on the asset. The per-asset max table is out of scope.
- Official initial margin to open: `position_size * mark_price / leverage`.
- Official maintenance margin: **half of the initial margin at max leverage**. That is half of maximum IMF.

Official add/remove difference after a position is open:

- Cross: the initial margin used by the position cannot be withdrawn.
- Isolated: adding and removing margin after open is supported (except strict isolated, which cannot remove margin except proportionally on close).
- Unrealized PnL on cross is automatically available as initial margin for new positions. Unrealized PnL on isolated is applied as additional margin for the open position.

Official text: leverage of an existing position can be increased without closing. Leverage is only checked on open. After that, monitoring usage is the user's responsibility. This page does not specify liquidation.

Source: [Margining](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/margining.md) — checked 2026-09-16.

---

## Transfer and withdraw floor

Official Margining page: unrealized PnL can be withdrawn from isolated positions or the cross account only if remaining margin meets both:

- the initial margin requirement, and
- **10%** of the total notional position value of all open positions.

Official formula on 2026-09-16:

`transfer_margin_required = max(initial_margin_required, 0.1 * total_position_value)`

Official meaning of “transferring” on that page: any action that removes margin from a position other than trading. Examples named there: withdrawals, transfer to spot wallet, isolated margin transfers.

Source: [Margining](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/margining.md) — checked 2026-09-16.

---

## Gaps inside this scope

- Which assets are strict isolated: **unknown here**.
- Per-asset max leverage: **unknown here** by scope. Official text says it depends on the asset.
- When liquidation starts, and how the book or backstop acts: **unknown here** by scope.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/margining.md | 1 | 2026-09-16 |
