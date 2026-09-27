# Referrals

| Field | Value |
|-------|--------|
| Shelf | Accounts, fees, rewards (`pages/accounts/`) |
| Scope | Referral codes, rewards, and discounts as official docs group them. Not a trading-fee schedule. Not builder-code fee logic. Not a live code dump. Not an API catalog. |
| Status | Accepted |
| Page `as-of` | 2026-09-27 |
| Rank | Claims below are Rank 1 unless tagged |

This page does not reprint perps or spot fee-tier tables. Those stay on [Trading fees](trading-fees.md). What a master, sub-account, or vault *is* stays on [Account types](account-types.md). What spot balance *is* stays on [Balances](balances.md). Builder codes as fee logic are a later accounts slot. How a signed claim or Info query is built is tooling, not this page.

Official docs group two objects under Referrals: the live program on the Referrals leaf, and a child **Proposal: Staking referral program**. They are not the same product. The proposal is labeled below and is not treated as mainnet.

---

## Live program

Official Referrals leaf, checked 2026-09-27.

A referral code is a published account reward and discount. Creating a code and using a code are separate published acts on the same first-party surface.

### Create a code (referrer)

After **$10,000** in volume, a user can create a referral code on the official referrals app page named by that leaf: [https://app.hyperliquid.xyz/referrals](https://app.hyperliquid.xyz/referrals).

Official reward: the referrer receives **10% of referred users' fees, less any fee discount they receive.**

Official share-link form printed on that leaf: `app.hyperliquid.xyz/join/YOURCODE`.

Those app URLs are first-party surfaces named by Rank 1. This page is not a catalogue of live codes.

### Use a code (referred)

Enter a code on the same official referrals app page, or use a friend's referral link.

Official discount: **4%** on fees for the referred user's first **$25M** in volume.

### Volume caps

Same two numbers on the Referrals leaf and on the Fees leaf:

- Referral **rewards** apply for a user's first **$1B** in volume.
- Referral **discounts** apply for a user's first **$25M** in volume.

Those caps are already recorded on [Trading fees](trading-fees.md) under “Referral volume caps only.” That page does not specify the program. This page is that program. Do not invent a third cap.

### Accrual and claim

Official:

- Rewards accrue for **all quote assets**.
- Rewards can be claimed once **>$1**.
- Claimed rewards are reflected in **spot balance**.

Spot balance as a bucket lives on [Balances](balances.md). This page does not write the claim action.

Info `type` `referral` is named on [Info endpoint](../tooling/info-endpoint.md). Exchange `{ "type": "claimRewards" }` is named on [Exchange endpoint](../tooling/exchange-endpoint.md). Those pages name the types. This page does not catalog payloads or how to sign them.

### Who the discount does not cover

Official Referrals leaf: referral discounts **do not apply to vaults or sub-accounts** because those are treated as independent accounts in the clearinghouse.

[Account types](account-types.md) already records the sub-account sentence and what those units are. This page names both exclusions from the Referrals leaf. It does not retell sub-account caps or vault trading limits.

### What “volume” meters

The Referrals leaf says “volume,” “first $1B in volume,” “first $25M in volume,” and “$10,000 in volume.” It does not define perps-versus-spot or 14-day weighted volume on that leaf. Whether those meters equal the Fees-page 14-day weighted volume used for fee tiers is **unknown here**. Do not substitute the fee-tier formula.

How “10% of referred users' fees, less any fee discount they receive” stacks with staking-tier fee columns beyond that printed sentence is **unknown here**.

Source: [Referrals](https://hyperliquid.gitbook.io/hyperliquid-docs/referrals.md) — checked 2026-09-27. Cap echo also on [Fees](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/fees.md) and [Trading fees](trading-fees.md).

---

## Proposal: staking referral program (not on mainnet)

Official child of the Referrals hub, checked 2026-09-27. Title on that leaf: **Proposal: Staking referral program.**

Opening sentence on that leaf: *“At this time, there is no definitive implementation for the staking referral program ready for mainnet. Based on extensive user and builder feedback, it is being re-evaluated to ensure fairness for all builders and a healthy builder ecosystem.”*

That leaf then prints “details for the original proposal.” Benefits on that leaf apply “once the feature is enabled on mainnet.” A sibling path `…/referrals/staking-referral-program.md` 404s on this check. Whether a later implementation has shipped after this `as-of` is **unknown here**. This page does not invent a shipped staking-referral product.

Original proposal text on that leaf (not current product):

- Staked builders and referrers keep a percentage of referred users’ trading fees, up to **40%** at the highest staking tier.
- They may share up to **50%** of that staking-referral revenue back to the referred user.
- If the builder or referrer has a higher staking tier than the referred user on a trade, they keep up to **100%** of the staking-tier difference, scaled by the referred user’s volume tier (**100%** at VIP 0 through **40%** at VIP 6). That leaf points those VIP rows at the Fees schedules. The schedules stay on [Trading fees](trading-fees.md). They are not reprinted here.

Official contrast on that same proposal leaf, used here only as grouping: referral codes are tied to the user and apply regardless of how the user trades; builder codes are a per-order fee; builder codes override referral codes **for that order**; referral codes are disabled after **$1B** cumulative volume. Builder-code approvals, caps, and SDK stay off this page.

Source: [Proposal: Staking referral program](https://hyperliquid.gitbook.io/hyperliquid-docs/referrals/proposal-staking-referral-program.md) — checked 2026-09-27.

---

## Official grouping

Official docs index [`llms.txt`](https://hyperliquid.gitbook.io/hyperliquid-docs/llms.txt) groups a Referrals hub plus that proposal child. That split is the grouping.

The official Points leaf names a historical affiliate-points rule. The live Referrals leaf does not. Ended points are not this program.

---

## Gaps inside this scope

- Whether create/use volume is the same meter as 14-day weighted fee volume: **unknown here**.
- Whether the staking-referral proposal has shipped after this `as-of`: official text on 2026-09-27 still says no definitive mainnet implementation.
- How 10%-less-discount stacks with staking-tier columns beyond the printed Referrals sentence: **unknown here**.
- Live list of referral codes: **unknown here** by scope.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/referrals.md | 1 | 2026-09-27 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/fees.md | 1 | 2026-09-27 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/referrals/proposal-staking-referral-program.md | 1 | 2026-09-27 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/sub-accounts.md | 1 | 2026-09-27 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/llms.txt | 1 | 2026-09-27 |
