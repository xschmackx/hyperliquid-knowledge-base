# Dual-block

| Field | Value |
|-------|--------|
| Shelf | Protocol (`pages/protocol/`) |
| Scope | HyperEVM fast/slow block design as protocol architecture. |
| Status | Accepted |
| Page `as-of` | 2026-09-16 |
| Rank | All claims below are Rank 1 |

This page does not cover L1 identity, native transfers, read precompiles, or CoreWriter. Those live on [What Hyperliquid is](what-hyperliquid-is.md) and [One state](one-state.md). It does not cover how to set RPC, sign an SDK call, or use an explorer.

---

## Why two HyperEVM block types

Official Dual-block architecture page: total HyperEVM throughput is split between **small blocks produced at a fast rate** and **large blocks produced at a slower rate**.

The published reason is to decouple block speed and block size when allocating throughput improvements. Official text: users want faster blocks for lower time to confirmation; builders want larger blocks to include larger transactions such as more complex contract deployments. Instead of a forced tradeoff, the dual-block system is described as allowing simultaneous improvement along both axes.

Whether HyperCore L1 blocks themselves use this split is **unknown on this page**. Official dual-block text is about HyperEVM block types under the L1.

Source: [Dual-block architecture](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm/dual-block-architecture.md) — checked 2026-09-16.

---

## Two mempools, one EVM number line

Official dual-block page: the HyperEVM “mempool” is still onchain state with respect to the umbrella L1 execution, but is split into **two independent mempools** that source transactions for the two block types.

The two block types are interleaved with a **unique increasing sequence of EVM block numbers**.

Official mempool bounds on that page:

- The onchain mempool implementation accepts only the **next 8 nonces** for each address.
- Transactions older than **1 day** in the mempool are pruned.

How a transaction is assigned to the small-block mempool versus the large-block mempool, other than the `usingBigBlocks` flag below, is **unknown here**.

Source: same Dual-block architecture page, checked 2026-09-16.

---

## When an L1 block produces an EVM block

Official dual-block page defines *block duration* of `x` as: the first L1 block for each value of `l1_block_time % x` produces an EVM block.

Official interaction-timings page uses the same idea without the modulo: some L1 blocks produce a HyperEVM block; on those L1 blocks an EVM block is built after the L1 block is built. That timings page does not state the `l1_block_time % x` rule. Dual-block architecture is the source for the duration rule.

What unit `l1_block_time` is stored in, and what happens if more than one L1 block shares the same `l1_block_time % x` value, is **unknown here** beyond “the first L1 block for each value.”

Sources:

- [Dual-block architecture](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm/dual-block-architecture.md) — checked 2026-09-16
- [Interaction timings](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm/interaction-timings.md) — checked 2026-09-16

---

## Initial published durations and gas limits (dated)

Official dual-block page: the initial configuration is set conservatively, and throughput is expected to increase over successive technical upgrades.

As published on that page when checked 2026-09-16:

| Official name | Published duration | Published gas limit |
|---------------|--------------------|---------------------|
| Fast / small | 1 second | 3M |
| Slow / large | 1 minute | 30M |

Those numbers can change. Treat them as the official published initial figures on 2026-09-16, not a measurement made by this desk. Live values after a later official upgrade are **unknown here** until this page is re-checked.

Source: [Dual-block architecture](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm/dual-block-architecture.md) — checked 2026-09-16.

---

## `usingBigBlocks` as HyperCore user state

Official dual-block page: HyperEVM transactions are directed to big blocks instead of small blocks by the HyperCore action `evmUserModify` with `usingBigBlocks` set true.

Official constraints on that flag:

- It is user state on the **HyperCore user**, not an EVM-only setting.
- It **must be unset again** to target small blocks.
- Like any HyperCore action, it requires an **existing Core user** to send.

How a stranger constructs or signs that action is out of scope. JSON-RPC helpers for big-block gas price are out of scope.

Source: same Dual-block architecture page, checked 2026-09-16.

---

## Gaps inside this scope

- Current live duration and gas limits after the “initial configuration”: **unknown here** if official docs have since changed; this page records the figures published on the Dual-block architecture page as of 2026-09-16.
- Unit and origin of `l1_block_time`: **unknown here** beyond the official modulo rule.
- How the two independent mempools select transactions aside from `usingBigBlocks`: **unknown here**.
- Whether small/fast and large/slow can be paired differently than the published initial table: **unknown here**.
- Dual-block behaviour for HyperCore matching-engine blocks (not HyperEVM): **unknown here**. Official text is HyperEVM architecture.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm/dual-block-architecture.md | 1 | 2026-09-16 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm/interaction-timings.md | 1 | 2026-09-16 |
