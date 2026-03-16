---
type:
  - "[[Working document]]"
tags:
  - Type/Workingdoc
Keywords:
  - "[[Tibbir]]"
  - "[[05 Workspaces/1. Projects/Faircaster/Fair]]"
  - "[[agentsfund.ai]]"
date created: "[[March 16, 2026]]"
date ended:
Status: false
project: "[[Tibbir x Fair Proposal]]"
author: "[[Claude agent]]"
---

# Pipeline Page Spec — agentsfund.ai/pipeline

## Purpose

Demo-ready pipeline page for Zack Rosen meeting (today 3:30 PM). Shows Fair's scouting engine actively tracking projects building revenue-generating agents and agent infrastructure.

**Audience:** Ribbit partner, side-by-side on laptop.
**Core message:** "The scouting engine is already running. Here's what it's found."

---

## Scope

**This is a prototype.** Build fast, ship before 3:30.

- One new page: `/pipeline`
- Slide-in panel for project detail (no new routes)
- Static data seeded from deep research results
- Fair (chatbot) will be briefed on the agent fund + given access to this data to speak intelligently about projects
- Tibbir-branded skin swap version (same layout, Tibbir colors/logo) — quick toggle or separate build

**Not in scope for v1:**
- Agent reasoning chat bar (phase 2)
- Live backend / API integration
- Portfolio page or other site pages

---

## Architecture

### Pipeline View (`/pipeline`)

Card layout. Fund-grade, minimal, **light theme** (matching existing site). Side-by-side optimized (normal text size, moderate density).

**Default view:** Curated — only Researching+ stage projects.
**Toggle:** "Show full funnel" reveals Scouting-stage projects too.

**Each project card shows:**

| Field | Description |
|-------|------------|
| Name | Project name |
| One-liner | What it does, one sentence |
| Category | Agent / Infrastructure / Protocol / Tool |
| Traction signal | Key metric: revenue, users, TVL, tx volume |
| Signal strength | Visual indicator (filled dots or bars, no number) |
| Stage | Scouting → Researching → Candidate → Invested |

**Filtering/sorting:**
- Filter by stage
- Filter by category (agents, infra, broader)
- Sort by signal strength (default), recency, or alphabetical

### Project Detail (slide-in panel)

Clicking a project opens a ~40% width panel from the right. Pipeline list stays visible on left.

**Panel contents:**

#### Summary
- What this project does (1 paragraph)
- Who built it (team, background, links)
- Why Fair flagged it — agent reasoning ("Fair discovered this because...")

#### Traction & Metrics
- Key numbers: revenue, users, TVL, volume — whatever's available
- Signal strength indicator (same as card view, but larger)
- Stage badge

#### Key Updates
- 3-5 curated milestones (seeded from deep research / Fair / manual)
- Each update: date, event description, source link

#### Sources (HIGH PRIORITY — this is the flex)
- **Key tweets/posts where Fair discovered this project** — the original social signals
- Linked back to Twitter/X, Farcaster, articles, GitHub
- Proves the scouting engine is real — not a manually assembled list
- Each source: type tag (mono label), snippet/quote, direct link

*Live feed of ongoing social data is phase 2. For v1, the curated source tweets are what matter.*

---

## Data

### Seeding strategy

1. **Deep research agent** runs now (prompt already written) — returns 15-20 projects with structured data
2. **Fair** gets briefed on the agent fund mandate + access to this data — can speak about projects intelligently in the meeting
3. **Manual curation** on top — Luc adjusts signal strength, adds context, picks stage assignments

### Known seed projects
- Felix (Nat Eliason)
- KellyClaude (Austen Allred)
- Prodia.com
- Austin Griffith's agent
- Droyd
- + 10-15 from deep research

### Data format (static JSON for v1)

```json
{
  "projects": [
    {
      "name": "Felix",
      "slug": "felix",
      "oneLiner": "Autonomous crypto agent by Nat Eliason",
      "category": "agent",
      "tractionSignal": "$X revenue",
      "signalStrength": 4,  // 1-5, rendered as filled dots
      "stage": "candidate",
      "summary": "...",
      "team": "Nat Eliason",
      "teamBackground": "...",
      "teamLinks": { "twitter": "...", "github": "..." },
      "whyFlagged": "Fair discovered this because...",
      "metrics": { "revenue": "...", "users": "..." },
      "milestones": [
        { "date": "2026-03-10", "event": "...", "source": "..." }
      ],
      "recentFeed": [
        { "date": "2026-03-15", "event": "...", "source": "...", "impact": "high" }
      ],
      "sources": [
        { "type": "tweet", "url": "...", "snippet": "..." }
      ]
    }
  ]
}
```

---

## Design

- **Consistent with existing site.** Light theme, indigo/purple primary, DM Sans + JetBrains Mono.
- **Not a dashboard.** Feels like a deal pipeline at a serious fund.
- **No flashy animations.** Credibility over novelty.
- **Side-by-side optimized:** Normal font size, good information density.
- **Slide-in panel:** Smooth CSS transition, clear close affordance. Pipeline list dims slightly when panel is open.

### Tibbir skin
- Same layout, same data
- Tibbir colors + logo swapped in
- Header: "Tibbir Agent Pipeline" (or similar)
- URL param toggle: `?brand=tibbir`

---

## Tech

- **Stack:** Static HTML + vanilla JS + inline CSS. Same architecture as existing `index.html` (single file, ~2000 lines).
- **File:** New `pipeline.html` in repo root
- **Deploy:** Vercel, same as current site
- **Repo:** https://github.com/CnxLuc/agentsfund-site
- **Data:** Inline JS array or separate `pipeline-data.js`. No backend.
- **Theming:** CSS variables, swap values via JS when `?brand=tibbir` detected

### Reuse from existing `index.html`

Copy the full CSS variable system and these component styles:
- **CSS vars:** `--bg`, `--surface`, `--border`, `--text`, `--text-dim`, `--text-muted`, `--primary`, `--purple`, `--cyan`, `--green`, `--font-body`, `--font-mono`, `--radius`
- **`.agent-card`** → project cards (hover lift + shadow transitions)
- **`.agent-card-header`** → icon + name + role → icon + name + category
- **`.artifact-tag`** → stage badges + category pills (color-coded per stage)
- **`.section-header`** → pipeline title with left border accent
- **`.kpi` row** → summary stats (projects tracked, sources processed, etc.)
- **`nav`** → same nav bar, add "Pipeline" as `.active` link
- **`.prose`** → summary text in detail panel
- **`.insight-callout`** → "Why Fair flagged this" reasoning block

### New components to build

- **Filter bar** — stage + category pill toggles, styled like `nav a` pills
- **Signal strength dots** — 5 small circles, filled up to conviction level, `--primary` color
- **Stage badge colors** — Scouting: `--text-muted` / Researching: `--cyan` / Candidate: `--purple` / Invested: `--primary`
- **Slide-in panel** — fixed right, 40% width, `transform: translateX` animation, `border-left` surface edge, barely perceptible backdrop (`rgba(0,0,0,0.06)`) — feels like a surface, not a modal
- **Source links** — list with mono text type labels styled as `.artifact-tag` (no emoji — breaks the tone)
- **Updates timeline** — vertical line connector, date + event + source per entry, milestones pinned top

---

## Demo Flow

In the meeting, the demo is 1 minute:
1. Open `/pipeline` — "Here's what Fair's scouting engine is tracking right now"
2. Point at signal strength dots, stage filters — "These are ranked by conviction"
3. Click one project — panel slides in — "Here's why Fair flagged this, here's the data"
4. Scroll to sources — "All sourced from real social data, 2.3M posts processed"
5. Close panel, back to pipeline — "This updates continuously. Next step is we pick one together."

---

## References

- **[[260316 agentsfund.ai Brand Guidelines]]** — full design system: colors, typography, compositional primitives, shadow recipe, gradient treatments. **The builder MUST read this before writing any CSS.**
- **Repo:** https://github.com/CnxLuc/agentsfund-site — existing `index.html` with full CSS system
- **Screenshot:** `/tmp/agentsfund-screenshot.png` — full-page capture of live site for visual reference
- **[[260316 Agent Scouting Prompt]]** — deep research prompt sent to find 15-20 revenue-generating agents. Results feed directly into pipeline data.
- **Deep research results:** (link TBD when results come back) — the actual project data to seed the pipeline

---

## Deadline

Ship before 3:30 PM today.
