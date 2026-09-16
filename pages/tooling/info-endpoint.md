# Info endpoint

| Field | Value |
|-------|--------|
| Shelf | APIs and tooling (`pages/tooling/`) |
| Scope | Official role of POST `/info`, and official request `type` strings as published on the three Rank 1 Info pages. Not signed exchange actions. Not WebSocket subscriptions or post-over-WS. Not HyperEVM JSON-RPC. Not hosts and paths (those stay on `api-servers.md`). Not market, fee, or risk meaning of returned data. |
| Status | Accepted |
| Page `as-of` | 2026-09-16 |
| Rank | Claims below are Rank 1 unless tagged |

This page does not list signed `exchange` actions, WebSocket channels, signing rules, official SDK usage, rate-limit weight tables, or HyperEVM JSON-RPC methods. Hosts and the `/info` path are recorded on [`api-servers.md`](api-servers.md). Point there. Do not treat this page as a second API-server page.

---

## What `/info` is for

Official Info endpoint page:

- The info endpoint is used to fetch information about the exchange and specific users.
- Different request bodies result in different corresponding response body schemas.

Official method and example URL on that page: `POST https://api.hyperliquid.xyz/info`. Official header published there: `Content-Type: application/json`. Official discriminator field: `type` (string).

Mainnet and testnet REST hosts, and the `/info` path, are already recorded on [`api-servers.md`](api-servers.md). Official Info hub examples use the mainnet URL only. Testnet host is on that servers page, not restated here.

Official naming note on the Info hub: the endpoints in this section as well as websocket subscriptions work for both Perpetuals and Spot. That sentence is a naming note. WebSocket channels stay off this page.

Sources: [Info endpoint](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/info-endpoint.md); [llms.txt](https://hyperliquid.gitbook.io/hyperliquid-docs/llms.txt) — checked 2026-09-16.

---

## Official grouping

Official docs tree and `llms.txt` group Info request types on three Rank 1 pages. That split is the grouping used here. This page does not invent a second taxonomy.

| Official page | What that page says it holds |
|---------------|------------------------------|
| Info hub | Types presented there as working for both perpetuals and spot, plus shared user, vault, staking, builder, and borrow/lend reads |
| Perpetuals child | Info endpoints that are specific to perpetuals |
| Spot child | Info endpoints that are specific to spot |

Sources: [Info endpoint](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/info-endpoint.md); [Perpetuals](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/info-endpoint/perpetuals.md); [Spot](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/info-endpoint/spot.md); [llms.txt](https://hyperliquid.gitbook.io/hyperliquid-docs/llms.txt) — checked 2026-09-16.

---

## Hub types (both perpetuals and spot, plus shared reads)

Official headings and request fields on the Info hub, checked 2026-09-16. Response field meaning stays off this page.

| `type` | Official heading | Request fields published on that heading |
|--------|------------------|------------------------------------------|
| `allMids` | Retrieve mids for all coins | `type`. Optional: `dex`. Official note: if the book is empty, the last trade price is used as a fallback |
| `openOrders` | Retrieve a user's open orders | `type`, `user`. Optional: `dex` |
| `frontendOpenOrders` | Retrieve a user's open orders with additional frontend info | `type`, `user`. Optional: `dex` |
| `userFills` | Retrieve a user's fills | `type`, `user`. Optional: `aggregateByTime`. Official note: at most 2000 most recent fills |
| `userFillsByTime` | Retrieve a user's fills by time | `type`, `user`, `startTime`. Optional: `endTime`, `aggregateByTime`. Official note: at most 2000 fills per response; only the 10000 most recent fills are available |
| `userRateLimit` | Query user rate limits | `type`, `user` |
| `orderStatus` | Query order status by oid or cloid | `type`, `user`, `oid` |
| `l2Book` | L2 book snapshot | `type`, `coin`. Optional: `nSigFigs`, `mantissa`. Official note: at most 20 levels per side |
| `candleSnapshot` | Candle snapshot | `type`, `req` (`coin`, `interval`, `startTime`, `endTime`). Official note: only the most recent 5000 candles are available |
| `maxBuilderFee` | Check builder fee approval | `type`, `user`, `builder` |
| `historicalOrders` | Retrieve a user's historical orders | `type`, `user`. Official note: at most 2000 most recent historical orders |
| `userTwapSliceFills` | Retrieve a user's TWAP slice fills | `type`, `user`. Official note: at most 2000 most recent TWAP slice fills |
| `subAccounts` | Retrieve a user's subaccounts | `type`, `user` |
| `vaultDetails` | Retrieve details for a vault | `type`, `vaultAddress`. Optional: `user` |
| `userVaultEquities` | Retrieve a user's vault deposits | `type`, `user` |
| `userRole` | Query a user's role | `type`, `user` |
| `portfolio` | Query a user's portfolio | `type`, `user` |
| `referral` | Query a user's referral information | `type`, `user` |
| `userFees` | Query a user's fees | `type`, `user` |
| `delegations` | Query a user's staking delegations | `type`, `user` |
| `delegatorSummary` | Query a user's staking summary | `type`, `user` |
| `delegatorHistory` | Query a user's staking history | `type`, `user` |
| `delegatorRewards` | Query a user's staking rewards | `type`, `user` |
| `userDexAbstraction` | Query a user's HIP-3 DEX abstraction state | `type`, `user` |
| `userAbstraction` | Query a user's abstraction state | `type`, `user` |
| `borrowLendUserState` | Query borrow/lend user state | `type`, `user` |
| `borrowLendReserveState` | Query borrow/lend reserve state | `type`, `token` |
| `allBorrowLendReserveStates` | Query all borrow/lend reserve states | `type` |
| `approvedBuilders` | Query approved builders for user | `type`, `user` |

Source: [Info endpoint](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/info-endpoint.md) — checked 2026-09-16.

---

## Perpetuals-specific types

Official Perpetuals child intro: the section documents the info endpoints that are specific to perpetuals. That page points at the official Rate limits page for weights. The weight table is not copied here.

| `type` | Official heading | Request fields published on that heading |
|--------|------------------|------------------------------------------|
| `perpDexs` | Retrieve all perpetual dexs | `type` |
| `meta` | Retrieve perpetuals metadata (universe and margin tables) | `type`. Optional: `dex` |
| `metaAndAssetCtxs` | Retrieve perpetuals asset contexts (includes mark price, current funding, open interest, etc.) | `type`. Optional: `dex` |
| `clearinghouseState` | Retrieve user's perpetuals account summary | `type`, `user`. Optional: `dex`. Official purpose line also says: see a user's open positions and margin summary for perpetuals trading |
| `userFunding` | Retrieve a user's funding history or non-funding ledger updates | `type`, `user`, `startTime`. Same official heading as `userNonFundingLedgerUpdates` |
| `userNonFundingLedgerUpdates` | Retrieve a user's funding history or non-funding ledger updates | `type`, `user`, `startTime`. Official note: non-funding ledger updates include deposits, transfers, and withdrawals |
| `fundingHistory` | Retrieve historical funding rates | `type`, `coin`, `startTime` |
| `predictedFundings` | Retrieve predicted funding rates for different venues | `type`. Official note: predicted funding rates is only supported for the first perp dex |
| `perpsAtOpenInterestCap` | Query perps at open interest caps | `type`. Optional: `dex` |
| `perpDeployAuctionStatus` | Retrieve information about the Perp Deploy Auction | `type` |
| `activeAssetData` | Retrieve User's Active Asset Data | `type`, `user`, `coin` |
| `perpDexLimits` | Retrieve Builder-Deployed Perp Market Limits | `type`, `dex` (empty string not allowed) |
| `perpDexStatus` | Get Perp Market Status | `type`, `dex` (empty string represents the first perp dex) |
| `allPerpMetas` | Retrieve all perpetuals metadata (universe and margin tables) | `type` |
| `perpAnnotation` | Retrieve perp annotation | `type`, `coin` |
| `perpCategories` | Retrieve perp categories | `type` |
| `perpConciseAnnotations` | Retrieve concise perp annotations | `type` |

Source: [Perpetuals](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/info-endpoint/perpetuals.md) — checked 2026-09-16.

---

## Spot-specific types

Official Spot child intro: the section documents the info endpoints that are specific to spot.

| `type` | Official heading | Request fields published on that heading |
|--------|------------------|------------------------------------------|
| `spotMeta` | Retrieve spot metadata | `type` |
| `spotMetaAndAssetCtxs` | Retrieve spot asset contexts | `type` |
| `spotClearinghouseState` | Retrieve a user's token balances | `type`, `user`. Official purpose line also says: under unified account or portfolio margin, this is the source of truth for trading account balance across spot and perps |
| `spotDeployState` | Retrieve information about the Spot Deploy Auction | `type`, `user` |
| `spotPairDeployAuctionStatus` | Retrieve information about the Spot Pair Deploy Auction | `type`. Official note: returns the status of the Dutch auction for spot pair deployments between existing base and quote tokens |
| `tokenDetails` | Retrieve information about a token | `type`, `tokenId` |
| `outcomeMeta` | Retrieve outcome metadata | `type` |
| `settledOutcome` | Retrieve information about a settled outcome | `type`, `outcome` |
| `outcomeDeployerLimits` | Retrieve outcome deployer limits | `type`, `venue` |

Source: [Spot](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/info-endpoint/spot.md) — checked 2026-09-16.

---

## Shared call notes on the Info hub

These rules are published on the Info hub. They are call-shape notes, not market or risk meaning.

**User address.** Official hub: to query the account data associated with a master or sub-account, pass the actual address of that account. Official common pitfall named there: using an agent wallet address yields an empty result.

**Pagination.** Official hub: responses that take a time range return at most 500 elements or distinct blocks of data. To query larger ranges, use the last returned timestamp as the next `startTime`. Separate official notes on fill and order types are in the hub table above (`userFills`, `userFillsByTime`, `historicalOrders`, `userTwapSliceFills`).

**`coin` naming.** Official hub:

- Perpetuals: `coin` is the name returned in the `meta` response.
- Spot: `PURR/USDC` for PURR; `@{index}` from the `universe` field of the `spotMeta` response for other spot pairs. Official example on this check: HYPE mainnet spot index `@107`.
- Official UI remapping note: `BTC/USDC` on the app can correspond to `UBTC/USDC` on HyperCore. Official detection named there: the L1 name on the token details explorer page.

This page states that naming rule. It does not write an asset-id treatise.

**`dex` field.** Official hub (and several perp types): empty string is the first perp dex. Official note: spot mids / spot open orders are only included with the first perp dex.

**HIP-3 candles.** Official `candleSnapshot` note: HIP-3 coins are prefixed with the dex name, for example `xyz:XYZ100`.

Source: [Info endpoint](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/info-endpoint.md) — checked 2026-09-16.

---

## Surfaces named, not ingested

| Surface | Why it is off this page |
|---------|-------------------------|
| POST `/exchange` | Signed actions. Later S5 slot. Official page exists. |
| WebSocket subscriptions and post-over-WS | Later S5 slot. Official page exists. The Info hub naming note is not a licence to ingest channels. |
| HyperEVM JSON-RPC | Separate official RPC surface. |
| Signing and official SDKs | Out of this page's scope. |
| Rate-limit weight table | Official table lives on the Rate limits page. `userRateLimit` is an Info `type` and is listed above. The weights are not. |
| Hosts and paths | Already on [`api-servers.md`](api-servers.md). |

---

## Gaps inside this scope

- Whether the live `/info` surface accepts `type` strings that are not on the three Rank 1 pages on this `as-of`: **unknown here**. Those three pages are the official catalog used on this page. Live `/info` was not walked type-by-type for this check. Older or third-party lists that show other strings are not used to assert a type exists.
- Request weights per type: **unknown here** by scope.
- Meaning of returned market, fee, margin, funding, borrow/lend, or outcome fields: **unknown here** by scope.
- How to sign, how to use an SDK, how to subscribe on WebSocket, how to POST `/exchange`: **unknown here** by scope.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/info-endpoint.md | 1 | 2026-09-16 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/info-endpoint/perpetuals.md | 1 | 2026-09-16 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/info-endpoint/spot.md | 1 | 2026-09-16 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/llms.txt | 1 | 2026-09-16 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api.md | 1 | 2026-09-16 |
