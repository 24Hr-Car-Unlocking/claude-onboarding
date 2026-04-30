# Use case 1 — Building features

The end-to-end loop, from idea to merged PR.

---

## Step 1 — Write the spec

```bash
cd D:/repos/phoenix-workspace/phoenix-docs
cp templates/feature-template.md specs/plans/SPEC-042-customer-history.md
code specs/plans/SPEC-042-customer-history.md
```

Fill in: problem, requirements, **non-goals**, design, edge cases, acceptance criteria.

Status starts as `draft`. Move to `ready` when you're done writing.

Commit the spec on its own branch:
```bash
git checkout -b docs/spec-042-customer-history
git add specs/plans/SPEC-042-customer-history.md
git commit -m "docs(SPEC-042): add customer history spec"
git push
```

---

## Step 2 — Create a feature branch in the right repo

```bash
cd D:/repos/phoenix-workspace/phoenix-ui
git checkout main
git pull
git checkout -b feature/customer-history
```

Branch naming: `feature/short-description` — slash required, lowercase with dashes.

> Reminder: Claude does **not** create branches. You do. Claude verifies it's on the right branch before making changes.

---

## Step 3 — Prompt Claude (the canonical pattern)

Drop this into Claude:

```
## Task
Implement SPEC-042: Customer History.

## Context
Read these files first:
1. phoenix-docs/documentation/agents/phoenix-ui.md
2. phoenix-docs/specs/plans/SPEC-042-customer-history.md

## Rules
- Follow TDD: write a failing test first
- Add REQ-ID comments referencing the spec for traceability
- Implement in small atomic steps — commit-worthy chunks
- Do not commit or push without asking
- Use plan mode first; show me the plan before implementing
```

---

## Step 4 — The TDD prompt

After Claude returns its plan, before you approve:

> *"This plan looks great! Please update the plan to follow our standard TDD best practices."*

Claude reorders the work into **RED → GREEN → REFACTOR** cycles:

- **RED** — write a failing test
- **GREEN** — minimal code to make it pass
- **REFACTOR** — clean up while tests stay green

Tests get written *alongside* code, not after. This catches misunderstandings early.

---

## Step 5 — Implement, review, commit per chunk

For each step in the plan:

1. Claude implements (you watch)
2. Claude shows the diff
3. **You read the diff**
4. Claude runs the tests, reports results
5. You approve → Claude drafts a conventional commit message
6. You approve the message → `git commit`
7. Move to next step

Don't batch 10 steps before reviewing. Review after each one.

---

## Step 6 — Update spec status as you go

When implementation starts:
```yaml
status: in-progress
```

When code is done, tests pass, PR is open:
```yaml
status: review-pending
```

When PR is **merged AND deployed to production**:
```yaml
status: complete
```

> Never skip `review-pending`. "Complete" is reserved for deployed code.

---

## Step 7 — Open the PR

```
You: Open a PR for this branch. Title in conventional commits 
     format. Body should summarize the spec, link to 
     phoenix-docs/specs/plans/SPEC-042-..., and list the 
     acceptance criteria with check marks.
```

Claude uses `gh pr create` to do this. PR title example:
```
feat(SPEC-042): customer history view in phoenix-ui
```

You merge with **squash merge** to keep `main` history clean.

Note:
Squash merge collapses all your atomic commits into one clean commit on main. Your messy work-in-progress history stays on the feature branch (which you delete after merging). Main stays readable.
