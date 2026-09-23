# SHELF — ACCOUNTS, FEES, REWARDS

This page names what belongs on the accounts / fees / rewards shelf. It is not an accepted corpus page. It does not ingest facts.

Use official names as Hyperliquid publishes them. Do not invent a parallel vocabulary. Do not copy live rate tables into this rule.

---

## Shelf

| Field | Value |
|-------|--------|
| Shelf | Accounts, fees, rewards |
| Corpus path | `pages/accounts/` |
| Question this shelf answers | How does an account hold value, what does it pay, and what does it earn? |

An accounts page explains balances and account types, trading-fee schedules and discounts, referrals, builder codes as fee logic, and staking *rewards* as payout. Consensus stake as security for HyperBFT stays on Protocol.

---

## In scope

Place a page on this shelf when its scoped question is one of these:

| Slot | About |
|------|--------|
| Account types | Master account, sub-accounts, vaults as separate fee-volume units, account abstraction modes as account rules. |
| Balances | Spot balance, perps account value, staking balance — what each holds. How to move value as a *user action* can live here; native transfer as L1 mechanism stays on Protocol. |
| Trading fees | Perps vs spot schedules. Maker / taker. 14-day volume tiers. Maker rebates. |
| Staking fee discount | Official staking tiers that change the trading fee. Not validator-set rules. |
| Referrals | Referral codes, rewards, and discounts as published. |
| Builder codes | Builder fee on fills, approvals, caps — as fee logic. SDK examples live on Tooling. |
| Staking rewards | Emissions, commission, compounding as *payout*. Lockup as an account rule. |
| Other published fee shares | HIP-3 deployer fee share *rates*, aligned-collateral fee discounts, protocol-vault fee-share *rates*. The vault or market *product* stays on Markets. |

Live numbers (tier tables, percents, volume cutoffs) belong only on accepted pages with `as-of` + URL. This shelf rule does not record them.

---

## Out of scope (other shelves)

| Topic | Shelf |
|-------|--------|
| HyperBFT, validator set, consensus stake as security | Protocol |
| Perps/spot as products, HIP-1/HIP-3 as listings, HLP as a liquidity product | Markets |
| Margin use, liquidation parameters, portfolio margin as risk | Risk and operations |
| REST / WebSocket / SDK calls that place orders or claim rewards | Tooling |
| Observation entries | Register |

If a page needs both the fee and the product, split it. Fee stays here. Link across.

---

## Filing

- Accepted pages: `pages/accounts/<slug>.md`
- Shelf index: `pages/accounts/README.md`
