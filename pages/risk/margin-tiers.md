# Margin tiers

| Field | Value |
|-------|--------|
| Shelf | Risk and operations (`pages/risk/`) |
| Scope | Official margin-tier behaviour as published: position-size tiers that change max leverage. Not the margin-modes catalog. Not the liquidation catalog. Not the ADL catalog. Not the portfolio-margin catalog. Not an API catalog. |
| Status | Accepted |
| Page `as-of` | 2026-09-17 |
| Rank | Claims below are Rank 1 unless tagged |

This page does not retell isolated versus cross. That stays on [Margin modes](margin-modes.md). Book attempt, partial liquidation, and backstop stay on [Liquidations](liquidations.md). Auto-deleveraging stays on [Auto-deleveraging](auto-deleveraging.md). PMR and borrow liquidation stay on [Portfolio margin](portfolio-margin.md). Live table lookup is the Info `meta` type on [Info endpoint](../tooling/info-endpoint.md). This page does not ingest that catalog.

---

## What margin tiers are for

Official Margin tiers page:

- Like most centralized exchanges, Hyperliquid uses a **tiered leverage formula**.
- Position notional changes **max leverage**.
- Maintenance margin is computed from those tiers so that total maintenance margin is a **continuous function of position size**.
- Official: `maintenance_margin_rate` and `maintenance_deduction` **depend only on the margin tiers, not the asset**.
- Official: margin tables have **unique IDs**; tiers can be found in the **`meta` Info response**.
- Official: for IDs **less than 50**, there is a **single tier with max leverage equal to the ID**.

Which *table* an asset sits on still depends on the asset. Rate and deduction depend only on the tiers.

The `meta` lookup is a pointer at [Info endpoint](../tooling/info-endpoint.md) (`type: meta`). This page does not ingest Info types.

Source: [Margin tiers](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/margin-tiers.md) — checked 2026-09-17.

---

## Official grouping vs other risk pages

Official docs list Margin tiers as its own `trading/` leaf, sibling to Margining, Liquidations, Auto-deleveraging, and Portfolio margin.

On this check:

- **Margin modes.** Isolated versus cross, strict isolated, and HIP-3 no-cross stay on [Margin modes](margin-modes.md). Official Margining page: leverage can be any integer from 1 to max leverage; max leverage depends on the asset. Tiers are how that max changes with **notional size**.
- **Liquidations.** Official Liquidations page: for assets with margin tiers, maintenance leverage in the liq-price formula depends on the unique margin tier for position value **at the liquidation price**. That hook is already on [Liquidations](liquidations.md). This page supplies the tier table and the continuous-MM formula. It does not retell book versus backstop.
- **ADL.** Official ADL page does not name margin tiers. This page does not invent a link.
- **Portfolio margin.** Official PM page does not name margin tiers. PMR stays on [Portfolio margin](portfolio-margin.md).

Sources: [Margin tiers](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/margin-tiers.md); [Liquidations](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/liquidations.md); [llms.txt](https://hyperliquid.gitbook.io/hyperliquid-docs/llms.txt) — checked 2026-09-17.

---

## Published formulas

Official Margin tiers page, checked 2026-09-17. Quoted as published. Not tidied into a third formula.

`maintenance_margin = notional_position_value * maintenance_margin_rate - maintenance_deduction`

`maintenance_margin_rate(tier = n) = (Initial Margin Rate at Maximum leverage at tier n) / 2`

Official example on that page: at **20x** max leverage, `maintenance_margin_rate = 2.5%`.

`maintenance_deduction(tier = 0) = 0`

`maintenance_deduction(tier = n) = maintenance_deduction(tier = n - 1) + notional_position_lower_bound(tier = n) * (maintenance_margin_rate(tier = n) - maintenance_margin_rate(tier = n - 1))` for `n > 0`

Official purpose of the deduction: new positions at each tier increase maintenance margin at that tier’s rate, while total maintenance margin stays continuous in position size.

Source: [Margin tiers](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/margin-tiers.md) — checked 2026-09-17.

---

## Published mainnet tables

Official heading: **Mainnet Margin Tiers**. Official: enabled for the assets below. Dated official publish on 2026-09-17. Can change. Coin names here are official labels on that page, not a markets-shelf ingest.

| Assets | Notional (USDC) | Max leverage |
|--------|-----------------|--------------|
| BTC | 0–150M | 40 |
| BTC | >150M | 20 |
| ETH | 0–100M | 25 |
| ETH | >100M | 15 |
| SOL | 0–70M | 20 |
| SOL | >70M | 10 |
| XRP | 0–40M | 20 |
| XRP | >40M | 10 |
| AAVE, ADA, APT, AVAX, BCH, CRV, DOGE, ENA, FARTCOIN, HYPE, kBONK, kPEPE, LINK, LTC, NEAR, PUMP, SUI, TRUMP, UNI, WLD, ZEC | 0–20M | 10 |
| same group | >20M | 5 |
| ARB, BNB, DOT, JUP, kSHIB, MKR, ONDO, PAXG, TON, TRX, XPL | 0–3M | 10 |
| same group | >3M | 5 |

Source: [Margin tiers](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/margin-tiers.md) — checked 2026-09-17.

---

## Published testnet tables

Official: tiers on testnet are lower than mainnet, for ease of testing. Dated official publish on 2026-09-17.

| Assets | Notional (USDC) | Max leverage |
|--------|-----------------|--------------|
| ARB, ATOM, AVAX, FARTCOIN, ICP, TAO (testnet only) | 0–10k | 10 |
| same group | >10k | 5 |
| DOGE, TIA, SUI, kSHIB, AAVE, TON (testnet only) | 0–20k | 10 |
| same group | >20k | 5 |
| ETH (testnet only) | 0–20k | 25 |
| ETH (testnet only) | 20–50k | 10 |
| ETH (testnet only) | >50k | 5 |
| BTC (testnet only) | 0–10k | 40 |
| BTC (testnet only) | 10–50k | 25 |
| BTC (testnet only) | >50k | 10 |

Source: [Margin tiers](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/margin-tiers.md) — checked 2026-09-17.

---

## Gaps inside this scope

- Whether every listed perp, and every HIP-3 perp, has a docs-page table versus only an ID<50 `meta` row: **unknown here** beyond the assets the official page names.
- Live `meta` versus this docs snapshot on a later day: **unknown here**. Live `meta` was not walked on this check.
- How isolated versus cross *chooses* among tiers beyond using position notional: **unknown here**. Official page is silent. The fence stays on [Margin modes](margin-modes.md).
- Interaction of tiers with PMR or ADL: **unknown here**. Those official pages do not name tiers.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/margin-tiers.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/liquidations.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/llms.txt | 1 | 2026-09-17 |
