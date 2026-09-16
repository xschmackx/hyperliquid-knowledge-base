# Funding

| Field | Value |
|-------|--------|
| Shelf | Markets (`pages/markets/`) |
| Scope | Funding as a market mechanism as official docs group it. Not a fee schedule. Not margin or liquidation math. Not a live rate dump. Not an API catalog. |
| Status | Accepted |
| Page `as-of` | 2026-09-17 |
| Rank | Claims below are Rank 1 unless tagged |

This page does not retell the validator-operated contract-spec table. That stays on [Perpetual markets](perpetual-markets.md). HIP-3 as a deployer product stays on [HIP-3 builder-deployed perps](hip-3-markets.md). How to read a rate over Info or WebSocket stays on [Info endpoint](../tooling/info-endpoint.md) and [WebSocket](../tooling/websocket.md). This page does not write mark-price construction.

---

## What funding is

Official Funding leaf: funding rates for crypto perpetual contracts are a mechanism used to keep the contract price close to the underlying asset's price.

Official transfer: a periodic fee paid by one side (long or short) to the other side. Official: funding is **purely peer-to-peer; no fees are collected on the payments.** That sentence is the transfer rule. It is not a trading-fee schedule.

Official Contract specifications page: Hyperliquid perpetuals have no expiration. They rely on funding payments to converge to the underlying spot price over time. Spec-table delivery / expiration on that page: **N/A (funding payments every hour)**.

Sources:

- [Funding](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/funding.md) — checked 2026-09-17
- [Contract specifications](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/contract-specifications.md) — checked 2026-09-17
- [Perpetual markets](perpetual-markets.md) (`as-of` 2026-09-16) already states that funding payments exist and leaves the formula off. This page is that formula.

---

## Cadence

Official Funding leaf:

- Paid **every hour**. Added or subtracted from contract holders' balances at the funding interval.
- The funding rate formula applies to an **8 hour** funding rate. Funding is paid every hour at **one eighth** of the computed rate for each hour.
- Official: the funding cap and funding interval **do not depend on the asset**.

Source: [Funding](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/funding.md) — checked 2026-09-17.

---

## Two published components

Official Funding leaf. Vanilla (validator-operated) interest is a published constant:

- Interest-rate component, predetermined at **0.01% every 8 hours**, which the same leaf also writes as **0.00125% every hour**, or **11.6% APR paid to short**. Official gloss: difference in cost to borrow USD versus spot crypto. Official also: “for consistency with CEXs.” That phrase is official gloss. This page does not import another venue's formula.
- Premium component from the difference between the perpetual contract's price and the underlying spot oracle price. If the contract is above oracle, premium and funding rate are positive and **long pays short**. If below, funding rate is negative and **short pays long**.

HIP-3 interest is not that constant. See the HIP-3 section below.

Source: [Funding](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/funding.md) — checked 2026-09-17.

---

## Formula as printed

Official Funding leaf:

```
Funding Rate (F) = Average Premium Index (P) + clamp (interest rate - Premium Index (P), -0.0005, 0.0005)
```

Premium is sampled every **5 seconds** and averaged over the hour.

Vanilla premium as printed:

```
premium = impact_price_difference / oracle_price
```

where

```
impact_price_difference = max(impact_bid_px - oracle_px, 0) - max(oracle_px - impact_ask_px, 0)
```

`impact_bid_px` / `impact_ask_px` are average execution prices to trade `impact_notional_usd` on each side.

Official impact notional on the Contract specifications table, checked 2026-09-17: **20000 USDC for BTC and ETH**; **6000 USDC for all other assets**. Those are mechanism parameters. They are not a live catalogue of markets. Do not invent other notionals. The HIP-3 product page does not publish a HIP-3 funding-impact table; this page does not invent one from the validator-operated spec table.

Source: [Funding](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/funding.md); [Contract specifications](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/contract-specifications.md) — checked 2026-09-17.

---

## Payment uses oracle, not mark

Official Funding leaf: funding payment at end of interval is

```
position_size * oracle_price * funding_rate
```

Official emphasis: spot **oracle** price converts size to notional, **not the mark price**.

Official oracle-for-funding sentences, not a mark recipe:

- [Robust price indices](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/robust-price-indices.md): “Oracle price is used to compute funding rates.”
- [Oracle](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/oracle.md): validators publish spot oracle prices for each perp asset every **3 seconds**; those prices are used to compute funding rates.

The Funding leaf also points at [Clearinghouse](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/clearinghouse.md) for how validators compute oracle prices. On 2026-09-17 that Clearinghouse leaf has **no** funding or oracle-formula sentences. Treat that pointer as a grouping link. Do not invent clearinghouse content. Mark-price construction stays off this page.

Sources: [Funding](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/funding.md); [Robust price indices](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/robust-price-indices.md); [Oracle](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/oracle.md) — checked 2026-09-17.

---

## Cap

Official Funding leaf: funding is capped at **4%/hour**. Official: much less aggressive than CEX counterparts. Official: the funding cap and funding interval do not depend on the asset.

This 4%/hour cap is not the same object as the vanilla formula clamp of **±0.0005** on `(interest − premium)`, and not the same object as the HIP-3 `setFundingClamps` default of **0.0003**. Do not collapse the three.

Source: [Funding](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/funding.md) — checked 2026-09-17.

---

## HIP-3 premium and deployer knobs

Official Funding leaf, HIP-3 premium as printed on the **same** leaf — not flattened into the vanilla formula:

```
premium = (0.5 * (impact_bid_px + impact_ask_px) / oracle_px) - 1
```

Official reason: HIP-3 perps use a more responsive premium so deployers can express a larger range of funding behaviors with the funding-rate multiplier and interest rate.

Official type comments on [HIP-3 deployer actions](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/hip-3-deployer-actions.md), checked 2026-09-17. These are published product knobs. This page does not document how to sign `perpDeploy`.

| Knob | Official published range |
|------|--------------------------|
| Funding-rate multipliers | between **0 and 10**; scale the funding rate |
| 8-hour interest rates | between **−0.01 and 0.01**; used as the interest-rate component |
| 8-hour clamps | between **0 and 0.01**; bound how far the funding rate can move away from the average premium toward the interest rate; **default 0.0003** |

Vanilla interest is the published constant above. HIP-3 interest is the deployer-set 8-hour value in that range. Current per-asset HIP-3 multiplier / interest / clamp values are **unknown here**.

Point at [HIP-3 builder-deployed perps](hip-3-markets.md). Do not rewrite that page.

Sources: [Funding](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/funding.md); [HIP-3 deployer actions](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/hip-3-deployer-actions.md) — checked 2026-09-17.

---

## Official siblings that change the oracle substitute

Official product leaves that name a funding deviation. One-line grouping each. No accepted hyperps or index-perp corpus page exists. This page does not open one and does not specify hyperp EWMA or NFTI composition.

- [Hyperps](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/hyperps.md): funding is determined relative to a moving-average hyperp mark in place of the usual spot price. Official: “Funding rate premium samples are computed as 1% of the usual clamped interest rate and premium formula.”
- [Index perpetual contracts](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/index-perpetual-contracts.md): validator-reported index values are used in place of the spot oracle formula to compute funding rates.

Sources: those two official leaves — checked 2026-09-17.

---

## Official numerical example (as printed)

The Funding leaf walks this illustration. Quoted as published. Not reconciled here.

1. Interest rate is 0.01% (fixed).
2. Perpetual is trading at a premium; impact bid **$10,100**; spot **$10,000**.
3. Premium index described on the leaf as the **$100** difference, then computed as `($10,100 − $10,000) / $10,000` = **0.01 (1%)**.
4. Funding interval named as **1 hour**.
5. Long **10** contracts, each **1 BTC** (size is named; the leaf does not finish a dollar payment from it).

Then: clamp interest-minus-premium at **±0.05%** → **−0.05%**. Funding rate = 1% + (−0.05%) = **0.95%**.

The same leaf says the formula applies to an 8-hour rate and hourly payment is one eighth of the computed rate. The example lands on 0.95% for a 1-hour interval without applying that one-eighth sentence, and it writes the clamp as ±0.05% while the formula line writes `±0.0005`. Whether the printed example is meant to be pre- or post-1/8 is **unknown here**. The tension is left written. This page does not “correct” units.

Source: [Funding](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/funding.md) — checked 2026-09-17.

---

## Where current rates are published (pointer only)

Official Info and WebSocket leaves name reads for current and historical funding. Accepted corpus pages already list those names. Point. Do not reprint request shapes or live rates. Do not turn this page into a cross-venue rate table.

- [Info endpoint](../tooling/info-endpoint.md): `metaAndAssetCtxs` (current funding), `userFunding`, `fundingHistory`, `predictedFundings`.
- [WebSocket](../tooling/websocket.md): `userFundings`.

`predictedFundings` on the official Info leaf returns other-venue labels in its example. That is a read-shape. It is not a catalogue of Hyperliquid rates.

---

## Official grouping

Official docs index [`llms.txt`](https://hyperliquid.gitbook.io/hyperliquid-docs/llms.txt) places the Funding leaf under Trading, next to Perpetual assets, Contract specifications, Robust price indices, and sibling product leaves. Official Trading hub: [Trading](https://hyperliquid.gitbook.io/hyperliquid-docs/trading.md).

---

## Gaps inside this scope

- Live per-market funding rates: **unknown here** by scope.
- Whether the printed numerical example is pre- or post-1/8, and whether ±0.05% in the example is the same object as formula `±0.0005`: **unknown here**. Both are official text on the same leaf.
- Current HIP-3 per-asset multiplier, interest, and clamp values: **unknown here**.
- HIP-3 funding-impact notional: **not published** on the HIP-3 product page.
- Hyperp and index internals beyond the official one-line deviations: **unknown here** by scope.
- Mark-price construction: **unknown here** by scope.
- Clearinghouse funding or oracle-formula sentences: **not present** on that leaf on this check.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/funding.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/contract-specifications.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/robust-price-indices.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/oracle.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/hip-3-deployer-actions.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/hyperps.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/index-perpetual-contracts.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/llms.txt | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/clearinghouse.md | 1 | 2026-09-17 |
