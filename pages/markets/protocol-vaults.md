# Protocol vaults

| Field | Value |
|-------|--------|
| Shelf | Markets (`pages/markets/`) |
| Scope | Official protocol vaults as published: HLP as a liquidity product, including deposit lock as a product rule. Not HIP-2 Hyperliquidity. Not a fee schedule. Not a live TVL dump. Not an API catalog. |
| Status | Accepted |
| Page `as-of` | 2026-09-17 |
| Rank | Claims below are Rank 1 unless tagged |

This page does not retell Hyperliquidity’s range or 0.3% / 3-second guarantee. That stays on [HIP-2 Hyperliquidity](hip-2-hyperliquidity.md). The legacy HyperCore vault as a separate account unit stays on [Account types](../accounts/account-types.md). Book versus backstop and the liquidator vault as an HLP component stay on [Liquidations](../risk/liquidations.md).

---

## What a protocol vault is

Official Protocol vaults leaf title: **Protocol vaults**. Official product named on that leaf: **Hyperliquidity Provider (HLP)**.

Official role sentences on that page, checked 2026-09-17:

- HLP is a protocol vault that provides liquidity to Hyperliquid through **multiple market making strategies**, **performs liquidations**, **supplies USDC in Earn**, and **accrues a portion of trading fees**.
- HLP democratizes strategies typically reserved for privileged parties on other exchanges. The community can provide liquidity for the vault and share its pnl.
- Official: **HLP is fully community-owned.**

On this check the Protocol vaults leaf names **only HLP**. No second protocol-vault ticker is published there. Whether any other protocol vault exists is **unknown here** unless another Rank 1 page names it. The liquidator vault is official as a **component strategy of HLP**, not a separately named protocol vault product. That component stays on [Liquidations](../risk/liquidations.md).

Earn is named as something HLP supplies USDC into. Earn mechanics are not this page.

Source: [Protocol vaults](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/vaults/protocol-vaults.md) — checked 2026-09-17.

---

## Official grouping vs HIP-2, accounts, and liquidation

- **HIP-2 Hyperliquidity.** Spot-book bootstrap with no operators. HLP is the perp-side contrast on that page. Point at [HIP-2 Hyperliquidity](hip-2-hyperliquidity.md). This page does not retell the 1.003 range.
- **Legacy vault as account.** Selection, master versus vault, no spot / no HIP-3: [Account types](../accounts/account-types.md).
- **Liquidations.** Book versus backstop and the HLP liquidator-vault component: [Liquidations](../risk/liquidations.md).

Official Vaults hub, sibling grouping, not this product’s center:

- Newer vaults: builders create and tokenize vaults on **HyperEVM**. Official: full access to Core features including **spot and HIP-3 in all quote assets**. Official: this is a **strict improvement** over legacy HyperCore vaults.
- Legacy HyperCore vaults: introduced in **2023**; official: **do not support HIP-3 or spot trading**.

HyperEVM builder vaults are official *other* vaults, not protocol vaults. This page does not write a CoreWriter how-to. How HyperEVM runs stays off.

Do not merge legacy HyperCore vaults and HyperEVM builder vaults into one trading-universe claim.

Sources: [Protocol vaults](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/vaults/protocol-vaults.md); [Vaults](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/vaults.md) — checked 2026-09-17.

---

## Deposit lock

Official Protocol vaults page, checked 2026-09-17:

- The deposit lock-up period is **4 days**.
- Official meaning: you can withdraw **4 days after your most recent deposit**.
- Official example: deposited Sep 14 at 08:00 → withdrawable Sep 18 at 08:00.

Official For vault depositors (legacy), same check:

- **HLP** lock-up: **4 days**.
- **User vaults** lock-up: **1 day**.

Both official numbers are recorded. User-vault 1-day lock is grouping. App how-to clicks stay off this page.

Sources: [Protocol vaults](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/vaults/protocol-vaults.md); [For vault depositors (legacy)](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/vaults/for-vault-depositors-legacy.md) — checked 2026-09-17.

---

## Fees and profit share as product rules

Official Protocol vaults page: HLP **accrues a portion of trading fees**.

Official HyperCore vaults (legacy): **protocol vaults do not have any fees or profit share**. Official on that page: vault owners of *user* vaults receive **10% of total profits**.

Both sentences are official. They are not flattened into one rate here. The first is HLP receiving some trading-fee flow. The second is protocol vaults versus leader profit-share on user vaults. The numeric portion of trading fees HLP accrues is **unpublished** on these pages. The 10% figure is legacy *user-vault* leader share, not an HLP rate. Volume maker/taker schedules stay off this page.

Official caution on the legacy vaults page: strategies have risk; assess history before depositing. That caution is official wording, not advice invented here.

Sources: [Protocol vaults](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/vaults/protocol-vaults.md); [HyperCore vaults (legacy)](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/vaults/hypercore-vaults-legacy.md) — checked 2026-09-17.

---

## Legacy user-vault constraints (grouping only)

Official For vault leaders (legacy). Already partly on [Account types](../accounts/account-types.md):

- Legacy vaults trade **validator-operated perps only**; **cannot trade spot**; **cannot trade HIP-3 perps**.

Official leader create rules on that page are **legacy user-vault** product rules, not HLP deposit-lock rules: name + description immutable; minimum **100 USDC** leader deposit; **10k USDC** gas fee; leader must maintain **≥5%** of the vault. This page does not become a how-to-run-a-vault catalog. Whether those leader rules apply to HLP is **unknown here**. Official texts treat HLP as the no-profit-share protocol vault with a 4-day lock.

Source: [For vault leaders (legacy)](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/vaults/for-vault-leaders-legacy.md) — checked 2026-09-17.

---

## Gaps inside this scope

- Whether any protocol vault besides HLP is named on Rank 1: **unknown here**. This leaf names only HLP.
- Numeric portion of trading fees HLP accrues: **unknown** on these pages.
- Earn mechanics when HLP supplies USDC: **unknown here**.
- Live HLP TVL, APY, strategy mix: **unknown here** by scope.
- Whether HyperEVM builder vaults have a protocol-set deposit lock: **unknown** on the Protocol vaults leaf.
- Leader create-gas / 5% floor / 20% close as applied to HLP: **unknown here**. Official texts treat those as legacy user-vault rules.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/vaults/protocol-vaults.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/vaults.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/vaults/hypercore-vaults-legacy.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/vaults/for-vault-depositors-legacy.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/vaults/for-vault-leaders-legacy.md | 1 | 2026-09-17 |
