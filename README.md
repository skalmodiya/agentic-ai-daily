# 🤖 Agentic AI Daily

A beautiful, self-refreshing GitHub Pages site that delivers a **new Agentic AI learning topic every day** — fully automated via GitHub Actions.

🌐 **Live site:** https://skalmodiya.github.io/agentic-ai-daily/

---

## What It Does

- Runs a GitHub Actions workflow **every day at 06:00 UTC**
- Picks today's topic from a library of 15+ deep-dive Agentic AI lessons (cycles continuously)
- Generates a stunning dark-mode responsive `index.html` with:
  - **Core concept** — clear explanation with examples
  - **Design pattern** — step-by-step + code snippet
  - **Did You Know?** — surprising facts about the field
  - **Interactive quiz** — test your knowledge with instant feedback
  - **Further reading** — curated links to papers and docs
  - **Progress tracker** — see how far through the library you are
- Commits the new `index.html` and deploys to **GitHub Pages** automatically

---

## Topics Covered

| # | Topic | Tag |
|---|-------|-----|
| 1 | What Is Agentic AI? | Foundations |
| 2 | Agent Memory Systems | Memory |
| 3 | Tool Use & Function Calling | Tools |
| 4 | Planning & Task Decomposition | Planning |
| 5 | Multi-Agent Systems | Architecture |
| 6 | Retrieval-Augmented Generation (RAG) | Knowledge |
| 7 | Agent Evaluation & Benchmarking | Quality |
| 8 | Human-in-the-Loop Design | Safety |
| 9 | Prompt Engineering for Agents | Prompting |
| 10 | LangChain & LangGraph | Frameworks |
| 11 | Model Context Protocol (MCP) | Protocols |
| 12 | Agent Security & Prompt Injection | Security |
| 13 | Autonomous Coding Agents | Applications |
| 14 | Structured Outputs & Reliability | Reliability |
| 15 | Agent Observability & Tracing | Operations |

Topics cycle — after day 15 the schedule restarts, so there's always fresh content.

---

## Setup (5 minutes)

### 1. Create a new GitHub repository

```bash
# On GitHub: Create a new repo named "agentic-ai-daily"
# Then push this project:
git init
git add .
git commit -m "feat: initial Agentic AI Daily setup"
git remote add origin https://github.com/skalmodiya/agentic-ai-daily.git
git push -u origin main
```

### 2. Enable GitHub Pages

1. Go to your repo → **Settings** → **Pages**
2. Under **Source**, select **"GitHub Actions"**
3. Click **Save**

### 3. Trigger the first build

The workflow runs automatically on push, so your first `git push` will kick off a build.
You can also go to **Actions** → **Daily Agentic AI Refresh** → **Run workflow** to trigger manually.

### 4. Access your site

After the workflow completes (~1-2 minutes), your site will be live at:
```
https://I560043.github.io/agentic-ai-daily/
```

---

## Project Structure

```
agentic-ai-daily/
├── .github/
│   └── workflows/
│       └── daily-build.yml     # GitHub Actions workflow (daily cron + Pages deploy)
├── scripts/
│   ├── content_library.py      # 15+ days of Agentic AI content
│   └── generate.py             # HTML generator (picks today's topic, builds index.html)
├── index.html                  # Auto-generated daily — do not edit manually
└── README.md
```

---

## How the Daily Rotation Works

The generator uses the **day-of-year** (1–365) modulo the number of topics to pick today's content:

```python
day_index = datetime.date.today().timetuple().tm_yday
topic = CONTENT_LIBRARY[day_index % len(CONTENT_LIBRARY)]
```

This means:
- Day 1 → Topic 1
- Day 16 → Topic 1 again (cycle repeats)
- No two consecutive days show the same topic (until cycle restarts)

---

## Adding More Topics

Edit `scripts/content_library.py` and add a new dict to `CONTENT_LIBRARY` following the existing structure:

```python
{
    "day_title": "Your Topic Title",
    "tag": "Category",
    "tag_color": "#hexcolor",
    "hero_icon": "🚀",
    "concept": { "title": "...", "body": "HTML content..." },
    "pattern": {
        "name": "Pattern Name",
        "description": "...",
        "steps": ["Step 1", "Step 2", ...],
        "code": "python code string"
    },
    "did_you_know": "Surprising fact...",
    "quiz": {
        "question": "...",
        "options": ["A", "B", "C", "D"],
        "answer": 1,  # 0-indexed
        "explanation": "..."
    },
    "resources": [{"title": "...", "url": "https://..."}],
    "key_terms": ["Term1", "Term2", ...]
}
```

---

## Tech Stack

- **Python 3.11** — content library + HTML generation
- **GitHub Actions** — daily cron scheduler + CI/CD
- **GitHub Pages** — free static hosting
- **No external dependencies** — pure Python stdlib, no `pip install` needed

---

*Built with GitHub Actions. Refreshes daily at 06:00 UTC.*
