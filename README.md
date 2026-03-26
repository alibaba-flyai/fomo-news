<p align="center">
  <img src="https://img.shields.io/badge/fomo--news-v1.0.3-blueviolet?style=for-the-badge" alt="version" />
  <img src="https://img.shields.io/badge/dependencies-zero-brightgreen?style=for-the-badge" alt="deps" />
  <img src="https://img.shields.io/badge/node-18%2B-green?style=for-the-badge&logo=node.js" alt="node" />
  <img src="https://img.shields.io/badge/license-MIT-blue?style=for-the-badge" alt="license" />
</p>

<h1 align="center">📰 fomo-news</h1>

<p align="center">
  <strong>Real-time news from 25+ sources — straight in your terminal.</strong><br/>
  GitHub trending · AI headlines · Tech leader buzz · Market moves
</p>

<p align="center">
  No browser tabs. No doomscrolling. Just <code>/fomo-news</code>.
</p>

<p align="center">
  <a href="#-demo">Demo</a> ·
  <a href="#-quick-start">Quick Start</a> ·
  <a href="#-who-we-track">Who We Track</a> ·
  <a href="#-categories">Categories</a> ·
  <a href="#-how-it-works">How It Works</a>
</p>

---

## 🎬 Demo

<p align="center">
  <img src="assets/demo.gif" alt="fomo-news in action inside OpenClaw" width="720" />
</p>

> *fomo-news running inside [OpenClaw](https://openclaw.com) — ask a question, get a live briefing.*

---

## ✨ Why fomo-news?

You're deep in the flow — coding, debugging, shipping. But the world keeps moving:

- A repo just hit **3,000 stars overnight** — and it does exactly what you need
- **Andrej Karpathy** just dropped a thread on a new training technique
- **Demis Hassabis** announced a DeepMind breakthrough at a keynote
- Reuters is reporting a market shift that affects your company

**fomo-news** brings all of it to you. One command. Zero context-switching.

---

## 🚀 Quick Start

### Option A — OpenClaw

**Via clawhub (recommended):**

```bash
clawhub install alibaba-flyai/fomo-news
```

**Via npx:**

```bash
npx skills add alibaba-flyai/fomo-news
```

### Option B — Claude Code

Clone the repo and copy it into your Claude Code skills directory:

```bash
git clone https://github.com/alibaba-flyai/fomo-news.git /tmp/fomo-news
mkdir -p ~/.claude/skills/
cp -r /tmp/fomo-news ~/.claude/skills/fomo-news
```

### ✅ Verify Installation

**OpenClaw** — run the slash command:

```
/fomo-news
```

**Claude Code** — ask your agent naturally:

> "What's trending on GitHub?"
> "Show me the latest AI news"

If you see a formatted news briefing, you're all set!

### Run Standalone

```bash
# Everything — GitHub + Social + News
node skills/fomo-news/scripts/fetch.mjs all

# Just GitHub trending
node skills/fomo-news/scripts/fetch.mjs github

# Just AI news, top 5
node skills/fomo-news/scripts/fetch.mjs ai --limit 5

# Machine-readable JSON output
node skills/fomo-news/scripts/fetch.mjs tech --json
```

---

## 🔭 Who We Track

fomo-news monitors news coverage of the **most influential voices in tech and AI** — the people whose words move markets, shape products, and define the frontier.

<table>
<tr>
<td width="50%" valign="top">

### 🤖 AI Pioneers

| Name | Known For |
|------|-----------|
| **Andrej Karpathy** | Ex-Tesla AI · LLM educator · ex-OpenAI |
| **Demis Hassabis** | DeepMind CEO · Nobel Laureate |
| **Sam Altman** | OpenAI CEO |
| **Dario Amodei** | Anthropic CEO |
| **Ilya Sutskever** | SSI · Co-founder of OpenAI |
| **Jensen Huang** | NVIDIA CEO · GPU kingpin |
| **Yann LeCun** | Meta Chief AI Scientist · Turing Award |

</td>
<td width="50%" valign="top">

### 💼 Tech Titans

| Name | Known For |
|------|-----------|
| **Elon Musk** | Tesla · SpaceX · xAI |
| **Satya Nadella** | Microsoft CEO |
| **Sundar Pichai** | Google / Alphabet CEO |
| **Mark Zuckerberg** | Meta CEO · Llama models |
| **Tim Cook** | Apple CEO |

</td>
</tr>
</table>

> When any of these people make headlines, fomo-news picks it up within hours via Google News RSS.

---

## 📂 Categories

Six categories. 25+ sources. One command.

| Category | Emoji | Sources |
|----------|:-----:|---------|
| `github` | ⭐ | GitHub Search API — top trending repos (general + AI + LLM) |
| `social` | 💬 | Google News RSS — 12 tech/AI leaders tracked in real-time |
| `tech` | 💻 | TechCrunch · Ars Technica · The Verge · Hacker News · Wired |
| `ai` | 🤖 | MIT Tech Review · VentureBeat |
| `economics` | 📈 | Reuters Business · CNBC · MarketWatch |
| `politics` | 🏛️ | AP News · BBC News · NPR |

Use `all` to get everything, or `news` for all news categories combined.

---

## 🧪 Examples

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

Just talk to your agent. fomo-news activates on intent:

> *"What's the latest in AI?"*
> *"Show me GitHub trending repos"*
> *"Any breaking tech news?"*
> *"What are people saying about Karpathy?"*
> *"Economics briefing, please"*

---

## ⚙️ How It Works

```
You ask a question ──→ Skill pattern matches ──→ fetch.mjs runs
                                                      │
                                         ┌────────────┼────────────┐
                                         │            │            │
                                    GitHub API   Google News   13 RSS Feeds
                                   (3 queries)  (12 people)   (tech/ai/econ/politics)
                                         │            │            │
                                         └────────────┼────────────┘
                                                      │
You see formatted news ←── Agent renders markdown ←───┘
```

- **Runtime**: Node.js v18+ (native `fetch`)
- **Dependencies**: Zero — no `npm install` needed
- **RSS Parsing**: Lightweight regex-based XML parser
- **Error Handling**: `Promise.allSettled()` — one failed feed never breaks the rest
- **Rate Limits**: GitHub unauthenticated = 60 req/hr. Set `GITHUB_TOKEN` for 5,000/hr

---

## 🔑 Configuration

### GitHub Token (optional)

For higher GitHub API rate limits:

```bash
export GITHUB_TOKEN="ghp_your_token_here"
```

Without a token, you get 60 requests/hour — plenty for casual use.

---

## 📁 Project Structure

```
fomo-news/
├── README.md
├── LICENSE
├── assets/
│   └── demo.gif              # Demo recording
└── skills/
    └── fomo-news/
        ├── SKILL.md           # Skill manifest & agent instructions
        ├── scripts/
        │   └── fetch.mjs      # Self-contained fetcher (zero deps)
        └── references/
            ├── github.md      # GitHub trending source config
            ├── social.md      # Social feed source config
            └── news.md        # News feed source config
```

---

<p align="center">
  <sub>Powered by <strong>📰 fomo-news</strong> · Built by <a href="https://github.com/alibaba-flyai">alibaba-flyai</a></sub><br/>
  <sub><a href="LICENSE">MIT License</a> · Copyright (c) 2026</sub>
</p>
