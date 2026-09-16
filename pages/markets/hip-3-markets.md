# HIP-3 builder-deployed perps

| Field | Value |
|-------|--------|
| Shelf | Markets (`pages/markets/`) |
| Scope | Official HIP-3 builder-deployed perpetual markets: market definition and deployer duties. Not the HyperCore component. Not HIP-3 margin across DEXs. Not a live listings dump. Not a fee table. Not an API catalog. |
| Status | Accepted |
| Page `as-of` | 2026-09-17 |
| Rank | Claims below are Rank 1 unless tagged |

This page does not retell the validator-operated contract-spec table. That stays on [Perpetual markets](perpetual-markets.md). Spot listing stays on [Spot markets](spot-markets.md). Book behaviour stays on [Order types and the book](order-types-and-the-book.md). Across-DEX sharing, no-cross, irreversible cross-enable, per-DEX backstop, and ADL fallback stay on [HIP-3 margin across DEXs](../risk/hip-3-margin.md).

---

## What a builder-deployed perp market is

Official HIP-3 page:

- The Hyperliquid protocol supports **permissionless builder-deployed perps (HIP-3)**, a key milestone toward fully decentralizing the perp listing process.
- HIP-3 inherits the HyperCore stack including its high performance margining and order books.

Official reminder on the same page: **each perp dex features independent margining, order books, and deployer settings.** One deployer that meets the stake rule can deploy **one** perp dex. Official future: a later upgrade may support multiple dex deployments sharing the same deployer and staking requirement. Whether that upgrade has shipped is **unknown here**. The official page still writes it as future.

How HyperCore runs as an execution component stays off this page. How to *trade* HIP-3 via Asset IDs stays off this page.

Source: [HIP-3: Builder-deployed perpetuals](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-3-builder-deployed-perpetuals.md) — checked 2026-09-17.

---

## Official grouping of deployer duties

Official HIP-3 page, two numbered responsibilities:

1. **Market definition**, including the oracle definition and contract specifications.
2. **Market operation**, including setting oracle prices, leverage limits, and settling the market if needed.

Validator-operated perp specs stay on [Perpetual markets](perpetual-markets.md). The HIP-3 page does not publish a HIP-3-specific IMF / MMF / funding-impact table. This page does not invent one from the validator-operated spec table.

Cross-DEX margin behaviour stays on [HIP-3 margin across DEXs](../risk/hip-3-margin.md).

Source: [HIP-3: Builder-deployed perpetuals](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-3-builder-deployed-perpetuals.md) — checked 2026-09-17.

---

## Stake to deploy

Official HIP-3 page, dated 2026-09-17:

- Mainnet stake to deploy: **500k HYPE**. Official: expected to decrease as infrastructure matures.
- Amount above the most recent requirement can be unstaked.
- Requirement maintained for a **minimum of 183 days** after the dex is deployed.
- Once **all assets are settled**, required stake is free to be unstaked.
- Stake remains slashable during the **7-day unstaking queue** even after unstake is initiated.

Source: [HIP-3: Builder-deployed perpetuals](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-3-builder-deployed-perpetuals.md) — checked 2026-09-17.

---

## Listing slots and the shared auction

Official HIP-3 page:

- First **3** assets on a perp dex do not require auction participation.
- Additional assets go through a **Dutch auction** with the same hyperparameters (frequency and minimum price) as the HIP-1 auction.
- That HIP-3 auction is **shared across all perp dexs**.
- Official reserve formula: deployers get `7 + 0.2 * n_auction_deployments` reserve deployments usable at the current auction price, **bypassing the auction timer**.

HIP-1 auction frequency and minimum price are **unknown here**. They live on the official [HIP-1](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-1-native-token-standard.md) page and are not copied. There is no accepted HIP-1 corpus page yet. This Issue does not open one.

This page is not a live list of HIP-3 coins.

Source: [HIP-3: Builder-deployed perpetuals](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-3-builder-deployed-perpetuals.md) — checked 2026-09-17.

---

## Collateral and quote-asset constraint

Official HIP-3 page: any quote asset can be the collateral asset for a dex. Assets that lose quote-asset status by validator vote **disable perp dexs that use that asset as collateral**. A **deployer-initiated** disable of quote asset does **not** disable those dexs. Official: HIP-3 deployers are **not** slashed for quote-asset issues. Future migration to a new collateral token is named and **not expected on mainnet**.

User-risk of a disable stays on [HIP-3 margin across DEXs](../risk/hip-3-margin.md). Here it is a product constraint on which markets can stay up.

Source: [HIP-3: Builder-deployed perpetuals](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-3-builder-deployed-perpetuals.md) — checked 2026-09-17.

---

## Fee share as a deployer setting

Official HIP-3 page: HIP-3 markets incorporate usual trading-fee discounts (staking, referral, aligned collateral). Deployers can configure an additional fee share **0–300%** (**0–100% for growth mode**). If the share is above 100%, the protocol fee is increased to equal the deployer fee.

This page is not a fee schedule. Growth-mode definition beyond that parenthetical is **unknown** on the HIP-3 page. Official aligned-collateral sentence: aligned stablecoin collateral will receive reduced fees once the alignment condition is implemented. Official: that condition “is being updated.” Details stay off this page.

Source: [HIP-3: Builder-deployed perpetuals](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-3-builder-deployed-perpetuals.md) — checked 2026-09-17.

---

## Settlement as market operation

Official HIP-3 page: a deployer may settle an asset with the `haltTrading` action. Official effect: cancels all orders and settles positions to the **current mark price**. The same action can **resume** trading, recycling the asset. Official use named: list dated contracts without a new auction each time.

`haltTrading` as a signed API payload is not this page. The product fact is settle-to-mark and recycle.

Source: [HIP-3: Builder-deployed perpetuals](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-3-builder-deployed-perpetuals.md) — checked 2026-09-17.

---

## Oracle as market definition

Official HIP-3 page: the oracle is completely general at the protocol level. Official guidance: perps make the most mathematical sense with a well-defined underlying that is hard to manipulate and has economic significance. Official: most price indices are not amenable as perp oracle sources. Official: deployers are subject to slashing for **all listed markets on their DEX**.

This page does not publish a HIP-3 mark formula. The official page does not publish one.

Source: [HIP-3: Builder-deployed perpetuals](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-3-builder-deployed-perpetuals.md) — checked 2026-09-17.

---

## Slashing as deployer-duty enforcement

Official HIP-3 page: slashing in this section is only in the HIP-3 context. Validators may slash deployer stake by stake-weighted vote for malicious market operation. Official guiding principle: prevent behavior that jeopardizes protocol correctness, uptime, or performance. Official rule of thumb: slashable behavior should be accompanied by a protocol bug fix; HIP-3 should not require slashing in its final state.

Official: slashing is technical and does not distinguish malicious versus incompetent, nor among (1) deviate from a well-designed spec, (2) faithfully follow a poorly designed spec, (3) compromised keys. Key factor: effect of deployer actions on the protocol.

Official guidelines for amount (stake-weighted median of validator votes is the actual amount):

- Irregular inputs that cause invalid state transitions or prolonged network downtime: up to **100%**.
- Irregular inputs causing brief network downtime: up to **50%**.
- Invalid inputs that cause network degradation or performance issues: up to **20%**.

Official: slashed stake is **burned**, not distributed to affected users. Official: protocol does not intervene in subjective matters; reputation sits on application/social layers. Official hoped outcome: slashing never happens on mainnet; barring implementation issues, HIP-3 inherits Hyperliquid’s mathematical solvency guarantees.

This page is not a slashing how-to and not a live incident log.

Source: [HIP-3: Builder-deployed perpetuals](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-3-builder-deployed-perpetuals.md) — checked 2026-09-17.

---

## Gaps inside this scope

- Live list of HIP-3 DEXs and coins: **unknown here** by scope.
- HIP-1 auction frequency and minimum price: **unknown here**. Named as shared; numbers live on the official HIP-1 page.
- Whether “one dex per deployer” has been upgraded to multiple dexes sharing stake: official text still says **future**.
- Growth-mode definition beyond the 0–100% fee-share cap: **unknown** on the HIP-3 page.
- Alignment-condition details for reduced fees: official text says the condition is being updated.
- HIP-3-specific contract-spec table (tick, lot, funding impact): **not published** on the HIP-3 page.
- Oracle / mark formula for a given HIP-3 market: **unknown here** beyond deployer-defined and slashable.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-3-builder-deployed-perpetuals.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-1-native-token-standard.md | 1 | 2026-09-17 |
