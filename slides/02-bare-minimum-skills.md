# Bare-minimum dev skills

You are not becoming a developer.

You are becoming the **product owner** of a developer (Claude) — and that role requires a small but non-zero amount of vocabulary and tooling fluency.

The next slides cover everything you need. Nothing more.

Note:
Skip none of these. Each one will be invoked in the daily workflow. The good news: you're not learning to *write* code, only to *direct* it. That dramatically shrinks the surface area.

----

## Skill 1 — The terminal

A "terminal" is a text window where you type commands instead of clicking. On Windows you have two:

- **PowerShell** — built in, ships with Windows
- **Git Bash** — comes with Git for Windows, uses Unix-style commands

We'll use **Git Bash** for everything in this deck because it matches what 99% of online tutorials assume.

```bash
pwd          # "print working directory" — where am I?
ls           # list files in this folder
cd somefolder    # change into a folder
cd ..        # go up one folder
cd D:/repos/phoenix-workspace   # jump anywhere by absolute path
```

Note:
On Windows, install Git for Windows from git-scm.com. It bundles Git Bash. To open it, right-click any folder in File Explorer and pick "Git Bash Here". That single trick saves you 80% of the typing.

----

## Skill 2 — Git, the absolute basics

Git tracks every change to every file as a series of snapshots called **commits**. Commits live on **branches**. Branches live in **repositories** (repos).

```bash
git status                    # what has changed?
git pull                      # download latest from GitHub
git checkout -b feature/xyz   # create + switch to a new branch
git add .                     # stage every changed file
git commit -m "feat: add x"   # snapshot the staged files
git push                      # upload to GitHub
git log --oneline -20         # see recent commits
```

That is genuinely 90% of what you'll type. Claude will run most of these for you — but you need to *recognize* them when they happen.

----

## Skill 3 — GitHub

GitHub hosts your repos online. Three concepts to know:

| Term | Meaning |
|------|---------|
| **Repository** | A project — code + history |
| **Branch** | A parallel line of changes that don't affect `main` |
| **Pull Request (PR)** | A formal proposal to merge a branch into `main` |

**The golden rule:** code never goes to `main` directly. It goes to a branch → PR → review → squash merge → `main`.

Note:
Even when you're the only person on the team, treat PRs as the contract. They force a moment of "do I really want to ship this?" Claude will draft the PR title and body for you. You click "merge".

----

## Skill 4 — Reading a diff

A "diff" shows what changed between two versions of a file.

```diff
function unlockCar(vin) {
-  return api.post('/unlock', { vin });
+  if (!vin) throw new Error('vin required');
+  return api.post('/unlock', { vin: vin.toUpperCase() });
 }
```

- Red lines (`-`) were removed
- Green lines (`+`) were added
- Unchanged lines have no marker

When reviewing Claude's work, read every diff. Look for:
- Lines you don't understand → ask Claude to explain
- Files changed that shouldn't have been → push back
- Hardcoded secrets, API keys, passwords → **stop immediately**

----

## Skill 5 — VS Code

[VS Code](https://code.visualstudio.com) is the editor most vibe coders use. It's free.

**Install these extensions** (Ctrl+Shift+X in VS Code):

- **GitLens** — see who changed every line, hover for history
- **Error Lens** — show errors inline next to the code
- **Markdown All in One** — for editing specs

Open a repo with `code D:/repos/phoenix-workspace/phoenix` from any terminal.

The integrated terminal (Ctrl+`) is your friend — runs Git Bash and Claude Code right in the editor.

----

## Skill 6 — Claude Code

You already have both:

- **Claude Code (CLI)** — run `claude` in any repo's terminal
- **Claude Code (Desktop)** — the standalone app

**When to use which:**

| Use the desktop app when... | Use the CLI when... |
|----------------------------|---------------------|
| You're starting a long session and want a clean window | You're already in VS Code's terminal |
| You're doing audits / read-only research | You're mid-flow on a feature and want to stay in the IDE |
| You want to share screenshots easily | You want everything in one tab |

Both connect to the same Claude. Pick whichever feels right that day.

Note:
If you're new, default to the desktop app for the first week. The CLI is faster once your muscle memory builds, but the desktop app gives you visual confirmation of every tool call which is reassuring early on.

----

## Skill 7 — The "working directory" concept

Every Claude session has a **working directory** — the folder Claude can see.

- If your task touches **one repo**, point Claude at that repo: `D:/repos/phoenix-workspace/phoenix-ui`
- If your task touches **multiple repos**, point Claude at the workspace root: `D:/repos/phoenix-workspace`
- Claude can read everything inside but **cannot** see outside the working directory

Pick the smallest directory that contains everything Claude needs. Smaller scope = better focus.
