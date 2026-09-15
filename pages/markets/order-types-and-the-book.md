# Order types and the book

| Field | Value |
|-------|--------|
| Shelf | Markets (`pages/markets/`) |
| Scope | Orders, cancels, triggers, and book behaviour as market structure. Not an API cookbook. Not fees. Not liquidation. |
| Status | Accepted |
| Page `as-of` | 2026-09-16 |
| Rank | All claims below are Rank 1 |

This page does not cover REST, WebSocket, or SDK request bodies, fee schedules, margin or liquidation math, HIP-2 strategy, or how to click the app. Perpetual and spot product identity live on [Perpetual markets](perpetual-markets.md) and [Spot markets](spot-markets.md).

---

## The book

Official Order book page: the book is **fully on-chain**. Orders are added where price is an integer multiple of the **tick size** and size is an integer multiple of the **lot size**. Orders are matched in **price-time priority**.

That page points at a HyperCore order-book implementation note for further detail. Implementation internals beyond those three rules are **unknown here** unless restated on the pages checked below.

What the live tick and lot are for each market is **unknown here**. Official text names the multiples; it does not list every market's sizes on these pages.

Source: [Order book](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/order-book.md) — checked 2026-09-16.

---

## Limit vs market

Official Order types page:

- **Market:** an order that executes immediately at the current market price.
- **Limit:** an order that executes at the selected limit price or better.

Source: [Order types](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/order-types.md) — checked 2026-09-16.

---

## Time-in-force names

Official Order types page, under order options:

| Official name | Official published behaviour on 2026-09-16 |
|---------------|--------------------------------------------|
| Good Til Cancel (GTC) | Rests on the book until it is filled or canceled. |
| Post Only (ALO) | Added to the book but does not execute immediately. Executed only as a resting order. |
| Immediate or Cancel (IOC) | Canceled if it is not immediately filled. |

Source: [Order types](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/order-types.md) — checked 2026-09-16.

---

## Reduce-only

Official Order types page: **Reduce Only** is an order that reduces a current position as opposed to opening a new position in the opposite direction.

Source: [Order types](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/order-types.md) — checked 2026-09-16.

---

## Triggers and TP/SL

Official Order types page names this trigger family:

| Official name | Official published behaviour on 2026-09-16 |
|---------------|--------------------------------------------|
| Stop Market | A market order activated when price reaches the selected trigger price. For long orders the trigger must be **higher than mid**. For short orders the trigger must be **lower than mid**. |
| Stop Limit | A limit order activated when price reaches the selected trigger price. |
| Take Market | A market order activated when price reaches the selected trigger price. For long orders the trigger must be **lower than mid**. For short orders the trigger must be **higher than mid**. |
| Take Limit | A limit order activated when price reaches the selected trigger price. |
| Take Profit (TP) | Triggers when the take-profit price is reached. Official text: TP and SL are automatically market orders; a limit price and a position amount can be set. |
| Stop Loss (SL) | Triggers when the stop-loss price is reached. Same official note as TP. |

Official Take profit and stop loss page: the **mark price** is used to trigger TP/SL orders.

Whether stop/take triggers use mid, mark, or both, outside the sentences above, is **unknown here**. This page records the mid-price rule where Order types states it, and the mark-price rule where the TP/SL page states it. It does not collapse those two official sentences into one index.

Sources:

- [Order types](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/order-types.md) — checked 2026-09-16
- [Take profit and stop loss orders (TP/SL)](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/take-profit-and-stop-loss-orders-tp-sl.md) — checked 2026-09-16

---

## Scale and TWAP (named types; dated constraints)

Official Order types page names **Scale** as multiple limit orders in a set price range. Further Scale constraints are **unknown here**.

Official Order types page names **TWAP** as a large order divided into smaller suborders and executed at regular intervals, based on order size and running time. Published constraints on 2026-09-16:

| Constraint | Official published figure |
|------------|---------------------------|
| Minimum interval | 30 seconds |
| Maximum suborder slippage | 3% |
| Randomize (if enabled) | each sub-order size adjusted randomly up to ±20% of the original trade size |
| Running time | 5 minutes to 7 days |
| Minimum total order size | $100 |
| Catch-up cap | later suborders subject to 3 times the normal suborder size |

Official TWAP text also: a trigger price can activate the TWAP when mark price reaches it; a max/min price can terminate it when mark price reaches that stop. Suborders that do not fill can leave the TWAP behind its elapsed-time target. Official text: TWAP suborders do not fill during the post-only period of a network upgrade, like normal market orders.

Official Order types page does **not** say whether the Scale scheduler or the TWAP scheduler itself runs on L1 or in a client. That is a written gap. Do not treat Scale or TWAP as proven L1 matching logic from these pages.

Source: [Order types](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/order-types.md) — checked 2026-09-16.

---

## Chase

Official Order types page: **Chase** is a Post Only (ALO) limit order that automatically re-prices to track the best bid or ask until it is filled or terminated. Official placement: one tick above the best bid (buys) or one tick below the best ask (sells), or at the best bid/ask when the spread is a single tick.

Official sentence on that page: Chase orders **run in the browser tab where they are created**, and up to **5** can be active at once.

This page does not treat Chase as L1 matching. Official text places it in the browser tab. 5 and one tick are official published figures on 2026-09-16.

Source: [Order types](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/order-types.md) — checked 2026-09-16.

---

## Gaps inside this scope

- Whether Scale and TWAP scheduling execute on L1 or in a client: **unknown here**. Official pages name the types and constraints; they do not name the execution venue except that TWAP suborders behave like market orders once sent, including during a network-upgrade post-only period.
- Live tick and lot for each market: **unknown here**.
- Cancel matching beyond GTC “filled or canceled” and IOC “canceled if not immediately filled”: **unknown here**.
- Self-trade prevention: official docs have a separate page; it is not specified here.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/order-book.md | 1 | 2026-09-16 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/order-types.md | 1 | 2026-09-16 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/take-profit-and-stop-loss-orders-tp-sl.md | 1 | 2026-09-16 |
