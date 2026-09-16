# Oracles and marks

| Field | Value |
|-------|--------|
| Shelf | Markets (`pages/markets/`) |
| Scope | Oracle and mark as market-definition primitives as official docs group them. Not trader-facing margin math. Not a funding-payment page. Not a live price dump. Not an API catalog. |
| Status | Accepted |
| Page `as-of` | 2026-09-17 |
| Rank | Claims below are Rank 1 unless tagged |

This page does not retell the validator-operated contract-spec table. That stays on [Perpetual markets](perpetual-markets.md). Funding as a payment mechanism stays on [Funding](funding.md). HIP-3 as a deployer product stays on [HIP-3 builder-deployed perps](hip-3-markets.md). Liquidation math stays on [Liquidations](../risk/liquidations.md). TP/SL trigger structure stays on [Order types and the book](order-types-and-the-book.md). How to read a live oracle or mark over Info stays on [Info endpoint](../tooling/info-endpoint.md).

---

## Official grouping

Official docs split the same two primitives across two Rank 1 leaves. That split is the grouping. This page does not invent a third taxonomy.

- [Oracle](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/oracle.md) sits under HyperCore. It is the spine for how the validator-operated spot oracle is built.
- [Robust price indices](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/robust-price-indices.md) sits under Trading. It is the spine for what mark is and the three-input median.

Official Contract specifications page: the underlying of a validator-operated perp is the Hyperliquid oracle index of that underlying spot asset. The spec-table **Mark price** row points at Robust price indices. Oracle denomination (typical **USDT**; official published exceptions **PURR-USD** and **HYPE-USD** in **USDC**) already lives on [Perpetual markets](perpetual-markets.md). Point. Do not retell the spec table.

Official Funding leaf also points at [Clearinghouse](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/clearinghouse.md) for oracle computation. On 2026-09-17 that Clearinghouse leaf has **no** oracle or mark formula sentences. Treat that pointer as a grouping link. Do not invent clearinghouse content.

Sources: [Oracle](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/oracle.md); [Robust price indices](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/robust-price-indices.md); [Contract specifications](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/contract-specifications.md); [llms.txt](https://hyperliquid.gitbook.io/hyperliquid-docs/llms.txt); [Trading](https://hyperliquid.gitbook.io/hyperliquid-docs/trading.md); [HyperCore](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore.md) — checked 2026-09-17.

---

## What the spot oracle is

Official Oracle leaf: validators publish spot oracle prices for each perp asset every **3 seconds**. Official Robust price indices: “approximately once every three seconds.”

Official uses of that oracle:

- Compute **funding rates**. Payment itself uses **oracle, not mark**. That claim is already accepted on [Funding](funding.md). This page does not reprint the funding formula.
- A **component of mark**.

Official Robust price indices: oracle is a weighted median of CEX prices and is robust because it **does not depend on Hyperliquid's market data at all**.

Sources: [Oracle](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/oracle.md); [Robust price indices](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/robust-price-indices.md) — checked 2026-09-17.

---

## How each validator builds the spot oracle

Official Oracle leaf. Per-validator construction: weighted median of **Binance, OKX, Bybit, Kraken, Kucoin, Gate IO, MEXC, and Hyperliquid spot** mid prices, weights **3, 2, 2, 1, 1, 1, 1, 1** respectively.

Official inclusion rules on the same leaf:

- Perps whose primary spot liquidity is on Hyperliquid (official example **HYPE**) **do not include external sources** until sufficient liquidity is met.
- Perps whose primary spot liquidity is outside Hyperliquid (official example **BTC**) **do not include Hyperliquid spot** in the oracle.

What “sufficient liquidity” equals is **unknown** on these leaves.

Official venue names appear because Hyperliquid published them as inputs. The oracle is not “the Binance price.”

This spot-input list is **not** the same list as mark input #3 below. Do not merge them.

Source: [Oracle](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/oracle.md) — checked 2026-09-17.

---

## Clearinghouse oracle

Official Oracle leaf: the final oracle price used by the clearinghouse is the weighted median of each validator's submitted oracle, validators weighted by **stake**.

Source: [Oracle](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/oracle.md) — checked 2026-09-17.

---

## What mark is

Official Robust price indices: mark price is an unbiased and robust estimate of the fair perp price.

Official published uses of that estimate: **margining, liquidations, triggering TP/SL, computing unrealized pnl**. Name those uses. This page does not write the liquidation, margin, or PnL formulas.

- Liquidations use mark: [Liquidations](../risk/liquidations.md).
- TP/SL triggers use mark: [Order types and the book](order-types-and-the-book.md).
- Unrealized pnl uses mark: official [Entry price and pnl](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/entry-price-and-pnl.md). No accepted corpus page owns that leaf. This page does not open one.

Official: mark is updated whenever validators publish new oracle prices. Therefore mark and oracle are both updated approximately once every **3 seconds**.

Source: [Robust price indices](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/robust-price-indices.md) — checked 2026-09-17.

---

## How mark is built (validator-operated perps)

Official Robust price indices. Mark is the **median** of:

1. Oracle + a **150 second** EMA of (Hyperliquid mid − oracle)
2. Median of best bid, best ask, last trade on Hyperliquid
3. Median of **Binance, OKX, Bybit, Gate IO, MEXC perp** mid prices, weights **3, 2, 2, 1, 1**

If **exactly two** of those three inputs exist, a **30 second** EMA of the median of Hyperliquid best bid, best ask, and last trade is also added to the median inputs. Existence rules beyond that printed clause are **unknown here**.

Official EMA update, for sample at duration `t` since last update:

```
ema = numerator / denominator
numerator -> numerator * exp(-t / 2.5 minutes) + sample * t
denominator -> denominator * exp(-t / 2.5 minutes) + t
```

150 seconds = 2.5 minutes. Treat as the same official constant written two ways. Do not invent another half-life.

Mark input #3 is a **perp** venue list. It is not the oracle **spot** venue list. Kraken, Kucoin, and Hyperliquid spot appear on the oracle list and not on mark input #3.

Source: [Robust price indices](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/robust-price-indices.md) — checked 2026-09-17.

---

## HIP-3 oracle and mark as published definition

Official HIP-3 page: the oracle is completely general at the protocol level. Market definition includes the oracle definition. Market operation includes setting oracle prices. Official: most price indices are not amenable as perp oracle sources. Official: deployers are subject to slashing for all listed markets on their DEX. Slashing tables stay on [HIP-3 builder-deployed perps](hip-3-markets.md). This page does not retell them. No HIP-3 mark formula is published on that product page.

Official `SetOracle` comments on [HIP-3 deployer actions](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/hip-3-deployer-actions.md), checked 2026-09-17. These are market-definition constraints. This page does not document how to sign `perpDeploy`. Use that `.md` path. A duplicate `hip-3-deployer-actions-1.md` exists in the index; it is not a second canon.

- Local mark = median(best bid, best ask, last trade) is used as the new mark-price update together with the submitted prices. Official: `markPxs` outer list can be length **0, 1, or 2**; the median of those inputs plus local mark is the update.
- Calls allowed multiple times; at least **2.5 seconds** between calls.
- Stale marks fall back to local mark after **10 seconds** of no updates; fallback counts as an update for max frequency. Official: **do not rely on the fallback**; deployers expected to call every **3 seconds** even with no changes.
- All prices clamped to **10×** start-of-day value.
- `markPx` moves clamped to **1%** from previous `markPx`.
- `markPx` cannot be updated such that open interest would be **10×** the open-interest cap.
- Fields named on that comment: `dex`; `oraclePxs` (sorted asset/price list); `markPxs` (outer list of inner sorted lists); `externalPerpPxs` (sorted; prevent sudden mark deviations; ideally external, may fall back to an EMA of recent marks; **must include all assets**).

Official HIP-3 product page, eligibility around that external price: each time `externalPerpPx` of an asset moves more than **50%** versus start-of-day, validators review for manipulation slashing. Assets where 50% daily moves are expected more than once a month are ineligible for cross and subject to deployer slashing. That is deployer-duty / eligibility, not liquidation math.

Sources: [HIP-3: Builder-deployed perpetuals](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-3-builder-deployed-perpetuals.md); [HIP-3 deployer actions](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/hip-3-deployer-actions.md) — checked 2026-09-17.

---

## Published substitutes (oracle / mark definition only)

Official product leaves that *replace* the usual spot oracle or mark inputs. Allowed here as definition. This page does not open a separate hyperps, index-perp, or Uniswap-perp corpus page.

### Hyperps

Official [Hyperps](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/hyperps.md): no underlying spot/index required at every moment. The external spot/index oracle is replaced by an **8 hour EWMA of the last day's minutely mark prices**. Formula as printed (official line spells `intial_mark_price` once; quoted, not silently corrected):

```
oracle_price(t) = min[sum_{i=0}^1439 [(t - i minutes < t_list ? initial_mark_price : mark_price(t - i minutes)) * exp(-i/480)] * (1 - exp(-1/480)) / (1 - exp(-3)), intial_mark_price * 4]
```

Official: `a ? b : c` evaluates to `b` if `a` is true and otherwise `c`. Samples: first block after each unix minute; timestamps nearest exact minute; fewer than **480** samples padded with initial mark.

Official mark of hyperps includes the weighted median of **pre-launch CEX perps** as a component of the usual mark formula.

Official caps:

- Hyperp mark ≤ **3×** the 8-hour mark EMA.
- Hyperps with external pre-launch listings: mark ≤ **1.5×** the median external perp price (third mark component).
- Oracle ≤ **4×** the one-month average mark.

Official conversion grouping only: for a hyperp tracking ABC, shortly after ABC/USDT lists on Binance, OKX, or Bybit spot, ABC-USD converts to a normal ABC-USD perp. Trading-advice sentences stay off.

Funding-premium “1% of the usual clamped formula” already lives on [Funding](funding.md). Point. Do not rewrite.

### Index perpetual contracts

Official [Index perpetual contracts](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/index-perpetual-contracts.md): track a formula, not a spot asset; otherwise function as normal perps. Validators periodically publish the index value to L1. The **median of those reports** is used in place of the spot oracle formula to compute funding rates.

Official NFTI-USD definition on that leaf, checked 2026-09-17: a 3-minute EMA of aggregated OpenSea+Blur floors, BAYC divided by 10, plus MAYC, Azuki, DeGods, Pudgy Penguins, and Milady Maker, then `/ 10000`, converted to USDT via the ETH-USDT spot oracle. Official: CryptoPunks were not included because they predate the NFT standard and are not listed on those marketplaces.

```
Index = 3 minute ema of [(BAYC floor price / 10) + (MAYC floor price) + (Azuki floor price) + (DeGods floor price) + (Pudgy Penguins floor price) + (Milady Maker floor price)] / 10000
```

Official FRIEND-USD text on the same leaf is a dated series of index definitions (August / September / October windows). Several headings have **no year**. Treat those rows as the official printed definitions on this check, not a proof the contracts still trade. Whether they remain listed is **unknown here**. This page does not reprint the subject lists.

### Uniswap perpetuals

Official [Uniswap perpetuals](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/uniswap-perpetuals.md): some perps use Uniswap V2 or V3 AMM price as the underlying spot. Pool prices are converted to USDT via **robust CEX oracle prices**. Official example pool on this check: RLB `0x510100d5143e011db24e2aa38abe85d73d5b2177`. Official product rule on that leaf: these contracts are **isolated-only**. Isolated versus cross as a margin mode stays on [Margin modes](../risk/margin-modes.md). This page does not write that math.

Sources: the three official product leaves — checked 2026-09-17.

---

## Where current prices are published (pointer only)

Accepted [Info endpoint](../tooling/info-endpoint.md) already names `metaAndAssetCtxs` under an official heading that includes mark price. Point. Do not reprint request shapes. Do not dump live oracle or mark values. Do not walk `/info`.

---

## Gaps inside this scope

- What “sufficient liquidity” equals before an HL-primary asset includes external oracle sources: **unknown** on these leaves.
- Live per-market oracle and mark values: **unknown here** by scope.
- Whether NFTI-USD or FRIEND-USD remain listed: **unknown here**. FRIEND-USD windows on the index leaf have no year on several headings.
- HIP-3 per-market oracle specs: **unknown here** beyond deployer-defined and the `SetOracle` constraints above.
- Clearinghouse-leaf oracle or mark formulas: **not present** on that leaf on this check.
- Mark-component existence rules beyond the printed “exactly two of three” clause: **unknown here**.
- Entry-price / PnL worked examples: **unknown here** by scope.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/oracle.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/robust-price-indices.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/contract-specifications.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-3-builder-deployed-perpetuals.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/hip-3-deployer-actions.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/hyperps.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/index-perpetual-contracts.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/uniswap-perpetuals.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/entry-price-and-pnl.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/llms.txt | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/clearinghouse.md | 1 | 2026-09-17 |
