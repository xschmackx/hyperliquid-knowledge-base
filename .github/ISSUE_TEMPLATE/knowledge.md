---
name: Knowledge Issue
about: One Taskmap item. TL writes from the OS Taskmap. Chat is not the contract.
title: "{{TASK_ID}} — {{SHORT_TITLE}}"
labels: []
---

# {{TASK_ID}} — {{SHORT_TITLE}}

**Repo:** https://github.com/xschmackx/hyperliquid-knowledge-base  
**Kind:** knowledge  
**Taskmap ID:** {{ID}}  
**Status:** DRAFT → TL-COMPLETE → RE-ANNOTATED → TE-READY → TE-DONE → IA-REVIEW → IA-PASS (closed) | IA-FAIL (open)  
**Opened by:** TL  
**Taskmap source:** https://github.com/xschmackx/hlkb-oversight TASKMAP.md — {{ID}}  
**Human decision required before TE:** NO

---

## 0. Lane contract (do not delete)

1. **TL** writes goal, hard constraints, scope, out-of-scope, acceptance, gates **from the OS Taskmap**. Chat is not the contract. TL opens or updates this Issue only after a Human packet that names the Taskmap ID.
2. **RE** adds evidence only. RE does not rewrite constraints or acceptance. Production three do not browse corpus `notes/`.
3. **TE** executes only when this Issue is decision-complete and evidence-annotated. Proof shape: knowledge ISSUE-TE.
4. **IA** reviews this Issue only → PASS or FAIL. PASS closes. FAIL stays open.
5. Conflict with the Taskmap → return to OS through the Human.

**Kind pack:** `kinds/knowledge/`.

---

## 1. TL — Decision artifact (from OS Taskmap)

### Goal
{{Copy from the Taskmap item.}}

### Why now
{{One paragraph.}}

### Hard constraints
- Standalone. No other project's terms.
- Official sources first. Unknown stays unknown.
- Stranger-usable voice.
- Page-level `as-of` + source URLs.
- Do not implement later Taskmap IDs on this Issue.

### Scope — In
- {{from Taskmap / shelf}}

### Scope — Out
- Implementation of later Taskmap IDs
- {{from Taskmap / shelf}}

### Acceptance criteria
- [ ] Accepted page or written gap at the path named in Section 1
- [ ] Every accepted page has `as-of` + URLs
- [ ] Evidence attached on this Issue
- [ ] IA PASS recorded below

### Gates
- **Start TE:** TL-COMPLETE + RE-ANNOTATED
- **Close Issue:** IA PASS and close. FAIL stays open.
- **Rollback:** revert the corpus commit named on the Issue

### TL sign-off
- Date:
- TL-COMPLETE: YES / NO
- Taskmap ID matched: YES / NO
- Human accept to proceed: N/A

---

## 2. RE — Evidence only

> RE fills this section. Do not edit Section 1.

### Sources
- Official / canonical:
- Repo / prior Issues:
- Secondary (flag confidence):
- Working-note citations:

### What TE must know
- Gotchas:
- Exact pointers:
- Conflicts with Section 1 hard constraints? **NO / YES → return to TL**

### RE sign-off
- Date:
- RE-ANNOTATED: YES / NO
- Confidence on evidence: HIGH / MEDIUM / LOW

---

## 3. TE — Execution record

### What was written or changed
- Pages added (`pages/…`):
- Pages revised:
- Notes left in `notes/` (not canon):
- Source-index rows touched:

### Provenance
- As-of date on each accepted page:
- Official sources used:
- Secondary sources used (flag confidence):
- Known unknowns left on the page:

### TE sign-off
- Date:
- TE-DONE: YES / NO
- Residuals:

---

## 4. IA — Independent assessment

```
Verdict: PASS | FAIL
Date:
Issue:
AC met:
AC unmet:
Constraint breaches:
Required fix (FAIL only):
Closed on PASS?: YES / NO
Notes:
```

### Checks
- [ ] Scope respected
- [ ] Hard constraints intact
- [ ] Acceptance criteria met or explicitly deferred
- [ ] Every accepted page has an as-of date
- [ ] Official sources listed before secondary
- [ ] Unknowns remain unknown
- [ ] Working notes were not cited as accepted pages
- [ ] Voice is usable by a stranger
