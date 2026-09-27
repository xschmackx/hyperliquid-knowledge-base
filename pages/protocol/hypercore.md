# HyperCore

| Field | Value |
|-------|--------|
| Shelf | Protocol (`pages/protocol/`) |
| Scope | Official execution component that holds matching-engine state and margin state (clearinghouse + per-asset books). The component, not the market catalogue. |
| Status | Accepted |
| Page `as-of` | 2026-09-27 |
| Rank | All claims below are Rank 1 |

L1 identity and the two-component split live on [What Hyperliquid is](what-hyperliquid-is.md). Rounds, commits, height, and one-block finality live on [HyperBFT](hyperbft.md). Shared state and Core↔EVM transfer live on [One state](one-state.md).

This page is not a listings catalogue, not a HyperEVM product page, not a HyperBFT rewrite, and not a node or API runbook.

---

## The execution component

Official docs split Hyperliquid state execution into two components: **HyperCore** and **HyperEVM**.

Official HyperCore overview: HyperCore includes **margin and matching engine state**. The same page says HyperCore does not rely on off-chain order books, and that one consistent order of transactions is achieved through HyperBFT.

Official About page: HyperCore includes fully onchain perpetual futures and spot order books. Every order, cancel, trade, and liquidation happens onchain with one-block finality inherited from HyperBFT.

Official site architecture copy uses the same two-component state and the same HyperBFT for both.

Official docs also group other leaves under a HyperCore *section* (USDC, API servers, oracle, staking, vaults, multi-sig, quote-asset HIPs, and others). Those leaves are other Taskmap slots or other shelves. This page names HyperCore as the execution component that holds matching and margin state. It is not an index of every leaf under that section.

Sources:

- [About Hyperliquid](https://hyperliquid.gitbook.io/hyperliquid-docs/about-hyperliquid.md) — checked 2026-09-27
- [HyperCore overview](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/overview.md) — checked 2026-09-27
- [HyperCore section index](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore.md) — checked 2026-09-27
- [Official site / tech](https://hyperliquid.xyz/tech) — checked 2026-09-27

---

## Margin state (clearinghouse)

Official Clearinghouse page: the perps clearinghouse is a component of **execution state on HyperCore**. It manages the perps margin state for each address, which includes balance and positions.

The same page:

- Deposits are first credited to an address's **cross** margin balance.
- Positions by default are also opened in cross margin mode.
- **Isolated** margin is also supported: margin can be allocated toward a specific position so that position's liquidation risk is disassociated from all other positions.
- The **spot clearinghouse** analogously manages spot user state for each address, including token balances and holds.

Cross and isolated here are account modes the clearinghouse holds. Maintenance fractions, tier tables, liquidation auction steps, auto-deleveraging, and portfolio-margin LTV caps are not this page. Those live on the risk shelf.

Source: [Clearinghouse](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/clearinghouse.md) — checked 2026-09-27.

---

## Matching-engine state (order books)

Official Order book page: HyperCore state includes an **order book for each asset**.

The same page:

- Orders are added where price is an integer multiple of the tick size, and size is an integer multiple of lot size.
- Orders are matched in **price-time priority**.
- Operations on order books for perp assets take a reference to the clearinghouse, because positions and margin checks are handled there.
- Margin checks happen on the opening of a new order, and again for the resting side at the matching of each order.

Matching state and margin state are two official pieces of the same component. This page does not list markets or order-type products.

Source: [Order book](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/order-book.md) — checked 2026-09-27.

---

## How book actions are applied in a block

Official Order book page: the L1 mempool and consensus logic are semantically aware of transactions that interact with HyperCore order books.

Within a block, actions are sorted within each consensus batch (the same page says there are usually 1–2 consensus batches of actions in a block):

1. Actions that do not send GTC or IOC orders to any book
2. Cancels
3. Actions that send at least one GTC or IOC

Within each category, actions are sorted in the order they were proposed by the block proposer. Modifies are categorized according to the new order they place.

That sort is how matching state is applied inside a committed batch. Rounds, commits, height, and vote protocol live on [HyperBFT](hyperbft.md). This page does not restate them.

Source: [Order book](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/order-book.md) — checked 2026-09-27.

---

## Same consensus as HyperEVM

Official HyperEVM hub: Hyperliquid has two key parts, HyperCore and HyperEVM. HyperEVM is not a separate chain. It is secured by the **same HyperBFT consensus as HyperCore**. The same hub says that lets HyperEVM interact directly with parts of HyperCore, such as spot and perp order books.

How that interaction is implemented (native transfer, precompiles, CoreWriter) lives on [One state](one-state.md). HyperEVM as its own execution component is a later Taskmap slot. This page does not write it.

Dual-block / fast-slow HyperEVM architecture is not required to explain HyperCore. It lives on [Dual-block](dual-block.md).

Sources:

- [HyperEVM](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperevm.md) — checked 2026-09-27
- [HyperCore overview](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/overview.md) — checked 2026-09-27

---

## Dated throughput and latency figures

Official About page, on this check: HyperCore currently supports **200k orders per second**, with throughput described as improving as node software is optimized.

Official HyperCore overview, on this check:

- End-to-end latency is the duration between sending a request and receiving a **committed** response.
- For an order placed from a geographically co-located client: median **0.2 seconds**, 99th percentile **0.9 seconds**.
- Mainnet currently supports approximately **200k orders/sec**. The current bottleneck is **execution**. The same page says consensus and networking can scale further once execution keeps up.

Treat those numbers as official published figures on 2026-09-27, not measurements made by this desk.

Sources:

- [About Hyperliquid](https://hyperliquid.gitbook.io/hyperliquid-docs/about-hyperliquid.md) — checked 2026-09-27
- [HyperCore overview](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/overview.md) — checked 2026-09-27

---

## Gaps inside this scope

- HyperCore source language, validator-client internals, and a dedicated “HyperCore spec” leaf beyond the overview + clearinghouse + order-book trio: **unknown here**. Official leaves checked on this `as-of` do not publish them.
- Whether “one-block finality inherited from HyperBFT” has exceptions: **unknown here**. About asserts the sentence. Conditions live, if anywhere, with [HyperBFT](hyperbft.md).
- Tick size, lot size, and the set of listed assets: market product, not this page.
- Liquidation parameters and margin *use* tables: risk shelf, not this page.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/about-hyperliquid.md | 1 | 2026-09-27 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/overview.md | 1 | 2026-09-27 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore.md | 1 | 2026-09-27 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/clearinghouse.md | 1 | 2026-09-27 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/order-book.md | 1 | 2026-09-27 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/hyperevm.md | 1 | 2026-09-27 |
| https://hyperliquid.xyz/tech | 1 | 2026-09-27 |
