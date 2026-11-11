# Trading fees

| Field | Value |
|-------|--------|
| Shelf | Accounts, fees, rewards (`pages/accounts/`) |
| Scope | Perps vs spot schedules, maker/taker, 14-day volume tiers, maker rebates, staking discount as a fee multiplier. Outcome-token fee treatment as published. Not referrals-as-a-product. Not builder-code SDK. Not staking-as-security. |
| Status | Accepted |
| Page `as-of` | 2026-11-11 |
| Rank | All claims below are Rank 1 unless tagged |

This page does not cover the referral program as a product, builder-code integration, staking APY or unstaking queues, margin, or liquidation. Account units live on [Account types](account-types.md). Balance buckets live on [Balances](balances.md). Outcome-market product lives on [HIP-4 outcome markets](../markets/hip-4-outcome-markets.md).

All tables below are official published figures on 2026-09-16, not a desk measurement. Official change on the Fees page makes this page stale until re-checked. Outcome-token rules below are from the Fees leaf checked 2026-11-11.

---

## How the tier is chosen

Official Fees page:

- Separate schedules for **perps** and **spot**.
- One fee tier per user across perps, HIP-3 perps, and spot.
- Fees use rolling **14-day** volume, assessed at the end of each day in **UTC**.
- Official weighted-volume formula: `(14d weighted volume) = (14d perps volume) + 2 * (14d spot volume)`.

Official account-unit sentence on that page: sub-account volume counts toward the master account and all sub-accounts share the same fee tier. Vault volume is treated separately from the master account.

Maker rebates are paid out continuously on each trade directly to the trading wallet.

Source: [Fees](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/fees) — checked 2026-09-16 (tier rules); outcome rules checked 2026-11-11.

---

## Perps fee tiers

Official published on 2026-09-16, not a desk measurement.

| Tier | 14d weighted volume ($) | Base taker | Base maker | Diamond taker | Diamond maker | Platinum taker | Platinum maker | Gold taker | Gold maker | Silver taker | Silver maker | Bronze taker | Bronze maker | Wood taker | Wood maker |
|------|-------------------------|------------|------------|---------------|---------------|----------------|----------------|------------|------------|--------------|--------------|--------------|--------------|------------|------------|
| 0 | | 0.045% | 0.015% | 0.0270% | 0.0090% | 0.0315% | 0.0105% | 0.0360% | 0.0120% | 0.0383% | 0.0128% | 0.0405% | 0.0135% | 0.0428% | 0.0143% |
| 1 | >5M | 0.040% | 0.012% | 0.0240% | 0.0072% | 0.0280% | 0.0084% | 0.0320% | 0.0096% | 0.0340% | 0.0102% | 0.0360% | 0.0108% | 0.0380% | 0.0114% |
| 2 | >25M | 0.035% | 0.008% | 0.0210% | 0.0048% | 0.0245% | 0.0056% | 0.0280% | 0.0064% | 0.0298% | 0.0068% | 0.0315% | 0.0072% | 0.0333% | 0.0076% |
| 3 | >100M | 0.030% | 0.004% | 0.0180% | 0.0024% | 0.0210% | 0.0028% | 0.0240% | 0.0032% | 0.0255% | 0.0034% | 0.0270% | 0.0036% | 0.0285% | 0.0038% |
| 4 | >500M | 0.028% | 0.000% | 0.0168% | 0.0000% | 0.0196% | 0.0000% | 0.0224% | 0.0000% | 0.0238% | 0.0000% | 0.0252% | 0.0000% | 0.0266% | 0.0000% |
| 5 | >2B | 0.026% | 0.000% | 0.0156% | 0.0000% | 0.0182% | 0.0000% | 0.0208% | 0.0000% | 0.0221% | 0.0000% | 0.0234% | 0.0000% | 0.0247% | 0.0000% |
| 6 | >7B | 0.024% | 0.000% | 0.0144% | 0.0000% | 0.0168% | 0.0000% | 0.0192% | 0.0000% | 0.0204% | 0.0000% | 0.0216% | 0.0000% | 0.0228% | 0.0000% |

Source: [Fees](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/fees) — checked 2026-09-16.

---

## Spot fee tiers

Official published on 2026-09-16, not a desk measurement.

| Tier | 14d weighted volume ($) | Base taker | Base maker | Diamond taker | Diamond maker | Platinum taker | Platinum maker | Gold taker | Gold maker | Silver taker | Silver maker | Bronze taker | Bronze maker | Wood taker | Wood maker |
|------|-------------------------|------------|------------|---------------|---------------|----------------|----------------|------------|------------|--------------|--------------|--------------|--------------|------------|------------|
| 0 | | 0.070% | 0.040% | 0.0420% | 0.0240% | 0.0490% | 0.0280% | 0.0560% | 0.0320% | 0.0595% | 0.0340% | 0.0630% | 0.0360% | 0.0665% | 0.0380% |
| 1 | >5M | 0.060% | 0.030% | 0.0360% | 0.0180% | 0.0420% | 0.0210% | 0.0480% | 0.0240% | 0.0510% | 0.0255% | 0.0540% | 0.0270% | 0.0570% | 0.0285% |
| 2 | >25M | 0.050% | 0.020% | 0.0300% | 0.0120% | 0.0350% | 0.0140% | 0.0400% | 0.0160% | 0.0425% | 0.0170% | 0.0450% | 0.0180% | 0.0475% | 0.0190% |
| 3 | >100M | 0.040% | 0.010% | 0.0240% | 0.0060% | 0.0280% | 0.0070% | 0.0320% | 0.0080% | 0.0340% | 0.0085% | 0.0360% | 0.0090% | 0.0380% | 0.0095% |
| 4 | >500M | 0.035% | 0.000% | 0.0210% | 0.0000% | 0.0245% | 0.0000% | 0.0280% | 0.0000% | 0.0298% | 0.0000% | 0.0315% | 0.0000% | 0.0333% | 0.0000% |
| 5 | >2B | 0.030% | 0.000% | 0.0180% | 0.0000% | 0.0210% | 0.0000% | 0.0240% | 0.0000% | 0.0255% | 0.0000% | 0.0270% | 0.0000% | 0.0285% | 0.0000% |
| 6 | >7B | 0.025% | 0.000% | 0.0150% | 0.0000% | 0.0175% | 0.0000% | 0.0200% | 0.0000% | 0.0213% | 0.0000% | 0.0225% | 0.0000% | 0.0238% | 0.0000% |

Source: [Fees](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/fees) — checked 2026-09-16.

---

## Maker-share rebate tiers

Official published on 2026-09-16, not a desk measurement.

| Tier | 14d weighted maker volume | Maker fee |
|------|---------------------------|-----------|
| 1 | >0.5% | -0.001% |
| 2 | >1.5% | -0.002% |
| 3 | >3.0% | -0.003% |

Source: [Fees](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/fees) — checked 2026-09-16.

---

## Staking discount (Wood–Diamond)

Official published on 2026-09-16, not a desk measurement. This is a fee multiplier, not staking-as-security.

| Tier | HYPE staked | Trading fee discount |
|------|-------------|----------------------|
| Wood | >10 | 5% |
| Bronze | >100 | 10% |
| Silver | >1,000 | 15% |
| Gold | >10,000 | 20% |
| Platinum | >100,000 | 30% |
| Diamond | >500,000 | 40% |

Official staking-linking rule on the same Fees page: a staking user and a trading user can be linked so staked HYPE on the staking user is attributed to the trading user's fees. Linking is permanent; unlinking is not supported. After the link, the staking user does not receive the staking-related fee discount. No link action is required if the same address both trades and stakes. How the signed link action is built is out of scope.

Source: [Fees](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/fees) — checked 2026-09-16.

---

## Quote-pair and aligned-quote multipliers

Official Fees page, dated 2026-09-16:

- Spot pairs between two spot quote assets have **80%** lower taker fees, maker rebates, and user volume contribution.
- Aligned quote assets: **20%** lower taker fees, **50%** better maker rebates, and **20%** more volume contribution toward fee tiers.

What counts as an aligned quote asset is not specified here.

Source: [Fees](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/fees) — checked 2026-09-16.

---

## Referral volume caps only

Official Fees page: referral **rewards** apply for a user's first **$1B** in volume. Referral **discounts** apply for a user's first **$25M** in volume. The referral program itself is not specified here.

Source: [Fees](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/fees) — checked 2026-09-16.

---

## HIP-3 growth mode (fee logic only)

Official Fees page:

- When growth mode is activated for an HIP-3 perp, protocol fees, rebates, volume contributions, and L1 user rate-limit contributions are reduced by **90%**. The growth-mode section also writes a **≥90%** reduction on all-in fees, rebates, and volume contributions. Both sentences are official; this page does not collapse them.
- HIP-3 deployers can configure an additional fee share between **0–300%** (**0–100%** for growth mode). If the share is above 100%, the protocol fee is also increased to equal the deployer fee.
- Growth mode applies on top of other multipliers, including staking discounts.
- Official growth-mode deployer fee scale bound on that page: scale must be set between **0 and 10**. Setting growth mode has a **30-day** cooldown per asset.

Eligibility lists and validator-vote examples on that page are not specified here.

Source: [Fees](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/fees) — checked 2026-09-16.

---

## Outcome-token fee treatment

Official Fees page, Outcome tokens section, checked 2026-11-11:

Outcome trading only charges fees when closing or settling, not when opening outcome positions. Only fee-paying volume is counted for outcome trading.

Six cases:

1. Minting, no one pays fee: no volume is counted
2a. Normal Trade where one side pays fee: both users get `fee_paying_px * sz`
2b. Normal Trade where no one pays fee: no volume is counted
3a. Burning, both sides pay fee: both users get `(maker_px + taker_px) * sz = 1 * sz`
3b. Burning, only taker pays fee: both users get `taker_px * sz`
4. Settlement: each user gets `settle_fraction * sz`

Outcome trading does not support rebates. Users who would receive rebates for spot and perp trading pay zero fees on maker orders.

An official announcement (Rank 3, 2026-08-14) states that the average outcome trading fee will be half that of non-outcome spot trading, and that outcome trading only charges fees when closing or settling, not when opening. Example given: Tier 0 user with no previous volume opens as taker (no fee) and closes as taker (0.07%). The Rank-1 Fees leaf does not print the "average half" phrase; it prints the close/settle rule, the six volume cases, and the no-rebates rule. This page tags the average-half claim as Rank 3.

The outcome-market product itself is on [HIP-4 outcome markets](../markets/hip-4-outcome-markets.md). Official HIP-4 page text (older) still says fees are currently zero for initial testing. Prefer this Fees treatment for current status. Any discrepancy is left as published.

No Rank-1 sentence on the Fees leaf invents stacking of outcome fees with staking discounts, builder fees, or referral caps beyond the printed no-rebates rule. Do not invent rates.

Sources: [Fees](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/fees) — checked 2026-11-11; [Announcement: Outcome (HIP-4) fees will be enabled](https://app.hyperliquid.xyz/announcement/tm2eqyd9aa) (Rank 3, 2026-08-14).

---

## Gaps inside this scope

- How Wood–Diamond columns combine with the separate staking-discount table when both apply: **unknown here** beyond the official tables sitting on the same page.
- Exact meaning of “14d weighted maker volume” percentages in the rebate table (share of exchange maker volume versus something else): **unknown here**. Official header is that phrase.
- How outcome fees stack with staking discounts, builder fees, or referral caps beyond the printed no-rebates rule: **unknown here**. Fees leaf is silent beyond no rebates.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/fees | 1 | 2026-09-16 (schedules); 2026-11-11 (outcome tokens) |
| https://app.hyperliquid.xyz/announcement/tm2eqyd9aa | 3 | 2026-11-11 |
