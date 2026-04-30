# Use case 5 — Audits & reports

Read-only Claude sessions that produce **markdown reports** you can act on later. The output of an audit is a file, not code.

---

## Where audits live

```
phoenix-docs/specs/audits/AUDIT-YYYY-MM-DD-topic.md
```

Examples:
- `AUDIT-2026-04-30-twilio-usage.md`
- `AUDIT-2026-05-15-dependency-cves.md`
- `AUDIT-2026-06-01-dead-code-customer-app.md`

Date-prefix lets you scan history. Each audit is its own commit on a `docs/` branch.

---

## Audit 1 — Security scan

```
Read every file in phoenix and phoenix-ui. Audit for OWASP 
Top 10 issues:
1. Injection (SQL, command, etc.)
2. Broken authentication
3. Sensitive data exposure
4. XML / XXE
5. Broken access control
6. Security misconfiguration
7. XSS
8. Insecure deserialization
9. Components with known vulnerabilities
10. Insufficient logging

Output a markdown report to 
phoenix-docs/specs/audits/AUDIT-2026-04-30-security.md with:
- Severity (Critical/High/Medium/Low)
- File:line reference
- Description
- Recommendation
- Effort to fix (S/M/L)

Do not edit any code.
```

---

## Audit 2 — Dependency health

```
For phoenix and phoenix-ui:
- List every dependency with its current version
- Flag any with known CVEs
- Flag any unmaintained (no commits in >12 months)
- Flag any with major-version updates available
- Estimate breaking-change risk for each upgrade

Output to phoenix-docs/specs/audits/AUDIT-2026-04-30-deps.md.
```

---

## Audit 3 — Dead code

```
Scan customer-app for:
- Exported functions/components never imported elsewhere
- Files unreferenced by any import statement
- TODO / FIXME / HACK comments older than 6 months (use git blame)
- Commented-out code blocks larger than 5 lines

Output to phoenix-docs/specs/audits/AUDIT-2026-04-30-deadcode-customer-app.md
with file:line references.
```

---

## Audit 4 — Test coverage gap

```
For phoenix:
- List every public function in src/services/
- For each, identify whether it has unit test coverage
- Group by: covered / partially covered / uncovered
- Prioritize by criticality (anything in the unlock flow is critical)

Output a markdown table with file:line and coverage status.
```

---

## Audit 5 — Convention compliance

```
Read phoenix-ui/CLAUDE.md and phoenix-docs/documentation/development-standards.md.

Then scan phoenix-ui for files that violate the conventions:
- Naming
- File structure
- Import order
- Test placement

For each violation, list file:line and the rule violated.
```

---

## The audit prompt template

Reusable structure for any audit:

```
TASK: Audit [scope] for [criteria]

CONSTRAINTS:
- Read-only — do not edit any code
- Output as markdown to phoenix-docs/specs/audits/AUDIT-{date}-{topic}.md
- Include severity, file:line, description, recommendation
- Sort by severity (highest first)
- End with a summary count by severity

DO NOT:
- Implement fixes
- Modify any files outside the audit report itself
```

Note:
The discipline of putting audit results in a file (not just chat) is what makes them useful. Chat scrolls away. A committed markdown report is something you can re-open in 3 months, link from a PR, or hand to a contractor.
