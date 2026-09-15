# Balances

| Field | Value |
|-------|--------|
| Shelf | Accounts, fees, rewards (`pages/accounts/`) |
| Scope | What each official balance holds, and official moves between those buckets. Not account types. Not the fee table. Not Core↔EVM mechanism internals. |
| Status | Accepted |
| Page `as-of` | 2026-09-16 |
| Rank | All claims below are Rank 1 |

This page does not cover master versus sub-account rules, maker/taker schedules, available-versus-transferred margin, staking APY, or validator-set rules. Account units live on [Account types](account-types.md). Core↔EVM native transfer lives on [One state](../protocol/one-state.md).

---

## Three buckets

Official docs treat these as separate balances on HyperCore:

| Bucket | What it holds |
|--------|----------------|
| Perps / collateral USDC | USDC used for perps margining. |
| Spot tokens | HIP-1 tokens, including **spot USDC**. |
| Staking HYPE | HYPE in the staking account, which may then be delegated. |

Official Staking page: just as USDC can be transferred between perps and spot accounts, HYPE can be transferred between spot and staking accounts.

Sources:

- [Staking](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/staking.md) — checked 2026-09-16
- [HIP-1: Native token standard](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-1-native-token-standard.md) — checked 2026-09-16

---

## Perps ↔ spot USDC

Official HIP-1 page: USDC is used for all perps margining, and with HIP-1 also becomes a spot token with an **atomic transfer between perps and spot wallet USDC**.

This page names that transfer. It does not write an API body or available-versus-transferred margin.

Source: [HIP-1: Native token standard](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-1-native-token-standard.md) — checked 2026-09-16.

---

## Spot HYPE ↔ staking

Official Staking page, dated 2026-09-16:

- Transfers from **spot to staking** are **instant**.
- Transfers from **staking to spot** have a **7-day** unstaking queue.
- Each address may have at most **5** pending withdrawals in that queue.

Official undelegation rules on the same page:

- Delegations to a particular validator have a lockup of **1 day**. After that lockup, delegations may be partially or fully undelegated at any time.
- **Undelegated balances instantly reflect in the staking account balance.** Instant undelegation credit is not the same as the 7-day staking-to-spot queue.

Source: [Staking](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/staking.md) — checked 2026-09-16.

---

## Bridge in and out (USDC)

Official Bridge page:

- Deposits to the bridge are signed by validators and are **credited when more than ⅔ of the staking power has signed** the deposit.
- Withdrawals from Hyperliquid are **immediately deducted from the L1 balance**. Validators sign the withdrawal as separate transactions. When ⅔ of the staking power has signed, an EVM transaction can request the withdrawal from the bridge.
- After a withdrawal is requested there is a **dispute period**, during which the bridge can be locked for a malicious withdrawal that does not match Hyperliquid state. Cold-wallet signatures of ⅔ of the stake-weighted validator set are required to unlock the bridge. How long that dispute period lasts is **unknown here**; the official page names it and does not publish a duration on that page.
- Withdrawals do not require Arbitrum ETH from the user. Official withdrawal gas: **1 USDC**, paid on Hyperliquid.

Official published **minimum deposit: 5 USDC**, on the official USDC / legacy-bridge developer page. That figure is dated 2026-09-16. CCTP and Arbitrum click-paths are out of scope.

Sources:

- [Bridge](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/bridge.md) — checked 2026-09-16
- [USDC (developer)](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/usdc.md) — checked 2026-09-16

---

## Core ↔ EVM value

Moves of value between HyperCore and HyperEVM as native transfer are on [One state](../protocol/one-state.md). This page does not retell system addresses.

---

## Gaps inside this scope

- Dispute-period duration: **unknown here**.
- Whether the 5 USDC minimum deposit applies to every later deposit rail (CCTP and others): **unknown here** beyond the official published 5 USDC figure on the USDC / legacy-bridge page.
- Which L1 bucket a bridge deposit lands in first (perps USDC versus spot USDC): **unknown here**. Official Bridge page credits the deposit; it does not name the bucket on that page.
- Isolated, unified, and portfolio-margin effects on what is transferable: **unknown here** by scope.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/staking.md | 1 | 2026-09-16 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-1-native-token-standard.md | 1 | 2026-09-16 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/bridge.md | 1 | 2026-09-16 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/usdc.md | 1 | 2026-09-16 |
