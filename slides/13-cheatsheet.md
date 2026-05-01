# Cheatsheet

Print this slide. Pin this slide.

----

## Branch prefixes

`feature/` · `bug/` · `hotfix/` · `chore/` · `docs/`

## Commit types

`feat` · `fix` · `docs` · `refactor` · `test` · `chore`

Format: `type(SPEC-NNN): description`

## Spec status flow

`draft` → `ready` → `in-progress` → `review-pending` → `complete`

> "Complete" means **deployed to production**, not "code is done."

----

## The 5 prompts you'll use most

**Session start:**
```
Read phoenix-docs/documentation/agents/[repo].md and 
phoenix-docs/documentation/development-standards.md. 
Confirm when ready.
```

**Implement a spec:**
```
Implement phoenix-docs/specs/active/SPEC-NNN.md. Read the 
agent brief first. Plan mode first. Do not commit without 
asking.
```

**Get a plan:**
```
Before implementing, explain your plan. What files will 
you modify? What tests will you write?
```

**Apply TDD structure:**
```
This plan looks great! Please update the plan to follow 
our standard TDD best practices.
```

**Course correct:**
```
Stop. That approach won't work because [reason]. Instead, 
[alternative approach].
```

----

## Things you must NEVER let Claude do without asking

- ❌ `git commit`
- ❌ `git push`
- ❌ `git push --force` *(rarely; never to main)*
- ❌ Delete files outside the working scope
- ❌ Run database migrations
- ❌ Modify CI/CD config without explanation
- ❌ Touch `main` directly
- ❌ Mark a spec `complete` before deploy

If in doubt, **ask Claude to show you what it's about to do, before it does it.**

----

## Where things live in `phoenix-docs`

```
phoenix-docs/
├── templates/              ← copy from here
├── specs/
│   ├── active/             ← in-flight specs (features, bugs, audits)
│   ├── plans/              ← long-horizon multi-phase plans
│   └── adrs/               ← permanent architecture decisions
└── documentation/
    ├── development-standards.md  ← "How We Work"
    ├── agents/             ← cross-repo briefs Claude reads first
    ├── repos/              ← detailed human-facing repo docs
    ├── guides/             ← system-overview, devops
    └── backend/            ← Phoenix API flows & feature deep-dives
```

----

## The protocol in 7 lines

1. **Spec first** — every non-trivial change
2. **Plan mode first** — every implementation
3. **TDD always** — RED → GREEN → REFACTOR
4. **Atomic commits** — one logical change each
5. **Conventional format** — commits, branches, PRs
6. **Review every diff** — no exceptions
7. **`complete` means deployed** — `review-pending` until then

----

## Final word

You don't need to be a developer.

You need to be a **disciplined director** of one.

The protocol is the discipline. Trust it, and you'll ship code your customers can rely on.

<br>

**Now go build.** 🔧

Note:
The single biggest predictor of vibe-coding success is whether you stick to the protocol on the day you don't feel like it. The whole point of having a written protocol is so willpower isn't required — you just follow the steps. Good luck, Robert.
