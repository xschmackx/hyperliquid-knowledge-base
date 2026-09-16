# WebSocket

| Field | Value |
|-------|--------|
| Shelf | APIs and tooling (`pages/tooling/`) |
| Scope | Official WebSocket subscriptions, post-over-WS, and disconnect/reconnect as published on the four Rank 1 Websocket pages. Not the Info catalog. Not the Exchange-action catalog. Not HyperEVM JSON-RPC. Not hosts and paths (those stay on `api-servers.md`). Not signing walkthroughs or SDK usage. Not market, fee, or risk meaning of subscribed data. |
| Status | Accepted |
| Page `as-of` | 2026-09-17 |
| Rank | Claims below are Rank 1 unless tagged |

This page does not reprint Info request types, Exchange action types, signing construction, official SDK usage, rate-limit weight tables, or HyperEVM JSON-RPC methods. WebSocket hosts are recorded on [`api-servers.md`](api-servers.md). Point there. Info read types stay on [`info-endpoint.md`](info-endpoint.md). Signed POST `/exchange` actions stay on [`exchange-endpoint.md`](exchange-endpoint.md).

---

## What the WebSocket surface is for

Official Websocket hub:

- WebSocket endpoints are available for real-time data streaming and as an alternative to HTTP request sending on the Hyperliquid exchange.
- Establish a WebSocket connection to the network URL. Once connected, send subscription messages to receive real-time updates.
- Official subscribe example on that page uses `method: subscribe` with `subscription.type` (example shown: `trades` / `SOL`).

Official hub also points at the Python SDK for TypeScript-style type defs and example connection code. That is a pointer. How to use an SDK stays off this page.

Mainnet and testnet WebSocket URLs are already recorded on [`api-servers.md`](api-servers.md). Official hub examples use those same URLs. They are not restated here as a new servers page.

Sources: [Websocket](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/websocket.md); [llms.txt](https://hyperliquid.gitbook.io/hyperliquid-docs/llms.txt) — checked 2026-09-17.

---

## Official grouping

`llms.txt` and the docs tree group the official WebSocket surface on **four Rank 1 pages**. That split is the grouping used here. This page does not invent a second taxonomy.

| Official page | What that page holds |
|---------------|----------------------|
| Websocket hub | Role, network URLs, connecting, disconnect/reconnect |
| Subscriptions | Subscribe / unsubscribe and the published subscription `type` list |
| Post requests | Post-over-WS wrapper for HTTP info requests and signed actions |
| Timeouts and heartbeats | Keep-alive |

Sources: [Websocket](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/websocket.md); [Subscriptions](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/websocket/subscriptions.md); [Post requests](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/websocket/post-requests.md); [Timeouts and heartbeats](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/websocket/timeouts-and-heartbeats.md); [llms.txt](https://hyperliquid.gitbook.io/hyperliquid-docs/llms.txt) — checked 2026-09-17.

---

## Disconnect and reconnect

Official Websocket hub, checked 2026-09-17:

- All automated users should handle disconnects from the server side and gracefully reconnect.
- Disconnection from API servers may happen periodically and without announcement.
- Missed data during the reconnect will be present in the snapshot ack on reconnect.
- Users can also manually query any missed data using the corresponding info request.

The last sentence is a pointer at Info. Those read types stay on [`info-endpoint.md`](info-endpoint.md).

Official Subscriptions page adds: subscription ack provides a snapshot of previous data for time series data (example named: user fills). Snapshot messages are tagged `isSnapshot: true` and can be ignored if previous messages were already processed.

This page records that published rule. It does not invent a reconnect procedure beyond snapshot-ack plus the corresponding info request.

Sources: [Websocket](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/websocket.md); [Subscriptions](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/websocket/subscriptions.md) — checked 2026-09-17.

---

## Timeouts and heartbeats

Official Timeouts and heartbeats page:

- The server will close any connection if it hasn't sent a message to it in the last 60 seconds.
- If the subscribed channel does not receive messages every 60 seconds, send `{ "method": "ping" }`.
- Server responds `{ "channel": "pong" }`.

`ping` is a method on that page. It is not a subscription `type`.

Source: [Timeouts and heartbeats](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/websocket/timeouts-and-heartbeats.md) — checked 2026-09-17.

---

## Subscribe and unsubscribe

Official Subscriptions page envelope:

```json
{ "method": "subscribe", "subscription": { } }
```

Unsubscribe uses the same object with `"method": "unsubscribe"`. Official: `subscription` must match the original subscribe object. Official: unsubscribing one feed does not affect other active subscriptions; multiple feeds need multiple unsubscribe messages.

Source: [Subscriptions](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/websocket/subscriptions.md) — checked 2026-09-17.

---

## Published subscription types

Official numbered catalog on the Subscriptions page, page order, checked 2026-09-17. Channel payload meaning stays off this page.

| # | `type` | Published subscription fields |
|---|--------|-------------------------------|
| 1 | `allMids` | Optional `dex` (default first perp dex; spot mids only with first perp dex) |
| 2 | `notification` | `user` |
| 3 | `webData3` | `user` |
| 4 | `twapStates` | `user`, `dex` |
| 5 | `clearinghouseState` | `user`, `dex` |
| 6 | `openOrders` | `user`, `dex` |
| 7 | `candle` | `coin`, `interval`. Official supported intervals: `1m`, `3m`, `5m`, `15m`, `30m`, `1h`, `2h`, `4h`, `8h`, `12h`, `1d`, `3d`, `1w`, `1M` |
| 8 | `l2Book` | `coin`. Optional: `nSigFigs`, `mantissa`, `fast` (official: 5 levels if fast, 20 if slow) |
| 9 | `trades` | `coin` |
| 10 | `orderUpdates` | `user` |
| 11 | `userEvents` | `user`. Official note: channel name for these messages is `"channel": "user"` |
| 12 | `userFills` | `user`. Optional: `aggregateByTime` |
| 13 | `userFundings` | `user` |
| 14 | `userNonFundingLedgerUpdates` | `user` |
| 15 | `activeAssetCtx` | `coin` |
| 16 | `activeAssetData` | `user`, `coin`. Official note: only supports perps |
| 17 | `userTwapSliceFills` | `user` |
| 18 | `userTwapHistory` | `user` |
| 19 | `bbo` | `coin` |
| 20 | `spotState` | `user`. Optional: `isPortfolioMargin` |
| 21 | `allDexsClearinghouseState` | `user` |
| 22 | `allDexsAssetCtxs` | None beyond `type` |
| 23 | `outcomeMetaUpdates` | None beyond `type` |
| 24 | `fastAssetCtxs` | None beyond `type`. Official encoding: payload is base64 + raw DEFLATE (no zlib/gzip wrapper); first message is a snapshot, later messages only updated coins |

Other types use their type name as channel unless the page states otherwise (`userEvents` above).

The Subscriptions “Examples” block still shows `{ "type": "webData", "user": "…" }`. That string is not in the numbered catalog (the catalog name is `webData3`). Whether `webData` remains a live type is **unknown**. This page does not assert it from the example.

Source: [Subscriptions](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/websocket/subscriptions.md) — checked 2026-09-17.

---

## Post-over-WS

Official Post requests page: the WebSocket API supports posting requests that you can normally post through the HTTP API. Those requests are either **info requests** or **signed actions**. Official: for payload examples, refer to the Info endpoint section and the Exchange endpoint section.

Official wrapper:

```json
{
  "method": "post",
  "id": 0,
  "request": {
    "type": "info",
    "payload": { }
  }
}
```

`request.type` is `info` or `action`. Official notes:

- `method` and `id` are mandatory. Unique `id` recommended to track outstanding requests.
- `explorer` requests are not supported via WebSocket.

Official response envelope: `channel: post`, echo `id`, `response.type` is `info` | `action` | `error`. Official: errors return a string mirroring the HTTP status code and description.

Official examples on that page wrap one Info `l2Book` payload and one Exchange `order` payload. Those examples prove the wrapper. They are not a second Info catalog or a second Exchange catalog. Point at [`info-endpoint.md`](info-endpoint.md) and [`exchange-endpoint.md`](exchange-endpoint.md).

Signatures inside an `action` payload stay off this page.

Source: [Post requests](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/websocket/post-requests.md) — checked 2026-09-17.

---

## Surfaces named, not ingested

| Surface | Why it is off this page |
|---------|-------------------------|
| POST `/info` | Read catalog. Already on [`info-endpoint.md`](info-endpoint.md). Post-over-WS may wrap those payloads. |
| POST `/exchange` | Action catalog. Already on [`exchange-endpoint.md`](exchange-endpoint.md). Post-over-WS may wrap those payloads. |
| Hosts and paths | Already on [`api-servers.md`](api-servers.md). |
| Signing construction and official SDKs | Official hub points at the Python SDK. Pointer only. |
| HyperEVM JSON-RPC | Separate official RPC surface. Not on these four pages. |
| Rate-limit weight table | Not published on these four pages on this `as-of`. |

---

## Gaps inside this scope

- Whether live WebSocket accepts subscription `type` strings that are not on the numbered list (including example-only `webData`): **unknown here**. The numbered catalog on the Subscriptions page is the official list used here. Live WS was not probed type-by-type for this check.
- Full payload field meaning for each channel: **unknown here** by scope.
- How to construct signatures for post-over-WS `action` payloads: **unknown here** by scope.
- HyperEVM JSON-RPC over WebSocket: **unknown here** by scope.
- Rate-limit weights for WS vs HTTP: **unknown here**. These four pages do not publish a WS weight table on this `as-of`.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/websocket.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/websocket/subscriptions.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/websocket/post-requests.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/websocket/timeouts-and-heartbeats.md | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/llms.txt | 1 | 2026-09-17 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api.md | 1 | 2026-09-17 |
