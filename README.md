<p align="center">
  <img src="https://img.shields.io/badge/fomo--news-v1.1.0-blueviolet?style=for-the-badge" alt="version" />
  <img src="https://img.shields.io/badge/dependencies-zero-brightgreen?style=for-the-badge" alt="deps" />
  <img src="https://img.shields.io/badge/node-18%2B-green?style=for-the-badge&logo=node.js" alt="node" />
  <img src="https://img.shields.io/badge/license-MIT-blue?style=for-the-badge" alt="license" />
</p>

<h1 align="center">📰 fomo-news</h1>

<p align="center">
  <strong>Real-time news from 40+ sources — straight in your terminal.</strong><br/>
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

**OpenClaw** — ask your agent naturally:

> "What's trending on GitHub?"
> "Show me the latest AI news"

**Claude Code** — ask your agent naturally:

> "What's trending on GitHub?"
> "Show me the latest AI news"

Or run the slash command directly:

```
/fomo-news Show me trending GitHub repos
```

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
| **Sam Altman** | OpenAI CEO |
| **Dario Amodei** | Anthropic CEO |
| **Demis Hassabis** | DeepMind CEO · Nobel Laureate |
| **Yann LeCun** | Meta Chief AI Scientist · Turing Award |
| **Ilya Sutskever** | SSI · Co-founder of OpenAI |
| **Andrej Karpathy** | Ex-Tesla AI · LLM educator · ex-OpenAI |
| **Arthur Mensch** | Mistral AI CEO |
| **Geoffrey Hinton** | Godfather of AI · Turing Award |
| **Fei-Fei Li** | Stanford HAI · ImageNet creator |
| **Andrew Ng** | DeepLearning.AI · Coursera |
| **Emad Mostaque** | Stability AI founder |

</td>
<td width="50%" valign="top">

### 💼 Tech Titans & Leaders

| Name | Known For |
|------|-----------|
| **Elon Musk** | Tesla · SpaceX · xAI |
| **Jensen Huang** | NVIDIA CEO · GPU kingpin |
| **Satya Nadella** | Microsoft CEO |
| **Sundar Pichai** | Google / Alphabet CEO |
| **Mark Zuckerberg** | Meta CEO · Llama models |
| **Tim Cook** | Apple CEO |
| **Andy Jassy** | Amazon / AWS CEO |
| **Lisa Su** | AMD CEO |
| **Marc Andreessen** | a16z · Tech investor |
| **Vinod Khosla** | Khosla Ventures · AI investor |
| **Donald Trump** | US President · Tech/AI policy |

</td>
</tr>
</table>

### 📝 Company Blogs

| Source | Category |
|--------|----------|
| **OpenAI Blog** | AI |
| **Anthropic Blog** | AI |
| **Google AI Blog** | AI |
| **Microsoft AI Blog** | AI |
| **Meta AI Blog** | AI |
| **NVIDIA Blog** | Tech |
| **Sam Altman's Blog** | AI |

> When any of these people make headlines or these blogs publish, fomo-news picks it up within hours via Google News RSS and direct RSS feeds.

---

## 📂 Categories

Six categories. 40+ sources. One command.

| Category | Emoji | Sources |
|----------|:-----:|---------|
| `github` | ⭐ | GitHub Search API — 5 parallel queries with progressive time windows (7d/30d/90d) |
| `social` | 💬 | Google News RSS — 22+ tech/AI leaders + 7 company blogs |
| `tech` | 💻 | TechCrunch · Ars Technica · The Verge · Hacker News · Wired |
| `ai` | 🤖 | MIT Tech Review AI · VentureBeat AI |
| `economics` | 📈 | Reuters Business · CNBC · MarketWatch |
| `politics` | 🏛️ | Reuters World · AP News · BBC News · NPR |

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
                                    GitHub API   Google News   14 RSS Feeds
                                   (5 queries)  (29 sources)  (tech/ai/econ/politics)
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

## 🔄 Update

### OpenClaw

```bash
clawhub update alibaba-flyai/fomo-news
```

Or via npx:

```bash
npx skills update alibaba-flyai/fomo-news
```

### Claude Code

Pull the latest and copy over your existing installation:

```bash
cd /tmp && rm -rf fomo-news && git clone https://github.com/alibaba-flyai/fomo-news.git
cp -r /tmp/fomo-news/skills/fomo-news ~/.claude/skills/fomo-news
```

### Standalone / Manual

If you cloned the repo directly, just pull:

```bash
cd path/to/fomo-news && git pull
```

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
