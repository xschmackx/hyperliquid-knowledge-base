> Copy for the corpus stranger. Decision home: [hlkb-oversight/SHELF-MARKETS.md](https://github.com/xschmackx/hlkb-oversight/blob/main/SHELF-MARKETS.md). Do not fork a second markets shelf.

# SHELF — MARKETS

Durable doctrine. S2. Recorded as D-HLKB-010.

This page names what belongs on the markets shelf. It is not an accepted corpus page. It does not ingest facts.

Use official names as Hyperliquid publishes them. Do not invent a parallel vocabulary.

Protocol mechanism stays on `SHELF-PROTOCOL.md`. This shelf is the tradable products and how those markets are defined and listed.

---

## Shelf

| Field | Value |
|-------|--------|
| Shelf | Markets |
| Corpus path | `pages/markets/` |
| Question this shelf answers | What can be traded, listed, or provided as liquidity, and how is that market defined? |

A markets page explains HyperCore products: perpetual and spot markets, order types and book behaviour as the user meets them, listing rules, builder-deployed markets, and protocol vaults as liquidity products.

---

## In scope

Place a page on this shelf when its scoped question is one of these:

| Slot | About |
|------|--------|
| Perpetual markets | What a perp market is on HyperCore. Contract specs as published. Not the HyperCore component itself. |
| Spot markets | What a spot market is on HyperCore. |
| Order types and the book | Orders, cancels, triggers, and book behaviour as market structure. |
| Listings and HIP-1 | How spot assets are listed, including the official auction named HIP-1. |
| HIP-3 | Builder-deployed perpetual markets. Market definition and deployer duties as published. |
| Oracles and marks | Oracle and mark used to *define* a market. Not trader-facing margin math. |
| Funding | Funding as a market mechanism. |
| Protocol vaults | HLP and other official protocol vaults as liquidity products. Deposit lock as product rule. Fee-share *rates* live on S3. |
| Aligned quote assets | Official aligned-quote primitive as a market building block. |

A live catalogue of every listed coin is not required for a page to belong here. If a page lists markets, every row needs `as-of` + URL. This shelf rule does not record that catalogue.

---

## Out of scope (other shelves)

| Topic | Shelf |
|-------|--------|
| HyperCore / HyperEVM as execution components; native transfers as L1 mechanism | S1 Protocol |
| Trading fees, maker/taker schedule, rewards, HYPE as discount or payout | S3 Accounts and fees |
| Liquidation *parameters*, margin *use*, position risk, incident response | S4 Risk and ops |
| How to send an order over REST, WebSocket, or SDK | S5 Tooling |
| Observation entries | S6 Register |

If a page needs both the product and the fee or the risk number, split it. Product stays here. Link across. Do not duplicate the claim in two voices.

---

## Filing

- Accepted pages, when they exist: `pages/markets/<slug>.md`
- Empty shelf marker now: corpus `pages/markets/README.md`
- This rule: oversight `SHELF-MARKETS.md`. Stranger copy: corpus `sources/SHELF-MARKETS.md`

No accepted markets page is opened by this decision. Slots above are names for later pages, not a promise that each slot is already known.

If official docs do not cover a slot, the later page writes a gap. It does not fill from chat.

---

## Where this rule lives

| Role | Where |
|------|--------|
| Decision home | `hlkb-oversight/SHELF-MARKETS.md` |
| Stranger copy | `hyperliquid-knowledge-base/sources/SHELF-MARKETS.md` |
| Pages | `hyperliquid-knowledge-base/pages/markets/` |

`DECISION-LOG.md` records acceptance. `Notebook/` is not this shelf.
