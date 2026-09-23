# REGISTER RULES — Hyperliquid Knowledge Base

This page is the status vocabulary and filing rule for the observation register. It does not fill the register. An observation does not create work.

Truth stays in `SOURCE-RANK.md`. Voice and coverage stay in `VOICE-AND-COVERAGE.md`.

---

## What the register is

The register is a public record of what exists or changed in the Hyperliquid ecosystem, filed so a stranger can see the observation later.

It exists so ecosystem change does not live as a private note.

It is not a to-do list, an assignment, or a hand-off. The register only records.

---

## Status vocabulary

Use only these statuses on a register entry. Do not invent a parallel set.

| Status | Meaning |
|--------|---------|
| `observed` | Something exists or happened. Source attached. Not judged against a corpus page. |
| `changed` | A Rank 1–3 source changed on a point that can be cited. |
| `affects-page` | This observation means a named corpus page is stale or incomplete under standing doctrine. |
| `noted` | Filed. No further register action on this entry. |

`affects-page` names the page and the change. It does not start rewrite work by itself.

Do not use `todo`, `assigned`, `blocked`, or another project's status words.

---

## Filing rule

One entry per observation. Do not bundle unrelated events.

Every entry includes:

| Field | Rule |
|-------|------|
| `id` | Stable local id (`R-HLKB-NNN`). Do not reuse. |
| `seen` | Date the observation was filed. |
| `as-of` | Date the cited source was checked. |
| `url` | Source URL. Required. |
| `rank` | Rank class from `SOURCE-RANK.md`, plus `secondary` / `community` tag when not Rank 1–3. |
| `status` | One word from the vocabulary above. |
| `what` | What exists or what changed, in stranger voice. One short block. |
| `pages` | Corpus page paths this may affect, or `none`. |

Live entries go in `register/` on this repository. This file is the rule, not an entry.

An unofficial mention with no URL is not an entry. Rank 4–5 may be filed if tagged. They still do not establish a fact on an accepted page.

Do not file private context.

---

## What the register must not do

- Create work from an observation.
- Assign work to anyone.
- Rewrite an accepted page from the observation alone.
- Hide an observation after the register exists.

If an observation implies a page is stale, mark `affects-page` and stop. Re-check and rewrite only when that work is separately named.
