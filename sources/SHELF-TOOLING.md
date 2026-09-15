> Copy for the corpus stranger. Decision home: [hlkb-oversight/SHELF-TOOLING.md](https://github.com/xschmackx/hlkb-oversight/blob/main/SHELF-TOOLING.md). Do not fork a second tooling shelf.

# SHELF — APIS AND TOOLING

Durable doctrine. S5. Recorded as D-HLKB-013.

This page names what belongs on the APIs-and-tooling shelf. It is not an accepted corpus page. It does not ingest facts.

Use official names as Hyperliquid publishes them. Do not invent a parallel vocabulary. Do not copy live URL lists or SDK versions into this rule.

---

## Shelf

| Field | Value |
|-------|--------|
| Shelf | APIs and tooling |
| Corpus path | `pages/tooling/` |
| Question this shelf answers | How does a stranger talk to Hyperliquid from software? |

A tooling page explains official interfaces: API servers, info and exchange endpoints, WebSocket, official SDKs, HyperEVM RPC, and how to run or read a node. What those calls *mean* as market, fee, or risk stays on S2–S4. What a node *is* in the L1 stays on S1.

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
| HyperEVM RPC | Official JSON-RPC and chain parameters *as connection data*. Dual-block as architecture stays on S1. |
| Nodes as clients | How to run or read a node, flags, data layouts. Node-as-L1-participant stays on S1. |
| Official explorers and status pages | First-party only unless tagged `secondary`. |

Live base URLs, chain IDs, and package versions belong only on accepted pages with `as-of` + URL. This shelf rule does not record them. I1 (official source index) is the place for a dated URL list, when named.

---

## Out of scope (other shelves)

| Topic | Shelf |
|-------|--------|
| HyperBFT, HyperCore/HyperEVM as components, node as L1 participant | S1 Protocol |
| What a perp or spot market *is* | S2 Markets |
| Fee schedules, referrals, builder-code *economics* | S3 Accounts |
| Margin, liquidation, ADL *rules* | S4 Risk |
| Observation entries | S6 Register |

A page that both explains an action and the risk it triggers splits: call shape here, risk there. Link across.

Community dashboards and unofficial clients may appear only tagged `secondary` or `community`. They cannot be the sole support for an accepted claim.

---

## Filing

- Accepted pages, when they exist: `pages/tooling/<slug>.md`
- Empty shelf marker now: corpus `pages/tooling/README.md`
- This rule: oversight `SHELF-TOOLING.md`. Stranger copy: corpus `sources/SHELF-TOOLING.md`

No accepted tooling page is opened by this decision.

---

## Where this rule lives

| Role | Where |
|------|--------|
| Decision home | `hlkb-oversight/SHELF-TOOLING.md` |
| Stranger copy | `hyperliquid-knowledge-base/sources/SHELF-TOOLING.md` |
| Pages | `hyperliquid-knowledge-base/pages/tooling/` |

`DECISION-LOG.md` records acceptance. `Notebook/` is not this shelf.
