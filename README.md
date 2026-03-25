<p align="center">
  <h1 align="center">📰 fomo-news</h1>
  <p align="center">
    <strong>Your terminal's live news feed — GitHub trending, tech headlines, and AI buzz, all in one place.</strong>
  </p>
  <p align="center">
    Never miss what matters. No browser tabs. No doomscrolling. Just <code>/fomo-news</code>.
  </p>
  <p align="center">
    <a href="#quick-start">Quick Start</a> ·
    <a href="#categories">Categories</a> ·
    <a href="#examples">Examples</a> ·
    <a href="#skill-integration">Skill Integration</a>
  </p>
</p>

---

## What is fomo-news?

You're in the flow — coding, debugging, shipping. But you also want to know what's happening: Is there a hot new repo blowing up? Did Sam Altman just announce something? What's Reuters saying about the market?

**fomo-news** pulls real-time updates from 25+ sources and delivers them as clean, formatted markdown — right inside Claude Code, OpenClaw, or any skill-compatible agent. Zero dependencies. Zero config. Just news.

```
┌─────────────────────────────────────────────────────────┐
│  ⭐ GitHub    💬 Social    💻 Tech    🤖 AI    📈 Econ  │
│─────────────────────────────────────────────────────────│
│                                                         │
│  ⭐ GitHub Trending                                     │
│                                                         │
│  ┌───────────────────┬───────┬────────┬──────────────┐  │
│  │ Repo              │ Stars │ Lang   │ Description  │  │
│  ├───────────────────┼───────┼────────┼──────────────┤  │
│  │ org/cool-project  │ 2,841 │ Rust   │ A blazingly  │  │
│  │ lab/neural-thing  │ 1,337 │ Python │ State of the │  │
│  └───────────────────┴───────┴────────┴──────────────┘  │
│                                                         │
│  💬 Social Updates                                      │
│                                                         │
│  • Sam Altman — OpenAI announces... · 2h ago            │
│  • Jensen Huang — NVIDIA reveals... · 4h ago            │
│                                                         │
│  💻 Tech News                                           │
│                                                         │
│  • TechCrunch — The startup that... · 1h ago            │
│  • Ars Technica — Why Linux just... · 3h ago            │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

## Quick Start

### Install as a Skill

```bash
# via npx
npx skills add alibaba-flyai/fomo-news
```

Then just ask your agent:

> "What's trending on GitHub?"
> "Show me the latest AI news"
> "Any updates from Elon Musk or Sam Altman?"

The skill activates automatically based on intent — no slash command needed.

### Run Standalone

No install required. Just run it:

```bash
# Everything — GitHub + Social + News
node skills/fomo-news/scripts/fetch.mjs all

# Just GitHub trending
node skills/fomo-news/scripts/fetch.mjs github

# Just AI news
node skills/fomo-news/scripts/fetch.mjs ai --limit 5

# Machine-readable output
node skills/fomo-news/scripts/fetch.mjs tech --json
```

## Categories

Six categories, 25+ sources, one command.

| Category | Emoji | What You Get |
|----------|-------|-------------|
| `github` | ⭐ | Top trending repos from the past 7 days — general, AI, and LLM focused |
| `social` | 💬 | Headlines about 12+ influential tech/AI figures via Google News |
| `tech` | 💻 | TechCrunch · Ars Technica · The Verge · Hacker News · Wired |
| `ai` | 🤖 | MIT Tech Review · VentureBeat |
| `economics` | 📈 | Reuters Business · CNBC · MarketWatch |
| `politics` | 🏛️ | AP News · BBC News · NPR |

### People Tracked (Social)

The social feed watches news coverage of key figures in tech and AI:

| AI | Tech |
|----|------|
| Sam Altman (OpenAI) | Elon Musk (Tesla/X) |
| Dario Amodei (Anthropic) | Satya Nadella (Microsoft) |
| Jensen Huang (NVIDIA) | Sundar Pichai (Google) |
| Demis Hassabis (DeepMind) | Mark Zuckerberg (Meta) |
| Ilya Sutskever | Tim Cook (Apple) |
| Andrej Karpathy | |
| Yann LeCun (Meta AI) | |

## Examples

```bash
# Morning briefing — everything at a glance
node skills/fomo-news/scripts/fetch.mjs all --limit 5

# What's hot on GitHub this week?
node skills/fomo-news/scripts/fetch.mjs github --limit 20

# AI-specific news only
node skills/fomo-news/scripts/fetch.mjs ai

# Market & economics headlines
node skills/fomo-news/scripts/fetch.mjs economics --limit 10

# Pipe JSON into jq for custom filtering
node skills/fomo-news/scripts/fetch.mjs tech --json | jq '.[0].data[:3]'
```

### Inside Claude Code / OpenClaw

The skill activates automatically when you mention news, trending, or updates:

> "What's the latest in AI?"

> "Show me GitHub trending repos"

> "Any breaking tech news?"

> "What are people saying about Sam Altman?"

> "Give me an economics briefing"

## How It Works

```
You ask a question ──→ Skill pattern matches ──→ fetch.mjs runs
                                                      │
                                                      ├── GitHub Search API (3 parallel queries)
                                                      ├── Google News RSS (12 people × 3 items)
                                                      └── 13 RSS feeds (tech/ai/econ/politics)
                                                      │
You see formatted news ←── Agent renders markdown ←───┘
```

- **Runtime**: Node.js (v18+ with native `fetch`)
- **Dependencies**: None — zero `npm install`, pure Node.js
- **RSS Parsing**: Lightweight regex-based XML parser (no `rss-parser` needed)
- **Error Handling**: `Promise.allSettled()` — one failed feed never breaks the rest
- **Rate Limits**: GitHub unauthenticated = 60 req/hr. Set `GITHUB_TOKEN` for 5,000/hr

## Configuration

### GitHub Token (optional)

For higher GitHub API rate limits:

```bash
export GITHUB_TOKEN="ghp_your_token_here"
```

Without a token, you get 60 requests/hour — plenty for casual use.

## Project Structure

```
fomo-news/
├── README.md
├── LICENSE
└── skills/
    └── fomo-news/
        ├── SKILL.md              # Skill manifest & agent instructions
        ├── fetch.mjs             # Self-contained fetcher (zero deps)
        └── references/
            ├── github.md         # GitHub trending source docs
            ├── social.md         # Social feed source docs
            └── news.md           # News feed source docs
```

## License

[MIT](LICENSE) — Copyright (c) 2026 alibaba-flyai
