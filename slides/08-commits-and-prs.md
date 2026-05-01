# Use case 3 — Commits and PRs

Convention is everything. Following it makes your history readable, your release notes generate themselves, and your PR descriptions write themselves.

---

## Conventional Commits

Format:
```
type(scope): description
```

**Types:** `feat`, `fix`, `docs`, `refactor`, `test`, `chore`

When implementing a spec, put the SPEC-ID in the scope:
```
feat(SPEC-042): add customer history view
fix(SPEC-051): handle empty VIN in unlock flow
docs(SPEC-042): update API docs for new endpoint
refactor(SPEC-073): extract auth middleware
test(SPEC-042): add edge case tests for empty input
chore: bump axios to 1.7.4
```

---

## Branch naming

`{type}/short-description` — slash is required, lowercase with dashes.

| Prefix | Use for |
|--------|---------|
| `feature/` | New features |
| `bug/` | Bug fixes |
| `hotfix/` | Urgent production fixes |
| `chore/` | Maintenance, dependencies |
| `docs/` | Documentation-only updates |

Examples: `feature/customer-history`, `bug/empty-vin-crash`, `hotfix/twilio-timeout`, `chore/bump-deps-2026-04`.

---

## The "atomic commit" rule

**One logical change per commit.** Claude will want to batch — you push back.

❌ Bad:
```
feat: add customer history, fix unrelated bug, refactor auth
```

✅ Good:
```
feat(SPEC-042): add customer history endpoint
test(SPEC-042): add tests for customer history
docs(SPEC-042): document customer history endpoint
```

If you can describe what changed in a single sentence without the word "and", it's atomic.

---

## The commit prompt

```
You: Stage the changes and draft a conventional commit message. 
     Show me the staged diff and the proposed message. Do not 
     run git commit yet.
```

Claude shows:
```
Staged diff:
  phoenix-ui/src/views/CustomerHistory.tsx (new file, 142 lines)
  phoenix-ui/src/api/customers.ts (modified, +12 -0)

Proposed message:
  feat(SPEC-042): add customer history view component
```

You read both. If good → "yes commit". If not → push back with specifics.

---

## The PR prompt

After all commits are pushed:

```
You: Open a PR for this branch.
     - Title: conventional commits format
     - Body: 3-section structure
       1. Summary (what + why, link to spec)
       2. Changes (bulleted list)
       3. Acceptance criteria (checked off from spec)
     - Mark draft if any criteria are still unchecked
```

Claude runs `gh pr create` with the drafted title and body. You review, then "ready for review" when satisfied.

---

## PR review etiquette

- **Squash merge**, never plain merge — keeps `main` clean
- **Never force-push** to `main` or shared branches
- If reviewers request changes, the spec status moves back to `in-progress`. Add their feedback to the **Reviewer Notes** section of the spec
- After approval, merge → spec stays `review-pending`
- After deploy → spec moves to `complete`

Note:
The "Reviewer Notes" section in the spec is your changelog of feedback rounds. It's invaluable when you come back in 3 months and wonder why the API ended up shaped a certain way.
