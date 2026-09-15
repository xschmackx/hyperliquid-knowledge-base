> Copy for the corpus stranger. Decision home: [hlkb-oversight/SHELF-RISK.md](https://github.com/xschmackx/hlkb-oversight/blob/main/SHELF-RISK.md). Do not fork a second risk shelf.

# SHELF — RISK AND OPERATIONS

Durable doctrine. S4. Recorded as D-HLKB-012.

This page names what belongs on the risk-and-operations shelf. It is not an accepted corpus page. It does not ingest facts.

Use official names as Hyperliquid publishes them. Do not invent a parallel vocabulary. Do not copy live formulas or thresholds into this rule.

---

## Shelf

| Field | Value |
|-------|--------|
| Shelf | Risk and operations |
| Corpus path | `pages/risk/` |
| Question this shelf answers | How can a position or the system fail, and what does the protocol do then? |

A risk page explains margin *use*, liquidation and auto-deleveraging, portfolio-margin risk, and operational acts that change a live position (halt, delist consequences). Account *types* and fee schedules stay on S3. Market *products* stay on S2.

---

## In scope

Place a page on this shelf when its scoped question is one of these:

| Slot | About |
|------|--------|
| Margin modes | Cross, isolated, strict isolated — how collateral is shared or fenced, as risk. |
| Initial and maintenance margin | What official docs call initial vs maintenance margin. Live percents wait for an accepted page with `as-of`. |
| Margin tiers | Position-size tiers that change max leverage, as risk. |
| Liquidations | When liquidation starts, book attempt vs backstop, isolated vs cross effects. |
| Auto-deleveraging | Official ADL behaviour. |
| Portfolio margin as risk | PMR, portfolio maintenance, borrow liquidation. The *choice* of account mode as an account rule stays on S3. |
| HIP-3 margin across DEXs | How cross margin behaves when positions sit on more than one perp DEX. HIP-3 as a *listing product* stays on S2. |
| Operational acts on live markets | Halt, settlement, delist *consequences for open risk*. The listing/delist product rule stays on S2. |
| Incidents | What changed for users when official sources say the system misbehaved or paused. Dated. Not a secret ops log. |

Clearinghouse as an execution *component* is Protocol (S1). Clearinghouse *margin state as user risk* is this shelf.

---

## Out of scope (other shelves)

| Topic | Shelf |
|-------|--------|
| HyperBFT, validator set, nodes as L1 participants | S1 Protocol |
| Perp/spot products, HIP-1/HIP-3 listings, HLP as a product | S2 Markets |
| Account types, balances, fee schedules, staking discounts and rewards | S3 Accounts |
| How to query margin or send an order over API | S5 Tooling |
| Observation entries | S6 Register |

If a page needs both the risk rule and the fee or the product, split it. Risk stays here. Link across.

---

## Filing

- Accepted pages, when they exist: `pages/risk/<slug>.md`
- Empty shelf marker now: corpus `pages/risk/README.md`
- This rule: oversight `SHELF-RISK.md`. Stranger copy: corpus `sources/SHELF-RISK.md`

No accepted risk page is opened by this decision. Formulas and thresholds are not recorded here.

---

## Where this rule lives

| Role | Where |
|------|--------|
| Decision home | `hlkb-oversight/SHELF-RISK.md` |
| Stranger copy | `hyperliquid-knowledge-base/sources/SHELF-RISK.md` |
| Pages | `hyperliquid-knowledge-base/pages/risk/` |

`DECISION-LOG.md` records acceptance. `Notebook/` is not this shelf.
