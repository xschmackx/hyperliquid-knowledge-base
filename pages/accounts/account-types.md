# Account types

| Field | Value |
|-------|--------|
| Shelf | Accounts, fees, rewards (`pages/accounts/`) |
| Scope | Master, sub-accounts, vaults as separate account units, and account-abstraction modes as account rules. Not balances. Not the fee table. Not liquidation math. |
| Status | Accepted |
| Page `as-of` | 2026-09-16 |
| Rank | All claims below are Rank 1 |

This page does not cover how balances move, maker/taker schedules, isolated versus cross as risk, LTV or portfolio-margin liquidation, API wallets, or HLP as a liquidity product.

---

## Master and sub-accounts

Official Sub-accounts page treats a **master** account as the parent and **sub-accounts** as additional accounts under it.

Dated official caps on 2026-09-16:

- Up to **10** sub-accounts can be created after reaching **$100,000** in volume.
- Every additional **$100M** in volume enables **1** more sub-account.
- Maximum **50** sub-accounts.

Official fee-tier rule, named not tabulated: sub-accounts **share the same fee tiers as the master account**. Official referral rule: **referral discounts do not apply to sub-accounts**. The schedule itself is out of scope.

How many API wallets attach to a master or sub-account is out of scope.

Source: [Sub-accounts](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/sub-accounts.md) — checked 2026-09-16.

---

## Account-abstraction modes

Official Account abstraction modes page: a user's **account abstraction mode** determines how spot and perps balances interact, and whether various assets are used as collateral for perps trading.

Official supported modes on 2026-09-16:

| Official name | Official published account rule |
|---------------|---------------------------------|
| Unified account | Single balance for each asset. That balance collateralizes all cross-margin positions in that asset and is unified with spot balance in that asset. Official example: USDC is the single source for validator-operated perps, XYZ perps, and spot trading against USDC as quote. USDT spot is the single source for CASH perps and spot trading against USDT as quote. |
| Portfolio margin | Single portfolio unifying all eligible assets, which are currently **HYPE, BTC, USDC, USDT**. What that portfolio does as LTV, borrow, or liquidation is out of scope. |
| Manual / Standard | Separate perp and spot balances, separate DEX balances. Cross margin applies to **each DEX separately**. |

Official discontinued mode, named for completeness:

- **DEX abstraction (discontinued):** USDC balances default to perps balance; all other collateral defaults to spot balance. Official warning on that page: cross margin on HIP-3 DEXs does not behave intuitively for DEX abstraction users.

Official HIP-3 / cross sentence from this modes page only: unified (and the unified-asset examples that include XYZ perps) share same-collateral margin across those venues; standard keeps DEX balances and cross margin **per DEX**. This page does not specify HIP-3 as a listing product.

Official extra account rules on the same page:

- Builder-code addresses **must be in standard mode** to accrue builder fees.
- Portfolio margin and unified account are limited to **50k user actions per day**. Standard mode has no such restriction. 50k is an official published figure on 2026-09-16.

How a stranger signs the mode-change action is out of scope.

Source: [Account abstraction modes](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/account-abstraction-modes.md) — checked 2026-09-16.

---

## Legacy HyperCore vault as a separate account

Official vault-leader docs: a vault is selected separately from the master account. Trades applied while that vault is selected apply to the vault, not the master.

Official published trading limits for that legacy HyperCore vault, on 2026-09-16:

- Vaults can trade **validator-operated perps**.
- They **cannot trade spot**.
- They **cannot trade HIP-3 perps**.

Official vaults hub also describes later vaults that are not this legacy unit. Those later vaults are **not specified here**. HLP as a liquidity product is out of scope.

Sources:

- [For vault leaders (legacy)](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/vaults/for-vault-leaders-legacy.md) — checked 2026-09-16
- [Vaults](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/vaults.md) — checked 2026-09-16

---

## Gaps inside this scope

- Whether every vault type on official docs is the legacy HyperCore vault: **unknown here** beyond the published split that later vaults exist and legacy vaults do not support spot or HIP-3.
- What “volume” in the sub-account caps includes (perps, spot, weighted): **unknown here**. Official Sub-accounts page says volume; it does not define the meter on that page.
- Isolated versus cross as margin modes: **unknown here** by scope.
- Portfolio-margin risk math: **unknown here** by scope.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/sub-accounts.md | 1 | 2026-09-16 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/account-abstraction-modes.md | 1 | 2026-09-16 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/vaults/for-vault-leaders-legacy.md | 1 | 2026-09-16 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/vaults.md | 1 | 2026-09-16 |
