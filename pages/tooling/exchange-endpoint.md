# Exchange endpoint

| Field | Value |
|-------|--------|
| Shelf | APIs and tooling (`pages/tooling/`) |
| Scope | Official role of POST `/exchange`, and official action `type` strings as published on the Rank 1 Exchange page. Not the Info catalog. Not WebSocket subscriptions or post-over-WS. Not HyperEVM JSON-RPC. Not hosts and paths (those stay on `api-servers.md`). Not signing walkthroughs or SDK usage. Not market, fee, or risk meaning of the actions. |
| Status | Accepted |
| Page `as-of` | 2026-09-17 |
| Rank | Claims below are Rank 1 unless tagged |

This page does not list Info request types, WebSocket channels, signing construction, official SDK usage, rate-limit weight tables, HyperEVM JSON-RPC methods, or HIP-3 / HIP-4 deployer-action catalogs. Hosts and the `/exchange` path are recorded on [`api-servers.md`](api-servers.md). Point there. Do not treat this page as a second API-server page. Do not treat it as [`info-endpoint.md`](info-endpoint.md).

---

## What `/exchange` is for

Official Exchange endpoint page:

- The exchange endpoint is used to interact with and trade on the Hyperliquid chain.
- See the Python SDK for code to generate signatures for these requests.

That second sentence is an official pointer that these requests are signed. How to construct a signature, and how to call an SDK, stay off this page.

Official method and example URL on that page: `POST https://api.hyperliquid.xyz/exchange`. Official header published there: `Content-Type: application/json`. Official discriminator field inside the `action` object: `type` (string).

Mainnet and testnet REST hosts, and the `/exchange` path, are already recorded on [`api-servers.md`](api-servers.md). Official Exchange examples use the mainnet URL only. Testnet host is on that servers page, not restated here.

Sources: [Exchange endpoint](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/exchange-endpoint.md); [llms.txt](https://hyperliquid.gitbook.io/hyperliquid-docs/llms.txt) — checked 2026-09-17.

---

## Official grouping

Unlike Info, official docs put Exchange actions on **one Rank 1 page**. `llms.txt` lists no Exchange child pages. The grouping a stranger can see on that page:

1. Three shared notes at the top: **Asset**, **Subaccounts and vaults**, **Expires After**.
2. Then one heading per published action, in page order.

This page follows that split. It does not invent a second taxonomy.

HIP-3 and HIP-4 deployer-action pages are separate official API leaves. They are not ingested here.

Sources: [Exchange endpoint](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/exchange-endpoint.md); [llms.txt](https://hyperliquid.gitbook.io/hyperliquid-docs/llms.txt) — checked 2026-09-17.

---

## Shared call notes on the Exchange page

These rules are published at the top of the Exchange page. They are call-shape notes, not market or risk meaning.

**Asset.** Official: many requests take `asset` as an input. Perpetuals: index in the `universe` field of the `meta` response. Spot: `10000 + index` where `index` is from `spotMeta.universe`. Official example: `PURR/USDC` uses asset `10000` because its spot-metadata index is `0`. This page states that rule. It does not rewrite Info `meta` / `spotMeta` tables.

**Subaccounts and vaults.** Official: subaccounts and vaults do not have private keys. Actions on behalf of a subaccount or vault are signed by the master account with `vaultAddress` set to that subaccount or vault address. Official page points at `basic_vault.py` in the Python SDK. This page names the field and the rule. It does not walk the SDK example.

**Expires After.** Official: some actions support optional `expiresAfter` (milliseconds timestamp after which the action is rejected). Official: user-signed actions such as Core USDC transfer do not support `expiresAfter`. Official: actions consume 5x the usual address-based rate limit when canceled due to a stale `expiresAfter`. Official: see the Python SDK for how to incorporate the field when signing. That is a pointer. The rate-limit weight table stays off this page.

**Envelope.** Headings on that page publish `action`, `nonce`, and `signature`. Where published: `vaultAddress`, `expiresAfter`. Official recommended nonce on those headings: current timestamp in milliseconds. How to construct `signature` is on the official Signing page and is out of scope here.

Source: [Exchange endpoint](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/exchange-endpoint.md) — checked 2026-09-17.

---

## Published actions

Official headings and `type` strings on the Exchange page, in page order, checked 2026-09-17. Meaning of leverage, margin, fees, vault economics, outcome markets, or aligned-quote risk-free rate stays off this page.

| Official heading | `type` | Official note on that heading |
|------------------|--------|-------------------------------|
| Place an order | `order` | TIF names published there for first book hit: `ALO`, `IOC`, `GTC`. Optional `cloid` |
| Cancel order(s) | `cancel` | |
| Cancel order(s) by cloid | `cancelByCloid` | |
| Schedule cancel (dead man's switch) | `scheduleCancel` | |
| Modify an order | `modify` | |
| Modify multiple orders | `batchModify` | |
| Update leverage | `updateLeverage` | |
| Update isolated margin | `updateIsolatedMargin` | Same heading also publishes alternate `type` `topUpIsolatedOnlyMargin` |
| Send Asset | `sendAsset` | |
| Agent Send Asset | `agentSendAsset` | |
| Send to EVM with data | `sendToEvmWithData` | Core-to-EVM transfer as published on this page. Not HyperEVM JSON-RPC |
| Core USDC transfer | `usdSend` | |
| Core spot transfer | `spotSend` | |
| Initiate a withdrawal request | `withdraw3` | |
| Transfer from Spot account to Perp account (and vice versa) | `usdClassTransfer` | |
| Deposit into staking | `cDeposit` | |
| Withdraw from staking | `cWithdraw` | |
| Delegate or undelegate stake from validator | `tokenDelegate` | |
| Deposit or withdraw from a vault | `vaultTransfer` | |
| Deposit or withdraw from an HIP-3 DEX's backstop liquidator | `hip3LiquidatorTransfer` | |
| Approve an API wallet | `approveAgent` | Official page points at [Nonces and API wallets](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/nonces-and-api-wallets.md) for API-wallet detail. That page is not ingested here |
| Approve a builder fee | `approveBuilderFee` | |
| Place a TWAP order | `twapOrder` | |
| Cancel a TWAP order | `twapCancel` | |
| Reserve Additional Actions | `reserveRequestWeight` | Official sentence on that heading: this action reserves additional actions for 0.0005 USDC per request, paid from the Perps balance. The full weight table is not copied here |
| Invalidate Pending Nonce (noop) | `noop` | Official: does not do anything except mark the nonce used |
| Enable HIP-3 DEX abstraction | `userDexAbstraction` | Official note: deprecated; prefer `userSetAbstraction` |
| Enable HIP-3 DEX abstraction (agent) | `agentEnableDexAbstraction` | Official note: deprecated; prefer `agentSetAbstraction` |
| Set User Abstraction | `userSetAbstraction` | |
| Set User Abstraction (agent) | `agentSetAbstraction` | |
| Split outcome | `userOutcome` | Variant field `splitOutcome` |
| Merge outcome | `userOutcome` | Variant field `mergeOutcome` |
| Merge question | `userOutcome` | Variant field `mergeQuestion` |
| Negate outcome | `userOutcome` | Variant field `negateOutcome` |
| Validator vote on risk-free rate for aligned quote asset | `validatorL1Stream` | |
| Authorize AQAv2 role | `authorizeAqav2Role` | |
| Claim rewards | `claimRewards` | |

Four outcome headings share `type` `userOutcome` and differ by the inner variant field. `topUpIsolatedOnlyMargin` is an alternate action on the isolated-margin heading, not its own heading.

Source: [Exchange endpoint](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/exchange-endpoint.md) — checked 2026-09-17.

---

## Surfaces named, not ingested

| Surface | Why it is off this page |
|---------|-------------------------|
| POST `/info` | Read requests. Already on [`info-endpoint.md`](info-endpoint.md). |
| WebSocket subscriptions and post-over-WS | Later S5 slot. Official page exists. |
| HyperEVM JSON-RPC | Separate official RPC surface. `sendToEvmWithData` is listed above only as an Exchange action. |
| Signing construction and official SDKs | Official Exchange page points at the Python SDK for signatures. Pointer only. |
| Nonces and API wallets detail | Official `approveAgent` pointer. Not ingested. |
| Rate-limit weight table | Official table lives on the Rate limits page. The two official sentences named above stay; the table does not. |
| HIP-3 / HIP-4 deployer actions | Separate official API leaves on `llms.txt`. Not this catalog. |
| Hosts and paths | Already on [`api-servers.md`](api-servers.md). |

---

## Gaps inside this scope

- Whether the live `/exchange` surface accepts action `type` strings that are not on the one Rank 1 Exchange page on this `as-of`: **unknown here**. That page is the official catalog used here. Live `/exchange` was not walked action-by-action for this check.
- HIP-3 / HIP-4 deployer actions published on other official API pages: **unknown here** by catalog scope. Whether those actions also POST `/exchange` is **unknown here** until those pages are a Taskmap item.
- How to construct signatures, nonces in detail, and SDK calls: **unknown here** by scope.
- Request weights per action, other than the official `expiresAfter` 5x stale-cancel sentence and the official `reserveRequestWeight` cost sentence: **unknown here** by scope.
- Meaning of the actions as market, fee, or risk: **unknown here** by scope.
- WebSocket post-over-WS as an alternative send path: **unknown here** by scope.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/exchange-endpoint.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/llms.txt | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api.md | 1 | 2026-09-17 |
