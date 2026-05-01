# ATLAS — Market Intelligence Engine

> Turn a company name into full B2B intelligence in under 3 minutes. Powered by Claude, GPT-4o, Gemini & Grok.

![ATLAS Banner](https://img.shields.io/badge/ATLAS-Intelligence_Engine-3b82f6?style=for-the-badge&logoColor=white)
![Multi-LLM](https://img.shields.io/badge/LLMs-Claude_+_GPT--4o_+_Gemini_+_Grok-8b5cf6?style=for-the-badge)
![Deploy](https://img.shields.io/badge/Deploy-Netlify_|_Vercel_|_GitHub_Pages-10b981?style=for-the-badge)

---

## What ATLAS Does

ATLAS is an autonomous market intelligence engine that runs **3 phases** and delivers **11 intelligence tabs** in a single scan:

| Phase | What Happens |
|-------|-------------|
| **Phase 01** | Claude (with live web search) + OpenAI + Gemini + Grok gather market intelligence in parallel |
| **Phase 02** | Claude identifies real decision-makers with contact information via web search |
| **Phase 03** | Claude generates personalized outreach (LinkedIn DM + Email + Follow-up sequence + Tracking logic) |

### 11 Intelligence Tabs
1. **Overview** — Founded, HQ, Scale, Business Model, Key Products
2. **Market Position** — Brand Perception, Market Share, USP, Recent Shifts
3. **Competitors** — Strengths & Gaps analysis per competitor
4. **Brand Activity** — Last 12–24 months of campaigns, launches, initiatives
5. **Events** — Experiential & events footprint
6. **Watchouts** — Strategic risks before engaging the brand
7. **AI Perspectives** — Independent analysis from each configured LLM
8. **Decision-Makers** — Real stakeholders with role relevance
9. **Contact Intel** — Emails (pattern-inferred), LinkedIn, Phone
10. **Outreach** — Personalized LinkedIn DM + Email + Follow-up sequence
11. **Tracking** — UTM, pixel tracking, CRM sync logic + System architecture

---

## Quick Start

### 1. Clone the repo
```bash
git clone https://github.com/YOUR_USERNAME/atlas-intelligence.git
cd atlas-intelligence
```

### 2. Open locally
```bash
# No build step needed — pure HTML/CSS/JS
open index.html

# Or use a local server:
npx serve .
# or
python3 -m http.server 8080
```

### 3. Add your API keys
Click **"API Keys"** in the top-right corner of the app and enter:

| Provider | Key Format | Get Key |
|----------|-----------|---------|
| **Claude** *(Required)* | `sk-ant-api03-...` | [console.anthropic.com](https://console.anthropic.com) |
| **OpenAI** *(Optional)* | `sk-proj-...` | [platform.openai.com/api-keys](https://platform.openai.com/api-keys) |
| **Gemini** *(Optional)* | `AIza...` | [aistudio.google.com](https://aistudio.google.com/app/apikey) |
| **Grok** *(Optional)* | `xai-...` | [console.x.ai](https://console.x.ai) |

> **Note:** Keys are stored in your browser's `localStorage` only — never sent to any server other than the respective AI provider's API.

### 4. Run a scan
Enter a company name + category, select your active LLMs, and click **Run Intelligence Scan**.

---

## Deploying to GitHub Pages

```bash
# 1. Push to GitHub
git add .
git commit -m "Initial commit"
git push origin main

# 2. Enable GitHub Pages
# Go to: Settings → Pages → Source: Deploy from branch → main / root
```

Your app will be live at: `https://YOUR_USERNAME.github.io/atlas-intelligence/`

---

## Deploying to Netlify

**Option A — Drag & Drop:**
1. Go to [netlify.com](https://netlify.com) → "Add new site" → "Deploy manually"
2. Drag the entire `atlas-intelligence/` folder

**Option B — Git Integration:**
1. Connect your GitHub repo on Netlify
2. Build command: *(leave empty)*
3. Publish directory: `.` (root)

The included `netlify.toml` handles all configuration automatically.

---

## Deploying to Vercel

```bash
# Install Vercel CLI
npm i -g vercel

# Deploy from project root
vercel

# Follow prompts — no build settings needed
```

The included `vercel.json` handles all configuration.

---

## Project Structure

```
atlas-intelligence/
├── index.html          ← Complete app (HTML + CSS + JS, no build needed)
├── README.md           ← This file
├── .gitignore          ← Standard git ignores
├── netlify.toml        ← Netlify deployment config
└── vercel.json         ← Vercel deployment config
```

---

## LLM Architecture

```
User Input (Company + Category)
        │
        ├─── Claude (web_search tool) ──→ Market Intelligence JSON
        ├─── OpenAI (GPT-4o) ──────────→ Intelligence Perspective
        ├─── Gemini (1.5 Pro) ─────────→ Intelligence Perspective  
        └─── Grok (xAI) ───────────────→ Intelligence Perspective
                │
                ▼
        Aggregated Intelligence
                │
                ├─── Claude (web_search) ──→ Decision-Maker Intel
                │
                └─── Claude ────────────────→ Personalized Outreach
                                              + Tracking Logic
```

**Why Claude as primary?**
Claude is the only model here with a native **web search tool** (`web_search_20250305`), making it the most accurate for real-time company data. Other models provide analytical perspective layers.

---

## API Usage & Costs (Estimated per scan)

| Provider | Model | ~Tokens Used | ~Cost |
|----------|-------|-------------|-------|
| Claude | claude-opus-4-5 | ~15,000 | ~$0.25 |
| OpenAI | gpt-4o | ~3,000 | ~$0.03 |
| Gemini | gemini-1.5-pro | ~3,000 | ~$0.02 |
| Grok | grok-3 | ~3,000 | ~$0.05 |

Claude handles 3 API calls (Phase 1, 2, 3). Others handle 1 call each.

---

## Customization

### Change the target industry / persona
In `index.html`, find Phase 3 prompt and update the StepOne context:
```javascript
// Line ~460: Update to your agency/company name and specialization
`You are an expert B2B outreach copywriter for [YOUR COMPANY]...`
```

### Add more quick-load samples
```html
<span class="ql-chip" onclick="ql('Company Name','Category description')">Label</span>
```

### Change active models
```javascript
// Swap model IDs in the callClaude/callOpenAI/etc functions
model: 'claude-opus-4-5'   // → 'claude-sonnet-4-6'
model: 'gpt-4o'             // → 'gpt-4-turbo'
model: 'gemini-1.5-pro'     // → 'gemini-2.0-flash'
model: 'grok-3'             // → 'grok-2'
```

---

## Known Limitations

- **Browser-only**: This is a static frontend app. API keys are stored in localStorage (suitable for personal/team use; not for public deployment with shared keys).
- **CORS**: All 4 providers support browser-side API calls. Claude requires `anthropic-dangerous-direct-browser-access: true` header (included).
- **Rate limits**: Running multiple LLMs in parallel may hit rate limits on free tiers.
- **Contact accuracy**: Email addresses are pattern-inferred, not verified. Always validate before outreach.

---

## Built With

- **No frameworks** — Pure HTML, CSS, JavaScript
- **No build step** — Open `index.html` and go
- **Fonts**: Bricolage Grotesque + JetBrains Mono (Google Fonts)
- **APIs**: Anthropic, OpenAI, Google AI, xAI

---

## License

MIT — use freely, attribution appreciated.

---

*Built for the StepOne AI Buildathon · ATLAS Intelligence Engine v2.0*
