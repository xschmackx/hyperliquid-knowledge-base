# Builder codes

| Field | Value |
|-------|--------|
| Shelf | Accounts, fees, rewards (`pages/accounts/`) |
| Scope | Builder fee on fills, approvals, and caps as official docs group them. Not a referral program. Not a trading-fee schedule. Not an SDK how-to. Not a live catalogue of builder codes. Not an API catalog. |
| Status | Accepted |
| Page `as-of` | 2026-09-27 |
| Rank | Claims below are Rank 1 unless tagged |

This page does not reprint perps or spot fee-tier tables. Those stay on [Trading fees](trading-fees.md). The live referral program stays on [Referrals](referrals.md). What spot balance *is* stays on [Balances](balances.md). What Manual / Standard mode *is* stays on [Account types](account-types.md). How a signed approve or order is built is tooling, not this page.

Official “builder” is used for more than one product. This page is **builder codes**: a per-order fee on fills an application sends on a user’s behalf. It is not [HIP-3 builder-deployed perpetuals](../markets/hip-3-markets.md). It is not a consensus block builder. Official Builder codes leaf: the term here is a DeFi application builder.

---

## What a builder code is

Official Builder codes leaf, checked 2026-09-27.

Builder codes let an application builder receive a fee on **fills they send on behalf of a user**. They are set **per-order**. Official: they are processed **onchain as part of the fee logic**.

That fee is **additional** to protocol maker/taker fees. Protocol schedules stay on [Trading fees](trading-fees.md). This page does not reprint those tables.

A first-party app surface named by product UI (Rank 3 UI; the fee rules stay Rank 1): [https://app.hyperliquid.xyz/builderCodes](https://app.hyperliquid.xyz/builderCodes). Printed there: applications charge a small fee on orders they send on the user’s behalf; each builder must be approved; previously approved builder codes can be removed there. That URL is not a live catalogue of every builder.

Source: [Builder codes](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/builder-codes.md) — checked 2026-09-27.

---

## Approval

Official:

- The user first approves a **maximum builder fee** for the builder address.
- That approval is the Exchange action `ApproveBuilderFee` / `{ "type": "approveBuilderFee" }`.
- The action must be signed by the user’s **main wallet, not an agent/API wallet**.
- Official Exchange field `maxFeeRate` is a **percent string**. Official example: `"0.001%"`, plus the `builder` address.
- Each user can have a maximum of **10 active** builder code approvals at a time.
- The user can **revoke permissions at any time**.

Official Exchange leaf on this check names `approveBuilderFee`. It does not name a separate `revokeBuilderFee` type. The exact signed revoke action is **unknown here**. The first-party `/builderCodes` surface says previously approved codes can be removed there.

How that action is signed is tooling. The type is named on [Exchange endpoint](../tooling/exchange-endpoint.md). Info `type` `maxBuilderFee` (user, builder) and `approvedBuilders` (user) are named on [Info endpoint](../tooling/info-endpoint.md). Those pages name the types. This page does not catalog payloads.

After approval, official Builder codes leaf: future order actions sent on behalf of the user may include the builder parameter. This page does not write agent how-to.

Sources: [Builder codes](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/builder-codes.md); [Exchange endpoint](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/exchange-endpoint.md) — checked 2026-09-27.

---

## Builder eligibility

These rules are on the **builder address that accrues the fee**, not on the user who approves.

Official Builder codes leaf:

- The builder must have at least **100 USDC in perps account value**.
- The builder must use **standard** as the account abstraction mode.

Official Account abstraction modes leaf: builder code addresses must be in **standard** mode to **accrue** builder fees. Official mode name on that leaf and on [Account types](account-types.md): **Manual / Standard**.

Whether the 100 USDC must stay there continuously after first use is **unknown here** beyond “must have.”

Sources: [Builder codes](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/builder-codes.md); [Account abstraction modes](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/account-abstraction-modes.md) — checked 2026-09-27.

---

## Where the fee applies

Official Builder codes leaf:

- Builder codes currently apply only to fees collected in the **quote or collateral asset**.
- They **do not** apply to the **buying side of spot** trades.
- They apply to **both sides of perp** trades.

Those are builder-fee collection rules. They are not the protocol perps/spot tier tables on [Trading fees](trading-fees.md).

Source: [Builder codes](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/builder-codes.md) — checked 2026-09-27.

---

## Caps and units

Official charged builder fees are at most **0.1% on perps** and **1% on spot**. Those are builder-fee caps, not protocol fee-tier tables.

Two official notations. Do not mix them without the published examples.

| Surface | Official unit | Official example |
|---------|---------------|------------------|
| Order field `f` | Tenths of a basis point | `f` of **10** means **1 basis point** of order notional charged to the user and sent to the builder |
| Info `maxBuilderFee` response | Same tenth-of-a-basis-point family | Official comment: `1` means `0.001%` |
| Exchange `approveBuilderFee` field `maxFeeRate` | Percent string | Official example `"0.001%"` |

Per-order attach after approval: optional `{"b": address, "f": number}`. `b` is the builder address. `f` is the builder fee in tenths of a basis point.

Official Info `userFills` comment used here only as fee logic: optional fill field `builderFee` is absent when 0; field `fee` is total **inclusive** of `builderFee`. Meaning-of-fields stays on [Info endpoint](../tooling/info-endpoint.md).

Sources: [Builder codes](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/builder-codes.md); [Exchange endpoint](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/exchange-endpoint.md); [Info endpoint](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/info-endpoint.md) — checked 2026-09-27.

---

## Claim

Official Builder codes leaf: builders claim builder-code fees through the **usual referral reward claim process**.

That claim path is already recorded on [Referrals](referrals.md). Claimed referral rewards land in **spot balance**, recorded on [Balances](balances.md). Info `type` `referral` includes `builderRewards` in the official example. Exchange `{ "type": "claimRewards" }` is named on [Exchange endpoint](../tooling/exchange-endpoint.md).

This page names the landing. It does not rewrite the live referral program and does not write the claim action.

Source: [Builder codes](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/builder-codes.md) — checked 2026-09-27. Claim landing also on [Referrals](referrals.md) and [Balances](balances.md).

---

## Override versus referrals

Official contrast on the Referrals child **Proposal: Staking referral program**, already recorded on [Referrals](referrals.md):

- Referral codes are tied to the user.
- Builder codes are a **per-order** fee.
- Builder codes override referral codes **for that order**.
- The builder fee goes **100% to the builder**.

That proposal leaf is labeled **not on mainnet** on [Referrals](referrals.md). The override and 100%-to-builder sentences are used here only as grouping. This page does not treat the staking-referral proposal as shipped product.

How builder fee stacks with staking-tier fee columns, or with HIP-3 deployer fee-share, beyond those printed sentences is **unknown here**. Staking-tier columns stay on [Trading fees](trading-fees.md). HIP-3 deployer share is a later accounts slot, not this page.

Source: [Proposal: Staking referral program](https://hyperliquid.gitbook.io/hyperliquid-docs/referrals/proposal-staking-referral-program.md) — checked 2026-09-27. Already accepted as contrast on [Referrals](referrals.md).

---

## Official grouping

Official docs index [`llms.txt`](https://hyperliquid.gitbook.io/hyperliquid-docs/llms.txt) groups a Trading child **Builder codes** next to Fees and Sub-accounts. That leaf is the grouping.

HIP-3 “builder-deployed perpetuals” is a different official product on [HIP-3 markets](../markets/hip-3-markets.md).

---

## Gaps inside this scope

- Exact signed revoke action name: **unknown here**. Official Exchange leaf on this check names `approveBuilderFee`, not a separate revoke type.
- Whether the builder’s 100 USDC perps minimum must stay after first use: **unknown here** beyond “must have.”
- How builder fee stacks with staking-tier columns or HIP-3 deployer share beyond the printed override / 100%-to-builder sentences: **unknown here**.
- Live list of builder addresses: **unknown here** by scope.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/builder-codes.md | 1 | 2026-09-27 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/account-abstraction-modes.md | 1 | 2026-09-27 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/exchange-endpoint.md | 1 | 2026-09-27 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/info-endpoint.md | 1 | 2026-09-27 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/referrals/proposal-staking-referral-program.md | 1 | 2026-09-27 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/llms.txt | 1 | 2026-09-27 |
| https://app.hyperliquid.xyz/builderCodes | 3 (first-party UI named for surface only) | 2026-09-27 |
