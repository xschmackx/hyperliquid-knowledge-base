# Nonces and API wallets

| Field | Value |
|-------|--------|
| Shelf | APIs and tooling (`pages/tooling/`) |
| Scope | Official published rules for nonces on signed actions and for API wallets (also called agent wallets). Not the exchange-action catalog. Not signing construction. Not info request types. Not WebSocket. Not SDK usage. Not rate limits. |
| Status | Accepted |
| Page `as-of` | 2026-11-09 |
| Rank | Claims below are Rank 1 unless tagged |

This page records the official rules Hyperliquid publishes for nonces and API wallets. It does not list exchange action `type` strings, construct signatures, catalog info requests, describe WebSocket channels, or show SDK calls. Those stay on their accepted S5 pages. The exchange endpoint envelope (including `nonce` and `signature`) is on [`exchange-endpoint.md`](exchange-endpoint.md). Official SDKs are on [`official-sdks.md`](official-sdks.md). Info and WebSocket stay on their pages.

---

## Background

A decentralized L1 must prevent replay attacks. When a user signs a USDC transfer transaction, the receiver cannot broadcast it multiple times to drain the sender's wallet. To solve this Ethereum stores a "nonce" for each address, which is a number that starts at 0. Each transaction must use exactly "nonce + 1" to be included.

Ethereum's design does not work for an onchain order book. A market making strategy can send thousands of orders and cancels in a second. Requiring a precise ordering of inclusion on the blockchain will break any strategy.

Sources: [Nonces and API wallets](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/nonces-and-api-wallets.md) — checked 2026-11-09.

---

## API wallets

These are also known as `agent wallets` in the docs. A master account can approve API wallets to sign on behalf of the master account or any of the sub-accounts.

Note that API wallets are only used to sign. To query the account data associated with a master or sub-account, you must pass in the actual address of that account. A common pitfall is to use the agent wallet which leads to an empty result.

Official `approveAgent` action (on the Exchange endpoint) publishes limits: an account can have 1 unnamed approved wallet and up to 3 named ones. Additional 2 named agents are allowed per subaccount. A custom expiration can be set by appending `valid_until {timestamp}` after the name. The expiration can be at most 180 days in the future. The nonce inside the action must match the nonce in the outer request body. See the accepted [`exchange-endpoint.md`](exchange-endpoint.md) for the action envelope and the official pointer back to this page. Do not rewrite that catalog here.

Sources: [Nonces and API wallets](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/nonces-and-api-wallets.md); [Exchange endpoint](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/exchange-endpoint.md) — checked 2026-11-09.

---

## API wallet pruning

API wallets and their associated nonce state may be pruned in the following cases:

1. The wallet is deregistered. This happens to an existing unnamed API Wallet when an ApproveAgent action is sent to register a new unnamed API Wallet. This also happens to an existing named API Wallet when an ApproveAgent action is sent with a matching name.
2. The wallet expires.
3. The account that registered the agent no longer has funds.

**Important:** for those using API wallets programmatically, it is **strongly** suggested to not reuse their addresses. Once an agent is deregistered, its used nonce state may be pruned. Generate a new agent wallet on future use to avoid unexpected behavior. For example, previously signed actions can be replayed once the nonce set is pruned.

Exact pruning timing or retention beyond these three cases is not published on this page. Unknown stays unknown.

Sources: [Nonces and API wallets](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/nonces-and-api-wallets.md) — checked 2026-11-09.

---

## Hyperliquid nonces

On Hyperliquid, the 100 highest nonces are stored per address. Every new transaction must have nonce larger than the smallest nonce in this set and also never have been used before. Nonces are tracked per signer, which is the user address if signed with private key of the address, or the agent address if signed with an API wallet.

Nonces must be within `(T - 2 days, T + 1 day)`, where `T` is the unix millisecond timestamp on the block of the transaction.

Official recommended practice on Exchange headings: use the current timestamp in milliseconds. An atomic counter can be fast-forwarded to current unix milliseconds if needed. The official page also notes a `noop` action that marks a nonce used without other effect (see [`exchange-endpoint.md`](exchange-endpoint.md)).

The following steps may help port over an automated strategy from a centralized exchange:

1. Use a API wallet per trading process. Note that nonces are stored per signer (i.e. private key), so separate subaccounts signed by the same API wallet will share the nonce tracker of the API wallet. It's recommended to use separate API wallets for different subaccounts.
2. In each trading process, have a task that periodically batches order and cancel requests every 0.1 seconds. It is recommended to batch IOC and GTC orders separately from ALO orders because ALO order-only batches are prioritized by the validators.
3. The trading logic tasks send orders and cancels to the batching task.
4. For each batch of orders or cancels, fetch and increment an atomic counter that ensures a unique nonce for the address. The atomic counter can be fast-forwarded to current unix milliseconds if needed.

This structure is robust to out-of-order transactions within 2 seconds, which should be sufficient for an automated strategy geographically near an API server.

Precise validator prioritization details beyond the ALO note are not published here. Unknown stays unknown.

Sources: [Nonces and API wallets](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/nonces-and-api-wallets.md); [Exchange endpoint](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/exchange-endpoint.md) — checked 2026-11-09.

---

## Suggestions for subaccount and vault users

Note that nonces are stored per signer, which is the address of the private key used to sign the transaction. Therefore, it's recommended that each trading process or frontend session use a separate private key for signing. In particular, a single API wallet signing for a user, vault, or subaccount all share the same nonce set.

If users want to use multiple subaccounts in parallel, it would easier to generate two separate API wallets under the master account, and use one API wallet for each subaccount. This avoids collisions between the nonce set used by each subaccount.

Sources: [Nonces and API wallets](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/nonces-and-api-wallets.md) — checked 2026-11-09.

---

## Surfaces named, not ingested

| Surface | Why it is off this page |
|---------|-------------------------|
| Exchange action catalog and envelope | Already on [`exchange-endpoint.md`](exchange-endpoint.md). `approveAgent` and `noop` are named there. |
| Signing construction | Official Signing page exists. How to build the payload and signature stays off this page. |
| Official SDKs | Already on [`official-sdks.md`](official-sdks.md). Python SDK is the official pointer for signature code. |
| Info endpoint | Read requests. Already on [`info-endpoint.md`](info-endpoint.md). Agent address for queries returns empty. |
| WebSocket | Subscriptions and post-over-WS. Already on [`websocket.md`](websocket.md). |
| Rate limits | Official table lives on its page. Not this nonce/API-wallet page. |

---

## Gaps inside this scope

- Exact pruning timing or retention of nonce state beyond the three published cases (deregistered, expired, no funds): **unknown here**.
- Precise validator prioritization details beyond the published ALO-order-only batch note: **unknown here**.
- Whether live behavior matches every sentence on the Rank 1 page after this `as-of`: **unknown here**. Live endpoints were not exercised for this check.
- Signing construction, full exchange action catalog, info types, WebSocket channels, SDK internals, rate-limit weights: **unknown here** by scope. Point at the accepted S5 pages named above.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/nonces-and-api-wallets.md | 1 | 2026-11-09 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/exchange-endpoint.md | 1 | 2026-11-09 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/signing.md | 1 | 2026-11-09 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/llms.txt | 1 | 2026-11-09 |

Accepted pages pointed at, not rewritten: [`exchange-endpoint.md`](exchange-endpoint.md) (`as-of` 2026-09-17), [`official-sdks.md`](official-sdks.md) (`as-of` 2026-09-28), [`info-endpoint.md`](info-endpoint.md), [`websocket.md`](websocket.md).
