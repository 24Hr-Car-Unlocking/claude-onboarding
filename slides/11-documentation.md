# Use case 6 — Writing & maintaining documentation

Three tiers of docs, three different audiences, three different update cadences.

---

## The three tiers

| Tier | Location | Audience | When updated |
|------|----------|----------|--------------|
| **Agent briefs** | `phoenix-docs/documentation/agents/*.md` | Claude (cross-repo work) | When inter-service contracts change |
| **Repo docs** | `phoenix-docs/documentation/repos/*.md` | Humans onboarding | When architecture or commands change |
| **Guides** | `phoenix-docs/documentation/guides/*.md` | Everyone (system-wide topics) | When a system-wide practice changes |

Plus: each repo has its own `CLAUDE.md` for repo-specific rules (commands, file structure, conventions).

---

## Tier 1 — Agent briefs

**Audience:** Claude doing cross-repo work.
**Length:** Short. 1-2 pages.
**Content:** What the service owns, depends on, exposes — no repo internals.

From the template:

- **Role in the system** — 2-3 sentences
- **Owns** — what data/concepts is this service the source of truth for?
- **Depends on** — table: service → how → details
- **Depended on by** — table: who calls this → how → details
- **API contract** — key endpoints other services rely on
- **Shared data models** — types/payloads that cross repo boundaries
- **Cross-repo patterns** — conventions that matter across repos
- **When working on this repo alongside others** — practical notes

> Agent briefs do **not** include: commands, project structure, env vars, testing. Those go in the repo's own `CLAUDE.md`.

---

## Tier 2 — Repo docs

**Audience:** A human (you, a contractor, a future developer) starting in this repo.
**Length:** As long as needed.
**Content:** Architecture, commands, concepts, env variables, testing approach, common gotchas.

Currently exists in `phoenix-docs/documentation/repos/` for: `phoenix-ui`, `phoenix`, `technician-app`. To be extended.

---

## Tier 3 — Guides

**Audience:** Everyone working anywhere.
**Length:** Medium.
**Content:** System-wide topics that span repos.

Common guides to write over time:
- `system-overview.md` — how the 6 repos fit together
- `local-development.md` — environment setup
- `testing.md` — testing strategy by layer
- `authentication.md` — auth flows
- `deployment.md` — deploy process
- `database-migrations.md` — migration workflow
- `troubleshooting.md` — common issues

---

## The "review against code" prompt

Documentation rots. Use Claude to detect rot:

```
Review phoenix-docs/documentation/repos/phoenix-ui.md 
against the actual phoenix-ui codebase. List every 
inaccuracy you find:
- Commands that no longer work
- Paths that have been moved or deleted
- Concepts that have been renamed
- Sections that describe deprecated behavior

Do not edit anything — review only. Output a markdown 
report I can use to drive an update.
```

Run this monthly per major doc.

---

## The "update after this PR" pattern

Whenever a PR changes architecture, the *same PR* should update the docs.

End-of-feature prompt:

```
The PR for SPEC-042 is about to merge. Update:
1. phoenix-docs/documentation/agents/phoenix-ui.md if 
   any cross-repo interface changed
2. phoenix-docs/documentation/repos/phoenix-ui.md if 
   architecture, commands, or env vars changed  
3. phoenix-ui/CLAUDE.md if any repo-specific convention 
   changed

Show me the diffs. Do not commit yet.
```

Note:
Treating doc updates as part of the PR (not as a separate "we'll get to it later") is the only way docs stay accurate. The minute it becomes optional, it stops happening.
