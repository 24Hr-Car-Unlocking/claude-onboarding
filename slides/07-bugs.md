# Use case 2 — Fixing bugs

Same protocol as features, with one critical twist: **failing test first, fix second.**

---

## Step 1 — Write the bug spec

```bash
cd D:/repos/phoenix-workspace/phoenix-docs
cp templates/bug-template.md specs/plans/SPEC-051-empty-vin-crash.md
```

The bug template forces you to fill in:

- **What's happening** — actual behavior
- **What should happen** — expected behavior
- **Steps to reproduce** — exact sequence
- **Environment** — service, version/commit, dev/staging/prod, browser
- **Where to look** — entry point file, related files, error logs
- **Severity** — P0 (critical) / P1 / P2 / P3

Severity goes in the frontmatter. P0 means production is down. P3 means cosmetic.

---

## Step 2 — Prompt Claude

```
## Task
Fix SPEC-051: Empty VIN crashes unlock flow.

## Context
1. phoenix-docs/documentation/agents/phoenix.md
2. phoenix-docs/specs/plans/SPEC-051-empty-vin-crash.md

## Rules
- Write a failing test that reproduces the bug FIRST
- Then implement the fix
- Verify the test passes
- Then check for similar patterns elsewhere in the codebase
- Update documentation if behavior changed
- Do not commit or push without asking
```

---

## Step 3 — The bug-fix checklist

The bug template ends with this checklist. Don't skip any item:

- [ ] Write failing test that reproduces the bug
- [ ] Implement fix
- [ ] Verify test passes
- [ ] **Check for similar patterns elsewhere in codebase**
- [ ] Update documentation if behavior changed

> The "similar patterns elsewhere" step is the difference between a fix and a *complete* fix. Bugs travel in families.

Note:
If you found a null-check missing in one place, there are usually 2-3 more places with the same gap. Always have Claude grep the codebase for sibling cases after the test passes.

---

## Step 4 — Branch & commit naming

Branch:
```bash
git checkout -b bug/empty-vin-crash
```

Or for urgent production fixes:
```bash
git checkout -b hotfix/empty-vin-crash
```

Commit:
```
fix(SPEC-051): handle empty VIN in unlock flow
```

PR title: same as commit.

---

## Step 5 — Root cause section

The bug template has a **Root Cause** section that's empty when you start. Fill it in *during investigation*, before you write the fix:

> *"What's actually wrong and why?"*

This forces you (or Claude) to articulate the underlying problem rather than slap a Band-Aid on a symptom. If the root cause is one sentence and obvious, fine. If it's three paragraphs, you've probably found a real architectural issue worth flagging.

Note:
The "fix" section of the spec might say "added null check on line 42." The "root cause" section says "the API endpoint trusts client-provided fields without validation, which is true throughout the unlock flow." The latter tells you whether you need a follow-up ADR.
