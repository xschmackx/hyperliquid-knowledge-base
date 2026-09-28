# HyperEVM RPC

| Field | Value |
|-------|--------|
| Shelf | APIs and tooling (`pages/tooling/`) |
| Scope | Official HyperEVM JSON-RPC and chain parameters as connection data a stranger uses to talk to HyperEVM from software. Not dual-block architecture. Not the HyperCore API server. Not an SDK catalog. Not a node runbook. Not official explorers as a product. Not market, fee, or risk meaning of the calls. |
| Status | Accepted |
| Page `as-of` | 2026-09-28 |
| Rank | Claims below are Rank 1 unless tagged |

This page names the official JSON-RPC hosts, chain IDs, and methods Hyperliquid publishes for HyperEVM. It does not restate dual-block architecture, fee burn, or Core↔EVM transfer procedure. Those stay on accepted S1 pages. HyperCore REST and WebSocket hosts stay on [`api-servers.md`](api-servers.md). Official SDKs stay on [`official-sdks.md`](official-sdks.md). Info types, exchange actions, and WebSocket channels stay on their accepted S5 pages.

---

## Official hosts

Official developer hub: there are currently no official frontend components of the EVM. All interaction with the EVM happens through the JSON-RPC. Users can add the chain to a wallet by entering the RPC URL and chain ID.

Dated connection facts on this `as-of`:

| Network | Chain ID | JSON-RPC URL |
|---------|----------|----------------|
| Mainnet | 999 | `https://rpc.hyperliquid.xyz/evm` |
| Testnet | 998 | `https://rpc.hyperliquid-testnet.xyz/evm` |

The same hub names HYPE as the native gas token, with 18 decimals on both mainnet and testnet. The wallet FAQ names the mainnet network **Hyperliquid** and the currency symbol **HYPE**. A testnet network name is not published on that FAQ leaf.

The same hub says the HyperEVM uses the Cancun hardfork without blobs, and that EIP-1559 is enabled. Base-fee and priority-fee burn is component behaviour already on [`../protocol/hyperevm.md`](../protocol/hyperevm.md). Not restated here.

HyperEVM Tools lists the same two URLs under its RPC section (mainnet, then testnet), before the third-party names in a later section.

Sources: [HyperEVM (developer)](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm.md); [HyperEVM Tools](https://hyperliquid.gitbook.io/hyperliquid-docs/builder-tools/hyperevm-tools.md); [How to use the HyperEVM](https://hyperliquid.gitbook.io/hyperliquid-docs/onboarding/how-to-use-the-hyperevm.md) — checked 2026-09-28.

---

## This surface is not the API server

REST `https://api.hyperliquid.xyz` and WebSocket `wss://api.hyperliquid.xyz/ws`, and the testnet pair, are HyperCore API hosts. They are not HyperEVM JSON-RPC URLs. Host table: [`api-servers.md`](api-servers.md). Info types: [`info-endpoint.md`](info-endpoint.md). Exchange actions: [`exchange-endpoint.md`](exchange-endpoint.md). WebSocket subscriptions: [`websocket.md`](websocket.md).

---

## Wallet add-network fields

Official onboarding FAQ, mainnet add-custom-network:

| Field | Published value |
|-------|-----------------|
| Chain ID | 999 |
| Network Name | Hyperliquid |
| RPC URL | `https://rpc.hyperliquid.xyz/evm` |
| Currency Symbol | HYPE |
| Block explorer URL | Optional. The FAQ lists `https://hyperevmscan.io/` and `https://www.hyperscan.com/` |

Those two explorer URLs are the optional wallet field on that leaf. What the explorers are, and status pages, stay unwritten (later S5 slot). This page does not make them an official explorer product.

The same FAQ names Chainlist `https://chainlist.org/chain/999` as an add-network helper. Tag: `secondary`. It is not the official host.

Pre-EIP-155 transactions are accepted. Official note on the developer hub: users generally should not use wallets that have previously sent pre-EIP-155 transactions.

This page is not a wallet-extension support article.

Sources: [How to use the HyperEVM](https://hyperliquid.gitbook.io/hyperliquid-docs/onboarding/how-to-use-the-hyperevm.md); [HyperEVM (developer)](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm.md) — checked 2026-09-28.

---

## Published JSON-RPC methods

Official JSON-RPC leaf, standard methods named on this check:

| Method | Published restriction |
|--------|------------------------|
| `net_version` | none on this leaf |
| `web3_clientVersion` | none on this leaf |
| `eth_blockNumber` | none on this leaf |
| `eth_call` | latest block only |
| `eth_chainId` | none on this leaf |
| `eth_estimateGas` | latest block only |
| `eth_feeHistory` | none on this leaf |
| `eth_gasPrice` | base fee for the next small block |
| `eth_getBalance` | latest block only |
| `eth_getBlockByHash` | none on this leaf |
| `eth_getBlockByNumber` | none on this leaf |
| `eth_getBlockReceipts` | none on this leaf |
| `eth_getBlockTransactionCountByHash` | none on this leaf |
| `eth_getBlockTransactionCountByNumber` | none on this leaf |
| `eth_getCode` | latest block only |
| `eth_getLogs` | up to 4 topics; up to 50 blocks in the query range |
| `eth_getStorageAt` | latest block only |
| `eth_getTransactionByBlockHashAndIndex` | none on this leaf |
| `eth_getTransactionByBlockNumberAndIndex` | none on this leaf |
| `eth_getTransactionByHash` | none on this leaf |
| `eth_getTransactionCount` | latest block only |
| `eth_getTransactionReceipt` | none on this leaf |
| `eth_maxPriorityFeePerGas` | always returns zero currently |
| `eth_syncing` | always returns false |

Custom methods named on the same leaf:

| Method | Published role |
|--------|----------------|
| `eth_bigBlockGasPrice` | base fee for the next big block |
| `eth_usingBigBlocks` | whether the address is using big blocks |
| `eth_getSystemTxsByBlockHash` | system transactions that originate from HyperCore |
| `eth_getSystemTxsByBlockNumber` | system transactions that originate from HyperCore |

Small-block vs big-block *meaning*, gas limits, and the HyperCore action `evmUserModify` stay on [`../protocol/dual-block.md`](../protocol/dual-block.md) and [`../protocol/hyperevm.md`](../protocol/hyperevm.md). The dual-block leaf says a caller may use JSON-RPC `bigBlockGasPrice` in place of `gasPrice` to estimate the base gas fee on the next big block. `evmUserModify` is an exchange action, not a JSON-RPC method. Not rewritten here.

`eth_getSystemTxsByBlockHash` and `eth_getSystemTxsByBlockNumber` return HyperCore-originated system transactions. Transfer procedure and precompile tables stay on S1. Whether those system transactions also appear inside `eth_getBlockByHash` / `eth_getBlockByNumber` on the official host: **unknown here**.

Unsupported on the default RPC implementation: requests that require historical state. Official text says independent archive node implementations are available, and points at the GitHub repository for local indexing. Read precompiles are only recorded for the calls actually made on each block. Hypothetical read precompile results could be obtained from a full L1 replay. How to run that indexer is not this page.

Not named on this official list on this check: `eth_sendRawTransaction`, `eth_sendTransaction`, `eth_subscribe`, `debug_*`, `trace_*`. Whether the default host accepts a send method: **unknown here**. A vendor method list is not Hyperliquid's list.

Source: [JSON-RPC](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm/json-rpc.md); [Dual-block architecture](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm/dual-block-architecture.md) — checked 2026-09-28.

---

## Websocket on the official host

Official developer hub: there is currently no websocket JSON-RPC support for the RPC at `rpc.hyperliquid.xyz/evm`. Other RPC implementations may support it. Those implementations are not the official host. `eth_subscribe` is not named on the official method list.

Source: [HyperEVM (developer)](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm.md) — checked 2026-09-28.

---

## Rate limits

Two published sentences. They are not merged into one quota on this page.

- JSON-RPC leaf: IP-based rate limits are the same as the API server.
- Rate limits page: maximum of 100 EVM JSON-RPC requests per minute for `rpc.hyperliquid.xyz/evm`. The same sentence says other JSON-RPC providers have more sophisticated rate limiting logic and archive node functionality.

The REST and WebSocket weight table is the API-server surface. Not reprinted here. The 100-per-minute sentence names `rpc.hyperliquid.xyz/evm` only. Whether that figure also binds `rpc.hyperliquid-testnet.xyz/evm`: **unknown here**.

Sources: [JSON-RPC](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm/json-rpc.md); [Rate limits and user limits](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/rate-limits-and-user-limits.md) — checked 2026-09-28.

---

## Other implementations (not official hosts)

Official FAQ: there is one rpc hosted at `rpc.hyperliquid.xyz/evm`. Other builders are launching their own. Users may run a node, but it is not a requirement to serve an RPC, as all data is uploaded real-time to S3.

HyperEVM Tools names third-party RPC and archival hosts beside the two official URLs. That listing proves Hyperliquid pointed at them. It does not make them official hosts. Tag: `secondary` / `community`. They cannot support a claim that the official RPC is one of these, or that the official host has websocket, archive, or trace support.

Names on that tools page, not connection strings to use as official:

| Tools heading | Names |
|---------------|--------|
| Archival RPC | Alchemy, Altitude, Chainstack, Dwellir, HypeRPC, Nanoreth (how to build an archive node), OnFinality, Quicknode |
| RPC, after the two official URLs | Chainlink (Testnet), dRPC, HypurrScan, Quicknode, Stakely |

Vendor path splits (for example a host that strips system transactions) are not official default-RPC behaviour.

Sources: [How to use the HyperEVM](https://hyperliquid.gitbook.io/hyperliquid-docs/onboarding/how-to-use-the-hyperevm.md); [HyperEVM Tools](https://hyperliquid.gitbook.io/hyperliquid-docs/builder-tools/hyperevm-tools.md) — checked 2026-09-28.

---

## Indexing without the public RPC

The FAQ and the raw HyperEVM block data leaf point at local indexing and a real-time S3 upload, and at the Python SDK example `evm_block_indexer.py`. That proves a stranger can index without the public RPC. How to run a node or consume that data is a later S5 slot. S3 layout is not ingested here.

HyperEVM Tools also points at `basic_evm_use_big_blocks.py`. That file is already named on [`official-sdks.md`](official-sdks.md). Not a second SDK page.

Error code 10055 (boundary errors between HyperCore and HyperEVM) and the HYPE Core→EVM system address `0x2222222222222222222222222222222222222222` are named on the developer hub. They are already recorded on [`../protocol/hyperevm.md`](../protocol/hyperevm.md). Transfer procedure stays on S1. Not a support article here.

Sources: [How to use the HyperEVM](https://hyperliquid.gitbook.io/hyperliquid-docs/onboarding/how-to-use-the-hyperevm.md); [Raw HyperEVM block data](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm/raw-hyperevm-block-data.md); [HyperEVM Tools](https://hyperliquid.gitbook.io/hyperliquid-docs/builder-tools/hyperevm-tools.md) — checked 2026-09-28.

---

## Gaps inside this scope

- Whether the default official RPC accepts `eth_sendRawTransaction` or `eth_sendTransaction`: **unknown here**. Not named on the official method list.
- Whether official websocket JSON-RPC will ship: **unknown here**. Current published fact is no websocket on `rpc.hyperliquid.xyz/evm`.
- Which historical-state methods a third-party archive matches to default-host semantics: **unknown here**.
- Whether system transactions appear inside `eth_getBlockBy*` on the official host: **unknown here**.
- Testnet EVM host rate limit beyond the JSON-RPC leaf's "same as the API server" sentence: **unknown here**.
- Live gas limits and `evmUserModify`: not this page. See [`../protocol/dual-block.md`](../protocol/dual-block.md).
- Explorer product and status pages: later S5 slot.
- Node-run flags and S3 layout: later S5 slot.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm.md | 1 | 2026-09-28 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm/json-rpc.md | 1 | 2026-09-28 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/onboarding/how-to-use-the-hyperevm.md | 1 | 2026-09-28 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm/dual-block-architecture.md | 1 | method names only; architecture not rewritten |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/rate-limits-and-user-limits.md | 1 | 100 rpm sentence only |
| https://hyperliquid.gitbook.io/hyperliquid-docs/builder-tools/hyperevm-tools.md | 1 | official RPC row + tagged third-party names |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm/raw-hyperevm-block-data.md | 1 | pointer only; not ingested |
| https://chainlist.org/chain/999 | secondary | named by the official FAQ; not an official host |

Accepted pages pointed at, not rewritten: [`../protocol/hyperevm.md`](../protocol/hyperevm.md) (`as-of` 2026-09-28), [`../protocol/dual-block.md`](../protocol/dual-block.md), [`api-servers.md`](api-servers.md) (`as-of` 2026-09-16), [`official-sdks.md`](official-sdks.md) (`as-of` 2026-09-28), [`info-endpoint.md`](info-endpoint.md), [`exchange-endpoint.md`](exchange-endpoint.md), [`websocket.md`](websocket.md).
