# Validators and consensus stake

| Field | Value |
|-------|--------|
| Shelf | Protocol (`pages/protocol/`) |
| Scope | How the validator set and stake secure the chain. Not rewards accounting. Not a node runbook. |
| Status | Accepted |
| Page `as-of` | 2026-09-16 |
| Rank | All claims below are Rank 1 |

This page does not cover L1 identity, native transfers, or dual-block production. Those live on [What Hyperliquid is](what-hyperliquid-is.md), [One state](one-state.md), and [Dual-block](dual-block.md). It does not cover staking rewards, undelegate or unstake queues, the Foundation delegation program, or how to run a node binary.

---

## Delegated proof-of-stake

Official Staking page: Hyperliquid only supports delegated proof-of-stake. On that page, **delegate** and **stake** are used interchangeably.

HYPE in a staking account may be staked to any number of validators. How value moves between spot and staking, and lockups on undelegation, are out of scope.

Source: [Staking](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/staking.md) — checked 2026-09-16.

---

## Who may run a node; who is in the active set

Official Running a validator page: running validating and non-validating nodes is **permissionless** — anyone can choose to do so.

The same page: the active set of validators is determined transparently based on the **top twenty-seven by stake**. Treat 27 as the official published active-set size on 2026-09-16, not a live count made by this desk.

Hardware, ports, seed IPs, and binary install steps are out of scope.

Source: [Running a validator](https://hyperliquid.gitbook.io/hyperliquid-docs/validators/running-a-validator.md) — checked 2026-09-16.

---

## Self-delegation to become active

Official Staking page: each validator has a self-delegation requirement of **10k HYPE** to become active. That self-delegation requirement is locked for **one year**.

Any time self-delegation for a validator drops below 10k HYPE, the validator enters **undelegate-only** mode: all future delegations to that validator are disabled, so its total stake can only decrease going forward.

10k HYPE and the one-year lock are official published figures on 2026-09-16.

Source: [Staking](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/staking.md) — checked 2026-09-16.

---

## Epochs: set and consensus stakes are static

Official Staking page: the validator set evolves in epochs of **100k rounds**, which is approximately **90 minutes** on mainnet. The validators and consensus stakes are static for each staking epoch.

100k rounds and ~90 minutes are official published figures on 2026-09-16. Whether every mainnet epoch is measured at 90 minutes, and what the testnet duration is, is **unknown here** beyond that sentence.

Official Staking page also: HyperBFT consensus proceeds in **rounds** — a discrete bundle of transactions along with signatures from a quorum of validators. A key property named there: all honest nodes agree on the ordered list of committed rounds. Vote, timeout, and view-change internals are **unknown on this page** and stay parked.

Source: [Staking](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/staking.md) — checked 2026-09-16.

---

## Quorum

Official Staking page: a quorum is any set of validators that has **more than ⅔ of the total stake** in the network. The operating requirement of consensus is that a quorum of stake is honest (non-Byzantine).

The same page: therefore it is an essential responsibility of every staker to only delegate to trusted validators.

⅔ is the official published threshold on 2026-09-16.

Source: [Staking](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/staking.md) — checked 2026-09-16.

---

## Jail is not slash

Official Staking page splits the two:

- **Jail.** Validators may vote to jail peers that do not respond with adequate latency or frequency to the consensus messages of the voter. Upon receiving a quorum of jail votes, a validator becomes jailed and no longer participates in consensus. A validator may **unjail** itself, subject to onchain unjailing rate limits. This page does not record how to diagnose, unjail, or operate a node.
- **Slash.** Jailing is not slashing. Official text reserves slashing for provably malicious behavior such as double-signing blocks at the same round. The same page: there is currently **no automatic slashing implemented** (official as of 2026-09-16).

What the onchain unjail rate limit is, in numbers, is **unknown here**. The Staking page names the limit; it does not state the rate.

Source: [Staking](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/staking.md) — checked 2026-09-16.

---

## Commission increase cap (set rule only)

Official Staking page: validators may charge a commission to their delegators. That commission cannot be increased unless the **new commission is less than or equal to 1%**.

Official reason on that page: this prevents a validator from attracting a large amount of stake and then raising commission significantly. Reward payout math is out of scope.

1% is the official published cap on 2026-09-16. Whether commission may be decreased without that cap is **unknown here**; the official sentence is about increases.

Source: [Staking](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/staking.md) — checked 2026-09-16.

---

## Gaps inside this scope

- Live count of active validators at any moment after this `as-of`: **unknown here**. Official rule on the Running a validator page is top 27 by stake.
- Testnet epoch length: **unknown here**. Official ~90 minutes is mainnet.
- Unjail rate-limit numbers: **unknown here**.
- When automatic slashing would be implemented, and the slash amount: **unknown here**. Official Staking page says slashing is reserved for provable malice and that automatic slashing is not currently implemented.
- HyperBFT vote, timeout, and view-change rules: **unknown here**. Parked.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/staking.md | 1 | 2026-09-16 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/validators/running-a-validator.md | 1 | 2026-09-16 |
