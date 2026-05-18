# Claude Code — the controls

A 5-minute tour of the buttons and modes that matter.

---

## Starting a session

```bash
cd D:/repos/phoenix-workspace/phoenix-ui
claude
```

That's it. Claude is now your pair programmer in this repo.

For cross-repo work:

```bash
cd D:/repos/phoenix-workspace
claude
```

Or just open the desktop app and pick the working directory.

Note:
Always launch from the directory you want Claude to see. Launching from your home folder gives Claude no codebase to work with.

---

## The four permission modes

Toggle with **Shift+Tab** (cycles through them) or via the menu.

| Mode              | What it does                                                | When to use                                            |
| ----------------- | ----------------------------------------------------------- | ------------------------------------------------------ |
| **Plan mode**     | Read-only. Claude researches and proposes a plan. No edits. | Start of every non-trivial task                        |
| **Default**       | Asks before each Edit/Bash                                  | Implementation work where you want to review each step |
| **Accept edits**  | Auto-approves edits, still asks for Bash                    | Fast loops once you trust the plan                     |
| **YOLO / bypass** | Approves everything                                         | Only inside ephemeral worktrees / sandboxes            |

**Default rule:** start in plan mode, drop to default once the plan is approved. Almost never use bypass.

---

## Plan mode is your superpower

In plan mode Claude:

- Reads files and explores the codebase
- Searches for existing patterns
- Drafts a step-by-step plan
- **Cannot edit or run destructive commands**

You read the plan, push back, refine. Once you're happy, Claude exits plan mode and implements.

> 💡 The single highest-leverage habit: **Never let Claude write code without first showing you a plan you've read.**

Note:
Plan mode is the seatbelt of vibe coding. It's the difference between "Claude rewrote half my codebase while I was getting coffee" and "Claude executed exactly what we agreed on."

---

## Slash commands you'll use weekly

| Command    | What it does                                     |
| ---------- | ------------------------------------------------ |
| `/init`    | Generate a CLAUDE.md for the current repo        |
| `/clear`   | Reset the conversation (start fresh)             |
| `/compact` | Compress conversation history to save context    |
| `/review`  | Review the pending changes on the current branch |
| `/help`    | List all available commands                      |

Type `/` in Claude to see the full list. Many more come from plugins.

---

## CLAUDE.md — the standing instructions

Every time you launch Claude in a directory, it auto-reads:

1. The `CLAUDE.md` at the workspace root (if launched there)
2. The `CLAUDE.md` of the repo you're in
3. Your global `~/.claude/CLAUDE.md` (your personal preferences)

Anything you'd otherwise repeat — "always read the agent brief first", "never commit without asking", "we use conventional commits" — belongs in `CLAUDE.md`.

Update CLAUDE.md whenever you catch yourself giving the same instruction twice.

---

## The "ask before committing" rule

This is the single most important standing instruction. Put it in every CLAUDE.md:

```
## Git rules
- Do not commit without explicit approval
- Do not push without explicit approval
- Never force push
- Never commit directly to main
- Branch names follow: {type}/short-description
- Commits follow Conventional Commits format
```

Claude will draft commit messages and run `git add`, but will pause and show you the diff before `git commit`. Always.

Note:
This one rule prevents 90% of "wait what just happened" disasters. Make it muscle memory: when Claude says "ready to commit?" you read the diff before saying yes.
