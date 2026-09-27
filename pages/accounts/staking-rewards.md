# Staking rewards

| Field | Value |
|-------|--------|
| Shelf | Accounts, fees, rewards (`pages/accounts/`) |
| Scope | Official staking payout: emissions, commission, compounding, and lockup as an account rule. Not validator-set rules. Not the staking-tier trading-fee discount. Not an API catalog. |
| Status | Accepted |
| Page `as-of` | 2026-09-27 |
| Rank | Claims below are Rank 1 unless tagged |

This page does not reprint Wood–Diamond trading-fee tiers. Those stay on [Staking fee discount](staking-fee-discount.md). The staking-balance bucket and the same two clocks already printed there stay on [Balances](balances.md). What a master, sub-account, or vault *is* stays on [Account types](account-types.md). Validator-set rules, HyperBFT, and consensus stake as security are not this page.

Official HyperCore Staking leaf groups account buckets, delegation lockup, the staking-to-spot queue, commission, emissions, accrue/distribute/compound, the epoch-minimum payout rule, and a short note that a jailed validator does not produce rewards for its delegators. That grouping is this product.

---

## What the payout is

Official Staking leaf, checked 2026-09-27.

HYPE on HyperCore moves from spot into a **staking account**, then may be **delegated** to any number of validators. Official: *delegate* and *stake* are used interchangeably; Hyperliquid only supports delegated proof-of-stake.

Staking rewards are HYPE paid from the **future emissions reserve**. This page is that payout plus the account lockups that bound it. It is not the Wood–Diamond trading-fee discount on [Staking fee discount](staking-fee-discount.md).

Named first-party surface on the how-to leaf: [https://app.hyperliquid.xyz/staking](https://app.hyperliquid.xyz/staking) (Rank 3 UI; the rules stay Rank 1). Other listed front-ends on that how-to are third-party and are not treated as product rules here.

Source: [Staking](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/staking.md) — checked 2026-09-27. UI named on [How to stake HYPE](https://hyperliquid.gitbook.io/hyperliquid-docs/onboarding/how-to-stake-hype.md).

---

## Emissions rate as printed

Official Staking leaf: the reward rate is inspired by Ethereum and is **inversely proportional to the square root of total HYPE staked**.

Printed example only: at **400M** total HYPE staked, the rate is approximately **2.37% per year**.

That leaf does not print the closed-form constant, the current total-staked input, or a live network APR. This page does not invent them. A first-party UI “Est. APR” is not treated as Rank 1.

Source: [Staking](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/staking.md) — checked 2026-09-27.

---

## Accrue, distribute, compound

Official Staking leaf, checked 2026-09-27.

- Rewards accrue **every minute**.
- They are distributed to stakers **every day**.
- Distributed rewards are **redelegated automatically** to the same validator (compounded).

Official: no separate claim step on that leaf. Do not invent one.

Whether “every day” is a UTC calendar day or a rolling 24 hours is **unknown here**.

Source: [Staking](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/staking.md) — checked 2026-09-27.

---

## Epoch-minimum payout

Official Staking leaf: rewards use the **minimum balance** a delegator had staked during each staking epoch.

Official epoch length used for that payout window: **100k rounds**, approximately **90 minutes** on mainnet.

That timing sentence is the payout window. Quorum, HyperBFT rounds, height, and jail-vote procedure are not this page.

Whether that minimum is taken per validator or summed across validators, and how jailed time inside an epoch hits the minimum, is **unknown here**.

Source: [Staking](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/staking.md) — checked 2026-09-27.

---

## Commission as payout split

Official Staking leaf: validators may charge a commission to their delegators. Official raise rule: commission **cannot be increased unless the new commission is less than or equal to 1%**.

Info `delegatorRewards` names two `source` values on the official sample: `delegation` (delegator payout) and `commission` (validator commission payout on that address). Those type names live on [Info endpoint](../tooling/info-endpoint.md). This page does not catalog payloads.

How net APR is computed from gross minus commission, beyond that named split, is **unknown here**.

Validator self-delegation (10k HYPE, one-year lock) and the active set are not this page.

Source: [Staking](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/staking.md) — checked 2026-09-27. Named types: [Info endpoint](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/info-endpoint.md).

---

## Jailing versus slashing, payout only

Official Staking leaf: a jailed validator **does not produce rewards for its delegators**.

Official: there is currently **no automatic slashing implemented**. Slashing is reserved for provably malicious behavior such as double-signing.

Jail mechanics, unjail rate limits, and slash conditions stay off this page. One payout sentence is enough.

Source: [Staking](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/staking.md) — checked 2026-09-27.

---

## Lockup as an account rule (two clocks)

Official Staking leaf, how-to, and unstaking FAQ, checked 2026-09-27. The same two clocks are already printed on [Balances](balances.md). This page is why they exist as payout/lockup, not a second balances table.

1. **Delegation lockup — 1 day** to a particular validator. After that, partial or full undelegation is allowed at any time. Undelegated HYPE **instantly** credits the staking-account balance. Instant undelegation is **not** the 7-day clock.
2. **Staking-account → spot — 7-day unstaking queue.** Spot → staking is **instant**. Each address may have at most **5** pending withdrawals in that queue.

Official worked example on the Staking leaf and the FAQ: a transfer of 100 HYPE at 08:00:00 UTC 11 Mar finalizes 08:00:01 UTC 18 Mar; 50 HYPE at 09:00:00 UTC 12 Mar finalizes 09:00:01 UTC 19 Mar.

Official FAQ: undelegation and transfer-to-spot are **two separate actions**. The 7-day queue starts when the staking→spot transfer is initiated, not when undelegation happens. Users who only undelegate and never start that transfer have not started the 7-day queue. Official: it is not possible to speed the staking→spot transfer to less than 7 days.

Sources: [Staking](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/staking.md); [How to stake HYPE](https://hyperliquid.gitbook.io/hyperliquid-docs/onboarding/how-to-stake-hype.md); [Unstaking transfer taking more than 7 days](https://hyperliquid.gitbook.io/hyperliquid-docs/support/faq/unstaking-and-link-staking-issues/unstaking-transfer-taking-more-than-7-days.md) — checked 2026-09-27.

---

## Not the fee discount

Staked HYPE also maps to Wood–Diamond trading-fee tiers. That product is already [Staking fee discount](staking-fee-discount.md). Those tiers are not reprinted here.

Snapshot timing for *fee* stake versus *rewards* epoch-minimum is already marked unknown on that sibling page. Do not import one clock onto the other.

---

## Named query surface only

Info types named on [Info endpoint](../tooling/info-endpoint.md): `delegations` (validator, amount, `lockedUntilTimestamp`), `delegatorSummary` (`delegated`, `undelegated`, `totalPendingWithdrawal`, `nPendingWithdrawals`), `delegatorRewards` (`time`, `source` of `delegation` or `commission`, `totalAmount`).

This page names those types. It does not catalog payloads or how to query them.

Source: [Info endpoint](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/info-endpoint.md) — checked 2026-09-27 as named types only.

---

## Official grouping

Official docs index [`llms.txt`](https://hyperliquid.gitbook.io/hyperliquid-docs/llms.txt) groups HyperCore Staking as its own leaf. That leaf is the spine. Fees **Staking tiers** stay on [Staking fee discount](staking-fee-discount.md). The staking bucket stays on [Balances](balances.md).

---

## Gaps inside this scope

- Closed-form reward constant (the *k* in an inverse-sqrt formula): **unknown here**. Official leaf prints the inverse-sqrt sentence and the 400M / ~2.37% example only.
- Current total HYPE staked as the input to that example, and any live network APR: **unknown here** as Rank 1.
- Whether Foundation or unvested stake earns rewards: **unknown here**. Rank 1 is silent.
- Whether daily distribution is a UTC day or a rolling 24 hours: **unknown here**.
- Whether epoch-minimum is per-validator or summed, and how jailed time inside an epoch hits that minimum: **unknown here**.
- How a first-party UI constructs an “Est. APR”: **unknown here**.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/staking.md | 1 | 2026-09-27 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/onboarding/how-to-stake-hype.md | 1 | 2026-09-27 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/support/faq/unstaking-and-link-staking-issues/unstaking-transfer-taking-more-than-7-days.md | 1 | 2026-09-27 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/info-endpoint.md | 1 | 2026-09-27 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/llms.txt | 1 | 2026-09-27 |
| https://app.hyperliquid.xyz/staking | 3 (first-party UI named for surface only) | 2026-09-27 |
