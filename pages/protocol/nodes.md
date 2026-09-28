# Nodes

| Field | Value |
|-------|--------|
| Shelf | Protocol (`pages/protocol/`) |
| Scope | What a node is as an L1 participant: official role names, permissionless run versus active-set participation, and where a node sits on the HyperBFT path. Not a runbook. Not HyperBFT internals. Not staking fee or reward accounting. |
| Status | Accepted |
| Page `as-of` | 2026-09-28 |
| Rank | Rank 1 unless a sentence is marked Rank 2 |

L1 identity lives on [What Hyperliquid is](what-hyperliquid-is.md). HyperBFT rounds, commits, height, and one-block finality live on [HyperBFT](hyperbft.md). Stake-set rules (self-delegation, top-27 active set, quorum, jail versus slash, commission cap) live on [Validators and consensus stake](validators-and-consensus-stake.md). HyperCore and HyperEVM as execution components live on [HyperCore](hypercore.md) and [HyperEVM](hyperevm.md). Shared state lives on [One state](one-state.md). This page does not rewrite those.

There is no official docs leaf titled “Nodes as L1 participants” (docs index checked 2026-09-28). Official names below are the names those leaves and the node repository use.

---

## Official role names

Official docs and the node repository use these names. This page does not add parallel ones.

- **Validating node** / **validator.** A consensus participant. Official HyperCore overview: blocks are produced by validators in proportion to the native token staked to each validator. How that stake set is formed is on [Validators and consensus stake](validators-and-consensus-stake.md).
- **Non-validating node** / **non-validator.** A node that is not in the validating role. Official Running a validator page treats running one as permissionless, same as running a validating node. Official Foundation leaf uses the name **non-validating node**.
- **Sentry.** Rank 2 (official node repository README): a non-validator peer a validator may connect. See below. Not a third consensus role.

“Full node”, “light node”, and “archive node” are **not** official names on the leaves checked 2026-09-28. They are not used here.

The official Nodes hub is a run pointer. Its title is documentation for running nodes, and it points at the node repository for non-validator and validator steps. It does not define participation. Install steps, hardware, ports, binary flags, and streaming outputs are out of scope.

Sources:

- [Running a validator](https://hyperliquid.gitbook.io/hyperliquid-docs/validators/running-a-validator.md) — checked 2026-09-28
- [Nodes](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/nodes.md) — checked 2026-09-28
- [HyperCore overview](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/overview.md) — checked 2026-09-28
- [Foundation non-validating node](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/nodes/foundation-non-validating-node.md) — checked 2026-09-28
- [node repository README](https://github.com/hyperliquid-dex/node) — Rank 2, checked 2026-09-28
- [Docs index (`llms.txt`)](https://hyperliquid.gitbook.io/hyperliquid-docs/llms.txt) — checked 2026-09-28

---

## Permissionless run is not an active-set seat

Official Running a validator page: running validating and non-validating nodes is **permissionless** — anyone can choose to do so.

The same page: the **active set** of validators is determined transparently based on the **top twenty-seven by stake**. Treat 27 as the official published active-set size on 2026-09-28, not a live count made by this desk.

Permissionless run does not mean every running validating node is in that active set. Who must self-delegate, the undelegate-only rule, and the static set inside an epoch live on [Validators and consensus stake](validators-and-consensus-stake.md). This page does not reprint those rules.

Rank 2 (node repository README): the validator set on **Testnet** is entirely permissionless (register and self-delegate). Whether mainnet registration is gated beyond the Rank 1 permissionless-run sentence and the top-27 active set is **unknown here**.

Sources:

- [Running a validator](https://hyperliquid.gitbook.io/hyperliquid-docs/validators/running-a-validator.md) — checked 2026-09-28
- [node repository README](https://github.com/hyperliquid-dex/node) — Rank 2, checked 2026-09-28

---

## Where a node sits on the L1 path

Official API servers page places the node on the request path. This is identity, not an API how-to.

- API servers **listen to updates from a node** and keep blockchain state locally.
- The API server serves information about that state and **forwards user transactions to the node**.
- The connected node **gossips the transaction as part of the HyperBFT consensus algorithm**.
- Once the transaction is in a **committed block on the L1**, the API server responds with the execution response from the L1.

Official HyperCore overview: Hyperliquid is secured by HyperBFT. Like most proof-of-stake chains, blocks are produced by validators in proportion to the native token staked to each validator.

What a committed round is, height, and one-block finality live on [HyperBFT](hyperbft.md). Official Staking page, already written there: all honest nodes agree on the ordered list of committed rounds. This page does not reopen rounds, commits, or quorum.

HyperCore and HyperEVM are not separate chains under a second consensus. That split lives on [HyperCore](hypercore.md), [HyperEVM](hyperevm.md), and [One state](one-state.md).

Sources:

- [API servers](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/api-servers.md) — checked 2026-09-28
- [HyperCore overview](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/overview.md) — checked 2026-09-28
- [About Hyperliquid](https://hyperliquid.gitbook.io/hyperliquid-docs/about-hyperliquid.md) — L1 name; checked 2026-09-28

---

## Signer and validator are not the same wallet

Rank 2 (node repository README). Official docs leaves checked here do not restate this split.

The README names two wallets:

- **Validator** wallet: holds funds and receives delegation rewards (called a cold wallet there).
- **Signer** wallet: used solely for signing consensus messages (called a hot wallet there).

Register publishes a `node_ip`, a **signer** address distinct from the **validator** wallet, a name, a description, and `initial_wei`. How to generate keys or submit that action is out of scope.

Reward accounting for the validator wallet is out of scope. Staking fee discount and staking rewards are not this page.

Source: [node repository README](https://github.com/hyperliquid-dex/node) — Rank 2, checked 2026-09-28.

---

## Jailed is not offline

Two official statements. They are not collapsed.

- Rank 1 (Staking): upon a quorum of jail votes, a validator becomes **jailed** and no longer participates in consensus. Jail is not slash. Procedure, unjail rate limits, and the “no automatic slashing” sentence live on [Validators and consensus stake](validators-and-consensus-stake.md). Not reprinted here.
- Rank 2 (node repository README): when a validator is jailed, it can still participate in the consensus network by **forwarding messages to peers**, but it **does not vote on or propose blocks**.

Rank 2 also: on first register, or after an IP change, the validator is **automatically jailed** and does not participate in consensus until it unjails itself (`unjailSelf`). `jailSelf` is how that README names exiting consensus before shutdown. Commands for either act are out of scope.

Source for the Rank 1 sentence: [Staking](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/staking.md) — checked 2026-09-28. Source for the Rank 2 sentences: [node repository README](https://github.com/hyperliquid-dex/node) — checked 2026-09-28.

---

## Sentry

Rank 2 (node repository README). No Rank 1 docs leaf checked here defines sentry.

A validator may connect **up to two** non-validator peers via `sentry_ips`. The README says sentry nodes should be run by the validator themselves. Stated purpose: validators should dedicate resources to consensus instead of serving many non-validators or running expensive local servers. Sentries can be used as public root peers, API servers, EVM RPCs, and similar.

That is role placement, not a peering guide. How to set `sentry_ips`, which ports to open, and how to serve RPC or info are out of scope.

Exact sentry-network topology beyond “up to two” is **unknown here**.

Source: [node repository README](https://github.com/hyperliquid-dex/node) — Rank 2, checked 2026-09-28.

---

## Foundation non-validating node is a named peer, not the definition

Official Foundation leaf: running a non-validating node is permissionless. The Foundation non-validating node is a **peer with fewer hops to validating nodes**, offered as best-effort public data. It is not the definition of a node, and it is not a sole source.

Eligibility (stake, maker tier, uptime, form) is operator access to that peer. It is not protocol identity. This page does not record how to apply. How many hops “fewer hops” means is **unknown here**.

A separate official leaf lists third-party peering for infra providers. That list is an operator marketplace, not a protocol fact, and is not copied here.

Sources:

- [Foundation non-validating node](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/nodes/foundation-non-validating-node.md) — checked 2026-09-28
- [Foundation non-validating node for infra providers](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/nodes/foundation-non-validating-node-for-infra-providers.md) — named only; checked 2026-09-28

---

## Gaps inside this scope

- Live count of validators after this `as-of`: **unknown here**. Official active-set rule is top 27 by stake.
- Whether mainnet registration is gated beyond permissionless run plus the top-27 active set: **unknown here**. Rank 1 states those two facts. Rank 2 states Testnet registration is entirely permissionless.
- Exact sentry topology beyond “up to two”: **unknown here**.
- How many hops “fewer hops to validating nodes” means: **unknown here**.
- Any node-count or geographic map: **unknown here**. Not published on the leaves checked.
- Official names “full node”, “light node”, “archive node”: **not on the leaves checked**. Not used.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/validators/running-a-validator.md | 1 | 2026-09-28 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/validators.md | 1 | 2026-09-28 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/staking.md | 1 | 2026-09-28 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/overview.md | 1 | 2026-09-28 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/about-hyperliquid.md | 1 | 2026-09-28 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/api-servers.md | 1 | 2026-09-28 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/nodes.md | 1 | 2026-09-28 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/nodes/foundation-non-validating-node.md | 1 | 2026-09-28 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/nodes/foundation-non-validating-node-for-infra-providers.md | 1 | 2026-09-28 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/llms.txt | 1 | 2026-09-28 |
| https://github.com/hyperliquid-dex/node | 2 | 2026-09-28 |
