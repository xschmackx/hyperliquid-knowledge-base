# HIP-3 margin across DEXs

| Field | Value |
|-------|--------|
| Shelf | Risk and operations (`pages/risk/`) |
| Scope | Official HIP-3 margin across DEXs as published: how cross margin behaves when positions sit on more than one perp DEX. Not the HIP-3 listing product. Not the margin-modes catalog. Not the liquidation catalog. Not the ADL catalog. Not the portfolio-margin catalog. Not the margin-tiers catalog. Not an API catalog. |
| Status | Accepted |
| Page `as-of` | 2026-09-17 |
| Rank | Claims below are Rank 1 unless tagged |

This page does not specify HIP-3 as a listing product. That product is named, not specified, on [Perpetual markets](../markets/perpetual-markets.md). Isolated versus cross as a fence stays on [Margin modes](margin-modes.md). The account-abstraction *menu* stays on [Account types](../accounts/account-types.md). Ordinary book attempt and the liquidator vault stay on [Liquidations](liquidations.md). The ADL sorting index stays on [Auto-deleveraging](auto-deleveraging.md). PMR stays on [Portfolio margin](portfolio-margin.md). Dated tier tables stay on [Margin tiers](margin-tiers.md).

---

## What this page is for

Official HIP-3 page: each perp dex features independent margining, order books, and deployer settings.

Official Margining heading: **HIP-3 Margin Modes.**

This page records the user-risk question those texts answer: how cross margin behaves when positions sit on more than one perp DEX. Auction, stake, fee share, asset-ID schema, haltTrading-as-listing, and oracle-design-for-deployers stay off.

Sources: [Margining](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/margining.md); [HIP-3: Builder-deployed perpetuals](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-3-builder-deployed-perpetuals.md) — checked 2026-09-17.

---

## Official grouping vs other risk pages

On this check:

- **Margin modes.** Isolated, cross, and strict isolated stay on [Margin modes](margin-modes.md). Official extra mode on HIP-3 DEXs: **no cross**. This page adds the across-DEX sharing rule. It does not retell the fence.
- **Account mode.** Sharing across DEXs is gated by abstraction mode. The menu stays on [Account types](../accounts/account-types.md). The risk sentence belongs here.
- **Ordinary liquidation.** The Liquidations page does not name HIP-3. Book-then-backstop for validator-operated perps stays on [Liquidations](liquidations.md). HIP-3 publishes a **per-DEX onchain backstop**. That is grouping, not a rewrite of the liquidator vault.
- **ADL.** The ADL page does not name HIP-3. The HIP-3 Backstop section does name ADL as a per-DEX fallback. The ADL formula stays on [Auto-deleveraging](auto-deleveraging.md).
- **Portfolio margin.** Official: all HIP-3 DEXs are included in PM; not all HIP-3 collateral assets are borrowable. PMR already sums `sum_{dex} cross_maintenance_margin(dex)`. That math stays on [Portfolio margin](portfolio-margin.md).
- **Margin tiers.** No HIP-3 table on the tiers page. Whether a given HIP-3 asset uses ID<50 is **unknown here**. Tables stay on [Margin tiers](margin-tiers.md).

Sources: [Margining](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/margining.md); [HIP-3: Builder-deployed perpetuals](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-3-builder-deployed-perpetuals.md); [Portfolio margin](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/portfolio-margin.md); [llms.txt](https://hyperliquid.gitbook.io/hyperliquid-docs/llms.txt) — checked 2026-09-17.

---

## Independent books vs shared collateral

Official HIP-3 page: each perp dex has **independent margining**.

Official Margining, HIP-3 Margin Modes, checked 2026-09-17:

- When users have perp positions **across multiple DEXs**, cross margin behaves differently depending on **account abstraction**.
- **Unified account and portfolio margin:** the user’s cross margin positions in DEXs with the **same collateral** all **share margin**.
- **Standard abstraction:** cross margin only applies to the assets **within the same DEX**.

Official Account abstraction modes, same check:

- Unified: single balance per asset collateralizes all cross-margin positions in that asset. Official example includes validator-operated perps and XYZ perps. The menu stays on [Account types](../accounts/account-types.md).
- Portfolio margin: single portfolio unifying eligible assets. Risk math stays on [Portfolio margin](portfolio-margin.md).
- Manual / Standard: separate perp and spot balances, **separate DEX balances**. Cross margin applies to **each DEX separately**.
- Discontinued **DEX abstraction:** official IMPORTANT: **cross margin on HIP-3 DEXs does not behave intuitively** for DEX-abstraction users.

“Independent margining” and “same-collateral share” are both official. They are not treated here as a contradiction: standard is per DEX; unified and portfolio margin share only where collateral matches.

Sources: [Margining](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/margining.md); [Account abstraction modes](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/account-abstraction-modes.md); [HIP-3: Builder-deployed perpetuals](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-3-builder-deployed-perpetuals.md) — checked 2026-09-17.

---

## No-cross on a HIP-3 DEX

Official Margining: HIP-3 DEXs also support **no cross** — isolated margin with margin removal enabled, but **does not allow cross margin**. That mode is already named on [Margin modes](margin-modes.md).

Across-DEX consequence published with that mode: no-cross positions do not join the same-collateral share described above.

Source: [Margining](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/margining.md) — checked 2026-09-17.

---

## Enabling cross on a HIP-3 asset

Official HIP-3 **Cross margin** section:

- IMPORTANT: enabling cross margin on an asset is **irreversible**.
- Users still take **greater risk** when using cross margin across DEXs with **different deployers**.
- Mainnet validators enforce that deployers only enable cross on assets that satisfy published eligibility: sufficient observable liquidity, a reliable external oracle source, and resilience to price manipulation.
- Official threshold: each time `externalPerpPx` of an asset moves more than **50%** relative to the **start of day** price, validators review whether the deployer should be slashed for manipulation.
- Official: assets where 50% daily moves are expected more than **once a month** are **ineligible for cross margin** and subject to deployer slashing.

Those figures are official eligibility thresholds, not a live scan of assets. This page is not a slashing-process or listing-quality guide. The user-risk claim is: cross-across-DEX is gated and irreversible; some HIP-3 assets will not share.

Source: [HIP-3: Builder-deployed perpetuals](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-3-builder-deployed-perpetuals.md) — checked 2026-09-17.

---

## Quote-asset collateral as a DEX-level disable

Official HIP-3 spec item 3: any quote asset can be the collateral asset for a dex. Assets that lose quote-asset status by validator vote **disable perp dexs that use this asset as collateral**. A **deployer-initiated** disabling of quote asset does **not** disable those dexs. Future migration to a new collateral token is named as not expected on mainnet.

That is operational risk to positions on that DEX. Stake and slash tables stay off this page.

Source: [HIP-3: Builder-deployed perpetuals](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-3-builder-deployed-perpetuals.md) — checked 2026-09-17.

---

## Per-DEX backstop and ADL fallback

Official HIP-3 **Backstop liquidator** section:

- Each HIP-3 DEX has a fully onchain strategy at **`0x400..00 + {dex_index}`** that takes over **backstop liquidatable positions from that designated HIP-3 DEX**.
- Those onchain backstop liquidators **only accept assets where cross margin is enabled**, making those assets **significantly less likely to experience ADL** during high volatility.
- Each DEX’s onchain backstop liquidator is an **independent user** and **falls back to ADL** to mathematically guarantee solvency of **the DEX**.
- Official user note: no action item for users. Once scaled out, backstop absorbs undercollateralized positions while avoiding bad debt and reducing the need for ADL.

Official texts name three backstops. They are not collapsed here:

- Ordinary liquidator vault (HLP component) on [Liquidations](liquidations.md)
- Portfolio-margin backstop `0xbbb...b` on [Portfolio margin](portfolio-margin.md)
- HIP-3 per-DEX backstop `0x400..00 + {dex_index}` on this page

What `{dex_index}` is for a named DEX is not this page. The ADL sorting index stays on [Auto-deleveraging](auto-deleveraging.md).

No other official numeric formula for how much margin is shared across DEXs is published on these pages beyond the same-collateral versus same-DEX split.

Source: [HIP-3: Builder-deployed perpetuals](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-3-builder-deployed-perpetuals.md) — checked 2026-09-17.

---

## Gaps inside this scope

- How much of a same-collateral unified/PM balance is consumed by each DEX (numeric allocation): **unknown here** beyond “share margin.”
- Whether ordinary book-phase liquidation runs on a given HIP-3 asset the same as validator-operated perps: **unknown here**. The Liquidations page does not name HIP-3. The HIP-3 page specifies the per-DEX backstop and ADL fallback.
- Live list of HIP-3 assets with cross enabled: **unknown here**. The eligibility rule is published; the set is not.
- Whether a HIP-3 asset uses a docs margin-tier table or only ID<50: **unknown here**. Already gapped on [Margin tiers](margin-tiers.md).
- Interaction of no-cross HIP-3 positions with PM PMR: **unknown here** beyond PM’s focus on *cross* + spot.
- What `{dex_index}` is for a named DEX: **unknown here** by scope.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/margining.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/account-abstraction-modes.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-3-builder-deployed-perpetuals.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/portfolio-margin.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/llms.txt | 1 | 2026-09-17 |
