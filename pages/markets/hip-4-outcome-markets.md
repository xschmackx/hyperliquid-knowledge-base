# HIP-4 outcome markets

| Field | Value |
|-------|--------|
| Shelf | Markets (`pages/markets/`) |
| Scope | Official HIP-4 outcome markets: the fully collateralized primitive, how markets are defined, and published live status (protocol-run daily binaries on mainnet; additional features in stages). Not fees, not risk math, not API how-to, not a live listings dump. |
| Status | Accepted |
| Page `as-of` | 2026-11-11 |
| Rank | Claims below are Rank 1 unless tagged |

This page does not retell spot or perp mechanics. Spot stays on [Spot markets](spot-markets.md). Perps stay on [Perpetual markets](perpetual-markets.md). Fees stay on [Fees](../accounts/fees.md) or the official fees leaf. How to place an order stays on tooling pages.

---

## What an outcome market is

Official HIP-4 page:

- Outcomes are **fully collateralized contracts that settle within a fixed range**.
- A general-purpose primitive useful for prediction markets and bounded options-like instruments.
- **No leverage or liquidations**.

Two sides (often named Yes and No) per outcome. At settlement, Yes converts to a fraction of the quote asset (`settleFraction`) and No converts to the complementary fraction (`1 - settleFraction`). The Yes and No order books are merged so that buying Yes at price *p* is equivalent to selling No at *1 - p*, sharing liquidity.

A **question** is a collection of outcomes where exactly one settles to Yes.

The first published market is a recurring binary outcome that settles daily at 06:00 UTC to the BTC mark price on HyperCore. Multi-outcome markets will be supported but are not part of the initial mainnet release. Additional features and markets are rolled out in stages.

Source: [HIP-4: Outcome markets](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-4-outcome-markets) — checked 2026-11-11.

---

## How a market is defined

Official Contract specifications page, Recurring outcomes section:

- Recurring outcomes are **automatically deployed and settled by the protocol** on a fixed cadence.
- The exact specification lives in the `description` field of `outcomeMeta`.
- Binary: settles to YES if and only if the interpolated mark price ≥ `targetPrice`.
- Multi-price: three buckets.
- Uniqueness: at most one recurring series per `(seriesType, underlying, period)`.

Official Info endpoint (spot) for outcome metadata:

- Outcomes and questions come from templates named `template:<id>`.
- Recurring series are named `Recurring` with a `|`-separated key:value description starting with `class`.
- `class:priceBinary` resolves to Yes if mark > `targetPrice` at expiry.
- `class:priceBucket` is a question with three index outcomes.

The description encodes the class, underlying, expiry, targetPrice or price thresholds, and period. Current live markets are as published in `outcomeMeta` on the network; this page does not dump them.

Sources:

- [Contract specifications](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/contract-specifications) — checked 2026-11-11
- [Info endpoint — spot / outcomeMeta](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/info-endpoint/spot) — checked 2026-11-11

---

## Live status as published

Official HIP-4 page (last updated ~5 months before this check): first market is the recurring daily BTC binary; multi-outcome not in the initial mainnet release; features and markets rolled out in stages.

Official deployer-actions page is labeled **Testnet-only**. Validators vote on outcome templates for permissionless deployments. Do not treat permissionless mainnet deployment as live from that page. Official text says additional features and markets are rolled out in stages.

Early official X (Rank 3, 2026-02-02): announced HyperCore would support outcome trading (HIP-4); testing on testnet at the time; canonical markets based on objective sources to be deployed (denominated in USDH then); pending feedback, extend to permissionless.

Later official X (Rank 3, 2026-05-14): canonical outcome markets will use USDC as quote in a future network upgrade.

Current quote asset for live markets is as published in `outcomeMeta` or the app. This page does not invent a current quote.

Sources:

- [HIP-4: Outcome markets](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-4-outcome-markets) — checked 2026-11-11
- [HIP-4 deployer actions](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/hip-4-deployer-actions) — checked 2026-11-11 (labeled Testnet-only)
- [Official X 2026-02-02](https://x.com/HyperliquidX/status/2018327360723202167) (Rank 3)
- [Official X 2026-05-14](https://x.com/HyperliquidX/status/2054895699498619143) (Rank 3)

---

## Asset representation

Official Asset IDs page:

- Derived from outcome id + binary side (0 or 1).
- Encoding = `10 * outcome + side`.
- Representations: coin `#<encoding>`, token `+<encoding>`, asset ID `100000000 + encoding`.
- Example: outcome 1 side 0 → `#10`, `+10`, `100000010`.

Outcome trading API is similar to spot, with these key differences in asset ids. Not the same as spot or perp asset ids.

Source: [Asset IDs](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/asset-ids) — checked 2026-11-11.

---

## Fees as published (pointer only)

Official HIP-4 page states fees are currently zero for initial testing. The more recently updated official Fees page states that outcome trading only charges fees when closing or settling (not when opening) and that there are no rebates on outcomes. An official announcement (Rank 3, 2026-08-14) states fees will be enabled on validator-deployed outcome markets, with the average outcome trading fee half of non-outcome spot, charged only on close/settle.

Prefer the Fees page and the announcement for current status. Any discrepancy between the HIP-4 page text and later sources is left as published.

This page is not a fee schedule.

Sources:

- [Fees — Outcome tokens](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/fees) — checked 2026-11-11
- [Announcement: Outcome (HIP-4) fees will be enabled](https://app.hyperliquid.xyz/announcement/tm2eqyd9aa) (Rank 3, 2026-08-14)

---

## Gaps inside this scope

- Live list of active outcome markets, their exact `outcomeMeta` descriptions, and current quote asset: **unknown here** by scope.
- Whether permissionless (deployer) outcome markets are live on mainnet: official deployer-actions page is Testnet-only; HIP-4 page says features rolled out in stages. **Unknown here** beyond that.
- Multi-outcome markets on mainnet: official HIP-4 page states they are not part of the initial mainnet release.
- Exact current fee schedule for outcomes: prefer the Fees page and announcement; residual discrepancy with the older HIP-4 page text is left as published.
- Full mechanics of split/merge/negate or question settlement beyond the published Yes/No conversion: pointed at in official docs; not expanded here.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-4-outcome-markets | 1 | 2026-11-11 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/contract-specifications | 1 | 2026-11-11 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/asset-ids | 1 | 2026-11-11 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/info-endpoint/spot | 1 | 2026-11-11 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/hip-4-deployer-actions | 1 | 2026-11-11 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/fees | 1 | 2026-11-11 |
| https://app.hyperliquid.xyz/announcement/tm2eqyd9aa | 3 | 2026-11-11 |
| https://x.com/HyperliquidX/status/2018327360723202167 | 3 | 2026-11-11 |
| https://x.com/HyperliquidX/status/2054895699498619143 | 3 | 2026-11-11 |
