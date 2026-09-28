# Official SDKs

| Field | Value |
|-------|--------|
| Shelf | APIs and tooling (`pages/tooling/`) |
| Scope | First-party SDKs and examples Hyperliquid publishes, as official interfaces a stranger uses to talk to Hyperliquid from software. Not the info-type catalog. Not the exchange-action catalog. Not WebSocket schemas. Not HyperEVM JSON-RPC hosts. Not a node runbook. Not market, fee, or risk meaning of the calls. |
| Status | Accepted |
| Page `as-of` | 2026-09-28 |
| Rank | Claims below are Rank 1 unless tagged |

This page names the SDKs and examples Hyperliquid publishes. It does not list `info` request types, signed `exchange` actions, WebSocket channels, signing construction, rate-limit tables, REST or WebSocket hosts, or HyperEVM JSON-RPC methods. Those stay on their own S5 pages. Hosts the SDKs wrap are already on [`api-servers.md`](api-servers.md). Info types are on [`info-endpoint.md`](info-endpoint.md). Exchange actions, and the official pointer to the Python SDK for signatures, are on [`exchange-endpoint.md`](exchange-endpoint.md). WebSocket subscriptions and post-over-WS are on [`websocket.md`](websocket.md).

---

## What the official API page names

Official API page wording, checked 2026-09-28:

- Python SDK: `https://github.com/hyperliquid-dex/hyperliquid-python-sdk`
- Rust SDK written by community member, Infinite Field: `https://github.com/infinitefield/hypersdk`
- Typescript SDKs written by members of the community: `https://github.com/nktkas/hyperliquid` and `https://github.com/nomeida/hyperliquid`
- CCXT, named there as a multi-language integration

The same split is on Builder Tools → HyperCore Tools: Python SDK first-party; Rust and TypeScript named as community.

That wording is the Rank 1 split. It does not name a first-party TypeScript SDK. It does not name the official-org Rust repository in the next section. Those are different facts.

The GitBook API page last-updated stamp was about eight months before this check. Exact stamp date is not copied here.

Sources: [API](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api.md); [HyperCore Tools](https://hyperliquid.gitbook.io/hyperliquid-docs/builder-tools/hypercore-tools.md) — checked 2026-09-28.

---

## Python SDK (first-party)

Official docs name this repo as the Python SDK. The repository is under the official GitHub org `hyperliquid-dex`.

| Fact | Published value on this `as-of` |
|------|----------------------------------|
| Repo | https://github.com/hyperliquid-dex/hyperliquid-python-sdk |
| README line | "SDK for Hyperliquid API trading with Python." |
| Install string | `pip install hyperliquid-python-sdk` |
| Package name | `hyperliquid-python-sdk` |
| Version | **0.24.0** |
| Authors line in `pyproject.toml` | Hyperliquid `<hello@hyperliquid.xyz>` |

Version **0.24.0** is the figure in repo `pyproject.toml` at commit `2fdb18f`, the GitHub release 0.24.0 by `traderben` on 2026-06-04, and the PyPI release 0.24.0 on 2026-06-04. Registry and repo URLs: [PyPI `hyperliquid-python-sdk`](https://pypi.org/project/hyperliquid-python-sdk/); [GitHub releases](https://github.com/hyperliquid-dex/hyperliquid-python-sdk/releases). Rank 2 for the version files and release; Rank 1 for the name on the API page. Whether PyPI lags git `master` after this check: **unknown here**.

Classes a stranger meets in that SDK (Rank 2, repo on this check): `hyperliquid.info.Info`, `hyperliquid.exchange.Exchange`, `hyperliquid.utils.constants` (`MAINNET_API_URL` / `TESTNET_API_URL`). Optional `skip_ws=True`. Examples live under `examples/`. Those constants wrap the hosts already recorded on [`api-servers.md`](api-servers.md). This page does not restate the host table.

**API wallet vs account address.** Official README on that repo: generate an API key at https://app.hyperliquid.xyz/API ; `secret_key` is the API wallet; `account_address` must remain the main wallet public key, not the API wallet. No other auth scheme is published on this page.

Signing construction stays on [`exchange-endpoint.md`](exchange-endpoint.md). Official Exchange docs already say to see the Python SDK for code to generate signatures. This page does not paste that code.

Source: [hyperliquid-python-sdk](https://github.com/hyperliquid-dex/hyperliquid-python-sdk) — checked 2026-09-28. Rank 2 artifact named by Rank 1.

---

## Rust: two different clients

Do not merge these names.

**Community client named on the Rank 1 API page.** Official wording: "Rust SDK written by community member, Infinite Field" at https://github.com/infinitefield/hypersdk . That sentence proves Hyperliquid pointed at it. It does not make the client Rank 1 or Rank 2. Tag: `community` / `secondary`. Feature parity with the org crate below: **unknown here**. Version of that community repo: **unknown here**.

**First-party artifact under the official org.** Not named on the Rank 1 API page.

| Fact | Published value on this `as-of` |
|------|----------------------------------|
| Repo | https://github.com/hyperliquid-dex/hyperliquid-rust-sdk |
| README line | "SDK for Hyperliquid API trading with Rust." |
| Install string | `cargo add hyperliquid_rust_sdk` |
| Package name in `Cargo.toml` | `hyperliquid_rust_sdk` |
| Version in `Cargo.toml` | **0.6.0** |
| Homepage in `Cargo.toml` | `https://hyperliquid.xyz/` |
| Examples | `src/bin` |

Rank 2. crates.io was not fetched on this check. Cite the official repo `Cargo.toml`, not a registry page. Whether the crates.io yank matches 0.6.0: **unknown here**.

The API page does not document this org crate. Do not say that it does.

Source: [hyperliquid-rust-sdk](https://github.com/hyperliquid-dex/hyperliquid-rust-sdk) — checked 2026-09-28.

---

## TypeScript: examples, not an SDK

No first-party TypeScript SDK is published on this check. Rank 1 text says TypeScript SDKs are "written by members of the community." Official first-party TypeScript SDK: **unpublished / unknown**.

Official org repo `hyperliquid-dex/ts-examples` is examples, not an SDK. README checked 2026-09-28: "Sample scripts/snippets for computing various frontend values. Refer to [@nktas/hyperliquid](https://github.com/nktkas/hyperliquid) or [hyperliquid-ts-sdk](https://github.com/nomeida/hyperliquid) for Typescript SDKs written by a member of the community."

The nktkas handle in that README is `@nktas`. The repo URL on the same line is `nktkas`. Both are recorded as published. Which spelling Hyperliquid intends beyond the published link target `nktkas/hyperliquid`: **unknown here**.

Source: [ts-examples](https://github.com/hyperliquid-dex/ts-examples) — checked 2026-09-28. Rank 2 examples repo.

---

## Community clients named by official docs

These may be listed only tagged. They cannot support a claim that Hyperliquid publishes an official TypeScript SDK, or that Infinite Field is the official-org Rust SDK.

| Official wording | URL | Tag |
|------------------|-----|-----|
| Rust SDK written by community member, Infinite Field | https://github.com/infinitefield/hypersdk | `community` / `secondary` |
| Typescript SDKs written by members of the community | https://github.com/nktkas/hyperliquid | `community` / `secondary` |
| Typescript SDKs written by members of the community | https://github.com/nomeida/hyperliquid | `community` / `secondary` |
| CCXT as a multi-language integration | https://docs.ccxt.com/#/exchanges/hyperliquid | `community` / `secondary` |

Official listing proves Hyperliquid pointed at them. It does not make them first-party. Other language wrappers that are not named on the official API page are not first-party on this check, and are not catalogued here.

---

## Official example file that is not a new SDK

HyperEVM Tools points at one first-party example file in the Python SDK, not a separate SDK: `https://github.com/hyperliquid-dex/hyperliquid-python-sdk/blob/master/examples/basic_evm_use_big_blocks.py`.

Dual-block architecture and HyperEVM RPC hosts stay off this page (later S5 slot / S1).

Source: [HyperEVM Tools](https://hyperliquid.gitbook.io/hyperliquid-docs/builder-tools/hyperevm-tools.md) — checked 2026-09-28.

---

## Org repos that are not this page

On this check the official org listed eight public repos. These are first-party repositories and are not official SDKs for talking to the public API. Named only so they are not read as this page:

- `node` — nodes as clients / L1 participant; not this page
- `contracts` — not this page
- `order_book_server` — not this page
- `hyper-evm-sync` — HyperEVM / S1; not this page
- `historical_data` — not this page

How to run a node, HyperEVM RPC connection data, and official explorers or status pages stay unwritten here.

Source: [hyperliquid-dex](https://github.com/hyperliquid-dex) — checked 2026-09-28. Rank 2.

---

## Gaps inside this scope

- Whether Hyperliquid will publish a first-party TypeScript SDK: **unknown here**.
- Whether `hyperliquid-dex/hyperliquid-rust-sdk` and Infinite Field `hypersdk` are feature-equivalent: **unknown here**.
- Whether PyPI or a crates registry lags git `master` after this check: **unknown here**. crates.io was not fetched.
- Whether every language wrapper that appears on Builder Tools is still current: **unknown here**.
- Info types, exchange actions, WebSocket channels, signing math, rate limits, REST and WebSocket hosts, HyperEVM RPC: **unknown here** by scope. Point at the accepted S5 pages named above.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api.md | 1 | 2026-09-28 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/builder-tools/hypercore-tools.md | 1 | 2026-09-28 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/builder-tools/hyperevm-tools.md | 1 | 2026-09-28 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/exchange-endpoint.md | 1 | already accepted; pointed at, not rewritten |
| https://github.com/hyperliquid-dex | 2 | 2026-09-28 |
| https://github.com/hyperliquid-dex/hyperliquid-python-sdk | 2 | 2026-09-28 |
| https://pypi.org/project/hyperliquid-python-sdk/ | 2 | 2026-09-28 |
| https://github.com/hyperliquid-dex/hyperliquid-python-sdk/releases | 2 | 2026-09-28 |
| https://github.com/hyperliquid-dex/hyperliquid-rust-sdk | 2 | 2026-09-28 |
| https://github.com/hyperliquid-dex/ts-examples | 2 | 2026-09-28 |
| https://github.com/infinitefield/hypersdk | community / secondary | named by Rank 1; not re-audited as canon |
| https://github.com/nktkas/hyperliquid | community / secondary | named by Rank 1; not re-audited as canon |
| https://github.com/nomeida/hyperliquid | community / secondary | named by Rank 1; not re-audited as canon |
| https://docs.ccxt.com/#/exchanges/hyperliquid | community / secondary | named by Rank 1 as integration; not first-party |

Accepted pages pointed at, not rewritten: [`api-servers.md`](api-servers.md) (`as-of` 2026-09-16), [`info-endpoint.md`](info-endpoint.md), [`exchange-endpoint.md`](exchange-endpoint.md), [`websocket.md`](websocket.md).
