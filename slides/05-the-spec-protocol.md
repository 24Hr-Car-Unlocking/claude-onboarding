# Document Driven Development (DDD)

The Phoenix Platform's name for the spec-first protocol.

> _"Documentation is the **first** artifact of every change, not an afterthought. Specs are written before code, reviewed like code, and archived for reference."_
> — `phoenix-docs/documentation/development-standards.md`

The single behavior change that separates production code from slop:

> **Never let Claude write code without an active spec.**
> Either you write it, or Claude drafts it and you approve it.

Note:
A spec is a 1-2 page document that answers: what are we building, why, what does "done" look like, and what are the edge cases. It takes 15-30 minutes to write and saves hours of bad implementation.

---

## The loop

```
SPEC  →  PLAN MODE  →  IMPLEMENTATION  →  REVIEW  →  PR  →  MERGE  →  DEPLOY
  ↑                                                                        │
  └─────── update status as work progresses ──────────────────────────────┘
```

Every piece of work that isn't a typo or dependency bump runs through this loop.

---

## Where specs live

In `phoenix-docs/specs/active/` — never in the code repo itself.

Naming: `SPEC-NNN-short-name.md` where NNN is a 3-digit number you increment manually (e.g. `SPEC-001-twilio-spend-audit.md`).

Templates to copy from `phoenix-docs/templates/`:

| Template                  | When to use                                         |
| ------------------------- | --------------------------------------------------- |
| `feature-template.md`     | New feature, new endpoint, new screen, **or audit** |
| `bug-template.md`         | Something is broken                                 |
| `adr-template.md`         | A permanent architecture decision                   |
| `agent-brief-template.md` | Setting up a new repo                               |

> ADRs go in `specs/adrs/` and are **never** archived or deleted.

---

## The canonical spec format

Every spec is a **single `.md` file** with YAML frontmatter and four canonical H2 sections:

```markdown
---
id: SPEC-NNN
title: "Short descriptive title"
status: draft
created: YYYY-MM-DD
author: "Your Name"
reviewers: []
affected_repos: [phoenix]
---

# SPEC-NNN — Title

## Overview

[2-3 sentences: what problem, why now, what happens if we don't]

## Requirements

### Must have

### Nice to have

### Non-goals

## Design

[Technical approach: DB changes, endpoints, UI changes,
cross-repo impact, edge cases]

## Tasks

- [ ] First atomic task
- [ ] Second atomic task
```

Don't create multi-file spec folders. One spec = one file.

---

## Spec status lifecycle

Update the `status` field in the frontmatter as work progresses.

| Status           | Meaning                                     |
| ---------------- | ------------------------------------------- |
| `draft`          | Being written, not ready for implementation |
| `ready`          | Spec complete, ready to implement           |
| `in-progress`    | Currently being implemented                 |
| `review-pending` | Code complete, PR awaiting review           |
| `complete`       | PR merged **and deployed to production**    |
| `deprecated`     | No longer pursuing or superseded            |

> ⚠️ **Critical:** "Complete" means deployed. Not merged. Not "code is done." **Deployed.** Use `review-pending` when the PR is open.

---

## Letting Claude help write the spec

You don't have to write specs from scratch. Pattern:

```
I want to add [rough description] to phoenix-ui.
Read phoenix-docs/templates/feature-template.md and
phoenix-docs/documentation/agents/phoenix-ui.md.

Ask me 5-8 clarifying questions, then draft a spec
to phoenix-docs/specs/active/SPEC-NNN-name.md.
```

Claude asks → you answer → Claude drafts → you edit and ship.

Note:
The clarifying-questions step is essential. Without it, Claude fills in plausible-but-wrong assumptions and you get a spec that's confidently incorrect. Always force the question round.
