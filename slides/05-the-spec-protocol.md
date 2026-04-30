# The Spec-First Protocol

The single behavior change that separates production code from slop.

> **Never let Claude write code without a written spec.**
> Either you write it, or Claude writes a draft and you approve it.

Note:
A spec is a 1-2 page document that answers: what are we building, why, what does "done" look like, and what are the edge cases. It takes 15-30 minutes to write and saves hours of bad implementation.

---

## The loop

```
SPEC  →  PLAN MODE  →  TDD IMPLEMENTATION  →  REVIEW  →  PR  →  MERGE
  ↑                                                                   │
  └─────── update status as work progresses ─────────────────────────┘
```

Every piece of work that isn't a typo fix runs through this loop.

---

## Where specs live

In `phoenix-docs/specs/plans/` — never in the code repo itself.

Naming: `SPEC-XXX-short-name.md` where XXX is a 3-digit number you increment manually (e.g. `SPEC-001-customer-vehicle-history.md`).

Templates to copy from `phoenix-docs/templates/`:

| Template | When to use |
|----------|-------------|
| `feature-template.md` | New feature, new endpoint, new screen |
| `bug-template.md` | Something is broken |
| `adr-template.md` | A permanent architecture decision |
| `agent-brief-template.md` | Setting up a new repo |

---

## Spec status lifecycle

Update the `status:` field in the spec's frontmatter as work progresses.

| Status | Meaning |
|--------|---------|
| `draft` | Being written, not ready for implementation |
| `ready` | Spec complete, ready for implementation |
| `in-progress` | Currently being implemented or revised |
| `review-pending` | Code complete, tests passing, PR open |
| `complete` | PR merged to main and **running in production** |
| `deprecated` | No longer pursuing |

> ⚠️ **Critical:** "Complete" means deployed. Not merged. Not "code is done." **Deployed.** Use `review-pending` when the PR is open.

---

## What a good spec looks like

A feature spec from `feature-template.md` has:

- **Problem** — 2-3 sentences. What user pain? Why now?
- **Requirements** — `WHEN [trigger], the system SHALL [behavior]`
- **Non-goals** — what this explicitly does NOT do *(prevents Claude from gold-plating)*
- **Design** — data model, API, UI, cross-repo impact
- **Edge cases** — empty input? invalid input? service unavailable? concurrent requests?
- **Error handling** — table of error codes → user-facing messages
- **Acceptance criteria** — testable, with inputs and expected outputs
- **Constraints** — must integrate with X, cannot modify Y

The non-goals section is the secret weapon. It's what stops Claude from "helpfully" rewriting your auth system because you asked it to add a button.

---

## Letting Claude help write the spec

You don't have to write specs from scratch. Two-step pattern:

```
You: I want to add [rough description] to phoenix-ui. Read 
     phoenix-docs/templates/feature-template.md and 
     phoenix-docs/documentation/agents/phoenix-ui.md, then 
     ask me 5-8 clarifying questions before drafting a spec.

Claude: [asks questions]

You: [answers]

Claude: [writes a draft spec to phoenix-docs/specs/plans/SPEC-042-...]

You: [edit, push back, ship it]
```

Note:
The clarifying-questions step is essential. Without it, Claude fills in plausible-but-wrong assumptions and you get a spec that's confidently incorrect. Always force the question round.
