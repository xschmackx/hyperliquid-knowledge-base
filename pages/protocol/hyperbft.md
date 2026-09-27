# HyperBFT

| Field | Value |
|-------|--------|
| Shelf | Protocol (`pages/protocol/`) |
| Scope | Official name of L1 consensus, rounds, commits, height, and one-block finality as published. Not validator-stake accounting. Not HyperCore or HyperEVM product catalogues. Not a node runbook. |
| Status | Accepted |
| Page `as-of` | 2026-09-27 |
| Rank | All claims below are Rank 1 |

L1 identity and the HyperCore / HyperEVM split live on [What Hyperliquid is](what-hyperliquid-is.md). Shared state and native transfer live on [One state](one-state.md). Validator-set size, self-delegation, jail procedure, and commission rules live on [Validators and consensus stake](validators-and-consensus-stake.md). HyperEVM fast and slow blocks live on [Dual-block](dual-block.md).

---

## Official name

Official docs name the L1 consensus algorithm **HyperBFT**.

Two official phrasings sit side by side. They are not collapsed here:

- About Hyperliquid: a custom consensus algorithm called HyperBFT **inspired by HotStuff and its successors**. The same page says the algorithm and networking stack are optimized from the ground up to support the unique demands of the L1.
- HyperCore overview: Hyperliquid is secured by HyperBFT, **a variant of HotStuff consensus**. The same page says HyperBFT is optimized for end-to-end latency.

There is no dedicated official docs leaf titled HyperBFT (checked against the docs index on this `as-of`).

Sources:

- [About Hyperliquid](https://hyperliquid.gitbook.io/hyperliquid-docs/about-hyperliquid.md) — checked 2026-09-27
- [HyperCore overview](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/overview.md) — checked 2026-09-27
- [Docs index (`llms.txt`)](https://hyperliquid.gitbook.io/hyperliquid-docs/llms.txt) — checked 2026-09-27

Vote-message types, timeouts, leader rotation, and view-change are **unknown on this page**. Official leaves name the algorithm and those two HotStuff phrasings. They do not publish those internals.

---

## Rounds, commits, height

Official Staking Technical Details is the Rank 1 page that defines HyperBFT rounds and commits.

- A **quorum** is any set of validators with **more than ⅔ of the total stake**. The operating requirement of consensus is that a quorum of stake is honest (non-Byzantine).
- HyperBFT consensus proceeds in **rounds**. A round is a fundamental discrete bundle of transactions along with signatures from a quorum of validators.
- Each round **may be committed** after certain conditions are met. Those conditions themselves are **unpublished** on the official leaves checked here. After a round is committed, it is sent to the execution state for processing.
- A key property named on that page: all honest nodes agree on the ordered list of committed rounds.
- Rounds **may** result in a new execution-state block. Execution blocks are indexed by a separate counter called **height**. Height increments only on consensus rounds with **at least one transaction**.

Round, height, and HyperEVM block index are not one counter. Dual-block numbers are not defined as HyperBFT rounds; they live on [Dual-block](dual-block.md).

Who is in the validator set, the 10k self-delegation rule, the top-27 active set, jail votes as an operator rule, and commission caps live on [Validators and consensus stake](validators-and-consensus-stake.md). This page does not reprint those tables.

Source: [Staking](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/staking.md) — checked 2026-09-27.

---

## Epoch as consensus clock

Official Staking page: the validator set evolves in epochs of **100k rounds**, which is approximately **90 minutes** on mainnet. Validators and consensus stakes are static for each staking epoch.

100k rounds and ~90 minutes are official published figures on 2026-09-27. Whether every mainnet epoch is measured at 90 minutes, and what the testnet duration is, is **unknown here** beyond that sentence.

Source: [Staking](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/staking.md) — checked 2026-09-27.

---

## Finality and committed response

Official About page: HyperCore orders, cancels, trades, and liquidations happen transparently with **one-block finality inherited from HyperBFT**. This page does not add exceptions that leaf does not state.

Official HyperCore overview: end-to-end latency is the duration between sending a request and receiving a **committed** response. Published co-located-client figures on that leaf on this check: median **0.2 seconds**, 99th percentile **0.9 seconds**. Treat those as official published figures on 2026-09-27, not measurements made by this desk.

Throughput figures on that overview (mainnet order rate; consensus plus networking scaling once execution keeps up) are execution capacity, not HyperBFT internals. They are not restated here.

Sources:

- [About Hyperliquid](https://hyperliquid.gitbook.io/hyperliquid-docs/about-hyperliquid.md) — checked 2026-09-27
- [HyperCore overview](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/overview.md) — checked 2026-09-27

---

## Same consensus for HyperCore and HyperEVM

Official HyperEVM hub: HyperEVM is not a separate chain. It is secured by the **same HyperBFT consensus as HyperCore**.

Official developer HyperEVM page: EVM blocks are built as part of Hyperliquid's execution and inherit all security from HyperBFT consensus.

Official HyperCore overview: one consistent order of transactions through HyperBFT. Shared-state and transfer mechanics live on [One state](one-state.md).

Sources:

- [HyperEVM](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperevm.md) — checked 2026-09-27
- [HyperEVM (developer)](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm.md) — checked 2026-09-27
- [HyperCore overview](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/overview.md) — checked 2026-09-27

---

## Gaps inside this scope

- Dedicated official HyperBFT specification leaf: **none** on the docs index checked 2026-09-27.
- Vote-message types, timeouts, leader rotation, view-change, and the unpublished “certain conditions” that commit a round: **unknown here**.
- Whether “one-block finality inherited from HyperBFT” has exceptions: **unknown here**. About asserts the sentence; this page does not add conditions.
- Testnet epoch length: **unknown here**. Official ~90 minutes is mainnet.
- HotStuff paper phases and any Tendermint-era history: **not used**. Official leaves checked here do not publish them.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/about-hyperliquid.md | 1 | 2026-09-27 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/overview.md | 1 | 2026-09-27 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/staking.md | 1 | 2026-09-27 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/hyperevm.md | 1 | 2026-09-27 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm.md | 1 | 2026-09-27 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/llms.txt | 1 | 2026-09-27 |
