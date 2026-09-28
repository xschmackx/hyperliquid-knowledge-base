# Nodes as clients

| Field | Value |
|-------|--------|
| Shelf | APIs and tooling (`pages/tooling/`) |
| Scope | How a stranger runs or reads a Hyperliquid node as a client: published flags, local data layouts, and official ingest paths. Not node-as-L1-participant. Not HyperBFT, HyperCore, or HyperEVM as architecture. Not dual-block architecture. Not the public JSON-RPC catalog. Not the public info, exchange, or WebSocket catalogs. Not official explorers or status pages as a product. Not market, fee, or risk meaning of the streams. |
| Status | Accepted |
| Page `as-of` | 2026-09-28 |
| Rank | Claims below are Rank 1 unless tagged |

This page names how to obtain the published binary, which flags write which local paths, and which S3 prefixes Hyperliquid publishes for ingest. It does not restate what a node is on the L1. That stays on [`../protocol/nodes.md`](../protocol/nodes.md). Public REST and WebSocket hosts stay on [`api-servers.md`](api-servers.md). The official HyperEVM JSON-RPC catalog stays on [`hyperevm-rpc.md`](hyperevm-rpc.md). Official SDKs stay on [`official-sdks.md`](official-sdks.md). Info types, exchange actions, and WebSocket channels stay on their accepted S5 pages. What a fill, funding event, or liquidation *means* stays on S2–S4.

Official names only. “Full node”, “light node”, and “archive node” are not official names on the leaves checked. They are not used here. Community archive builds already noted on [`hyperevm-rpc.md`](hyperevm-rpc.md) stay tagged there. They are not how-to on this page.

---

## Where the flags live

The Nodes hub is a run pointer. It points at the node repository. It does not list flags.

The live Rank 1 schema leaf is [L1 data schemas](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/nodes/l1-data-schemas.md). It names local paths, example JSON, and misc-event type names, and defers flags to the repository.

The node repository README still links `for-developers/nodes/reading-l1-data`. That URL 404s on this check (docs index `llms.txt`, 2026-09-28: no live leaf of that name). Cite L1 data schemas, not the stale path.

Flag names, binaries, ports, and local servers below are Rank 2 from the node repository README at commit `405cc08b17a727ee51b0f9128918955a84439915` (README blob `dd24feed0a56915d085203f74f4b55b11a6792eb`), checked 2026-09-28, unless a sentence is marked Rank 1.

Sources: [Nodes](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/nodes.md); [L1 data schemas](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/nodes/l1-data-schemas.md); [docs index](https://hyperliquid.gitbook.io/hyperliquid-docs/llms.txt); [node repository](https://github.com/hyperliquid-dex/node) — checked 2026-09-28.

---

## Binary and chain file

Dated client facts, Rank 2, `as-of` 2026-09-28. Source: [node repository README](https://github.com/hyperliquid-dex/node).

`hl-visor` spawns and manages the child node process. Published download hosts:

| Chain | Binary | Signature |
|-------|--------|-----------|
| Mainnet | `https://binaries.hyperliquid.xyz/Mainnet/hl-visor` | `https://binaries.hyperliquid.xyz/Mainnet/hl-visor.asc` |
| Testnet | `https://binaries.hyperliquid-testnet.xyz/Testnet/hl-visor` | `https://binaries.hyperliquid-testnet.xyz/Testnet/hl-visor.asc` |

Signatures verify against `pub_key.asc` in that repository (`gpg --import pub_key.asc`, then `gpg --verify`). The README says `hl-visor` also verifies `hl-node` and will not upgrade on verification failure.

Chain file, either chain: `~/visor.json` with `{"chain": "Testnet"}` or `{"chain": "Mainnet"}`.

Non-validating start, same command on either chain once `~/visor.json` is set:

```bash
~/hl-visor run-non-validator
```

The README says logs such as `applied block X` indicate live streaming. How long peer discovery takes is not a published number.

A validating node is started with `hl-visor run-validator` after the non-validating setup. That is the client start name only. Register, self-delegate, unjail, jail, staking-deposit, alerting, and aligned-quote publishing stay on [`../protocol/nodes.md`](../protocol/nodes.md) and the repository. Not reprinted here.

---

## Machine, OS, ports

Dated client facts, Rank 2, `as-of` 2026-09-28. Not L1 identity. Source: [node repository README](https://github.com/hyperliquid-dex/node).

| Role | vCPUs | RAM | Storage |
|------|-------|-----|---------|
| Non-validator | 16 | 128 GB | 500 GB SSD |
| Validator | 32 | 128 GB | 1 TB SSD |

Ubuntu 24.04 is the only OS named as supported on this check.

Gossip ports **4001** and **4002** must be open to the public. Otherwise the node IP is deprioritized by peers. Validators: ports **4000–4010** open to other validators. The README says only **4001–4006** are used now, and that further ports in that range may be used later. Lowest-latency sentence on the same README: run the node in Tokyo, Japan.

Optional operator notes, same repository `README_misc.md`, Rank 2, not a second identity: `n_gossip_peers` between 8 and 100 inclusive in `override_gossip_config.json`; public IP override file `~/hl/override_public_ip_address`; systemd and Docker are optional run methods. Source: [README_misc.md](https://github.com/hyperliquid-dex/node/blob/405cc08b17a727ee51b0f9128918955a84439915/README_misc.md) — checked 2026-09-28.

---

## Write flags and local paths

Dated flag list, Rank 2, `as-of` 2026-09-28. Source: [node repository README](https://github.com/hyperliquid-dex/node). The README says these flags work independently of the chain setting in `~/visor.json`. Output base is `~/hl/data`.

| Flag | Local path on this check |
|------|--------------------------|
| `--write-trades` | `~/hl/data/node_trades/hourly/{date}/{hour}` |
| `--write-fills` | `~/hl/data/node_fills/hourly/{date}/{hour}`, plus TWAP statuses `~/hl/data/node_twap_statuses/{date}/{hour}` |
| `--write-order-statuses` | `~/hl/data/node_order_statuses/hourly/{date}/{hour}` |
| `--write-raw-book-diffs` | `~/hl/data/node_raw_book_diffs/hourly/{date}/{hour}` |
| `--write-hip3-oracle-updates` | `~/hl/data/hip3_oracle_updates/hourly/{date}/{hour}` |
| `--write-misc-events` | `~/hl/data/misc_events/hourly/{date}/{hour}` |
| `--write-system-and-core-writer-actions` | `~/hl/data/system_and_core_writer_actions/hourly/{date}/{hour}` |

`--write-fills` overrides `--write-trades` if both are set. The README says fills are in the API fills format, and that `deployerFee` is included on HIP-3 fills. What a fill or a fee *is* stays on S2–S3. Not restated here.

`--batch-by-block` writes those files one block per line. Schema named on the README: `{local_time, block_time, block_number, events}`, where `events` is a list. `--stream-with-block-info` writes events as processed, same schema, so the line carries block metadata.

`--replica-cmds-style` configures `~/hl/data/replica_cmds/{start_time}/{date}/{height}`. Published values: `actions` (default), `actions-and-responses`, `recent-actions` (only the two latest height files).

`--disable-output-file-buffering` flushes each line immediately. The README says this reduces latency and increases disk IO.

`--serve-eth-rpc` and `--serve-info` are in the next section.

One extra write flag is on the HIP-3 deployer-actions leaf, not the README, Rank 1, `as-of` 2026-09-28: `--write-user-account-summaries <dex>` writes `~/hl/data/dex_user_account_summaries/hourly/<date>/<hour>`. Each line is a JSON array `[time, messages]`. The first line of each file, and the first line after the node starts, is a snapshot; other lines are diffs. Field names `a` and `b` are on that leaf. HIP-3 product rules are not ingested here. Source: [HIP-3 deployer actions](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/hip-3-deployer-actions.md).

Rank 1 volume sentence, same `as-of`, also on the README: with default settings the network generates around **100 GB** of logs per day. Archive or delete old files. Source: [L1 data schemas](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/nodes/l1-data-schemas.md).

---

## Layouts that are always on

No extra write flag is named for these. Rank 2 paths match the Rank 1 schema leaf. `as-of` 2026-09-28.

| Layout | Path |
|--------|------|
| Transaction blocks (`replica_cmds`) | `~/hl/data/replica_cmds/{start_time}/{date}/{height}` |
| State snapshots, every 10,000 blocks | `~/hl/data/periodic_abci_states/{date}/{height}.rmp` |
| Raw HyperEVM blocks and receipts | `~/hl/data/evm_block_and_receipts` |

Translate a snapshot to JSON: `hl-node --chain <chain> translate-abci-state <rmp> <out.json>`. L4 from a snapshot: `hl-node --chain <chain> compute-l4-snapshots <abci-state-path> <out-path>`.

L4, as the schema leaf defines the layout: the entire order book with full order information, usable as a checkpoint the order-status stream can be applied to. Orders at one price are time-ordered; trigger orders come at the end and are marked `isTrigger`. That is layout, not a market rule.

Misc-event type names on the same leaf, layout only: `MiscEvent` with `time`, `hash`, and `inner`. Named inner types: `CDeposit`, `Delegation`, `CWithdrawal`, `ValidatorRewards`, `Funding`, `LedgerUpdate`. Staking and funding rules stay on S3–S4.

The schema leaf publishes a trade example object. Field names on that example: `coin`, `side`, `time`, `px`, `sz`, `hash`, `trade_dir_override`, `side_info` (length 2). What a trade is stays on S2.

Sources: [L1 data schemas](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/nodes/l1-data-schemas.md); [Raw HyperEVM block data](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm/raw-hyperevm-block-data.md); [node repository README](https://github.com/hyperliquid-dex/node) — checked 2026-09-28.

---

## Local servers

These are node flags. They are not the public hosts.

`--serve-eth-rpc` serves a local EVM JSON-RPC. Published example, Rank 2, `as-of` 2026-09-28: `http://localhost:3001/evm`. The README curl uses `eth_getBlockByNumber`. The public method catalog, chain IDs, and official hosts stay on [`hyperevm-rpc.md`](hyperevm-rpc.md). Whether the local server implements that full catalog: **unknown here**.

`--serve-info` serves a local info HTTP server. Published example, same `as-of`: `http://localhost:3001/info`. The README says this is a subset of requests that are a function of local state. Historical time series queries and websockets are not supported locally. Public hosts and the public type catalog stay on [`api-servers.md`](api-servers.md) and [`info-endpoint.md`](info-endpoint.md). Exchange actions stay on [`exchange-endpoint.md`](exchange-endpoint.md). WebSocket channels stay on [`websocket.md`](websocket.md).

Local info types named on the README on this check, and no others:

`meta`, `spotMeta`, `clearinghouseState`, `spotClearinghouseState`, `openOrders`, `exchangeStatus`, `frontendOpenOrders`, `liquidatable`, `activeAssetData`, `maxMarketOrderNtls`, `vaultSummaries`, `userVaultEquities`, `leadingVaults`, `extraAgents`, `subAccounts`, `userFees`, `userRateLimit`, `spotDeployState`, `perpDeployAuctionStatus`, `delegations`, `delegatorSummary`, `maxBuilderFee`, `userToMultiSigSigners`, `userRole`, `perpsAtOpenInterestCap`, `validatorL1Votes`, `marginTable`, `perpDexs`, `webData2` (does not compute `assetCtxs`).

`l2Book` is not supported locally. The README says to poll or subscribe on the public API. `fileSnapshot` writes a large snapshot to `outPath`. Published request types: `referrerStates`; `l4Snapshots` with `includeUsers` and `includeTriggerOrders`. Optional `includeHeightInOutput`.

Staleness check named on the README: ping `exchangeStatus` and compare the L1 timestamp with local time. Ignore the server when the L1 timestamp is sufficiently stale. The README does not publish a numeric staleness threshold. That threshold is **unknown here**. The same note says this applies to Testnet and Mainnet.

Source: [node repository README](https://github.com/hyperliquid-dex/node) — checked 2026-09-28.

---

## Official ingest (S3)

Requester pays transfer costs. Published flag on the raw-block leaf: `--request-payer requester`. Do not omit it. `as-of` 2026-09-28.

Raw HyperEVM blocks, Rank 1. Source: [Raw HyperEVM block data](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm/raw-hyperevm-block-data.md).

| Network | Bucket |
|---------|--------|
| Mainnet | `s3://hl-mainnet-evm-blocks/` |
| Testnet | `s3://hl-testnet-evm-blocks/` |

Format: MessagePack, LZ4. Example key: `s3://hl-mainnet-evm-blocks/0/6000/6123.rmp.lz4`. Testnet objects start at directory `18000000`. Earlier testnet RPC blocks are not backfilled on that leaf. The Python SDK example named there is `examples/evm_block_indexer.py`. That file is a pointer to [`official-sdks.md`](official-sdks.md) and the SDK repo. Not a second SDK page.

L1 and archive prefixes, Rank 1. Source: [Historical data](https://hyperliquid.gitbook.io/hyperliquid-docs/historical-data.md).

Archive bucket `s3://hyperliquid-archive/`, uploaded about once a month. No guarantee of timely updates. Data may be missing. Format strings on that leaf:

- `s3://hyperliquid-archive/market_data/[date]/[hour]/[datatype]/[coin].lz4`
- `s3://hyperliquid-archive/asset_ctxs/[date].csv.lz4`

Node-data bucket `s3://hl-mainnet-node-data/`. Prefixes named on that leaf:

| Prefix | Published note |
|--------|----------------|
| `node_fills_by_block` | Fills streamed via `--write-fills --batch-by-block` from a non-validating node |
| `node_fills` | Older format. Matches the API format |
| `node_trades` | Older format. Does not match the API format |
| `explorer_blocks` | Data prefix. Not an explorer product |
| `replica_cmds` | Data prefix |
| `misc_events_by_block` | Data prefix |

`explorer_blocks` is not the official-explorers page. That slot stays unwritten (later S5). A testnet twin of `s3://hl-mainnet-node-data/` is not named on this leaf. **Unknown here.**

---

## Foundation peer is access, not the definition

What the Foundation non-validating node *is* stays on [`../protocol/nodes.md`](../protocol/nodes.md): a named peer, not the definition of a node. This section is how a stranger connects.

Rank 1 use, `as-of` 2026-09-28. Source: [Foundation non-validating node](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/nodes/foundation-non-validating-node.md).

A local non-validating node can be pointed at the Foundation non-validating node. The leaf’s client use is: record fills and orders with output buffering disabled, and point a local API server at that local node. The Foundation node runs in AWS AZ `apne1-az1`.

Eligibility on that leaf, dated access facts, not protocol identity: staked 10,000 HYPE; Maker Rebate Tier 1 or above (`>0.5%` of 14-day weighted maker volume); connecting peer at 98% time-weighted uptime, which the leaf says follows from non-validator ports open to the public plus monitoring; applicable-law and sanctions limits as written on the leaf. The Foundation may adjust the criteria. Discretionary access for ecosystem work is also named there. Not copied as a second identity.

A separate leaf is a directory of third-party peering for infra providers. It is not a vendor how-to. Directory eligibility on that leaf, not the Foundation-peer numbers above: 99.9% uptime and a price benchmark under $1000/month, plus operating-history criteria. Vendor SLA pages are not official node behaviour. Tag any vendor path split `secondary`. Source: [Foundation non-validating node for infra providers](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/nodes/foundation-non-validating-node-for-infra-providers.md) — checked 2026-09-28.

---

## Gaps inside this scope

- `for-developers/nodes/reading-l1-data`: **404** on this check. Not a live source.
- Numeric staleness threshold for local `exchangeStatus`: **unknown here**.
- Whether local `--serve-eth-rpc` matches the public JSON-RPC method list: **unknown here**. Public catalog is on [`hyperevm-rpc.md`](hyperevm-rpc.md).
- Testnet L1 node-data bucket beside `s3://hl-mainnet-node-data/`: **unknown here**.
- Whether every archive `[datatype]` under `market_data/` is still written: **unknown here**. The format string is what the leaf publishes.
- Validator register, jail, stake CLI, alerting, aligned-quote publisher: not this page. See [`../protocol/nodes.md`](../protocol/nodes.md) and the repository.
- Official explorers and status pages: later S5 slot. `explorer_blocks` above is a prefix only.
- Community or vendor archive nodes: not sole support. Already tagged on [`hyperevm-rpc.md`](hyperevm-rpc.md).

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/nodes.md | 1 | 2026-09-28 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/nodes/l1-data-schemas.md | 1 | 2026-09-28 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/nodes/foundation-non-validating-node.md | 1 | 2026-09-28 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/nodes/foundation-non-validating-node-for-infra-providers.md | 1 | directory only; vendor how-to not copied |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm/raw-hyperevm-block-data.md | 1 | 2026-09-28 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/historical-data.md | 1 | 2026-09-28 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/hip-3-deployer-actions.md | 1 | flag and path only |
| https://hyperliquid.gitbook.io/hyperliquid-docs/validators/running-a-validator.md | 1 | start pointer only; participation not rewritten |
| https://hyperliquid.gitbook.io/hyperliquid-docs/llms.txt | 1 | 2026-09-28; `reading-l1-data` absent |
| https://github.com/hyperliquid-dex/node | 2 | 2026-09-28; SHA `405cc08b17a727ee51b0f9128918955a84439915` |
| https://github.com/hyperliquid-dex/node/blob/405cc08b17a727ee51b0f9128918955a84439915/README_misc.md | 2 | optional operator notes |
| https://binaries.hyperliquid.xyz/Mainnet/hl-visor | 2 | host named by the README |
| https://binaries.hyperliquid-testnet.xyz/Testnet/hl-visor | 2 | host named by the README |

Accepted pages pointed at, not rewritten: [`../protocol/nodes.md`](../protocol/nodes.md) (`as-of` 2026-09-28), [`api-servers.md`](api-servers.md) (`as-of` 2026-09-16), [`hyperevm-rpc.md`](hyperevm-rpc.md) (`as-of` 2026-09-28), [`official-sdks.md`](official-sdks.md) (`as-of` 2026-09-28), [`info-endpoint.md`](info-endpoint.md), [`exchange-endpoint.md`](exchange-endpoint.md), [`websocket.md`](websocket.md).
