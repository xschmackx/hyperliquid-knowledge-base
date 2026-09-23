# OFFICIAL SOURCE INDEX

**Page `as-of`:** 2026-09-15  
**Checked:** official docs index `llms.txt` plus the official GitHub org landing page.

This file lists first-party sources a later accepted page may cite. It is not an accepted coverage page. It does not explain how Hyperliquid works.

Rank and stale rules: `SOURCE-RANK.md`.

---

## How to use this file

- Prefer Rank 1–3 from this list.
- Re-check `llms.txt` before treating a missing docs URL as unknown.
- If an official source here has changed on a cited point, pages that cited the old point are stale.
- Community tools linked *from* official docs stay Rank 4 unless Hyperliquid itself publishes them.

---

## Hubs (Rank 1 — official written canon)

| Source | URL |
|--------|-----|
| Hyperliquid Docs (root) | https://hyperliquid.gitbook.io/hyperliquid-docs |
| Docs index (`llms.txt`) | https://hyperliquid.gitbook.io/hyperliquid-docs/llms.txt |
| About Hyperliquid | https://hyperliquid.gitbook.io/hyperliquid-docs/about-hyperliquid.md |
| API (public API overview) | https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api.md |
| Nodes | https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/nodes.md |
| HyperCore hub | https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore.md |
| HyperEVM hub | https://hyperliquid.gitbook.io/hyperliquid-docs/hyperevm.md |
| HIPs hub | https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips.md |
| Trading hub | https://hyperliquid.gitbook.io/hyperliquid-docs/trading.md |

The complete official page list on 2026-09-15 is `llms.txt`. This index does not duplicate every leaf.

---

## Docs sections → corpus shelves

Where a later page should live if it draws from that official section.

| Official section | Shelf |
|------------------|--------|
| About, HyperCore overview, HyperEVM architecture, dual-block, validators, staking-as-consensus, nodes-as-L1 | Protocol — `pages/protocol/` |
| Trading products, order types, books, funding, HIP-1 / HIP-2 / HIP-3 / HIP-4, vaults as products, aligned quote assets | Markets — `pages/markets/` |
| Fees, sub-accounts, referrals, points, builder codes as fee logic, staking rewards | Accounts — `pages/accounts/` |
| Margining, margin tiers, liquidations, ADL, portfolio margin as risk, delist consequences | Risk — `pages/risk/` |
| API, info, exchange, WebSocket, signing, rate limits, JSON-RPC, node how-to, official SDKs | Tooling — `pages/tooling/` |
| Support FAQ, onboarding how-to | Split: user action on Accounts or Tooling; L1 mechanism on Protocol. Do not file FAQ as protocol fact without the Rank 1 page. |

---

## Official artifacts (Rank 2)

| Source | URL | Notes |
|--------|-----|--------|
| GitHub org | https://github.com/hyperliquid-dex | Org landing checked 2026-09-15. |
| Python SDK | https://github.com/hyperliquid-dex/hyperliquid-python-sdk | Linked from official API page. |
| Rust SDK (org) | https://github.com/hyperliquid-dex/hyperliquid-rust-sdk | Under the official org. |
| Node | https://github.com/hyperliquid-dex/node | |
| Contracts | https://github.com/hyperliquid-dex/contracts | Listed on the org page. |

Other repos under the same org may exist. Absence from this table is not a claim they are unofficial. Add them when next checked.

---

## Official API hosts (Rank 2 — as published on the API page)

From https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api.md (checked 2026-09-15):

| Network | REST / info+exchange | WebSocket |
|---------|----------------------|-----------|
| Mainnet | https://api.hyperliquid.xyz | wss://api.hyperliquid.xyz/ws |
| Testnet | https://api.hyperliquid-testnet.xyz | wss://api.hyperliquid-testnet.xyz/ws |

HyperEVM JSON-RPC hosts published on official HyperEVM docs (checked 2026-09-15, still treated as official on this `as-of`):

| Network | JSON-RPC |
|---------|----------|
| Mainnet | https://rpc.hyperliquid.xyz/evm |
| Testnet | https://rpc.hyperliquid-testnet.xyz/evm |

Re-check those two RPC URLs against the live HyperEVM doc before an accepted tooling page cites them.

---

## Official product / foundation surfaces (Rank 3 unless the page is written docs)

| Source | URL | Rank |
|--------|-----|------|
| App | https://app.hyperliquid.xyz | 3 (first-party product UI) |
| Foundation site (linked from official GitHub org) | https://hyperfoundation.org | 3 |
| X account linked from official GitHub org | https://x.com/HyperliquidX | 3 |

A single official post is Rank 3. It does not replace Rank 1 docs.

---

## Linked from official docs, not first-party (Rank 4)

The official API page and Builder Tools pages list third-party SDKs, RPCs, and peering providers. Those listings prove Hyperliquid *pointed at* them. They do not make the third party Rank 1–2.

Examples noted 2026-09-15 (not exhaustive):

- Community TypeScript SDKs named on the API page
- Community Rust SDK (Infinite Field / hypersdk) named on the API page — distinct from `hyperliquid-dex/hyperliquid-rust-sdk`
- Builder-tools RPC and peering directories

Cite them only tagged `secondary`.

---

## Gaps on this check

- Support FAQ subtree in `llms.txt` was not walked leaf-by-leaf.
- Brand kit, audits, bug bounty, historical data are official pages; not mapped in detail here.
- Whether every repo under `hyperliquid-dex` is first-party publish is **unknown** until listed on a later check.
- Official Discord is linked from the GitHub org; channel-level canon is **unknown** without a Rank 1 statement that a given channel is official communication.

Refresh this file when `llms.txt` or the official org page changes on a cited hub. Do not silently keep a stale hub URL.
