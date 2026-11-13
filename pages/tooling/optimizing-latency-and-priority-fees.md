# Optimizing latency and priority fees

| Field | Value |
|-------|--------|
| Shelf | APIs and tooling (`pages/tooling/`) |
| Scope | Official published guidance on optimizing read and write latency, and on priority fees (gossip and order). Includes mempool prioritization restrictions and priority-fee timing as published. Not fee economics or risk rules. Not unofficial clients. |
| Status | Accepted |
| Page `as-of` | 2026-11-13 |
| Rank | Claims below are Rank 1 unless tagged |

This page records the official suggestions for reducing latency when reading market data or sending orders and cancels, and the official priority-fee mechanisms. A stranger can use it to understand the published options for lower latency and the current mempool and fee rules. Official names only. Unknown stays unknown. The suggestions are informational only and do not guarantee any latency or trading outcome.

Sources: [Optimizing latency](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/optimizing-latency.md); [Priority fees](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/priority-fees.md) — checked 2026-11-13.

---

## Optimizing read latency (receiving market data)

Official page publishes these starting points:

1. Run a non-validating node against a reliable peer, such as the Hyper Foundation non-validator.
2. Run the node with `--disable-output-file-buffering` to get outputs as soon as blocks are executed.
3. Run the node with sufficient machine specs: at least 32 logical cores, 128 GB RAM, and 500 MB/s disk throughput. Increasing cores can reduce latency because blocks execute faster.
4. Construct the book and other exchange state locally using node outputs, which have faster and more granular data than the API. See the order_book_server repository for an example of building an order book on the same machine as a node. That repository is not actively maintained. Fork it or write an implementation from scratch to incorporate details such as ALO priority fees or other edge cases.
5. `--batch-by-block` on the node waits until the end of the block to write the data. The example order book server uses this to simplify logic; a further optimization is to turn the flag off and infer block boundaries otherwise.
6. Latency-sensitive users may find `split_client_blocks: true` useful. It streams transactions to be committed before they are included in client blocks. This can lead to a 70-150 ms improvement in latency when reading inputs. These are the fastest transaction inputs to execution, broadcast even before the L1 executes them. The tradeoff is that execution results are not yet available. For simple actions like orders, the consumer can stream estimated account values for all users to predict execution results with reasonable accuracy.
7. The Foundation non-validator is one of the highest-uptime and low-latency non-validator peers. Access details are on the Foundation non-validating node page.
8. Read priority fees are the fastest way to read raw data from the network. See the priority fees section below.

Node flags, local data layouts, and Foundation peer access stay on [`nodes-as-clients.md`](nodes-as-clients.md). What a node is on the L1 stays on the protocol shelf.

Source: [Optimizing latency](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/optimizing-latency.md) — checked 2026-11-13.

---

## Optimizing write latency (sending orders and cancels)

Official page publishes these points:

1. Cancels should be sent with the fast flag. There is no disadvantage to the fast flag, except that fast cancels cannot cancel trigger orders. Fast cancel details stay on [`exchange-endpoint.md`](exchange-endpoint.md).
2. Write priority fees are the fastest way to send orders to the network. See the priority fees section below.
3. Hyperliquid's execution logic protects makers against toxic flow so that end users see tight spreads and deep liquidity even during volatility. The primary driver is that cancels and ALO orders sent at time t almost always execute before IOC and GTC orders sent at time t. This prioritization spans several blocks. The secondary effect is that each L1 block contains only a few consensus bundles. Within each bundle, ALO and cancels execute before other transactions.
4. End-to-end latency on Hyperliquid is not apples-to-apples with centralized matching engines because the order book is fully onchain. End-to-end latency includes time to the API server, mempool inclusion time, and time to commit (usually 2 blocks in pipelined HyperBFT consensus). The sequencing of transactions has far less noise than the end-to-end latency suggests. While a cancel or ALO order can show ~380 ms end-to-end latency, users should be able to run experiments with <10 ms variation between send times and see predictable ordering on the L1.
5. Users who want to reduce the end-to-end write latency (for example to predict the sequence of transactions that will be committed) can read them from split client blocks in the non-validating node. This approach does not include the execution result of the transaction.
6. Mempool prioritization has restrictions on the actions sent:
   - Mempool prioritization works only for users in Standard abstraction. Latency-sensitive users should not use abstractions such as Unified Account and Portfolio Margin.
   - Actions other than `noop`, `scheduledCancel`, `cancel`, `cancelByCloid`, `order`, `modify`, `batchModify` sent on HyperCore cause all actions to be deprioritized while that action has not yet been committed. This holds across sub-accounts associated with and vaults led by the same master user which originate the non-trading action sent. It does not affect other subaccounts of vaults of the same master account.
   - Users who have ever directly sent CoreWriter actions are deprioritized in the mempool. This does not affect the vast majority of CoreWriter use cases that go through smart contracts rather than the user itself.
   - IOC and ALO priority fees require a minimum delegatable balance of 10 HYPE. The priority fee charged remains a function of only the executed size.

Source: [Optimizing latency](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/optimizing-latency.md) — checked 2026-11-13.

---

## Priority fees

Priority fees are an advanced feature for latency-sensitive users. Official page covers gossip (read) priority and order (write) priority.

### Gossip (read) priority

There are 3 independent Dutch auctions synced to the same 3-minute schedule. The auction indices are optionally interpreted by nodes as an ordering for their peers when sending data. The priority ordering affects both split client blocks and normal client blocks that include responses. The Foundation non-validator opts into respecting the gossip priority auction ordering.

The independent slot auctions are not additive, so an IP bidding multiple slots is prioritized according to its lowest slot. For the auction to affect latency, the on-chain IP must exactly match the IP seen by the peer sending data. Each auction's results only affect the duration of the following auction. For nodes connected via a chain of nodes to the validating network, each network hop may or may not respect the priority auction depending on how the parent node is configured.

Lower auction indices are strictly prioritized over higher indices. The prioritization applies to all data in the mempool transactions stream equally. The ordering should be relatively consistent in expectation but is subject to variance from the p2p consensus network. Gossip priority applies only to reading data. For prioritization of sending data, see order priority below. Nodes respecting gossip priority use the previous auction winners relative to that node's current execution state. Fees come out of spot balance and are burned.

The previous auction winners (current gossip priority ordering) and current auction statuses can be queried using the info request `{"type": "gossipPriorityAuctionStatus"}`. Info request types stay on [`info-endpoint.md`](info-endpoint.md).

To participate in the auction, users send the action `{"type": "gossipPriorityBid", "slotId": 0, "ip": "1.2.3.4", "maxGas": 100000000}` where gas is wei (units of 0.00000001 HYPE) of HYPE charged from spot balance. Each auction resets to 10 times the previous winning price of that slot and has a minimum price of 0.1 HYPE. Any address may bid on behalf of any IP address.

The current empirical effect of gossip priority on mainnet is approximately 20 ms reduction in latency per auction slot.

### Order (write) priority

Order priority reduces the need for market makers to hyper-optimize their order entry and connectivity and instead focus on the strategy itself. It further protects makers and allows responsiveness to price moves driven by other venues.

Priority grouping is only supported for order actions where both:

1. every order is on a non-outcome asset
2. every order is IOC, or every order is a non-reduce-only ALO

Orders can be sent with grouping of the form `{"p": 12345}` where the rate is interpreted as a fraction `p / 100000000.0`. The rate is charged from undelegated staking balance as a fraction of the filled notional in the case of IOC, and resting notional in the case of ALO. The priority gas charged is converted to HYPE using the spot mark price.

#### IOC priority

The priority rate has a linear effect on end-to-end latency from 0-8 bps, i.e. `p = 80000`. The current empirical effect of order priority fees on mainnet is approximately 45 ms reduction in end-to-end latency per 1 bp of priority fee paid. Even with order priority, all cancels are prioritized before all immediately executable orders. Higher priority orders are prioritized before lower priority orders as a linear function of priority rate.

The max priority rate is 100%. Any priority between 8 bps and 100% is treated with identical time preference in the mempool. However, IOC orders with at least 8 bps priority fee that would be executed by the block proposer in each 70 ms unix time bucket (usually corresponding to 1 block) are sorted in decreasing order of priority fee. The 0-8 bps range effects temporal prioritization, and the 8 bps-100% range breaks ties among orders in this range received at a similar time.

Although blocks are discrete, order prioritization is continuous with respect to order write priority fee. The mempool transactions are effectively sorted by `effective_time = arrival_time + f(action, priority_fee)` where `f` is a strictly decreasing function of priority fee, and zero for prioritized actions such as cancels. For a given action type, boundaries between blocks are not relevant for relative prioritization, as the transactions within a block are still sorted according to `effective_time`.

Order priority applies only to sending data. For prioritization of reading data, see gossip priority above. Order priority fees are burned.

IOC priority fee paid can be read from the `user_fills` file written by the nodes as field `priorityGas`.

#### ALO priority

On the timescale of `T = 400 ms`, ALO orders are sorted by priority. More precisely, the tail of the queue at each level consisting of orders placed within the past `T` is sorted in decreasing order of priority rate.

As a consequence, any slot in the queue is eligible for priority fee bidding for a window of duration `T`. Each new order compares against the tail of orders less than `T` old at placement time. The `T` window is continuous, not bucketed. ALO priority fees are deducted at the time of placing the order regardless of whether the order fills.

Unlike for IOC orders, ALO priority fees do not effect mempool prioritization. ALO orders are processed FIFO as transactions always, with similar end-to-end latency as cancels. The priority fee implementation affects place in queue across transactions. ALO orders are prioritized similarly in the mempool regardless of their priority, but queue position can change on a 400 ms time scale after order transactions are executed on the L1.

Gossip priority fees can be read from the `replica_cmds` files recorded by nodes. The USDC value of the priority fee amounts can be computed as `order_price * order_sz * grouping_priority_rate`. The order_book_server maintains the correct level ordering by using the `insertBefore` field on `RawBookDiff::New` from the `raw_book_diff` files.

Source: [Priority fees](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/priority-fees.md) — checked 2026-11-13.

---

## Gaps inside this scope

- Exact numeric effect of machine specs, peer choice, or flag combinations beyond the published starting points and empirical notes: **unknown here**. Official page does not publish further numbers on this `as-of`.
- Whether the order_book_server example incorporates the latest ALO or mempool rules: **unknown here**. Official page notes it is not actively maintained.
- Full mechanics of CoreWriter, Unified Account, or Portfolio Margin beyond the published deprioritization notes: **unknown here**. Those stay on other shelves.
- Community or unofficial clients as sole support: not used. Official sources first.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/optimizing-latency.md | 1 | 2026-11-13 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/priority-fees.md | 1 | 2026-11-13 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/llms.txt | 1 | 2026-11-13 |
