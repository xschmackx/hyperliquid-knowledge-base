# Staking fee discount

| Field | Value |
|-------|--------|
| Shelf | Accounts, fees, rewards (`pages/accounts/`) |
| Scope | Official staking tiers that change the trading fee, and official staking-linking as fee attribution. Not validator-set rules. Not staking-rewards payout. Not a fee-schedule reprint. Not an API catalog. |
| Status | Accepted |
| Page `as-of` | 2026-09-27 |
| Rank | Claims below are Rank 1 unless tagged |

This page does not reprint perps or spot fee-tier tables. Those stay on [Trading fees](trading-fees.md). The live referral program stays on [Referrals](referrals.md). Builder codes as fee logic stay on [Builder codes](builder-codes.md). What a master, sub-account, or vault *is* stays on [Account types](account-types.md). The staking-balance bucket stays on [Balances](balances.md). How a signed link action or Info query is built is tooling, not this page.

Official Fees leaf groups a **Staking tiers** table and a **Staking linking** section on the same page as the volume schedules. That grouping is this product. It is not HyperCore staking as validator security or as a rewards payout.

---

## What the discount is

Official Fees leaf, checked 2026-09-27.

Staked HYPE maps to a named staking tier. That tier is a **percentage discount on trading fees**. Official names: Wood, Bronze, Silver, Gold, Platinum, Diamond. Maximum published discount is **40%** (Diamond).

It is a multiplier on the trading fee, not a second volume tier. Volume still chooses Tier 0–6 from 14-day weighted volume. That schedule stays on [Trading fees](trading-fees.md). Staking chooses the Wood–Diamond column / the discount percent. Official perps and spot tables already print those multiplied rates next to the Base column. They are not reprinted here.

Source: [Fees](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/fees.md) — checked 2026-09-27.

---

## Official staking tiers

Official published on 2026-09-27, not a desk measurement. Thresholds are strict **greater-than**. Exactly 10 HYPE is not Wood on the printed table.

| Tier | HYPE staked | Trading fee discount |
|------|-------------|----------------------|
| Wood | >10 | 5% |
| Bronze | >100 | 10% |
| Silver | >1,000 | 15% |
| Gold | >10,000 | 20% |
| Platinum | >100,000 | 30% |
| Diamond | >500,000 | 40% |

Source: [Fees](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/fees.md) — checked 2026-09-27.

---

## Same address needs no link

Official Fees leaf: no action is required if you plan to trade and stake from the same address.

Support restatement of that same rule: the linking feature is only for users who want to trade and stake on separate accounts.

Sources: [Fees](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/fees.md); [Staking and trading account linking issues](https://hyperliquid.gitbook.io/hyperliquid-docs/support/faq/unstaking-and-link-staking-issues/staking-and-trading-account-linking-issues.md) — checked 2026-09-27.

---

## Linking separate addresses

Official Fees leaf **Staking linking** block, checked 2026-09-27.

A “staking user” and a “trading user” can be linked so that the staking user’s HYPE staked is attributed to the trading user’s fees.

Official rules on that block:

- Both must be controlled by the same user.
- After the link, the staking user can unilaterally transfer all funds from the trading user to the staking user’s account in a single irreversible transaction. Official warning: a trading user should never link to a staking user controlled by another user.
- A staking user may send an EIP-712 signed action with primary type `HyperliquidTransaction:StakingLinkDisableTradingUser` and payload `{tradingUser, nonce}` that renders the trading user unusable and locks funds. One year after locking, those funds automatically transfer to the staking user. Official: irreversible and not recommended under normal operation.
- Linking is permanent. Unlinking is not supported.
- After being linked, the staking user does not receive any staking-related fee discount.
- Linking requires the trading user to send an action first; the staking user finalizes.

Named first-party surface on that leaf: “Link Staking” at [https://app.hyperliquid.xyz/portfolio](https://app.hyperliquid.xyz/portfolio) (Rank 3 UI; the rules stay Rank 1).

How that action is signed is tooling. This page names the official type as a control warning. It does not write the payload how-to.

Sub-accounts sharing a volume tier with the master is a different axis from this link. Volume-tier sharing is already on [Trading fees](trading-fees.md) and [Account types](account-types.md). Do not collapse the two.

Sources: [Fees](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/fees.md); [Staking and trading account linking issues](https://hyperliquid.gitbook.io/hyperliquid-docs/support/faq/unstaking-and-link-staking-issues/staking-and-trading-account-linking-issues.md) — checked 2026-09-27.

---

## Printed stacking only

Official Fees leaf: growth mode applies on top of other multipliers, such as staking discounts. Growth-mode eligibility and deployer-scale math stay on [Trading fees](trading-fees.md). They are not rewritten here.

The live referral discount is a separate product on [Referrals](referrals.md). Builder codes are a separate product on [Builder codes](builder-codes.md).

How the discount compounds with referral, builder, aligned-quote, or deployer-share beyond sentences already printed on Fees and those sibling pages is **unknown here**. Do not invent a closed-form stack.

An official Referrals child **Proposal: Staking referral program** uses staking *tiers* as a *referrer* share of someone else’s fees. That program is labeled not on mainnet on [Referrals](referrals.md). It is not this discount.

Source: [Fees](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/fees.md) — checked 2026-09-27. Contrast already accepted on [Referrals](referrals.md).

---

## Named query surface only

Info `type` `userFees` is named on [Info endpoint](../tooling/info-endpoint.md). Official sample fields on that type include `feeSchedule.stakingDiscountTiers`, `stakingLink`, and `activeStakingDiscount`. Official sample `discount: "0.3"` matches Platinum 30% as a fraction.

The Fees table keys tiers by **HYPE staked**. The Info example also keys `stakingDiscountTiers` by `bpsOfMaxSupply`. Official Fees leaf does not print a conversion between those units. That conversion is **unknown here**. Prefer the Fees table as the stranger-facing rule.

This page does not catalog payloads.

Source: [Info endpoint](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/info-endpoint.md) — checked 2026-09-27 as named type only.

---

## Official grouping

Official docs index [`llms.txt`](https://hyperliquid.gitbook.io/hyperliquid-docs/llms.txt) groups Fees as a Trading child. The staking-tier table and staking-linking block live on that Fees leaf. That split is the grouping.

The HyperCore Staking leaf is validator self-delegation, commission, emissions, and lockup. That is not this page. The staking-balance bucket already lives on [Balances](balances.md).

---

## Gaps inside this scope

- How often the fee-facing stake snapshot updates (live versus any staking-epoch minimum used for rewards): **unknown here**. The Fees leaf does not print that timing.
- How `bpsOfMaxSupply` on the Info example converts to HYPE staked on the Fees table: **unknown here**.
- Whether one staking user can be linked to more than one trading user, or whether linked stake sums across more than one pair: **unknown here**.
- How the discount compounds with referral / builder / aligned-quote / deployer-share beyond sentences already printed on sibling pages: **unknown here**.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/fees.md | 1 | 2026-09-27 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/support/faq/unstaking-and-link-staking-issues/staking-and-trading-account-linking-issues.md | 1 | 2026-09-27 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/info-endpoint.md | 1 | 2026-09-27 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/llms.txt | 1 | 2026-09-27 |
| https://app.hyperliquid.xyz/portfolio | 3 (first-party UI named for surface only) | 2026-09-27 |
