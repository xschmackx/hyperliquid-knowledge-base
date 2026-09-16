# Portfolio margin

| Field | Value |
|-------|--------|
| Shelf | Risk and operations (`pages/risk/`) |
| Scope | Official portfolio-margin risk as published: PMR, portfolio maintenance, borrow liquidation. Not the account-mode catalog. Not the ordinary liquidation catalog. Not the ADL catalog. Not an API catalog. |
| Status | Accepted |
| Page `as-of` | 2026-09-17 |
| Rank | Claims below are Rank 1 unless tagged |

This page does not retell how a user chooses an account-abstraction mode. That stays on [Account types](../accounts/account-types.md). Isolated versus cross as a collateral fence stays on [Margin modes](margin-modes.md). Ordinary book attempt and the liquidator vault stay on [Liquidations](liquidations.md). Auto-deleveraging stays on [Auto-deleveraging](auto-deleveraging.md). This page is not a second liquidation or ADL page.

---

## What portfolio margin does as risk

Official Portfolio margin page:

- Under portfolio margin, a user’s spot and perps trading are unified.
- Spot and perp pnl offset each other, protecting against liquidation on the perp position.
- Official Liquidations section on that page: portfolio margin is a generalization of cross margin. Instead of margining all perp positions within one DEX together, all **cross margin perp positions and spot balances** are collectively margined together within one account.
- Official: sub-accounts are still treated separately under portfolio margin.

Eligible assets named on that page and on Account abstraction modes: **HYPE, BTC, USDC, USDT**. Official: all HIP-3 DEXs are included in portfolio margin, though not all HIP-3 DEX collateral assets are borrowable.

How the mode is chosen stays on [Account types](../accounts/account-types.md).

Sources: [Portfolio margin](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/portfolio-margin.md); [Account abstraction modes](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/account-abstraction-modes.md) — checked 2026-09-17.

---

## Official grouping vs margin modes, liquidation, and ADL

Official docs list Portfolio margin as its own `trading/` leaf, sibling to Margining, Liquidations, and Auto-deleveraging.

On this check:

- **Margin modes.** Isolated versus cross is on [Margin modes](margin-modes.md). Official PM page: PM generalizes *cross* margin across perps and spot in one account. It does not publish a new isolated/cross fence.
- **Ordinary liquidation.** The Liquidations page does not name portfolio margin or borrow liquidation. Book-then-backstop for ordinary perps stays on [Liquidations](liquidations.md). Official PM page: PM liquidations are taken over **directly by the backstop liquidator**; **unlike perps, there is no market liquidation phase.**
- **ADL.** The ADL page does not name portfolio margin. Official PM pages do not name ADL. This page does not infer a PM-specific ADL rule.

Sources: [Portfolio margin](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/portfolio-margin.md); [Liquidations](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/liquidations.md); [Auto-deleveraging](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/auto-deleveraging.md); [llms.txt](https://hyperliquid.gitbook.io/hyperliquid-docs/llms.txt) — checked 2026-09-17.

---

## LTV and auto-borrow

Official product page: eligible collateral LTV is between 0 and 1. Official dated values on that page: **HYPE 0.65**, **BTC 0.5**.

Official auto-borrow when placing spot and perp orders, up to

`token_balance * borrow_oracle_price * ltv`

(price denominated in the asset being borrowed).

Source: [Portfolio margin](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/portfolio-margin.md) — checked 2026-09-17.

---

## Interest as a risk buffer

Official product page: borrowed assets accrue interest continuously, indexed hourly to match the perp funding interval. Official stablecoin borrow rate:

`0.05 + 4.75 * max(0, utilization - 0.8)` APY

with `utilization = total_borrowed_value / total_supplied_value`, compounded continuously.

Official: the protocol retains **10%** of borrowed interest as a buffer for future liquidations.

Yield-on-idle as a product pitch is not this page’s center.

Source: [Portfolio margin](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/portfolio-margin.md) — checked 2026-09-17.

---

## Trigger and PMR

Official product page: liquidations are triggered when the entire portfolio margin account is below its portfolio maintenance margin requirement. Users monitor via the portfolio margin ratio.

Official formulas on that page, checked 2026-09-17. Quoted as published. Not tidied into a third formula.

`portfolio_margin_ratio = max_{borrowable_token} (portfolio_maintenance_requirement(borrowable_token) / portfolio_liquidation_value(borrowable_token))`

`portfolio_maintenance_requirement(token) = min_borrow_offset + sum_{dex} cross_maintenance_margin(dex) + borrowed_size_for_maintenance(token) * borrow_oracle_price(token)`

`portfolio_liquidation_value(token) = portfolio_balance(token) + min(borrow_cap(token), min(portfolio_balance(token), supply_cap(token)) * borrow_oracle_price(token) * liquidation_threshold(token))`

`liquidation_threshold(token) = 0.5 + 0.5 * LTV(token)`

`borrow_oracle_price(token) = median(HL_spot_USDC_price, HL_perp_mark_price * USDT_USDC_oracle, HL_perp_oracle_price * USDT_USDC_oracle)`

`USDT_USDC_oracle = 1 / HL_spot_oracle_price(USDC)`

`min_borrow_offset = 20 USDC`

Official product page: the account becomes liquidatable when **`portfolio_margin_ratio > 0.95`**. All notionals in that definition converted to USDC using `borrow_oracle_price(token)`.

Official FAQ page uses “≥ 95%” in its liquidations subsection and points at the product Liquidations section for the full technical breakdown. Both official wordings are recorded. This page does not invent a third cutoff.

Sources: [Portfolio margin](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/portfolio-margin.md); [FAQ — Portfolio margin](https://hyperliquid.gitbook.io/hyperliquid-docs/support/faq/portfolio-margin.md) — checked 2026-09-17.

---

## Caps and fallback

Official product page: after borrow caps are hit, additional margin used must be supplied by the user using the settlement asset, regardless of whether portfolio margin is active. Official IMPORTANT block on that page: PM accounts **fall back to non-portfolio margin behavior when caps are hit**.

Published cap table on that page, dated 2026-09-17 (risk-relevant because it changes the fallback):

| Asset | Official published caps |
|-------|-------------------------|
| USDT | 50M global supply, 10M global borrow, 5M user supply, 1M user borrow |
| USDC | 1B global supply, 500M global borrow, 250M user supply, 50M user borrow |
| HYPE | 10M global supply, 1M user supply |
| BTC | 2k global supply, 200 BTC user supply |

Official product-page enable-adjacent list on the same check also names: master account >$5M weighted volume **or** account value >$10k; account value **<$25M**. How a stranger turns the mode on is not this page.

Official FAQ how-to on the same check: account value must be **<$5,000,000**. Same-rank official pages, different numbers. This page does not pick a winner. Unknown which figure is current until a later official `as-of` wins.

Sources: [Portfolio margin](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/portfolio-margin.md); [FAQ — Portfolio margin](https://hyperliquid.gitbook.io/hyperliquid-docs/support/faq/portfolio-margin.md) — checked 2026-09-17.

---

## Borrow / backstop takeover

Official product page:

- Depending on the order of oracle price updates, either perp positions or spot borrows may be liquidated first. Official: once PMR is liquidatable, users should **not expect a deterministic liquidation sequence**.
- PM liquidations are taken over directly by the backstop liquidator at system address **`0xbbb...b`**.
- If user health is below the **full liquidation threshold**: supplied assets with positive LTV and borrowed assets are **fully** taken over.
- If user health is between the **partial** and **full** liquidation thresholds: those assets are taken over in **20% intervals**, stopping when the user is no longer liquidatable.
- Official slippage threshold for takeover:

`size_liquidated * oracle_price * (LTV(asset) + 2) / 3) * width`

with width **3M USDC** for HYPE and **300k USDC** for BTC.

- Official: the backstop liquidator converts collateral assets to debt assets for repayment using a TWAP with a **half life of 10 minutes**.
- Official: unlike perps, **no market liquidation phase**, because spot books have less consistent liquidity than perps.

The product page names “partial liquidation threshold” and “full liquidation threshold” but does **not** publish the numeric definitions of those two thresholds on that page.

Source: [Portfolio margin](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/portfolio-margin.md) — checked 2026-09-17.

---

## FAQ-only published extras

Official support FAQ leaf, checked 2026-09-17. These strings are **not** in the product-page PMR block. They are recorded here as published on the FAQ URL.

- Auto-borrow against collateral to prevent perp liquidation when equity falls below maintenance; automatic repayment of borrows from deposits and realized profits; borrowable balance cannot be withdrawn or transferred.
- **Health Factor:** `Account Value weighted by LTV / Borrowed Amount`. Official FAQ: Health Factor <100% does not directly imply liquidation risk, but the account will not be able to borrow more.
- Partial borrow liquidation threshold: `collateral_value × (LTV + (1 - LTV) × ½)`. Official FAQ: occurs every 3 seconds until no longer liquidatable.
- Full borrow liquidation threshold: `collateral_value × (LTV + (1 - LTV) × ⅔)`.

This page does not rewrite those FAQ formulas as if they appeared in the product `portfolio_margin_ratio` block.

Source: [FAQ — Portfolio margin](https://hyperliquid.gitbook.io/hyperliquid-docs/support/faq/portfolio-margin.md) — checked 2026-09-17.

---

## Gaps inside this scope

- Numeric definition of “user health” / partial vs full threshold **on the product page**: **unknown there**. FAQ publishes collateral-value formulas; those are not treated as if they were in the PMR block.
- Which of <$25M (product) vs <$5M (FAQ) is the current account-value cap: **unknown** (same-rank disagreement).
- Whether ADL runs after a PM backstop takeover: **unknown**. Neither official PM page nor the ADL page names the other.
- Deterministic order of perp vs spot-borrow liquidation: official text says there is none.
- Live cap utilization on a given day: **unknown**. The table is a dated official publish, not a live meter.
- How isolated positions inside a PM account interact with PMR beyond the product page’s focus on *cross* + spot: **unknown** except official “generalization of cross margin.”

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/portfolio-margin.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/support/faq/portfolio-margin.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/account-abstraction-modes.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/liquidations.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/auto-deleveraging.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/llms.txt | 1 | 2026-09-17 |
