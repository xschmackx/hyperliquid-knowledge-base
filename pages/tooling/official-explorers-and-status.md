# Official explorers and status pages

| Field | Value |
|-------|--------|
| Shelf | APIs and tooling (`pages/tooling/`) |
| Scope | First-party explorers and official status surfaces a stranger can open to inspect Hyperliquid state and operational status. Not node-as-client ingest. Not node-as-L1-participant. Not the public API catalogs. Not HyperEVM JSON-RPC. Not dated incident narrative. Not market, fee, or risk meaning of what those views show. |
| Status | Accepted |
| Page `as-of` | 2026-09-28 |
| Rank | Claims below are Rank 1 unless tagged |

Two first-party inspect surfaces. They are not the same product.

The app explorer is where Rank 1 docs send a stranger to look at L1 state on the official app. The status hub is the operational ledger for named components and dated incidents. Do not collapse them.

What a perp, spot market, fee, or margin rule *means* stays on S2–S4. Dated incident rows stay on [`../risk/incidents.md`](../risk/incidents.md). Node flags, local paths, and S3 prefixes — including `explorer_blocks` — stay on [`nodes-as-clients.md`](nodes-as-clients.md). Public API hosts stay on [`api-servers.md`](api-servers.md). Official HyperEVM chain parameters and JSON-RPC stay on [`hyperevm-rpc.md`](hyperevm-rpc.md). Node-as-L1-participant stays on [`../protocol/nodes.md`](../protocol/nodes.md).

Official names only. The Rank 1 name for the first-party explorer is **Hyperliquid.xyz**. Not “HyperScan”. Not “HyperEVMScan”.

---

## Mainnet explorer

Rank 1 HyperCore Tools lists **Hyperliquid.xyz** first under Explorers.

URL, `as-of` 2026-09-28: https://app.hyperliquid.xyz/explorer

Source: [HyperCore Tools](https://hyperliquid.gitbook.io/hyperliquid-docs/builder-tools/hypercore-tools).

Rank 1 info endpoint documents a token-details path on that explorer. The sentence is: the L1 name on the token details page can be used to detect remappings. Example URL on that leaf: https://app.hyperliquid.xyz/explorer/token/0x8f254b963e8468305d409b33aa137c67

Remapping rules stay on [`info-endpoint.md`](info-endpoint.md). This page only names the path.

Source: [Info endpoint](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/info-endpoint.md) — checked 2026-09-28.

Product UI on that URL, Rank 2/3, same `as-of`: the page title is Hyperliquid. Visible section labels include **Latest Blocks**, **Latest Transactions**, **View All Blocks**, **View All Transactions**. That is the chrome on this check. It is not a published feature catalog. In-app announcement lines on the same screen are not the status hub.

Rank 1 withdrawal FAQ: if a withdrawal status says Completed, click the explorer link next to the timestamp to check the destination address. That link is the destination-chain explorer for the withdrawal. It is not a second Hyperliquid explorer product.

Source: [Withdrawal has not arrived in my wallet](https://hyperliquid.gitbook.io/hyperliquid-docs/support/faq/withdrawal-issues/withdrawal-has-not-arrived-in-my-wallet.md) — checked 2026-09-28.

---

## Testnet explorer

Rank 1 testnet faucet names the official testnet app host https://app.hyperliquid-testnet.xyz and the drip path `/drip`. It does not title an explorer.

The explorer path on that host is first-party product UI, Rank 2, `as-of` 2026-09-28: https://app.hyperliquid-testnet.xyz/explorer

Safe reading: the testnet counterpart of the mainnet explorer path, on the official testnet app host. Not a Rank 1 sentence. Do not cite a docs title that is not there.

Source: [Testnet faucet](https://hyperliquid.gitbook.io/hyperliquid-docs/onboarding/testnet-faucet) — host and drip only.

---

## Status hub

Official status surface, Rank 2/3, `as-of` 2026-09-28.

| Surface | URL |
|---------|-----|
| Hub | https://hyperliquid.statuspage.io/ |
| History | https://hyperliquid.statuspage.io/history |

Page title on this check: **Hyperliquid Status**. Heading: **All Systems Operational**. Named components only: **Frontend**, **Hyperliquid L1**, **API**. Each was Operational on this check. No HyperEVM component on that hub. Do not read “All Systems Operational” as HyperEVM coverage. That coverage is **unknown** on this surface.

A subscribe control is on the hub. The hub also links **View historical uptime** at https://hyperliquid.statuspage.io/uptime on this check. What that uptime view counts is not restated here.

Rank 1 docs do not contain a dedicated status-page leaf that names this URL on this check. The hub is still the Hyperliquid-branded operational artifact. Same rank treatment as [`../risk/incidents.md`](../risk/incidents.md).

Dated rows — Network upgrade windows, the 29 Jul 2025 API server order delays, the 12 Nov 2025 Arbitrum bridge lock — stay on that incidents page. This page does not rewrite them. Rank 1 Order types names a **post-only period of a network upgrade**. Matching effect stays on the incidents page. This page only names the status surface those windows are published on.

The status component **API** is a component name. Public host list stays on [`api-servers.md`](api-servers.md). Whether each public host maps 1:1 onto that component: **unknown here**.

Official channels on Support Read Me — https://hyperfoundation.org/, the trade UI, X, Telegram announcements — are not this status product. Dated announcement text used as incident evidence stays on the incidents page.

An info method `exchangeStatus` is not a published official status product on Rank 1 info-endpoint on this check. Local use of that name as a node staleness ping stays on [`nodes-as-clients.md`](nodes-as-clients.md). **Unknown** as an official status API.

---

## Not an official HyperEVM explorer

Rank 1 How to use the HyperEVM, wallet add-network fields, `as-of` 2026-09-28:

- Chain ID: 999
- Network Name: Hyperliquid
- RPC URL: https://rpc.hyperliquid.xyz/evm
- Block explorer URL (optional): left blank

No official HyperEVM explorer URL is published on that leaf. Chain parameters and the JSON-RPC catalog stay on [`hyperevm-rpc.md`](hyperevm-rpc.md).

Source: [How to use the HyperEVM](https://hyperliquid.gitbook.io/hyperliquid-docs/onboarding/how-to-use-the-hyperevm).

Rank 1 HyperEVM Tools lists explorer names under Explorers. Listing is not an official-product claim. Tag `secondary`. They cannot be sole support that the official HyperEVM explorer is one of these.

| Docs label | URL on that leaf | Tag |
|------------|------------------|-----|
| Blockscout | https://www.hyperscan.com/ | `secondary` |
| Etherscan | https://hyperevmscan.io/ | `secondary` |
| Hyperscan | https://hyperscan.com/ | `secondary` |
| Owlscan | https://owlscan.org/ | `secondary` |

Source: [HyperEVM Tools](https://hyperliquid.gitbook.io/hyperliquid-docs/builder-tools/hyperevm-tools) — checked 2026-09-28.

---

## Listed, not first-party (HyperCore)

Rank 1 HyperCore Tools lists two more names under Explorers, after Hyperliquid.xyz. Listing proves the docs pointed at them. It does not make them first-party. Tag `secondary`. Not sole support.

| Docs label | URL on that leaf | Tag |
|------------|------------------|-----|
| Flowscan | https://flowscan.xyz | `secondary` |
| HypurrScan | https://hypurrscan.io | `secondary` |

The same leaf has a separate Analytics heading. Those dashboards are not explorers and not status pages. Not copied here.

---

## Not this page

- `explorer_blocks` and other S3 prefixes are node-as-client ingest. See [`nodes-as-clients.md`](nodes-as-clients.md). Not an explorer product.
- Node-as-L1-participant: [`../protocol/nodes.md`](../protocol/nodes.md).
- Official SDKs: [`official-sdks.md`](official-sdks.md).
- Info, exchange, and WebSocket catalogs: their accepted S5 pages.
- Community analytics dashboards: not status pages. Not copied.

---

## Gaps inside this scope

- Official HyperEVM explorer product: **unknown**. Wallet leaf leaves Block explorer URL blank.
- Rank 1 title for the testnet explorer path: **unknown** (not on the faucet leaf). The URL above is product UI on the official testnet host.
- Status-hub HyperEVM component: **not named** on this check. Coverage: **unknown**.
- Mapping of status component **API** to each public host: **unknown here**.
- Official status API on Rank 1 info-endpoint: **unknown** on this check.
- Completeness of status history rows: not this page. See [`../risk/incidents.md`](../risk/incidents.md).
- Destination-chain explorer linked from a completed withdrawal: not a Hyperliquid explorer product.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/builder-tools/hypercore-tools | 1 | 2026-09-28 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/builder-tools/hyperevm-tools | 1 | 2026-09-28 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/onboarding/how-to-use-the-hyperevm | 1 | 2026-09-28 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/info-endpoint.md | 1 | 2026-09-28; token-details path only |
| https://hyperliquid.gitbook.io/hyperliquid-docs/onboarding/testnet-faucet | 1 | 2026-09-28; host and drip; explorer not titled |
| https://hyperliquid.gitbook.io/hyperliquid-docs/support/faq/withdrawal-issues/withdrawal-has-not-arrived-in-my-wallet.md | 1 | 2026-09-28; destination-chain link |
| https://hyperliquid.gitbook.io/hyperliquid-docs/trading/order-types.md | 1 | name pointer only; matching not rewritten |
| https://app.hyperliquid.xyz/explorer | 1 name; 2/3 UI labels | 2026-09-28 |
| https://app.hyperliquid-testnet.xyz/explorer | 2 | 2026-09-28; path on official testnet host; Rank 1 does not title it |
| https://hyperliquid.statuspage.io/ | 2/3 | 2026-09-28 |
| https://hyperliquid.statuspage.io/history | 2/3 | 2026-09-28 |
| https://hyperliquid.statuspage.io/uptime | 2/3 | link observed on the hub 2026-09-28 |

Accepted pages pointed at, not rewritten: [`../risk/incidents.md`](../risk/incidents.md) (`as-of` 2026-09-28), [`nodes-as-clients.md`](nodes-as-clients.md) (`as-of` 2026-09-28), [`api-servers.md`](api-servers.md) (`as-of` 2026-09-16), [`hyperevm-rpc.md`](hyperevm-rpc.md) (`as-of` 2026-09-28), [`official-sdks.md`](official-sdks.md) (`as-of` 2026-09-28), [`info-endpoint.md`](info-endpoint.md), [`../protocol/nodes.md`](../protocol/nodes.md).
