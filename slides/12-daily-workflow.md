# Putting it together — a typical day

What a day of vibe coding looks like, start to finish.

----

## Morning — pick a task

You've got a task in mind. First decision: **does it need a spec?**

✅ **Yes, write a spec:**
- New features
- Bug fixes that change behavior
- Significant changes to existing behavior
- Architectural decisions (also gets an ADR)

❌ **No, just do it:**
- Typo fixes
- Dependency bumps
- Minor refactoring with no behavior change
- Adding tests for existing code

----

## Step 1 — Pull latest, branch up

```bash
cd D:/repos/phoenix-workspace/phoenix-ui
git checkout main
git pull
git checkout -b feature/SPEC-042-customer-history
```

----

## Step 2 — Launch Claude in plan mode

```bash
claude
```

Or open the desktop app pointed at the same directory. Toggle to **plan mode** (Shift+Tab).

----

## Step 3 — Hand Claude its briefing

```
Read these in order, then confirm you're ready:
1. phoenix-docs/documentation/development-standards.md
2. phoenix-docs/documentation/agents/phoenix-ui.md
3. phoenix-ui/CLAUDE.md
4. phoenix-docs/specs/active/SPEC-042-customer-history.md
```

Claude reads, confirms. Now you're aligned on the rules and the work.

----

## Step 4 — Get a plan

```
Draft an implementation plan for SPEC-042. Show me which 
files you'll modify, which tests you'll write, and the 
order of operations. Do not implement yet.
```

You read, push back, refine. When happy:

```
This plan looks great! Please update the plan to follow 
our standard TDD best practices.
```

----

## Step 5 — Implement, one chunk at a time

Drop out of plan mode (Shift+Tab → Default). For each plan step:

1. Claude writes test → runs it → confirms RED
2. Claude writes code → runs test → confirms GREEN
3. Claude refactors → runs test → confirms still GREEN
4. **You read the diff**
5. Claude drafts a conventional commit message
6. You approve → `git commit`

Move spec status: `ready` → `in-progress`.

----

## Step 6 — Push & open PR

```
You: Push the branch and open a PR. Title in conventional 
     commits format. Body with summary, changes list, and 
     spec acceptance criteria as a checklist.
```

Move spec status: `in-progress` → `review-pending`.

----

## Step 7 — Review feedback (if any)

If the reviewer (you, a teammate, or another agent) requests changes:

- Spec status: `review-pending` → `in-progress`
- Add feedback to the **Reviewer Notes** section of the spec
- Address the feedback
- Push again
- Status: `in-progress` → `review-pending`

----

## Step 8 — Merge & deploy

- Squash merge the PR
- Watch the deploy
- Once it's running in production: spec status → `complete`
- The completed spec stays in `specs/active/` as a permanent record. Phoenix doesn't archive — the YAML status field is the source of truth.

----

## End of day — quick hygiene

- Push any in-progress branches (don't lose work)
- Commit any in-progress spec edits
- `/clear` your Claude session if it got long — context resets are cheap

Note:
A clean Claude session every morning is one of the highest-leverage habits. Long sessions accumulate noise and Claude starts repeating mistakes. Fresh context = fresh thinking.
