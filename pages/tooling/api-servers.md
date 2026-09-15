# API servers

| Field | Value |
|-------|--------|
| Shelf | APIs and tooling (`pages/tooling/`) |
| Scope | What an official API server does, and the published hosts and paths used to call it. Not the info-type catalog. Not the exchange-action catalog. Not WebSocket subscription or post schemas. Not HyperEVM JSON-RPC. Not a node runbook. |
| Status | Accepted |
| Page `as-of` | 2026-09-16 |
| Rank | Claims below are Rank 1 unless tagged |

This page does not list `info` request types, signed `exchange` actions, WebSocket channels, signing rules, rate-limit tables, or official SDK usage. Those are other S5 slots.

---

## What an API server does

Official API servers page:

- An API server listens to updates from a node and maintains blockchain state locally.
- It serves information about that state.
- It forwards user transactions to the connected node.
- It serves two sources of data: **REST** and **WebSocket**.

Official forward path for user transactions on that page: the API server forwards the transaction to the connected node; the node gossips it as part of the HyperBFT consensus algorithm; once the transaction is included in a committed L1 block, the API server responds to the original request with the execution response from the L1.

Source: [API servers](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/api-servers.md) — checked 2026-09-16.

---

## Published REST hosts

Official API page: example calls use the mainnet URL. The same requests can be made against testnet using the corresponding URL.

| Network | REST host |
|---------|-----------|
| Mainnet | `https://api.hyperliquid.xyz` |
| Testnet | `https://api.hyperliquid-testnet.xyz` |

Source: [API](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api.md) — checked 2026-09-16.

---

## Published REST paths

Official Info endpoint page: the info endpoint fetches information about the exchange and specific users. Official method and mainnet URL on that page: `POST https://api.hyperliquid.xyz/info`.

Official Exchange endpoint page: the exchange endpoint is used to interact with and trade on the Hyperliquid chain. Official method and mainnet URL on that page: `POST https://api.hyperliquid.xyz/exchange`. Official note there: see the Python SDK for code to generate signatures.

This page records those two paths. It does not ingest the request-type lists behind them.

Sources: [Info endpoint](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/info-endpoint.md); [Exchange endpoint](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/exchange-endpoint.md) — checked 2026-09-16.

---

## Published WebSocket hosts

Official Websocket page: WebSocket endpoints are available for real-time data streaming and as an alternative to HTTP request sending.

| Network | WebSocket URL |
|---------|---------------|
| Mainnet | `wss://api.hyperliquid.xyz/ws` |
| Testnet | `wss://api.hyperliquid-testnet.xyz/ws` |

Official operational note on that page: automated users should handle server-side disconnects and reconnect. Disconnection from API servers may happen periodically and without announcement. Official recovery named there: missed data during reconnect will be present in the snapshot ack on reconnect; users can also query missed data with the corresponding info request.

Source: [Websocket](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/websocket.md) — checked 2026-09-16.

---

## Surfaces named, not ingested

Official docs name these call surfaces on the same public API hosts. Catalogs stay off this page.

| Surface | Official role on this `as-of` | Later slot |
|---------|-------------------------------|------------|
| Info | Read exchange and user state | Info endpoint |
| Exchange | Signed actions on the chain | Exchange endpoint |
| WebSocket | Subscriptions and post-over-WS | WebSocket |
| HyperEVM JSON-RPC | Separate official RPC surface | HyperEVM RPC |

How a node is run, and what a node is as an L1 participant, stay off this page.

---

## Gaps inside this scope

- Whether a stranger can run their own API server against a node, and which flags do that: **unknown here**. The official API servers page describes the role; it does not publish a runbook. Nodes-as-clients is a later S5 slot.
- Whether additional official REST or WebSocket hosts exist beyond the four URLs above: **unknown here**. These four are the ones published on the API and Websocket pages on this `as-of`.
- Info types, exchange actions, WebSocket schemas, signing, and rate-limit tables: **unknown here** by scope.
- HyperEVM JSON-RPC hosts and methods: **unknown here** by scope.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/api-servers.md | 1 | 2026-09-16 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api.md | 1 | 2026-09-16 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/info-endpoint.md | 1 | 2026-09-16 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/exchange-endpoint.md | 1 | 2026-09-16 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/websocket.md | 1 | 2026-09-16 |
