# Rate limits and user limits

| Field | Value |
|-------|--------|
| Shelf | APIs and tooling (`pages/tooling/`) |
| Scope | Official published rate limits per IP (REST aggregated weight, WebSocket caps, EVM RPC) and address-based user limits on Hyperliquid. Not the role or catalog of the info endpoint, exchange endpoint, or WebSocket (those stay on accepted pages). Not official SDK usage. Not nonce or API wallet rules. |
| Status | Accepted |
| Page `as-of` | 2026-11-11 |
| Rank | Claims below are Rank 1 unless tagged |

This page records the official rate limits and user limits as published. A stranger can use it to stay inside the published request limits per IP, per WebSocket, and per trading address and avoid silent failures or 429s. What the info endpoint *is*, what the exchange endpoint *is*, and what WebSocket channels exist stay on the accepted pages. Official names only. Unknown stays unknown.

Rank-1 re-check on 2026-11-11 found no material clarifications versus the prior as-of 2026-11-09. Weights, address vs IP treatment, batched requests, congestion rules, userRateLimit fields, and the expiresAfter note remain as published. Unpublished edge cases stay unknown.

Sources: [Rate limits and user limits](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/rate-limits-and-user-limits.md) — checked 2026-11-11.

---

## IP-based rate limits

Official page: the following rate limits apply per IP address.

REST requests share an aggregated weight limit of 1200 per minute.

- All documented exchange API requests have a weight of `1 + floor(batch_length / 40)`. For example, unbatched actions have weight 1 and a batched order request of length 79 has weight 2. Here, `batch_length` is the length of the array in the action, e.g. the number of orders in a batched order action. Exchange actions themselves stay on [`exchange-endpoint.md`](exchange-endpoint.md).
- The following info requests have weight 2: `l2Book`, `allMids`, `clearinghouseState`, `orderStatus`, `spotClearinghouseState`, `exchangeStatus`.
- The following info requests have weight 60: `userRole`.
- All other documented info requests have weight 20.
- The following info endpoints have an additional rate limit weight per 20 items returned in the response: `recentTrades`, `historicalOrders`, `userFills`, `userFillsByTime`, `fundingHistory`, `userFunding`, `nonUserFundingUpdates`, `twapHistory`, `userTwapSliceFills`, `userTwapSliceFillsByTime`, `delegatorHistory`, `delegatorRewards`, `validatorStats`.
- The `candleSnapshot` info endpoint has an additional rate limit weight per 60 items returned in the response.

Info request types and their fields stay on [`info-endpoint.md`](info-endpoint.md). Do not treat this weight list as a second catalog of types.

- All explorer API requests have a weight of 40. `blockList` has an additional rate limit of 1 per block. Note that older blocks which have not been recently queried may be weighted more heavily. For large batch requests, use the S3 bucket instead.

WebSocket limits per IP:

- Maximum of 10 websocket connections
- Maximum of 30 new websocket connections per minute
- Maximum of 1000 websocket subscriptions
- Maximum of 10 unique users across user-specific websocket subscriptions
- Maximum of 2000 messages sent to Hyperliquid per minute across all websocket connections
- Maximum of 100 simultaneous inflight post messages across all websocket connections

WebSocket subscriptions, post-over-WS, and disconnect rules stay on [`websocket.md`](websocket.md). Official rate-limits page points at the Python SDK for a full-featured example. Official SDK usage stays on [`official-sdks.md`](official-sdks.md).

Maximum of 100 EVM JSON-RPC requests per minute for `rpc.hyperliquid.xyz/evm`. Note that other JSON-RPC providers have more sophisticated rate limiting logic and archive node functionality. HyperEVM RPC details beyond this published limit stay on [`hyperevm-rpc.md`](hyperevm-rpc.md).

Official page: Use websockets for lowest latency realtime data.

Source: [Rate limits and user limits](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/rate-limits-and-user-limits.md) — checked 2026-11-11.

---

## Address-based limits

Official page: Address-based limits apply per user, with sub-accounts treated as separate users.

The rate limiting logic allows 1 request per 1 USDC traded cumulatively since address inception. For example, with an order value of 100 USDC, this requires a fill rate of 1%. Each address starts with an initial buffer of 10000 requests. When rate limited, an address is allowed one request every 10 seconds. Cancels have cumulative limit `min(limit + 100000, limit * 2)` where `limit` is the default limit for other actions. This way, hitting the address-based rate limit still allows open orders to be canceled. Note that this rate limit only applies to actions, not info requests.

Each user has a default open order limit of 1000 plus one additional order for every 5M USDC of volume, capped at a total of 5000 open orders. When an order is placed with at least 1000 other open orders by the same user, it will be rejected if it is reduce-only or a trigger order.

During high congestion, addresses are limited to use 2x their previous day maker share percentage of the block space. The maker share is scaled by the same factor as the volume contribution of that asset towards fee tiers. For example, HIP-3 assets under growth mode count less towards this rate limit. The maker share is computed once per UTC date. During high traffic, it can therefore be helpful to not resend cancels whose results have already been returned via the API. During congestion, the weight of a batched action is proportional both to its batch size and a constant per-action weight. Therefore, batching cancels or orders together will strictly decrease their weighting and reduce rate limit usage.

Official exchange endpoint notes that actions consume 5x usual address-based rate limit when canceled due to stale `expiresAfter`. That note stays on [`exchange-endpoint.md`](exchange-endpoint.md). Nonce rules are separate and stay on [`nonces-and-api-wallets.md`](nonces-and-api-wallets.md).

Source: [Rate limits and user limits](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/rate-limits-and-user-limits.md) — checked 2026-11-11.

---

## Batched requests

Official page: A batched request with `n` orders (or cancels) is treated as one request for IP based rate limiting, but as `n` requests for address-based rate limiting.

Source: [Rate limits and user limits](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/rate-limits-and-user-limits.md) — checked 2026-11-11.

---

## Querying remaining address capacity

Official info endpoint provides type `userRateLimit` to query user rate limits. Response fields published on the info page: `cumVlm`, `nRequestsUsed`, `nRequestsCap`, `nRequestsSurplus`.

The type itself and its request shape stay on [`info-endpoint.md`](info-endpoint.md). This page does not rewrite the info catalog.

Weight for this info request is 20 (all other documented info requests).

Source: [Info endpoint](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/info-endpoint.md) — checked 2026-11-11; weight context from the rate-limits page.

---

## Published consequence of exceeding limits

Official page publishes the limits themselves. It does not detail the HTTP status body, Retry-After header, or exact rejection message on exceed. Those stay unknown here. A stranger can observe 429s in practice, but the published rule is the limit.

---

## Gaps inside this scope

- Exact HTTP response, status code body, or retry guidance when a limit is exceeded: **unknown here**. Official page does not publish it on this `as-of`.
- Whether other unofficial or community-reported weights or caps exist: **unknown here**. Official page is the source used.
- Full fee-tier scaling math for maker share beyond the published example: **unknown here** by scope. Fee schedules stay out of this shelf.
- Special cases for outcome markets (HIP-4) or other new actions on rate limits: **unknown here**. Not published on Rank-1 sources as of this check.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/rate-limits-and-user-limits.md | 1 | 2026-11-11 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/info-endpoint.md | 1 | 2026-11-11 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/exchange-endpoint.md | 1 | 2026-11-11 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/error-responses.md | 1 | 2026-11-11 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/llms.txt | 1 | 2026-11-11 |
