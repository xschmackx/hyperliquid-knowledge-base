# Operational acts on live markets

| Field | Value |
|-------|--------|
| Shelf | Risk and operations (`pages/risk/`) |
| Scope | Official halt, settlement, and delist consequences for already-open risk. Not the listing or delist product rule. Not incidents. Not liquidations, ADL, initial or maintenance margin, margin tiers, portfolio margin, or HIP-3 margin. Not an API how-to. |
| Status | Accepted |
| Page `as-of` | 2026-09-28 |
| Rank | Claims below are Rank 1 unless tagged |

This page starts after an official act has been named. How a market is listed, voted onto the product set, or taken off as a product stays on [Listings and HIP-1](../markets/hip-1-listings.md) and [HIP-3 builder-deployed perps](../markets/hip-3-markets.md). What settlement uses as a price input stays on [Oracles and marks](../markets/oracles-and-marks.md) and [Funding](../markets/funding.md) only as those pages already publish it. Liquidations, ADL, initial and maintenance margin, tiers, portfolio margin, and HIP-3 margin across DEXs stay on those S4 pages. Dated “what broke or paused when” stays off this page.

---

## Official names

Official docs name these acts:

- **delist / delisting** — validator vote on validator-operated perps.
- **`haltTrading`** with **`isHalted`** — HIP-3 deployer settle and resume.
- **settle / settlement** — positions closed at the official settlement price of that path.
- **resume trading** / **recycle the asset** — same `haltTrading` action used to start the book again.
- **`disableDex`** — official deployer-action name on the HIP-3 deployer-actions page.
- **`delistedCanceled`** — official order-status string: canceled due to asset delisting.

This page does not invent “market freeze,” “expiry auction,” or CEX expiry names.

Sources: [Delisting](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/delisting.md); [HIP-3: Builder-deployed perpetuals](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-3-builder-deployed-perpetuals.md); [HIP-3 deployer actions](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/hip-3-deployer-actions.md); [Info endpoint](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/info-endpoint) — checked 2026-09-28.

---

## Two official settlement paths

Two operators. Two settlement prices. They are not the same act.

| Path | Who names the act | Official settlement price | Open-risk effect as published |
|------|-------------------|---------------------------|-------------------------------|
| Validator-operated perp **delist** | Validators vote whether to delist | **1 hour time-weighted spot oracle price before the scheduled delisting voting time** | All positions settled; open orders cancelled; after settlement no new orders accepted |
| HIP-3 deployer **`haltTrading`** | Deployer | **Current mark price** | Cancels all orders and settles positions to the current mark price. Same action can resume trading and recycle the asset |

Do not collapse the two prices. Unknown whether validator-operated delist ever uses mark instead of that 1h TWAP. This page does not reconcile them.

1h TWAP is the official named method. It is not expanded here. How mark is built stays on [Oracles and marks](../markets/oracles-and-marks.md).

Sources: [Delisting](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/delisting.md); [HIP-3: Builder-deployed perpetuals](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-3-builder-deployed-perpetuals.md) — checked 2026-09-28.

---

## Validator-operated delist: open risk

Official Delisting page, validator-operated perps only:

- Validators vote on whether to delist.
- If they vote to delist, the perps settle to the **1 hour time-weighted spot oracle price before the scheduled delisting voting time**.
- When an asset is delisted, **all positions are settled and open orders are cancelled**.
- Users who wish to avoid automatic settlement should close beforehand.
- **After settlement, no new orders will be accepted.**

Official order-status string for that cancel: **`delistedCanceled`** — “Canceled due to asset delisting.” Adjacent cancel statuses (`liquidatedCanceled`, `marginCanceled`) stay on [Liquidations](liquidations.md) and [Initial and maintenance margin](initial-and-maintenance-margin.md).

How the vote is scheduled as a listing/product rule stays on [Listings and HIP-1](../markets/hip-1-listings.md). That page already records that the official Delisting page names validator-operated perps only.

Sources: [Delisting](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/delisting.md); [Info endpoint](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/info-endpoint) — checked 2026-09-28.

---

## HIP-3 `haltTrading`: open risk

Official HIP-3 Settlement section: a deployer may settle an asset using the `haltTrading` action. Official effect: **cancels all orders and settles positions to the current mark price**. The same action can **resume trading**, recycling the asset. Official use named on the product page: dated-contract reuse. Product listing, stake, auction, and recycle as a market operation stay on [HIP-3 builder-deployed perps](../markets/hip-3-markets.md). This page only restates what happens to an already-open position and working orders.

Official payload shape on the deployer-actions page (name only, not a how-to): `haltTrading: { coin: string; isHalted: boolean }`. Official text also names `disableDex` and a sub-deployer variant that can include `haltTrading`.

Rank 1 Settlement prose describes settle and resume. It does not separately define a halt that leaves positions open without settlement. Whether `isHalted: true` can halt matching without settling is **unknown** on that Rank 1 prose. This page does not invent a three-state machine.

Once **all assets are settled**, required stake may be unstaked. Stake numbers and the 183-day rule stay on [HIP-3 builder-deployed perps](../markets/hip-3-markets.md).

Sources: [HIP-3: Builder-deployed perpetuals](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-3-builder-deployed-perpetuals.md); [HIP-3 deployer actions](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/hip-3-deployer-actions.md) — checked 2026-09-28.

---

## Quote-asset disable as an operational act

Official HIP-3 product page: assets that lose quote-asset status by **onchain validator vote** also **disable perp DEXs that use this asset as collateral**. A **deployer-initiated** disable of quote asset does **not** disable those DEXs.

That is an operational act on live DEX collateral. How cross margin then behaves across DEXs stays on [HIP-3 margin](hip-3-margin.md). Quote-asset product status stays on [Aligned quote assets](../markets/aligned-quote-assets.md) and the HIP-3 markets page.

Source: [HIP-3: Builder-deployed perpetuals](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-3-builder-deployed-perpetuals.md) — checked 2026-09-28.

---

## What this is not

- **Not HIP-1 spot delist.** Official Delisting page names validator-operated perps only. Whether a listed HIP-1 spot token is delisted by that vote is **unknown**. Do not apply perp settlement language to spot balances. Same unknown already sits on [Listings and HIP-1](../markets/hip-1-listings.md).
- **Not a network-upgrade pause.** Official Order types page: market orders and TWAP suborders **do not fill during the post-only period of a network upgrade**. That is a system-wide matching restriction, not Delisting and not HIP-3 `haltTrading`. Whether resting GTC is cancelled in that window is **unknown** here. Dated upgrade windows are not this page.
- **Not a live ticker list** of votes or sunsets. Official announcements have reused the Rank 1 settlement sentences; they are not ingested here as an ops log.
- **Not a general margin-return rule.** Where settled margin lands after the act is **unknown** on Rank 1 Delisting and HIP-3 Settlement paragraphs. Do not generalise a destination from a single announcement.

Source for the upgrade distinction: [Order types](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/order-types.md) — checked 2026-09-28.

---

## Gaps inside this scope

- HIP-1 spot delist by the validator Delisting vote: **unknown**.
- Whether `haltTrading` / `isHalted: true` can halt matching without settling positions: **unknown** on Rank 1 Settlement prose.
- Margin-return destination after settlement as a general rule: **unknown** on Rank 1.
- Whether validator-operated delist ever settles to mark instead of the 1h TWAP spot oracle: **unknown**.
- Any unpublished halt of validator-operated books that is not the Delisting page: **unknown**.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/delisting.md | 1 | 2026-09-28 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-3-builder-deployed-perpetuals.md | 1 | 2026-09-28 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/hip-3-deployer-actions.md | 1 | 2026-09-28 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/info-endpoint | 1 | 2026-09-28 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/order-types.md | 1 | 2026-09-28 |
