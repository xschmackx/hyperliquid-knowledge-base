# Aligned quote assets

| Field | Value |
|-------|--------|
| Shelf | Markets (`pages/markets/`) |
| Scope | Official aligned-quote primitive as a market building block. Not a fee schedule. Not a listing catalog. Not a live asset dump. Not an API catalog. |
| Status | Accepted |
| Page `as-of` | 2026-09-17 |
| Rank | Claims below are Rank 1 unless tagged |

This page does not retell spot listing or quote-token mechanics. Those stay on [Spot markets](spot-markets.md) and [HIP-1 listings](hip-1-listings.md). HIP-3 as a deployer product, including quote-as-collateral and quote-disable, stays on [HIP-3 builder-deployed perps](hip-3-markets.md). Fee *schedules* and the already-recorded 20 / 50 / 20 multipliers stay on [Trading fees](../accounts/trading-fees.md).

---

## What an aligned quote asset is

Official Aligned quote assets leaf: the protocol supports “aligned stablecoins” as a **permissionless primitive** for stablecoin issuers to use Hyperliquid distribution and scale together with the protocol.

Official motivation: an opt-in setting for new stablecoin teams to bootstrap network effects and share upside proportionally. Official grouping on that leaf: similar to permissionless spot listings, HIP-3, and builder codes. Listing product stays on [HIP-1 listings](hip-1-listings.md). HIP-3 product stays on [HIP-3 builder-deployed perps](hip-3-markets.md). Builder-code fee logic stays on S3. This page does not ingest those products.

Official names on that leaf: “aligned stablecoins,” “aligned quote asset,” **AQAv1**, **AQAv2**. Those two specs are different objects. Do not collapse them.

Official docs index places this leaf under HyperCore, sibling to [Permissionless spot quote assets](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/permissionless-spot-quote-assets.md). That sibling is the quote-*token* primitive. Alignment is a further designation on some quote assets.

Source: [Aligned quote assets](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/aligned-quote-assets.md) — checked 2026-09-17.

---

## Quote-token prerequisite

Alignment assumes a permissionless quote token first. Official quote-token leaf, checked 2026-09-17, published facts used only as that prerequisite:

- Wei decimals **8** and size decimals **2**; zero deployer fee share on the quote token.
- **200k HYPE** staked (testnet **50 HYPE**). USDC and USDT are exempt from that stake.
- Peg and HYPE/QUOTE book tests; **3-year** commitment.
- `enableQuoteToken` is irreversible and has no gas cost.

That is how a token *becomes a quote*. This page names the step. It is not a second HIP-1 or quote-token page.

Quote-token stake (**200k**) is not the same object as AQAv1 extra stake or AQAv2 deployer stakes. Do not add them into one number except where the AQA leaf itself writes “total of 1M including the 200k.”

Sources: [Permissionless spot quote assets](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/permissionless-spot-quote-assets.md); [Aligned quote assets](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/aligned-quote-assets.md) — checked 2026-09-17.

---

## AQAv1

Official use surface: lower trading fees, larger maker rebates, and higher volume contribution toward fee tiers when used as the **quote asset for a spot pair** or the **collateral asset for HIP-3 perps**.

Official AQAv1 benefit bullets on that leaf (also on the Fees leaf and already recorded on [Trading fees](../accounts/trading-fees.md)). These three lines are the published *definition of what v1 alignment confers*. They are not a reprint of the perps/spot tier tables.

1. **20%** lower taker fees
2. **50%** larger maker rebates
3. **20%** more volume contribution toward fee tiers

Those multipliers apply to AQAv1. They do **not** apply to AQAv2.

### Onchain requirements (as printed)

1. Enabled as a permissionless quote token.
2. **800k additional** staked HYPE by the deployer, meaning a **total of 1M** staked HYPE including the **200k** staked for quote-token deployment.
3. **50%** of the AQA rate flows to the protocol. Validators may vote to update the calculation methodology as regulatory standards evolve. AQA rate is an onchain stake-weighted median of validator-reported values. A CoreWriter action lets the deployer reflect minted HyperEVM balance onto HyperCore for an automated fee-share as L1 execution.

### Offchain requirements (validator-voted)

Official: enforced through onchain quorum of validator votes. Official: offchain conditions are **not** in the state machine.

As printed on the AQA leaf:

1. 1:1 backing by cash / short-term US treasuries / tokenized US treasury or money-market funds to the extent permitted; par redemption at all times with a public timely redemption service. Guiding requirement printed: a large percentage of the world's circulating dollars could compliantly convert to the aligned stablecoin.
2. Full supply natively minted on HyperEVM as source chain.
3. Deployer may only deploy assets that directly support the aligned stablecoin and must share half of offchain yield income. Deployer and affiliates may not take conversion-tied benefits (revenue share, order-flow payments, rate-linked compensation named).
4. Team must be independent and dedicated to building on Hyperliquid.

Source: [Aligned quote assets](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/aligned-quote-assets.md) — checked 2026-09-17.

---

## AQAv2

Official: extends “aligned quote asset” to stablecoins that are **not exclusive to Hyperliquid**.

Official share: deployers share **approximately 90%** of cost-adjusted reserve yield revenue on their Hyperliquid supply with the protocol. Official: the treasury address shares **100% of the AQA rate** (cost-adjusted onchain reference rate oracle) with the protocol through the onchain AQA mechanic. Official: this is **twice** the revenue-share rate of the existing AQA spec.

Official: **no trading fee or volume contribution benefit** to AQAv2. Other quote assets remain supported for other markets, including spot and HIP-3 perps.

Official future: AQAv2 **will be a requirement** for quote assets listed against **HIP-4** and **validator-operated perp markets** on a **future network upgrade**. Whether that upgrade has shipped is **unknown** on this leaf. This page does not open a HIP-4 page.

### Two deployer roles

- **Treasury deployer** stakes **500k HYPE**. Designates a treasury address. Stake is slashable if that address lacks balance for onchain revenue deduction.
- **Technical deployer** stakes **500k HYPE**. Must ensure reliable mint, redemption, and cross-chain transfer infrastructure.

Both require **6 months** minimum notice before ceasing; stake is slashable for those commitments during notice.

Activation: **validator vote**, after both have staked and sent authorization transactions from the staking accounts.

### Published v2 mechanics (named, not a how-to)

- Linked HyperEVM contract that connects to HyperCore rebalances with the treasury address.
- HyperEVM balance corresponding to minted HyperCore tokens held **9:1** treasury address : technical deployer’s linked EVM contract.
- Reserve yield accrues in **30-day** intervals on the UTC-date block; automatically sent to the **Assistance Fund 8 days** after each interval completes. Intervals begin on the activation date.
- If the system interest address `0x50...00 + {token_index}` has insufficient balance, treasury deployer stake is eligible to be slashed at **2% per day**.

Official concrete payment example on that leaf:

```
Jan 1: X1 = balance at 0 UTC, RATE1 = AQA-publisher effective rate, published onchain by validators
Jan 2: X2, RATE2
...
Jan 31: X31, RATE31
Feb 1: X32, RATE32
Feb 7: X38, RATE38
Feb 28: X59, RATE59
Mar 1: X60, RATE60

System interest address pays X1 * RATE1 + … + X30 * RATE30 on Feb 7 at 0 UTC
System interest address pays X31 * RATE31 + … + X60 * RATE60 on Mar 9 at 0 UTC
```

Treat as official illustration. Do not invent a second calendar. This page does not write an EVM integration how-to.

Source: [Aligned quote assets](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/aligned-quote-assets.md) — checked 2026-09-17.

---

## HIP-3 grouping

Official HIP-3 page: HIP-3 markets incorporate “aligned collateral discount.” Official: aligned stablecoin collateral will automatically receive reduced fees once the alignment condition (which is being updated based on user and deployer feedback) is implemented. Whether that condition has been implemented, and how it maps onto AQAv1 versus AQAv2, is **unknown here**. Do not resolve it from the v1/v2 prose above.

Any quote asset may be HIP-3 collateral; losing quote-asset status by validator vote disables those DEXs. That product fact already lives on [HIP-3 builder-deployed perps](hip-3-markets.md).

Official `SetDeployerFees` comment on [HIP-3 deployer actions](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/hip-3-deployer-actions.md), checked 2026-09-17: “Note that there are currently no aligned quote assets on mainnet.” Treat that sentence as official published state on that leaf on this check, not a live scan. This page is not a token catalogue. Signing `perpDeploy` stays off.

Sources: [HIP-3: Builder-deployed perpetuals](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-3-builder-deployed-perpetuals.md); [HIP-3 deployer actions](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/hip-3-deployer-actions.md) — checked 2026-09-17.

---

## Where the fee numbers live

AQAv1’s 20 / 50 / 20 bullets are properties of the primitive, quoted above from the AQA leaf. The trading-fee *schedules* and those same multipliers already live on [Trading fees](../accounts/trading-fees.md) (`as-of` 2026-09-16). That S3 page already says what counts as an aligned quote asset is not specified there. This page is that specification. Do not reprint perps/spot tier tables.

Official Fees leaf: [Fees](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/fees.md).

---

## Official grouping

Official docs index [`llms.txt`](https://hyperliquid.gitbook.io/hyperliquid-docs/llms.txt) places the Aligned quote assets leaf under HyperCore, next to Permissionless spot quote assets. Official HyperCore hub: [HyperCore](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore.md).

---

## Gaps inside this scope

- Whether any aligned quote asset exists on mainnet beyond the deployer-actions “none on mainnet” note: **unknown here** as a live scan. That note is official published state on 2026-09-17.
- Whether an AQAv2 activation vote has occurred: **unknown** on these leaves.
- Live HIP-3 “alignment condition” update: official text still says it is being updated.
- HIP-4 / validator-operated-perp AQAv2 requirement ship date: official text still says **future**.
- AQA-rate calculation methodology beyond “stake-weighted median of validator-reported values”: **unknown here**.
- Live list of aligned tokens: **unknown here** by scope.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/aligned-quote-assets.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/permissionless-spot-quote-assets.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/fees.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-3-builder-deployed-perpetuals.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/hip-3-deployer-actions.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/llms.txt | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore.md | 1 | 2026-09-17 |
