# One state

| Field | Value |
|-------|--------|
| Shelf | Protocol (`pages/protocol/`) |
| Scope | How HyperCore and HyperEVM share HyperBFT and pass value or reads. Native transfer as an L1 mechanism. |
| Status | Accepted |
| Page `as-of` | 2026-09-16 |
| Rank | All claims below are Rank 1 |

This page does not cover dual-block production, validators, how a user moves balances in the app, market products, or how to call the API. Identity of the L1 and the two execution names lives on [What Hyperliquid is](what-hyperliquid-is.md).

---

## Same chain, one consensus, one state

Official docs split Hyperliquid state execution into HyperCore and HyperEVM. They also say those two parts are not two chains.

The HyperEVM is secured by the same HyperBFT consensus as HyperCore. Official HyperCore overview: the Hyperliquid state consists of HyperCore and the general-purpose HyperEVM, with one consistent order of transactions through HyperBFT.

Official HyperEVM hub: there is no bridging risk between HyperCore and HyperEVM as one unified state. The same hub says this lets the HyperEVM interact directly with parts of HyperCore, such as spot and perp order books.

Sources:

- [About Hyperliquid](https://hyperliquid.gitbook.io/hyperliquid-docs/about-hyperliquid.md) — checked 2026-09-16
- [HyperCore overview](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/overview.md) — checked 2026-09-16
- [HyperEVM](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperevm.md) — checked 2026-09-16

How HyperBFT votes, times out, or changes view is **unknown on this page**. Validator-set rules are out of scope.

---

## Passing value: native transfer between HyperCore and HyperEVM

Official docs describe a native conversion between HyperCore spot and HyperEVM once a Core spot asset is **linked** to an EVM contract. Until that link exists, official transfer docs say conversion between the two sides is not available for that token.

HYPE is a special case. Official transfer docs: as the native token on HyperCore, HYPE links to the native HyperEVM balance rather than an ERC-20 contract. Official developer HyperEVM page: HYPE is the native gas token on the HyperEVM.

### System addresses

Official transfer docs give each token a system address on HyperCore: first byte `0x20`, remaining bytes zero except the token index encoded big-endian. Example from that page: token index 200 uses `0x20000000000000000000000000000000000000c8`.

HYPE is the published exception. Its system address is `0x2222222222222222222222222222222222222222`.

### Direction: HyperCore → HyperEVM

Official transfer docs: after a token is linked, a Core-to-EVM move uses a `sendAsset` action (or the official frontend) with the corresponding system address as destination. Tokens are credited by a system transaction that calls `transfer(recipient, amount)` on the linked contract as the system address, where `recipient` is the sender of `sendAsset`.

The same page says a transfer from HyperCore to HyperEVM costs 200k gas at the base gas price of the next HyperEVM block. Treat that gas figure as the official published number on 2026-09-16, not a measurement made by this desk.

### Direction: HyperEVM → HyperCore

Official transfer docs: an EVM-to-Core move of a linked ERC-20 is an ERC-20 `transfer` to the system address. Tokens are credited on HyperCore from the emitted `Transfer(address from, address to, uint256 value)` log on the linked contract.

HYPE back to HyperCore is sent as transaction value to `0x2222222222222222222222222222222222222222`. Official docs: that address is a system contract whose payable `receive()` emits `Received(address indexed user, uint256 amount)` with `user` equal to `msg.sender`, so both EOAs and contracts can move HYPE back to HyperCore. Emitting the log has a gas cost on the EVM side.

### Timing of the two directions

Official interaction-timings page:

- Transfers from HyperCore to HyperEVM are queued on the L1 until the next HyperEVM block.
- Transfers from HyperEVM to HyperCore happen in the same L1 block as the HyperEVM block, immediately after the HyperEVM block is built.

On an L1 block that produces a HyperEVM block, official order is: L1 block built, then EVM block built, then EVM → Core transfers processed, then CoreWriter actions processed.

Why some L1 blocks produce a HyperEVM block and others do not is **out of this page's scope** (dual-block).

### Limits official docs put on the mechanism

Official transfer docs also state:

- Linking expects the system address on one side to hold the total non-system balance equal to max supply on the other side.
- There are currently no checks that the system address has sufficient supply or that the contract is a valid ERC-20.
- The linked contract may have arbitrary bytecode. Official docs say there are no guarantees about what the `transfer` call does on the EVM, and not to assume accurate fungibility between Core and EVM spot.
- If the EVM contract has extra wei decimals and a relevant log value is not round to those extra decimals, the non-round amount is burned (officially guaranteed to be less than 1 wei).

How a stranger clicks the app, signs a particular API body, or chooses a wallet is out of scope.

Sources:

- [HyperCore <> HyperEVM transfers](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm/hypercore-less-than-greater-than-hyperevm-transfers.md) — checked 2026-09-16
- [HyperEVM (developer)](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm.md) — checked 2026-09-16
- [Interaction timings](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm/interaction-timings.md) — checked 2026-09-16

---

## Passing reads (and writes) across the same state

Official HyperEVM hub: a contract can read HyperCore order-book prices using a **read precompile**, and can send orders on HyperCore books using a **write system contract**.

### Reads

Official interacting-with-HyperCore page: the testnet EVM provides read precompiles starting at `0x0000000000000000000000000000000000000800`. Methods described there query perps positions, spot balances, vault equity, staking delegations, oracle prices, and the L1 block number. Values are guaranteed to match the latest HyperCore state at the time the EVM block is constructed.

Whether every listed precompile is live on mainnet is **unknown on this page**. The interacting page introduces them as a testnet EVM feature. The HyperEVM hub describes a read precompile without a network qualifier. This desk does not collapse those two sentences into a mainnet inventory.

### Writes

Official interacting-with-HyperCore page: a CoreWriter system contract at `0x3333333333333333333333333333333333333333` sends transactions from the HyperEVM to HyperCore by emitting a log that HyperCore processes as an action. Official action types exist on that page (orders, vault transfer, staking, spot send, and others). Action-encoding bytes and field layouts are tooling, not this page.

The same page: order actions and vault transfers sent from CoreWriter are delayed onchain for a few seconds so HyperEVM cannot bypass the L1 mempool for latency. Those delayed actions appear twice on the L1 explorer: enqueue, then HyperCore execution.

Official interaction timings: the account performing a CoreWriter action must exist on HyperCore before the EVM block is built. An EVM → Core transfer that initializes the account in the same block still leaves the CoreWriter action rejected.

Official HyperEVM hub, under “What stage is the HyperEVM in?”: the HyperEVM is in the alpha stage, and “higher throughput and write system contracts are not live on mainnet yet.” This page does not treat that sentence and the CoreWriter address as the same object. Whether CoreWriter on mainnet is that “write system contract,” and which write actions are live where, is **unknown here** beyond what those two official pages separately say.

Sources:

- [HyperEVM](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperevm.md) — checked 2026-09-16
- [Interacting with HyperCore](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm/interacting-with-hypercore.md) — checked 2026-09-16
- [Interaction timings](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm/interaction-timings.md) — checked 2026-09-16

---

## Gaps inside this scope

- Exact HyperBFT internals that produce the single transaction order: **unknown here**. Official overview names one consistent order through HyperBFT. It does not specify the vote protocol on these pages.
- Mainnet inventory of read precompiles: **unknown here**. Official interacting page is framed as testnet EVM.
- Whether “write system contracts are not live on mainnet” (HyperEVM hub) names the CoreWriter contract at `0x333…3`: **unknown here**.
- Atomicity, failure, and revert behaviour when a system `transfer` on the EVM side does not match Core credit: official docs warn there are no guarantees about what `transfer` does; further failure cases are **unknown here**.
- Linking steps as a signed API sequence: out of scope (tooling). That a link must exist before conversion is in scope above.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/about-hyperliquid.md | 1 | 2026-09-16 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/overview.md | 1 | 2026-09-16 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/hyperevm.md | 1 | 2026-09-16 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm.md | 1 | 2026-09-16 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm/hypercore-less-than-greater-than-hyperevm-transfers.md | 1 | 2026-09-16 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm/interaction-timings.md | 1 | 2026-09-16 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm/interacting-with-hypercore.md | 1 | 2026-09-16 |
