# HyperEVM

| Field | Value |
|-------|--------|
| Shelf | Protocol (`pages/protocol/`) |
| Scope | Official execution component for general-purpose contracts. Same consensus as HyperCore. The component, not a dapp directory. |
| Status | Accepted |
| Page `as-of` | 2026-09-28 |
| Rank | Claims below are Rank 1 unless a source row says otherwise |

L1 identity and the two-component split live on [What Hyperliquid is](what-hyperliquid-is.md). Rounds, commits, height, and one-block finality live on [HyperBFT](hyperbft.md). Matching and margin execution state live on [HyperCore](hypercore.md). Native transfer, read precompiles, and CoreWriter live on [One state](one-state.md). Fast and slow HyperEVM blocks live on [Dual-block](dual-block.md).

This page is not a dapp catalogue, not a HyperCore rewrite, not a HyperBFT rewrite, and not an RPC or node runbook.

---

## The execution component

Official docs split Hyperliquid state execution into two components: **HyperCore** and **HyperEVM**.

Official About page: the HyperEVM brings the familiar general-purpose smart contract platform pioneered by Ethereum to the Hyperliquid blockchain. The same page says HyperCore liquidity and primitives are available as permissionless building blocks through HyperEVM.

Official HyperCore overview: the Hyperliquid state consists of HyperCore and the general-purpose HyperEVM.

Official HyperEVM hub: the Hyperliquid blockchain features two key parts, HyperCore and HyperEVM. HyperEVM is **not a separate chain**. It is secured by the **same HyperBFT consensus as HyperCore**. That is what the hub says lets HyperEVM interact directly with parts of HyperCore, such as spot and perp order books.

Official developer HyperEVM page: the HyperEVM consists of EVM blocks built as part of Hyperliquid's execution, inheriting all security from HyperBFT consensus.

Official site architecture copy uses the same two-component state and the same HyperBFT for both. That site sentence is identity only.

Do not read HyperEVM as an L2, a sidechain, or an appchain. Official hub and About name it as an execution component on the same L1.

Sources:

- [About Hyperliquid](https://hyperliquid.gitbook.io/hyperliquid-docs/about-hyperliquid.md) — checked 2026-09-28
- [HyperCore overview](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/overview.md) — checked 2026-09-28
- [HyperEVM](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperevm.md) — checked 2026-09-28
- [HyperEVM (developer)](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm.md) — checked 2026-09-28
- [Official site / tech](https://hyperliquid.xyz/tech) — checked 2026-09-28

---

## What this component executes

Official developer HyperEVM page, on this check:

- HYPE is the native gas token on the HyperEVM.
- On both mainnet and testnet, HYPE on the HyperEVM has 18 decimals.
- The HyperEVM uses the Cancun hardfork without blobs.
- EIP-1559 is enabled.
- Mainnet chain ID is 999. Testnet chain ID is 998.
- There are currently no official frontend components of the EVM. Interaction is via JSON-RPC. Official docs publish a JSON-RPC host for each network on that same leaf.

Chain ID and the fact of a published JSON-RPC host are component identity. Add-network steps, wallet setup, SDK lists, explorer URLs, and RPC how-to are not this page.

To move HYPE from HyperCore to HyperEVM, official developer docs say send HYPE to `0x2222222222222222222222222222222222222222`. HYPE links to the native EVM balance, not an ERC-20. Transfer rules, other token system addresses, and link/finalize live on [One state](one-state.md). This page does not reprint them.

The same developer leaf publishes error code 10055 for errors at the boundary between HyperCore and HyperEVM (examples there include nonce errors, insufficient funds, duplicate transaction hashes, or underpriced replacement transactions). That code names the boundary. It is not a troubleshooting guide.

Sources:

- [HyperEVM (developer)](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm.md) — checked 2026-09-28
- [HyperCore <> HyperEVM transfers](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm/hypercore-less-than-greater-than-hyperevm-transfers.md) — checked 2026-09-28

---

## Fee burn on this component

Official developer HyperEVM page:

- Base fees are burned as usual. Burned fees are removed from the total EVM supply.
- Unlike most other EVM chains, priority fees are also burned, because the HyperEVM uses HyperBFT consensus. Burned priority fees are sent to the zero address's EVM balance.

That burn is how this execution component handles EIP-1559 under HyperBFT. Staking discounts, builder codes, and trading fees are not this page.

Source: [HyperEVM (developer)](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm.md) — checked 2026-09-28.

---

## Same consensus, not a second write of HyperCore

HyperEVM does not have its own consensus. Official hub: same HyperBFT as HyperCore. How rounds, commits, height, and one-block finality work lives on [HyperBFT](hyperbft.md).

HyperCore is the other execution component: matching-engine state and margin state. That catalogue lives on [HyperCore](hypercore.md). This page does not restate order books, clearinghouse modes, or in-block book sort.

Official hub examples of the component, not a project list:

- A contract on HyperEVM can be linked to a HyperCore spot asset, so the same asset can be used in HyperEVM applications and traded on the native spot book. The hub says there is no bridging risk between HyperCore and HyperEVM as one unified state.
- A lending pool contract can read prices from HyperCore books with a read precompile, and can send orders on those books with a write system contract.

How native transfer, read precompiles (`0x0000…0800`), and the CoreWriter system contract (`0x3333…3333`) work lives on [One state](one-state.md). Action-ID tables and transfer gas figures are not this page.

Sources:

- [HyperEVM](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperevm.md) — checked 2026-09-28
- [Interacting with HyperCore](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm/interacting-with-hypercore.md) — checked 2026-09-28

---

## Dual-block, as component context only

Official onboarding FAQ names two main differences versus other EVMs: a dual-block system (fast small blocks and slow big blocks), and interactions with HyperCore. The same FAQ says Hyperliquid is one state with HyperCore state and HyperEVM state, and that the HyperEVM is Cancun without blobs.

Official dual-block page: HyperEVM throughput is split between small blocks produced at a fast rate and large blocks produced at a slower rate. The two block types are interleaved with a unique increasing sequence of EVM block numbers.

Block sizes, gas limits, mempool split, and `evmUserModify` / `usingBigBlocks` live on [Dual-block](dual-block.md). This page does not restate those figures.

Sources:

- [How to use the HyperEVM](https://hyperliquid.gitbook.io/hyperliquid-docs/onboarding/how-to-use-the-hyperevm.md) — checked 2026-09-28
- [Dual-block architecture](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm/dual-block-architecture.md) — checked 2026-09-28

---

## Alpha stage, dated, not resolved here

Official HyperEVM hub, on this check: the HyperEVM is in the alpha stage. The same answer says higher throughput and write system contracts are not live on mainnet yet, but will be in due time.

The interacting-with-HyperCore leaf documents a CoreWriter system contract and read precompiles. [One state](one-state.md) already records that those two official pages are not collapsed into one mainnet inventory on this desk. This page does not resolve the tension and does not invent a feature-gate status.

The hub also links community app directories. Those listings are not this page. This page does not name projects.

Source: [HyperEVM](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperevm.md) — checked 2026-09-28.

---

## Gaps inside this scope

- Client language, validator-EVM internals, and a dedicated HyperEVM spec beyond the hub + developer leaf + dual-block + transfers + interaction set: **unknown here**. Official leaves checked on this `as-of` do not publish them.
- Current live gas limits and which block size is the default: not restated here. See [Dual-block](dual-block.md).
- Whether the hub sentence “write system contracts are not live on mainnet yet” names CoreWriter: **unknown here**. See [One state](one-state.md).
- JSON-RPC methods, websocket support on the published host, wallet steps, SDKs, and explorers: later Taskmap slots, not this page.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/about-hyperliquid.md | 1 | 2026-09-28 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/overview.md | 1 | 2026-09-28 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/hyperevm.md | 1 | 2026-09-28 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm.md | 1 | 2026-09-28 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm/dual-block-architecture.md | 1 | 2026-09-28 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm/hypercore-less-than-greater-than-hyperevm-transfers.md | 1 | 2026-09-28 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm/interacting-with-hypercore.md | 1 | 2026-09-28 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/onboarding/how-to-use-the-hyperevm.md | 1 | 2026-09-28 |
| https://hyperliquid.xyz/tech | 2 | 2026-09-28 |
