# Claude Onboarding Deck — Robert Ramirez

A reveal.js presentation that teaches you how to ship production-grade software with Claude Code across the Phoenix workspace.

## Open the deck

The slides are loaded from separate `.md` files, which browsers block when you double-click `index.html` (the `file://` protocol). You need a tiny local web server. Pick one:

### Option A — Node (if you have it)

```bash
cd D:\repos\phoenix-workspace\claude-onboarding
npx serve .
```

Then open the URL it prints (usually `http://localhost:3000`).

### Option B — Python (every Windows install ships with one if you've used it)

```bash
cd D:\repos\phoenix-workspace\claude-onboarding
python -m http.server 8000
```

Then open `http://localhost:8000`.

### Option C — VS Code Live Server extension

Install the **Live Server** extension, right-click `index.html`, "Open with Live Server".

## Navigation

| Key           | Action                             |
| ------------- | ---------------------------------- |
| `→` / `Space` | Next slide                         |
| `←`           | Previous slide                     |
| `↓` / `↑`     | Vertical sub-slides (when present) |
| `Esc`         | Slide overview                     |
| `S`           | Speaker notes window               |
| `F`           | Fullscreen                         |
| `?`           | Keyboard shortcuts                 |

## Edit slides later

Each slide section is a separate file in `slides/`. Edit the markdown, refresh the browser. No build step.

## Print to PDF

Open `http://localhost:3000/?print-pdf` then `Ctrl+P` → Save as PDF.
