# HYPE token and Assistance Fund mechanics

| Field | Value |
|-------|--------|
| Shelf | Accounts, fees, rewards (`pages/accounts/`) |
| Scope | HYPE token mechanics related to the Assistance Fund: system address, fee-to-HYPE conversion as L1 execution, burn treatment, AQAv2 reserve-yield inflows, and supply accounting implications. Not trading-fee schedules. Not multi-sig. Not validator consensus. |
| Status | Accepted |
| Page `as-of` | 2026-11-14 |
| Rank | All claims below are Rank 1 unless tagged |

This page does not cover trading-fee schedules, maker/taker tiers, or staking discounts. Those stay on [Trading fees](trading-fees.md). Aligned-quote product details and AQAv1/v2 stake requirements stay on [Aligned quote assets](../markets/aligned-quote-assets.md). Multi-sig as an account primitive is out of scope.

---

## Assistance Fund system address

Official Fees page: the Assistance Fund uses system address `0xfefefefefefefefefefefefefefefefefefefefe`. Fees directed to the community (HLP, the assistance fund, and deployers) are converted in a fully automated manner as part of L1 execution.

This address is distinct from the HYPE system address used for Core↔EVM transfers. Pointers to system addresses are for documentation only; no user-callable conversion sequence is published on the checked leaves.

Source: [Fees](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/fees) — checked 2026-11-14.

---

## Fee-to-HYPE conversion and burn

Official Fees page: the Assistance Fund converts trading fees to HYPE in a fully automated manner as part of the L1 execution. HYPE in the assistance fund is burned, removing the tokens permanently from the circulating and total supply.

Official Hyperliquid 101 for non-crypto audiences: more than $1B in annualized fees go toward programmatically buying back the HYPE token.

Burn treatment is permanent removal from both circulating and total supply. Official sources on the checked pages do not publish live circulating or total supply figures, nor historical burn totals. Those remain unknown here.

Sources: [Fees](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/fees); [Hyperliquid 101 for non-crypto audiences](https://hyperliquid.gitbook.io/hyperliquid-docs/about-hyperliquid/hyperliquid-101-for-non-crypto-audiences) — checked 2026-11-14.

---

## AQAv2 reserve-yield inflows

Official Aligned quote assets page: for AQAv2, reserve yield revenue accrues in 30-day intervals based on the block on each UTC date. It is automatically sent to the Assistance Fund 8 days after each interval completes.

System interest address is `0x50...00 + {token_index}`. If that address has insufficient balance, the treasury deployer stake is eligible to be slashed.

This is distinct from AQAv1 revenue-share language on the same page. AQAv2 has no trading-fee or volume-contribution benefit.

Source: [Aligned quote assets](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/aligned-quote-assets) — checked 2026-11-14.

---

## Non-USDC quote token fees

Official HIP-1 native token standard: for other quote tokens besides USDC, the fees are sent to the Assistance Fund. Supply may decrease over time due to spot order book fees or future burn mechanisms.

USDC-denominated fees follow the community-direction sentence on the Fees page (HLP, assistance fund, and deployers).

Source: [HIP-1: Native token standard](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-1-native-token-standard) — checked 2026-11-14.

---

## Supply accounting

Burn of HYPE acquired by the Assistance Fund removes those tokens permanently from circulating and total supply. Official sources do not publish current circulating or total supply figures on the checked pages. Live or historical supply numbers remain unknown here.

Non-USDC quote fees directed to the Assistance Fund can contribute to supply decrease via the same conversion-and-burn path, or via future burn mechanisms named on the HIP-1 page. No additional numerical accounting is published on the checked leaves.

---

## Gaps inside this scope

- Live circulating or total HYPE supply figures: **unknown here**. Official checked pages do not publish them.
- Historical total HYPE burned by the Assistance Fund: **unknown here**.
- Exact fee-split percentages among HLP, Assistance Fund, and deployers beyond the direction sentence: **unknown here**.
- Whether any user-callable action initiates the conversion: **unknown here** (explicitly out of scope; conversion is L1 execution).

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/fees | 1 | 2026-11-14 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/aligned-quote-assets | 1 | 2026-11-14 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-1-native-token-standard | 1 | 2026-11-14 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/about-hyperliquid/hyperliquid-101-for-non-crypto-audiences | 1 | 2026-11-14 |
