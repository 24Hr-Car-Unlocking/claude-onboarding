# Workspace setup

Your workspace is `D:\repos\phoenix-workspace\` — every repo lives as a sibling folder inside it.

```
D:\repos\phoenix-workspace\
├── phoenix\           # backend / API
├── phoenix-ui\        # frontend web app
├── phoenix-docs\      # 🌟 the meta-docs repo (specs, ADRs, agent briefs)
├── phoenix-press\     # marketing / WordPress site
├── customer-app\      # mobile app for customers
└── technician-app\    # mobile app for technicians
```

Note:
This sibling layout is critical. Claude can see across all repos when launched from the workspace root, which is essential for cross-repo work.

---

## Cloning the repos

If a repo isn't already on disk, clone it. Open Git Bash in `D:\repos\phoenix-workspace` and run:

```bash
git clone https://github.com/24Hr-Car-Unlocking/phoenix
git clone https://github.com/24Hr-Car-Unlocking/phoenix-ui
git clone https://github.com/24Hr-Car-Unlocking/phoenix-docs
git clone https://github.com/24Hr-Car-Unlocking/phoenix-press
git clone https://github.com/24Hr-Car-Unlocking/customer-app
git clone https://github.com/24Hr-Car-Unlocking/technician-app
```

Already cloned? Just `git pull` inside each one to update.

---

## Meet `phoenix-docs` — the brain of the operation

`phoenix-docs` is **not** documentation for the `phoenix` web app. It is the **central docs repo for every project in the workspace** — the home of **Document Driven Development (DDD)**.

| Folder                                   | What lives there                                                    |
| ---------------------------------------- | ------------------------------------------------------------------- |
| `templates/`                             | Canonical templates — feature, bug, ADR, agent-brief. Never modify. |
| `specs/active/`                          | In-flight specs (`SPEC-NNN-name.md`) — features, bugs, audits       |
| `specs/plans/`                           | Long-horizon multi-phase plans                                      |
| `specs/adrs/`                            | Architecture Decision Records (permanent — never deleted)           |
| `documentation/development-standards.md` | "How We Work" — the source of truth for conventions                 |
| `documentation/agents/`                  | Cross-repo briefs Claude reads first                                |
| `documentation/repos/`                   | Detailed human-facing docs per repo                                 |
| `documentation/guides/`                  | System-wide topics (system-overview, devops)                        |
| `documentation/backend/`                 | Phoenix API deep-dives — `flows/` and `features/`                   |

> Currently `documentation/repos/` and `documentation/agents/` cover `phoenix-ui`, `phoenix`, and `technician-app`. Coverage will extend to the other repos over time.

Note:
The Phoenix Platform per the dev-standards doc = 4 core repos (phoenix, phoenix-ui, technician-app, phoenix-docs). phoenix-press and customer-app are auxiliary. You'll do most of your work in the 4 core repos.

Note:
Every workflow in this deck flows through phoenix-docs. Specs are written there, ADRs live there, agent briefs sit there. Treat this repo as the operating manual for the whole platform.

---

## Per-repo `CLAUDE.md` files

Every repo should have a `CLAUDE.md` file at its root. Claude Code automatically reads it when launched from that folder.

It contains repo-specific rules:

- Commands to run tests
- Commands to start the dev server
- File structure conventions
- Common gotchas

If a repo doesn't have one, run this once inside the repo:

```bash
claude
> /init
```

The `/init` slash command makes Claude scan the repo and draft a `CLAUDE.md`. **Review it before committing** — never blindly accept generated docs.

---

## Workspace-level `CLAUDE.md`

There's also a `CLAUDE.md` at `D:\repos\phoenix-workspace\` that covers cross-repo behavior. Claude reads this whenever you launch from the workspace root.

Use it to encode rules like:

- "Always check `phoenix-docs/specs/active/` for an active spec before writing code"
- "Always read the agent brief in `phoenix-docs/documentation/agents/` first"
- "Never commit without asking"

Note:
Think of CLAUDE.md files as standing instructions. They're loaded into every session for free, so anything you'd otherwise type at the start of every chat belongs in CLAUDE.md.
