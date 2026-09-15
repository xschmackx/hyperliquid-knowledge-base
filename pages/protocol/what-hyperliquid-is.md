# What Hyperliquid is

| Field | Value |
|-------|--------|
| Shelf | Protocol (`pages/protocol/`) |
| Scope | Official identity of the Hyperliquid L1: what it is, what HyperBFT is named as, and how official docs split state execution into HyperCore and HyperEVM. |
| Status | Accepted |
| Page `as-of` | 2026-09-15 |
| Rank | All claims below are Rank 1 |

This page does not cover market products, fees, margin, or how to call the API. Those live on other shelves.

---

## Identity

Hyperliquid is a layer-one blockchain. Official docs also describe it as a performant blockchain built toward a fully onchain open financial system.

Source: [About Hyperliquid](https://hyperliquid.gitbook.io/hyperliquid-docs/about-hyperliquid.md) — checked 2026-09-15.

## Consensus name

The L1 uses a custom consensus algorithm official docs name **HyperBFT**. Official docs say it is inspired by HotStuff and its successors, and that both the algorithm and the networking stack are built to support the L1.

Source: same About page, checked 2026-09-15.

How HyperBFT works internally (timeouts, voting, view change) is **unknown on this page**. Official About text names the algorithm and its inspiration. It does not specify the protocol in this source.

## Two execution components

Official docs split Hyperliquid state execution into two components:

| Name | What official docs say it is |
|------|------------------------------|
| **HyperCore** | Fully onchain perpetual futures and spot order books. Every order, cancel, trade, and liquidation happens onchain. One-block finality inherited from HyperBFT. Also described as including margin and matching-engine state, without off-chain order books. |
| **HyperEVM** | A general-purpose smart-contract platform in the style of Ethereum, on the same Hyperliquid blockchain. Official docs say HyperCore liquidity and primitives are available as permissionless building blocks through HyperEVM. |

Official HyperCore overview: the Hyperliquid state consists of HyperCore and the general-purpose HyperEVM, with one consistent order of transactions through HyperBFT.

Sources:

- [About Hyperliquid](https://hyperliquid.gitbook.io/hyperliquid-docs/about-hyperliquid.md) — checked 2026-09-15
- [HyperCore overview](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/overview.md) — checked 2026-09-15

Native transfers between HyperCore and HyperEVM, and HyperEVM dual-block production, are **out of this page's scope**. Official pages exist; they are not summarised here.

## Throughput claim on HyperCore (dated)

As of this page's check, official About text says HyperCore currently supports 200k orders per second, with throughput described as improving as node software is optimized.

That number can change. Treat it as the official published figure on 2026-09-15, not a measurement made by this desk.

Source: [About Hyperliquid](https://hyperliquid.gitbook.io/hyperliquid-docs/about-hyperliquid.md) — checked 2026-09-15.

## Gaps inside this scope

- Validator-set size, staking amounts required to participate, and jail rules: not on this page. Official validator and staking docs exist.
- Whether “one-block finality” has exceptions under official docs: **unknown here**. About asserts one-block finality inherited from HyperBFT. This page does not add conditions.
- Legal or corporate identity of the publisher vs the protocol: **unknown here**. This page describes the chain as official docs describe it.

---

## Sources checked

| URL | Rank | Checked |
|-----|------|---------|
| https://hyperliquid.gitbook.io/hyperliquid-docs/about-hyperliquid.md | 1 | 2026-09-15 |
| https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/overview.md | 1 | 2026-09-15 |
