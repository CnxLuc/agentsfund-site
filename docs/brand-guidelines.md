---
type:
  - "[[Working document]]"
tags:
  - Type/Workingdoc
Keywords:
  - "[[agentsfund.ai]]"
  - "[[05 Workspaces/1. Projects/Faircaster/Fair]]"
date created: "[[March 16, 2026]]"
Status: false
project: "[[Tibbir x Fair Proposal]]"
author: "[[Claude agent]]"
---

# agentsfund.ai — Brand Guidelines

Extracted from live site on March 16, 2026. Refined after visual audit of screenshot + full HTML source.

Source: https://agentsfund.ai

---

## Design Philosophy

This site communicates one thing: a system that is serious, precise, and already running. Every design choice serves institutional credibility. It reads like a technical paper presented as a product page — not a marketing site that borrows technical aesthetics.

The visual language is built from a small number of primitives composed consistently. New pages must use these same primitives. Inventing new visual patterns is a bug.

---

## Color Palette

### Primary
- **Primary:** `#4f46e5` (Indigo) — UI accents, active states, CTAs
- **Primary Dim:** `rgba(79, 70, 229, 0.06)` — subtle backgrounds, hover tints
- **Primary Border:** `#4338ca` — accent borders, tag text on indigo-dim backgrounds

### Accent Colors
| Name | Hex | Dim | Border | Semantic Role |
|------|-----|-----|--------|---------------|
| Purple | `#7c3aed` | `rgba(124, 58, 237, 0.06)` | `#6d28d9` | Secondary accent, thesis/interpretation layer |
| Cyan | `#0891b2` | `rgba(8, 145, 178, 0.06)` | `#0e7490` | Research, scouting, perception |
| Green | `#059669` | `rgba(5, 150, 105, 0.06)` | `#047857` | Success, execution, active/confirmed |
| Red | `#dc2626` | `rgba(220, 38, 38, 0.06)` | `#b91c1c` | Alert, risk, policy gate, hard stops |
| Blue | `#2563eb` | `rgba(37, 99, 235, 0.06)` | `#1d4ed8` | Information, ledger, data layer |
| Orange | `#ea580c` | `rgba(234, 88, 12, 0.06)` | `#c2410c` | Warning, attention |
| Pink | `#db2777` | `rgba(219, 39, 119, 0.06)` | `#be185d` | Highlight, outcomes, feedback |

**Every accent follows a three-token pattern:** `--color`, `--color-dim` (0.06 opacity for backgrounds), `--color-border` (darker variant for text-on-dim and borders). No exceptions. New components must use this pattern, never raw hex values.

### Neutrals
| Token | Hex | Usage |
|-------|-----|-------|
| `--bg` | `#f7f8fb` | Page background (off-white with blue undertone — not pure gray) |
| `--surface` | `#ffffff` | Card backgrounds |
| `--surface2` | `#f0f2f7` | Hover backgrounds, table header gradients, secondary surfaces |
| `--surface3` | `#e6e9f0` | Tertiary surfaces, heavier delineation |
| `--text` | `#0c1024` | Primary text (near-black with blue-purple undertone, NOT pure #000) |
| `--text-dim` | `#5a6378` | Body text, descriptions, secondary content |
| `--text-muted` | `#8e96a8` | Labels, metadata, mono labels, placeholder-level content |
| `--border` | `rgba(0,0,0,0.07)` | Default card/component borders |
| `--border-bright` | `rgba(0,0,0,0.12)` | Table header borders, stronger delineation |

### Spatial Backgrounds (two layers, both `background-attachment: fixed`)

**Layer 1 — Indigo radial glow:**
```css
radial-gradient(ellipse 1200px 800px at 50% -100px, rgba(79, 70, 229, 0.07) 0%, transparent 70%)
```
Creates a subtle atmospheric glow at the top of the page. Felt more than seen. The hero section has an additional, more intense glow via `::before` pseudo-element (`rgba(79, 70, 229, 0.16)` center, larger radius).

**Layer 2 — Dot grid:**
```css
radial-gradient(circle at 1px 1px, rgba(0,0,0,0.04) 1px, transparent 0)
/* 24px x 24px repeat */
```
The dots are barely visible. They provide micro-texture that prevents the off-white from feeling flat. The indigo glow bleeds through the dots, creating subtle depth without any parallax tricks.

**Section dividers** — the horizontal gradient line at the bottom of every section:
```css
background-image: linear-gradient(to right, transparent, rgba(79, 70, 229, 0.12), transparent);
background-size: 100% 1px;
background-position: bottom;
```
This replaces hard `border-bottom` rules. The gradient fades in and out, so sections feel separated atmospherically rather than mechanically. This is a signature pattern — use it, don't replace it with solid lines.

---

## Typography

### Font Families
- **Body:** `'DM Sans', system-ui, sans-serif` — geometric, clean, slightly warm
- **Mono:** `'JetBrains Mono', 'SF Mono', Consolas, monospace` — used for all data, metadata, labels, tags

### Type Scale

| Element | Size | Weight | Tracking | Line Height | Notes |
|---------|------|--------|----------|-------------|-------|
| Hero H1 | 68px (36px mobile) | 700 | -3px (-1.8px mobile) | 1.0 | Gradient text fill (indigo-purple) |
| Section H2 | 36px (26px mobile) | 700 | -1.6px | 1.1 | Inside `.section-header` with left border |
| Sub-section H2 | 22px | 700 | -1.6px | 1.1 | Used for sub-headings within sections |
| Card H3 | 15px | 600 | -0.2px | — | Agent/component names |
| Smaller H3 | 14-14.5px | 600 | -0.2px | — | Eval cards, safeguard cards |
| Body (global) | 15px | 400 | -0.1px | **1.6** | Global body `line-height` |
| Prose body | 15px | 400 | -0.1px | **1.75** | `.prose p` — more generous for long-form |
| Card description | 13px | 400 | -0.05px | 1.65 | `.agent-desc` — denser than prose |
| Insight callout | 15.5px | 400 | — | 1.85 | Most generous line-height on the site |
| Nav link | 13px | 500 (600 active) | -0.2px | — | |
| Mono label | 10-10.5px | 600-700 | 0.4-1.8px | — | UPPERCASE. Tags, tier labels, metadata |
| KPI value | 40px (28px mobile) | 700 | -2px (-1.2px mobile) | 1.1 | Different gradient than hero (see below) |
| Table body | 13px | 400 | — | 1.6 | |
| Table header | 10px mono | 700 | 1.4px | — | UPPERCASE, dim text on surface2 gradient |
| Footer | 11px mono | 400 | 0.4px | — | |

**Key typography rule:** Monospace is *only* for computed/structured content — labels, tags, metadata, table headers, code snippets. Never for prose or headings. This separation between DM Sans (human voice) and JetBrains Mono (system voice) is the typographic backbone.

### Gradient Text

**Hero title gradient** (indigo-purple-indigo):
```css
background: linear-gradient(135deg, #4f46e5 0%, #7c3aed 50%, #4338ca 100%);
-webkit-background-clip: text;
-webkit-text-fill-color: transparent;
```

**KPI value gradient** (dark-to-indigo, different from hero):
```css
background: linear-gradient(140deg, #0c1024 0%, #4f46e5 80%);
-webkit-background-clip: text;
-webkit-text-fill-color: transparent;
```
The KPI gradient starts from near-black and fades *into* indigo. This creates an "ink dissolving into color" effect that makes numbers feel grounded. The hero gradient is pure color. Do not swap them.

**Nav brand gradient** (indigo-purple, two-stop):
```css
background: linear-gradient(135deg, #4f46e5 0%, #6d28d9 100%);
```

**Tier count gradients** vary by tier (t1: indigo-purple, t2: purple-indigo, t3: plain `--text-dim`). The gradient direction signals hierarchy.

---

## Layout

### Container
- Max-width: `1200px`
- Padding: `0 40px` (desktop), `0 16px` (mobile)
- Breakpoint: `768px` — single breakpoint, everything stacks

### Spacing Rhythm
- **Section padding:** `80px 0` (desktop), `32px 0` (mobile) — this is very generous. Sections breathe.
- **Section header margin-bottom:** `40px` — substantial gap between header and content
- **Card padding:** `24-28px` — consistent across card types
- **Grid gap:** `16px` for cards, `12px` for tighter lists (loop steps), `20px` for state grid
- **Border radius:** `12px` (cards, `--radius`), `8px` (smaller components, `--radius-sm`), `6px` (tags/pills), `4px` (inline code), `13px` (agent icons — slightly squircle), `20px` (pill badges)
- **Prose max-width:** `100%` (fills container, not constrained — the container itself is 1200px)
- **Hero description max-width:** `720px`

### Grids
- **Agent cards:** `repeat(auto-fill, minmax(340px, 1fr))` — typically 2-3 columns
- **Eval cards:** `repeat(auto-fill, minmax(280px, 1fr))` — typically 3 columns
- **3-col tiers:** `repeat(3, 1fr)` — forced 3-column, stacks on mobile
- **State grid:** `1fr 1fr` — forced 2-column comparison
- **Loop steps:** single column, stacked

---

## Shadow System

The shadow system is the primary depth mechanism. The site achieves its "floating paper" quality through a specific three-layer shadow recipe. This is the most important visual pattern to replicate correctly.

### Standard Card Shadow (resting)
```css
box-shadow:
  0 1px 2px rgba(0, 0, 0, 0.04),    /* edge definition — tight */
  0 4px 16px rgba(0, 0, 0, 0.05),    /* float — medium distance */
  0 12px 40px rgba(0, 0, 0, 0.03);   /* atmosphere — soft, wide */
```

### Card Shadow (hover)
```css
box-shadow:
  0 2px 8px rgba(79, 70, 229, 0.06),   /* edge — indigo-tinted */
  0 8px 32px rgba(79, 70, 229, 0.1),    /* float — indigo glow */
  0 20px 60px rgba(0, 0, 0, 0.06);      /* atmosphere — deeper */
```
On hover, the shadow shifts from neutral gray to indigo-tinted. This is subtle but critical — it connects the elevation change to the brand color.

### Featured Card Shadow (animated pulse)
The MD card uses a pulsing indigo glow:
```css
@keyframes md-pulse {
  0%, 100% { box-shadow: 0 0 0 0 rgba(79, 70, 229, 0), 0 0 20px rgba(79, 70, 229, 0.1); }
  50% { box-shadow: 0 0 0 6px rgba(79, 70, 229, 0.06), 0 0 32px rgba(79, 70, 229, 0.18); }
}
```

### Lighter Variants
- **Mermaid/diagram sections:** Slightly heavier resting shadow (`0 16px 48px`) plus a 3px indigo top border
- **Principle accordion items:** Lighter (`0 1px 3px` + `0 4px 14px`) — less float, more grounded
- **Agent icon:** Includes `inset 0 1px 0 rgba(255,255,255,0.8)` for a glass highlight effect

**Rule:** Never use a single-layer shadow. Always use at least the tight + medium layers. The atmosphere layer is optional for smaller components.

---

## Compositional Primitives

These are the four recurring structural patterns. Every component on the site is built from one or more of these. New components (including pipeline page components) should be composed from these same primitives.

### 1. Left-Border Accent
A 3-4px colored border on the left edge, signaling "this block has a specific semantic role."

| Component | Border Width | Color | Notes |
|-----------|-------------|-------|-------|
| Section header | 3px | Gradient: primary → purple | `border-image` on left |
| Insight callout | 4px | `var(--primary)` (or contextual: `var(--red)` for risk) | Rounded right corners only |
| Mantra block | 3px | `var(--primary)` | Same as insight callout variant |
| Loop steps | 3px | Color-coded per step (cyan, purple, primary, red, green, pink) | Sequential color assignment |
| State cards | 3px | Blue (ledger) or orange (snapshot) | Semantic color pairing |

### 2. Top-Border Accent
A 3px colored border on the top edge, used for category/type signaling on cards that are part of a grid.

| Component | Color Logic |
|-----------|-------------|
| Eval cards | Cyan (routing), Purple (thesis), Green (execution) — matches learning loop colors |
| Tier cards | Primary (tier 1), Purple (tier 2), Muted (tier 3) — hierarchy signal |
| Safeguard cards | Color-coded by nth-child: red, blue, purple, orange, green, pink |
| Mermaid sections | 3px `var(--primary)` top border — marks diagram containers |

### 3. Color-Coded Dim Background
The `--color-dim` + `--color-border` pattern for tags, badges, and inline indicators. Background at 0.06 opacity, text in the darker border variant.

```css
/* Pattern */
background: var(--cyan-dim);     /* rgba(8, 145, 178, 0.06) */
color: var(--cyan-border);        /* #0e7490 */
```

Used on: artifact tags, weight badges, hero badge, table code blocks, loop step number circles.

### 4. Gradient Background Fade
A subtle gradient from a tinted color to white/surface, creating directional emphasis.

```css
/* Insight callout */
background: linear-gradient(135deg, rgba(79, 70, 229, 0.04) 0%, rgba(79, 70, 229, 0.02) 40%, var(--surface) 70%);

/* Table header */
background: linear-gradient(to bottom, var(--surface2), rgba(240, 242, 247, 0.6));
```

---

## Components

### Navigation
- Sticky, `z-index: 100`
- Frosted glass: `rgba(247,248,251,0.88)` + `backdrop-filter: blur(12px)`
- Inner container: `max-width: 1200px`, flex layout, horizontal scroll on overflow
- Nav padding: `8px 0` inner, `0 40px` outer (matches container)
- Brand name: gradient text (indigo-purple), 16px, weight 700, with `nav-divider` (1px vertical line, 16px height) separating it from links
- Links: 13px, weight 500, `--text-dim`, `padding: 6px 12px`, `border-radius: 6px`
- Link hover: `--text` color + `--surface2` background
- Active link: `--primary` color + `--primary-dim` background, weight 600

### Cards (`.agent-card`)
- `var(--surface)` background, `var(--border)` border, three-layer shadow
- Hover: indigo-tinted shadow, `border-color: rgba(79, 70, 229, 0.2)`, `translateY(-3px)` lift
- Transition: `0.2s ease` on shadow, border-color, and transform
- Header: flex row with `12px` gap, `12px` margin-bottom
- Icon: `44x44px`, `border-radius: 13px`, flex centered, 20px emoji, `--border` border, inner shadow + glass highlight
- Name: 15px weight 600, tight tracking
- Role label: mono, 10px, weight 600, `--text-muted`, uppercase, `0.6px` tracking, `2px` margin-top
- Description: 13px, `--text-dim`, `line-height: 1.65`, `14px` margin-bottom
- Artifacts row: flex wrap, `6px` gap

### Tags (`.artifact-tag`)
- Mono, 10px, weight 600
- Padding: `4px 9px`, radius `6px`
- Color-coded using the dim/border pattern
- `letter-spacing: 0.2px`, `white-space: nowrap`

### Badges (pill-shaped)
- Mono, 10px, weight 600
- Pill shape: `border-radius: 20px`
- Padding: `6px 16px` (hero badge), `2px 8px` (weight badge), `4px 10px` (tier weight)
- Color-coded using dim/border pattern
- Optional: `1px solid` border at ~0.15 opacity of accent color, subtle box-shadow

### Insight Callout
- Left border: `4px solid var(--primary)` (or contextual color)
- `border: 1px solid rgba(79, 70, 229, 0.1)` on other sides
- Gradient background fading from indigo-tint to surface
- Rounded right corners only: `border-radius: 0 var(--radius) var(--radius) 0`
- Padding: `28px 36px`
- Subtle indigo-tinted shadow: `0 2px 8px rgba(79, 70, 229, 0.05), 0 8px 24px rgba(79, 70, 229, 0.03)`
- Text: 15.5px, `--text-dim`, `line-height: 1.85` — the most open text on the site
- `strong` tags render in `--text` at weight 600

### Section Headers
- Left border: `3px`, gradient from primary to purple via `border-image`
- Padding-left: `18px`
- Margin-bottom: `40px`
- H2: 36px, weight 700, tracking -1.6px, `line-height: 1.1`, `margin-bottom: 10px`
- Description: 15px, `--text-dim`, `line-height: 1.65`

### Tables
- Wrapped in a container with surface background, border, border-radius, and card shadow
- Header: gradient background (surface2 → transparent), mono, 10px, weight 700, uppercase, 1.4px tracking
- Header padding: `14px 18px`, bottom border `--border-bright`
- Body cells: `13px`, `padding: 13px 18px`, `line-height: 1.6`, top-aligned
- Alternating rows: `rgba(240, 242, 247, 0.5)` — barely there
- Hover row: `rgba(79, 70, 229, 0.05)` — indigo tint
- Inline code in tables: mono 10px, `--primary-dim` background, `--primary` text, `2px 7px` padding, 4px radius

### Accordion (`.principle-item`)
- Uses native `<details>` element
- Surface background, border, border-radius, lighter shadow
- Summary: 15px, weight 600, `20px 24px` padding, flex row with dot indicator
- Summary hover: `--surface2` background
- Open state: summary gets `--surface2` background, top-rounded only
- Arrow: mono `▸` character, auto-margin-left, rotates 90deg on open (turns indigo)
- Detail content: `16px 24px 22px 44px` padding, 14px text, `--text-dim`, `line-height: 1.8`, `--surface2` background, bottom-rounded

### Loop Steps
- Single-column stacked list, `10px` gap
- Grid layout per step: `44px 1fr` with `16px` gap
- Left border: 3px, color-coded by position (cyan → purple → primary → red → green → pink)
- Number circle: 38px diameter, 50% radius, weight 700, 14px, color-coded dim/border
- Heading: 14px, weight 600
- Description: 12.5px, `--text-dim`, `line-height: 1.55`
- Hover: `translateX(3px)` — horizontal shift, not vertical lift. Only component that does this.

### Footer
- Border-top: `1px solid var(--border)`
- Padding: `32px 40px`
- Flex row: brand (gradient, 13px, weight 700) | center text (mono, 11px, uppercase) | year (60% opacity)

---

## Transitions & Interactions

All transitions use `0.2s ease` (occasionally `0.15s` for link color/background). Consistency matters here.

| Component | Hover Effect |
|-----------|-------------|
| Cards (agent, eval, safeguard, tier, state) | `translateY(-2px to -3px)` lift + shadow intensification |
| Loop steps | `translateX(3px)` horizontal shift (exception to vertical lift pattern) |
| Ladder boxes | `translateY(-1px)` micro-lift |
| Nav links | Color shift to `--text` + `--surface2` background |
| Table rows | `rgba(79, 70, 229, 0.05)` indigo tint |
| Accordion summary | `--surface2` background |
| Principle items | Border-color shift to indigo at 0.18 opacity |

**No hover uses opacity changes, scale transforms, or color shifts on the element itself.** Elevation (translate + shadow) and background tinting are the only two hover mechanisms.

---

## Dashed Connectors (Org Chart Pattern)

The org chart uses SVG dashed lines to connect the MD card to branch labels:
```
stroke: rgba(79, 70, 229, 0.25)
stroke-width: 1.5
stroke-dasharray: 4 3
fill: none
```
This is the connector pattern. Reuse it for any timeline or relationship visualization (e.g., pipeline detail panel update timeline).

---

## Aesthetic Principles

1. **Institutional restraint** — this reads like a fund document, not a startup landing page. The visual language communicates "we have already built this" rather than "imagine what we could build." New components must maintain this tone.

2. **Depth via shadow layering** — the three-layer shadow system is the primary spatial mechanism. Cards float on the off-white background. There are no hard drops, no colored shadows (except hover), no flat cards. Every surface has at least two shadow layers.

3. **Monospace as system voice** — JetBrains Mono signals "this is computed/structured data." It appears in labels, tags, metadata, table headers, code, and tier labels. DM Sans is the human voice for prose and headings. Never mix them. Never use monospace for headings or prose for metadata.

4. **Generous negative space** — 80px section padding, 40px header-to-content gaps, 24-28px card padding. This generosity is structural, not decorative. Reducing it makes the site feel like a dashboard. The pipeline page must maintain this breathing room even with higher information density.

5. **Gradient accents are rare and meaningful** — gradients appear in exactly four places: hero title, KPI values, nav brand, and section header left borders. They are never decorative. Adding gradient backgrounds, gradient borders on cards, or gradient text to body content would degrade the system.

6. **Color signals category, not decoration** — every color use is semantic. Cyan = scouting/perception. Purple = interpretation/thesis. Green = execution/confirmed. Red = risk/policy. These meanings must be maintained on the pipeline page (see Stage Badge Colors below).

7. **Light theme, no dark mode** — the `#f7f8fb` background with blue undertone, the dot grid, and the indigo glow are load-bearing. The spec's mention of "dark" for the pipeline page is incorrect and would break visual continuity.

---

## Pipeline Page: Design Guidance

Specific guidance for the `/pipeline` page to ensure visual consistency.

### What to reuse verbatim
- Full CSS variable system
- Navigation (add "Pipeline" link as `.active`)
- Section header pattern for page title
- Card pattern for project cards (hover lift, three-layer shadow)
- Tag pattern for stage badges and category pills
- Insight callout for "Why Fair flagged this" block
- Table pattern for any structured data in detail panel
- Mono label pattern for all metadata

### Stage Badge Colors (mapping to existing semantic palette)
| Stage | Color Token | Rationale |
|-------|-------------|-----------|
| Scouting | `--text-muted` (gray) | Lowest conviction, not yet evaluated |
| Researching | `--cyan` | Active investigation (matches Sourcing Analyst color) |
| Candidate | `--purple` | Thesis formed (matches Principal/thesis color) |
| Invested | `--primary` (indigo) | Committed (matches Fair/MD color) |

### Signal Strength Dots
- 5 small circles, `6px` diameter, `2px` gap
- Filled dots: `var(--primary)` — unfilled: `var(--border-bright)`
- Label above or beside: mono, 10px, uppercase, "SIGNAL" or "CONVICTION"
- Keep compact. This is a glanceable indicator, not a chart.

### Slide-in Panel
- Use `var(--surface)` background, not a modal overlay
- Width: ~40% of viewport, `transform: translateX(100%)` → `translateX(0)` animation
- Backdrop: `rgba(0,0,0,0.06)` over the pipeline list — barely dims, doesn't feel modal
- Panel border-left: `1px solid var(--border)` — it's a surface, not a popup
- Internal sections should use the section header pattern (smaller, ~22px H2) and spacing
- Close button: subtle, top-right, mono `x` or `ESC` hint

### Filter Bar
- Style as a row of pill toggles matching `nav a` link styling
- Active filter: `--primary` text + `--primary-dim` background (same as active nav)
- Inactive: `--text-dim`, `--surface2` background on hover
- Padding, radius, and font specs: identical to nav links

### Source Type Indicators
Do NOT use raw emoji for source types. The existing site uses emoji only inside the 44x44 `agent-icon` containers. For inline source indicators:
- Use mono text labels: `TWEET`, `ARTICLE`, `GITHUB`, `FARCASTER`
- Style as small artifact tags (dim background, mono 10px, appropriate color)

### Update Timeline
- Use the dashed connector pattern from the org chart (indigo at 0.25, dasharray 4 3)
- Each entry: date (mono, 10px) + event text (13px, `--text-dim`) + source link
- Pinned milestones: use a left-border accent (3px, `--primary`) to distinguish from regular updates
- Vertical connector line: 1.5px, `rgba(79, 70, 229, 0.15)`, left-aligned

### What NOT to do
- Do not use dark backgrounds. The spec mentions "dark" — ignore this.
- Do not introduce new animation patterns (no slide-ups, fades, or stagger animations beyond the existing hover lifts and panel slide)
- Do not add colored card backgrounds. Cards are always `var(--surface)` white.
- Do not use more than 3 accent colors on the pipeline page. Stick to: `--primary` (invested), `--purple` (candidate), `--cyan` (researching), `--text-muted` (scouting).
- Do not reduce spacing to "increase density." The generosity IS the design.
