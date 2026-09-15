> Copy for the corpus stranger. Decision home: [hlkb-oversight/SHELF-PROTOCOL.md](https://github.com/xschmackx/hlkb-oversight/blob/main/SHELF-PROTOCOL.md). Do not fork a second protocol shelf.

# SHELF — PROTOCOL

Durable doctrine. S1. Recorded as D-HLKB-009.

This page names what belongs on the protocol shelf. It is not an accepted corpus page. It does not ingest facts.

Use official names as Hyperliquid publishes them. Do not invent a parallel vocabulary.

---

## Shelf

| Field | Value |
|-------|--------|
| Shelf | Protocol |
| Corpus path | `pages/protocol/` |
| Question this shelf answers | What is the Hyperliquid chain, and how does it run? |

A protocol page explains the L1 itself: consensus, execution split, validators as consensus participants, and the mechanisms that make HyperCore and HyperEVM one state.

---

## In scope

Place a page on this shelf when its scoped question is one of these:

| Slot | About |
|------|--------|
| What Hyperliquid is | L1 identity. Not a venue list. |
| HyperBFT | Consensus. Rounds, commits, what official docs call HyperBFT. |
| Validators and consensus stake | How the validator set and stake secure the chain. Not fee-discount or rewards accounting. |
| HyperCore | Execution component that holds matching and margin state. The component, not the market catalogue. |
| HyperEVM | Execution component for general-purpose contracts. Same consensus. Not a dapp directory. |
| One state | How HyperCore and HyperEVM share HyperBFT and pass value or reads. Native transfers belong here as mechanism. |
| Dual-block | HyperEVM fast/slow block design as protocol architecture. |
| Nodes as L1 participants | What a node is in the protocol. Runbooks and client how-to live on Tooling (S5) or Risk and ops (S4). |

Throughput, latency, chain IDs, and similar figures may appear on a protocol page only with `as-of` + URL under `SOURCE-RANK.md`. This shelf rule does not record those figures.

---

## Out of scope (other shelves)

| Topic | Shelf |
|-------|--------|
| Order types, books, listings, HIP-3 markets as products | S2 Markets |
| Fees, rewards, HYPE as discount or payout | S3 Accounts and fees |
| Liquidation *parameters*, margin *use*, incident response | S4 Risk and ops |
| REST, WebSocket, RPC how-to, SDKs, explorers | S5 Tooling |
| Observation entries | S6 Register |

If a page needs both the mechanism and the product, split it. Mechanism stays here. Product goes to the other shelf. Link across. Do not duplicate the claim in two voices.

---

## Filing

- Accepted pages, when they exist: `pages/protocol/<slug>.md`
- Empty shelf marker now: corpus `pages/protocol/README.md`
- This rule: oversight `SHELF-PROTOCOL.md`. Stranger copy: corpus `sources/SHELF-PROTOCOL.md`

No accepted protocol page is opened by this decision. Slots above are names for later pages, not a promise that each slot is already known.

If official docs do not cover a slot, the later page writes a gap. It does not fill from chat.

---

## Where this rule lives

| Role | Where |
|------|--------|
| Decision home | `hlkb-oversight/SHELF-PROTOCOL.md` |
| Stranger copy | `hyperliquid-knowledge-base/sources/SHELF-PROTOCOL.md` |
| Pages | `hyperliquid-knowledge-base/pages/protocol/` |

`DECISION-LOG.md` records acceptance. `Notebook/` is not this shelf.
