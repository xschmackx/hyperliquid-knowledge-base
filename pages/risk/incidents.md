# Incidents and published pauses

| Field | Value |
|-------|--------|
| Shelf | Risk and operations (`pages/risk/`) |
| Scope | Dated official statements that the system misbehaved, paused, delayed orders, or locked a named bridge, plus the user-facing change those sources stated. Not standing halt, settlement, or delist rules. Not liquidations, ADL, or margin. Not an unpublished ops log. |
| Status | Accepted |
| Page `as-of` | 2026-09-28 |
| Rank | Claims below are Rank 1 unless tagged |

This page is the dated public record. Standing named acts on already-open markets — validator **delist**, HIP-3 **`haltTrading`**, quote-asset disable — stay on [Operational acts on live markets](operational-acts.md). Those acts are product rules. An event belongs here only when an official source dated a misbehaviour, pause, delay, or lock and stated what changed for users.

This page is not a complete history of every user-visible glitch. It records what Rank 1 docs and Rank 2/3 official surfaces published. Absence from those surfaces is not proof that nothing happened. That absence is **unknown**.

---

## Official names on official surfaces

Official docs and the official status page use these names:

- **Network upgrade** — scheduled maintenance on the official status page. Typical published text: expect about 10 minutes of downtime. Completed entries often name the component **Hyperliquid L1**.
- **Post-only period of a network upgrade** — Rank 1 Order types name for the matching window during that upgrade.
- **API server order delays** — official status incident name. Components on that surface: **Frontend**, **Hyperliquid L1**, **API**.
- **Arbitrum bridge** / **automatic locking** / **automatically locked** — official announcements and later official clarification for a dated deposit/withdraw pause on that bridge.
- **POPCAT** — market name used in the official Nov 2025 clarification.

This page does not invent “market freeze,” “circuit breaker,” “kill switch,” or CEX incident taxonomies.

The official status hub and history are the dated ledger for named upgrades and status incidents. A later tooling page owns explorers and status pages as a product. This page only cites those URLs.

Sources: [Order types](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/order-types.md) (Rank 1); [Hyperliquid status](https://hyperliquid.statuspage.io/) and [status history](https://hyperliquid.statuspage.io/history) (Rank 2/3) — checked 2026-09-28.

---

## Matching during a network-upgrade post-only period

Rank 1 Order types: market orders and TWAP suborders **do not fill during the post-only period of a network upgrade**.

That is the published matching effect of a dated upgrade window. It is not Delisting and not HIP-3 `haltTrading`. Whether resting GTC is cancelled in that window is **unknown** on Rank 1. This page does not invent cancel behaviour for resting GTC.

Source: [Order types](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/order-types.md) — checked 2026-09-28.

---

## Dated official rows

Only rows with a date and an official URL. Unpublished events stay **unknown**.

### Scheduled network upgrades (pattern)

The official status history publishes repeating **Network upgrade** windows. Typical published user-facing text: expect about 10 minutes of downtime. Completed rows often state that scheduled maintenance affected **Hyperliquid L1**.

Examples visible on the history slice checked 2026-09-28 (UTC windows as published on that surface): 26 Sep 2026 08:30–08:50; 19 Sep 2026 08:30–08:50; 5 Sep 2026 09:30–09:45; 29 Aug 2026 08:30–08:39; 23 Aug 2026 08:15–08:35; 15 Aug 2026 08:00–08:20; 25 Jul 2026 07:30–07:50. One completed example page: [25 Jul 2026 Network upgrade](https://hyperliquid.statuspage.io/incidents/yy1hx8bn903c).

This list is not every historical row. The history UI is paged. Do not treat this page as a complete 2023–2026 catalogue. Use the [status history](https://hyperliquid.statuspage.io/history) for further dated windows.

User-facing change as published for those windows: expected short downtime; Rank 1 matching restriction above during the post-only period.

### 29 Jul 2025 — API server order delays

Official status incident [API server order delays](https://stspg.io/tscs80p22yyb) (Rank 2/3). Published text: issue with API servers **between 14:10 and 14:47 UTC**; **orders were delayed in being sent to the nodes**; **significant spike in traffic**; **no hack or exploit**; patched; further protections promised.

User-facing change as published: delayed order submission to nodes for that window. Official text names API servers, not an L1 freeze. Do not read this row as a book halt.

### 12 Nov 2025 — Arbitrum bridge automatic locking (POPCAT named in later official text)

Official announcements channel (Rank 3), 12 Nov 2025: **“The Arbitrum bridge's automatic locking was triggered by a conservative set of conditions, and the bridge was unlocked after the situation was thoroughly investigated within ~25 minutes. Funds are safe. The Hyperliquid blockchain itself was not impacted and experienced no downtime.”**

Later official written clarification on Hyperliquid-controlled channels (Rank 3): **“Suspicious activity on POPCAT in Nov 2025 did not cause the L1 to freeze, nor were any user funds frozen. The L1 was entirely operational, and any observer can see the blocks that were produced during this time. The Arbitrum bridge was automatically locked after the incident due to abnormal variation in account balances.”** Same clarification names the Arbitrum bridge as **not as secure as natively minted USDC**, **conservative automated locking mechanisms**, locking mechanism **audited and open sourced**, and the bridge **being deprecated** with native USDC.

User-facing change as published: Arbitrum-bridge deposit and withdraw paused for that window; unlocked after investigation of about 25 minutes; funds safe; L1 not frozen; user funds not frozen. Official text does not describe L1 trading as paused.

This page does not reconstruct HLP PnL, wallet counts, or unofficial root cause. Journalism on the same dates exists as Rank 4 and does not establish those figures here.

Channel: [hyperliquid_announcements](https://t.me/hyperliquid_announcements).

### 11 Oct 2025 — official non-incident

@HyperliquidX (listed on the official source index), [11 Oct 2025](https://x.com/HyperliquidX/status/1976888543948816750) (Rank 3): **zero downtime or latency issues** during that volatility window; risk and margining **functioned as designed**.

That is an official *non-incident* statement. 10–11 Oct 2025 is not listed here as an outage.

---

## What this is not

- **Not standing operational acts.** Delist, `haltTrading`, `disableDex`, and `delistedCanceled` stay on [Operational acts on live markets](operational-acts.md). A dated announcement that only restates those product rules is not an incident on this page.
- **Not liquidations, ADL, or margin.** Those stay on the accepted S4 pages for those mechanisms.
- **Not a secret ops log.** Discord-only remarks are not enough unless the same words appear on Statuspage, @HyperliquidX, official announcements, or Rank 1 docs.
- **Not native USDC migration as an incident.** Official posts that frame a product migration, without a published pause, stay off this page.
- **Not JellyJelly or other 2025 market events** unless Rank 1–3 dated a misbehaviour or pause. Without that text they stay **unknown** / omitted. Delist-as-product stays on operational acts and listings pages.

---

## Gaps inside this scope

- Completeness of every status-page history row across years: **unknown** (paged UI; this page lists pattern examples only).
- Resting GTC behaviour during the post-only period of a network upgrade: **unknown** on Rank 1.
- Any event official Rank 1–3 surfaces did not publish: **unknown**.
- Root-cause, HLP PnL, and wallet-graph reconstructions from Rank 4 journalism: not accepted fact on this page.
- Rank 1 docs have no dedicated incidents or post-mortem leaf (`llms.txt` checked 2026-09-28).

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/order-types.md | 1 | 2026-09-28 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/llms.txt | 1 | 2026-09-28 |
| https://hyperliquid.statuspage.io/ | 2/3 | 2026-09-28 |
| https://hyperliquid.statuspage.io/history | 2/3 | 2026-09-28 |
| https://hyperliquid.statuspage.io/incidents/yy1hx8bn903c | 2/3 | 2026-09-28 |
| https://stspg.io/tscs80p22yyb | 2/3 | 2026-09-28 |
| https://t.me/hyperliquid_announcements | 3 | 2026-09-28 |
| https://x.com/HyperliquidX/status/1976888543948816750 | 3 | 2026-09-28 |
