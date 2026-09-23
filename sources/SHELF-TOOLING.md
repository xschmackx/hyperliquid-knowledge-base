# SHELF — APIS AND TOOLING

This page names what belongs on the APIs-and-tooling shelf. It is not an accepted corpus page. It does not ingest facts.

Use official names as Hyperliquid publishes them. Do not invent a parallel vocabulary. Do not copy live URL lists or SDK versions into this rule.

---

## Shelf

| Field | Value |
|-------|--------|
| Shelf | APIs and tooling |
| Corpus path | `pages/tooling/` |
| Question this shelf answers | How does a stranger talk to Hyperliquid from software? |

A tooling page explains official interfaces: API servers, info and exchange endpoints, WebSocket, official SDKs, HyperEVM RPC, and how to run or read a node. What those calls *mean* as market, fee, or risk stays on Markets, Accounts, or Risk. What a node *is* in the L1 stays on Protocol.

---

## In scope

Place a page on this shelf when its scoped question is one of these:

| Slot | About |
|------|--------|
| API servers | What an official API server does (serves state, forwards transactions). Endpoints as *how to call*, not as L1 architecture. |
| Info endpoint | Read requests. Official `info` types as published. |
| Exchange endpoint | Signed actions. Official `exchange` actions as published. |
| WebSocket | Subscriptions and post-over-WS. Disconnect / reconnect as published. |
| Official SDKs | First-party SDKs and examples Hyperliquid publishes. |
| HyperEVM RPC | Official JSON-RPC and chain parameters *as connection data*. Dual-block as architecture stays on Protocol. |
| Nodes as clients | How to run or read a node, flags, data layouts. Node-as-L1-participant stays on Protocol. |
| Official explorers and status pages | First-party only unless tagged `secondary`. |

Live base URLs, chain IDs, and package versions belong only on accepted pages with `as-of` + URL. This shelf rule does not record them. The official source index is the place for a dated URL list.

---

## Out of scope (other shelves)

| Topic | Shelf |
|-------|--------|
| HyperBFT, HyperCore/HyperEVM as components, node as L1 participant | Protocol |
| What a perp or spot market *is* | Markets |
| Fee schedules, referrals, builder-code *economics* | Accounts |
| Margin, liquidation, ADL *rules* | Risk |
| Observation entries | Register |

A page that both explains an action and the risk it triggers splits: call shape here, risk there. Link across.

Community dashboards and unofficial clients may appear only tagged `secondary` or `community`. They cannot be the sole support for an accepted claim.

---

## Filing

- Accepted pages: `pages/tooling/<slug>.md`
- Shelf index: `pages/tooling/README.md`
