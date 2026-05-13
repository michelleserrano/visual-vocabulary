# Bento Box Style Guide
**UI Styles Library — Version 2.0**  
Category: Compositional · Year of origin: 2022 (Apple iOS 16 Home Screen widget grid)

---

## Personality

**Five words:** Modular. Apple. Compositional. Asymmetric-grid. Marketing-page-as-aesthetic.

**Voice of this style:** "Layout is the aesthetic. Each cell is a self-contained moment — a stat, a quote, a feature, a fill. The interest comes from the composition itself, not from material treatments. Generous radius, near-zero borders, a single accent color, and SF Pro tracked tight."

**Use when:** Marketing landing pages (iPhone 15 Pro page, Linear, Raycast, Vercel, OpenAI), product overviews, dashboard summaries, content hubs, anywhere you want to communicate breadth and variety without filling the screen with text. Bento naturally implies "there's a lot here, organized." Designers reach for it when the message is *richness through modularity*.

**Do NOT use when:**
- Linear flows that should feel continuous (forms, checkout, reading)
- Data-dense apps where the overhead of cell chrome wastes screen real estate
- Brands that need a strong, distinctive visual voice — bento is the *default* now, so it can read as undifferentiated

---

## Quick Start — Copy & Paste

```css
:root {
  /* ── Surfaces ──────────────────────── */
  --bg:           #f5f5f7;     /* Apple marketing off-white */
  --bg-dark:      #000000;     /* dark mode bento */
  --surface-1:    #ffffff;     /* card surface (light) */
  --surface-2:    #1d1d1f;     /* Apple near-black (cards in dark mode, accent fills) */
  --surface-3:    #fbfbfd;     /* faint tint for hover */

  /* ── iOS 6-color system (cell fills) ─ */
  --surface-blue:   #0071e3;   /* THE accent */
  --surface-purple: #5856d6;
  --surface-orange: #ff9500;
  --surface-green:  #34c759;
  --surface-pink:   #ff2d55;
  --surface-teal:   #5ac8fa;
  --surface-indigo: #4a3aff;
  --surface-yellow: #ffd60a;
  --surface-red:    #ff3b30;

  /* ── Text ──────────────────────────── */
  --t1:    #1d1d1f;            /* Apple charcoal */
  --t2:    #515154;
  --t3:    #86868b;
  --t-inv: #f5f5f7;            /* on dark surfaces */

  /* ── Accent (the only one) ─────────── */
  --ac:        #0071e3;
  --ac-hi:     #0077ed;
  --ac-active: #006edb;

  /* ── Borders ───────────────────────── */
  --border:      1px solid rgba(0,0,0,0.06);    /* near-invisible hairline */
  --border-dark: 1px solid rgba(255,255,255,0.08);

  /* ── Radius (generous) ─────────────── */
  --r-sm:   12px;
  --r:      18px;
  --r-md:   24px;              /* default cell radius */
  --r-lg:   32px;
  --r-xl:   40px;
  --r-full: 9999px;

  /* ── Grid ──────────────────────────── */
  --gap:    12px;              /* tight gutters */
  --gap-lg: 16px;

  /* ── Type ──────────────────────────── */
  --f-disp: 'SF Pro Display', -apple-system, BlinkMacSystemFont, 'Inter', sans-serif;
  --f:      'SF Pro Text',    -apple-system, BlinkMacSystemFont, 'Inter', sans-serif;
  --f-mono: 'SF Mono', 'JetBrains Mono', ui-monospace, monospace;

  /* ── Motion ────────────────────────── */
  --ease:   cubic-bezier(0.4, 0, 0.2, 1);
  --spring: cubic-bezier(0.32, 0.72, 0, 1);   /* Apple's spring */
  --dur:    200ms;
}

body {
  font-family: var(--f);
  background: var(--bg);
  color: var(--t1);
  letter-spacing: -0.011em;            /* THE body tracking rule */
  -webkit-font-smoothing: antialiased;
}
```

**Google Fonts fallback** (use Inter when SF isn't available):

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800;900&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
```

---

## THE Bento Grid Recipe

The single most important code in this entire style guide:

```css
.bento {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: 180px;
  gap: var(--gap);
}

.bento-cell {
  background: var(--surface-1);
  border: var(--border);
  border-radius: var(--r-md);
  padding: 1.5rem;
  display: flex;
  flex-direction: column;
  position: relative;
  overflow: hidden;
  transition: transform 0.32s var(--spring),
              box-shadow 0.32s var(--ease);
}
.bento-cell:hover {
  transform: translateY(-2px);
  box-shadow: 0 10px 28px rgba(0,0,0,0.06);
}

/* Span classes — vary these to compose */
.bento-cell.span-2x1 { grid-column: span 2; }
.bento-cell.span-3x1 { grid-column: span 3; }
.bento-cell.span-4x1 { grid-column: span 4; }
.bento-cell.span-1x2 { grid-row: span 2; }
.bento-cell.span-2x2 { grid-column: span 2; grid-row: span 2; }
.bento-cell.span-3x2 { grid-column: span 3; grid-row: span 2; }

/* Tonal variants */
.bento-cell.dark {
  background: var(--surface-2);
  color: var(--t-inv);
  border-color: rgba(255,255,255,0.08);
}
```

**Critical numbers:**
- 4 columns. Always. (Drop to 2 columns at ≤900px, 1 column at ≤560px.)
- 180px row height. (Cells span integer multiples — never fractional.)
- 12px gap. (Tighter than typical Tailwind grids.)
- 24px radius on the cell, not 16px and not 32px. The default radius IS the look.
- 1.5rem (24px) inner padding.

---

## The 6 Cell Types — Catalog

A bento page is a composition of these six cell archetypes. Mix at least 4 in any single grid.

| # | Type | Anatomy | When |
|---|------|---------|------|
| 1 | **Stat** | Huge number (5rem, weight 700, tracking −0.045em) at top, small label below | Hero claim, proof point, "X+" / "Y%" / "Zk users" |
| 2 | **Quote** | Open-quote glyph in iOS blue, italic SF Pro Display 500 pull quote, small mono attribution | Testimonials, manifestos, marketing voice |
| 3 | **Fill** | Solid Apple system color (or 2-color gradient) with white name + hex | Color visualization, decorative breaks, icon backgrounds |
| 4 | **Feature** | Tinted icon top-left → SF Pro Display 600 title → 13px description | Feature lists, capability bullets, the workhorse cell |
| 5 | **Chart** | Subtle SVG line/bar/sparkline, usually paired with a stat or label | Data moments, trends, metrics |
| 6 | **CTA** | iOS-blue-filled cell, centered text, optional secondary button | "Try it", "Get the app", section closers |

### Stat cell

```css
.cell-stat { justify-content: space-between; }
.stat-num {
  font-family: var(--f-disp);
  font-size: clamp(3.5rem, 7vw, 5rem);
  font-weight: 700;
  letter-spacing: -0.045em;
  line-height: 0.95;
  color: var(--t1);
  font-feature-settings: "tnum" on;
}
.stat-num .small { font-size: 0.4em; color: var(--t3); }
.stat-label {
  font-size: 0.875rem;
  font-weight: 500;
  color: var(--t2);
}
```

### Quote cell

```css
.quote-mark {
  font-family: var(--f-disp);
  font-size: 3.5rem;
  font-weight: 700;
  line-height: 0.6;
  color: var(--ac);
}
.quote-text {
  font-family: var(--f-disp);
  font-style: italic;
  font-weight: 500;
  font-size: 1.375rem;
  letter-spacing: -0.022em;
  line-height: 1.25;
}
.quote-attr {
  font-family: var(--f-mono);
  font-size: 0.6875rem;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  color: var(--t3);
}
```

### Feature cell (icon → title → desc)

```css
.cell-feature { gap: 0.5rem; justify-content: space-between; }
.feat-icon {
  width: 40px; height: 40px;
  border-radius: 11px;
  display: flex; align-items: center; justify-content: center;
  background: rgba(0,113,227,0.08);
  color: var(--ac);
}
.feat-title {
  font-family: var(--f-disp);
  font-size: 1.25rem;
  font-weight: 600;
  letter-spacing: -0.022em;
}
.feat-desc {
  font-size: 0.8125rem;
  line-height: 1.45;
  color: var(--t2);
}
```

### Spec callout (a bento cell with iOS blue accent bar)

```css
.spec-callout {
  background: var(--surface-1);
  border: var(--border);
  border-radius: var(--r-md);
  padding: 1rem 1.25rem 1rem 1.5rem;
  position: relative;
  overflow: hidden;
}
.spec-callout::before {
  content: '';
  position: absolute;
  left: 0; top: 0; bottom: 0;
  width: 4px;
  background: var(--ac);
}
```

---

## iOS Color System

Apple's six system colors — used as cell fills, never as text on white.

| Token | Hex | Role |
|-------|-----|------|
| `--surface-blue` | `#0071e3` | **THE accent.** All buttons, links, focus rings, active states. |
| `--surface-purple` | `#5856d6` | Secondary fill, often paired with blue in gradients |
| `--surface-orange` | `#ff9500` | Warmth, energy, "download" type CTAs |
| `--surface-green` | `#34c759` | Success, positive metric, on-state of toggles |
| `--surface-pink` | `#ff2d55` | Like, favorite, romance |
| `--surface-teal` | `#5ac8fa` | Cool, tech, often the secondary in dark-mode bento |
| `--surface-yellow` | `#ffd60a` | Warning, accent — text stays dark on this fill |
| `--surface-red` | `#ff3b30` | Destructive only |
| `--surface-indigo` | `#4a3aff` | Pairs with blue in gradients |

### Light / Dark surfaces

| Token | Hex | Use |
|-------|-----|-----|
| `--bg` | `#f5f5f7` | Page background (light) |
| `--bg-dark` | `#000000` | Page background (dark) |
| `--surface-1` | `#ffffff` | Light cell |
| `--surface-2` | `#1d1d1f` | Dark cell (the "Apple charcoal") |
| `--surface-3` | `#fbfbfd` | Faint hover tint |

**Critical rule:** Use *one* accent across the whole page. iOS blue. Other system colors appear *only* in fill cells (color-fill cards). Never use orange or pink as a text color or button.

---

## SF Pro Typography Scale

**Typeface:** SF Pro Display (headings) + SF Pro Text (body). Native on Apple platforms; fall back to `-apple-system, BlinkMacSystemFont, 'Inter'` everywhere else.

**Why SF Pro:** It IS the Apple voice. The optical scale switches between Display (≥20pt) and Text (<20pt) automatically — Display has tighter spacing and smaller x-height, Text is built for legibility at small sizes.

| Level | Size | Weight | Letter-spacing | Line-height | Use |
|-------|------|--------|----------------|-------------|-----|
| Display | 80px+ | 700 | **−0.045em** | 0.96 | Hero headlines |
| H1 | 40px | 700 | **−0.035em** | 1.04 | Section titles |
| H2 | 30px | 600 | **−0.025em** | 1.1 | Subheads, cell hero text |
| H3 | 22px | 600 | **−0.022em** | 1.18 | Feature titles |
| H4 | 18px | 600 | −0.018em | 1.25 | Card titles |
| Body LG | 18px | 400 | −0.011em | 1.5 | Lead paragraphs |
| **Body** | **17px** | **400** | **−0.011em** | **1.5** | **Apple body size — the default** |
| Body SM | 15px | 400 | −0.011em | 1.45 | Secondary copy |
| Caption | 13px | 500 | −0.005em | 1.4 | Field labels |
| Mono kicker | 11px | 500 | **+0.08em UC** | 1.4 | iOS-blue uppercase labels (`01 · COLORS`) |

### THE tracking rule (memorize this)

```
Display (>3rem)   →  letter-spacing: -0.04em  to  -0.045em
Heading (1.5–3rem) →  letter-spacing: -0.022em to  -0.025em
Body                →  letter-spacing: -0.011em
Mono kicker         →  letter-spacing:  0.08em (positive, uppercase)
```

This single rule is what distinguishes Apple-tracked SF from an amateur SF use. Without negative tracking on display, the headlines look loose and webby. Without `-0.011em` on body, the page reads as not-Apple.

**No serifs anywhere.** Bento is a sans-serif aesthetic.

---

## Spacing Scale

| Step | px | rem | Use |
|------|----|-----|-----|
| 1 | 4px | 0.25rem | Icon–text micro gap |
| 2 | 8px | 0.5rem | Tight stacking inside a cell |
| 3 | 12px | 0.75rem | **Bento gutter** (`--gap`) |
| 4 | 16px | 1rem | Larger gutters, stat→label spacing |
| 5 | 24px | 1.5rem | **Default cell padding** |
| 6 | 32px | 2rem | Hero cell padding |
| 7 | 64px | 4rem | Section vertical rhythm (top of `.sec`) |
| 8 | 96px | 6rem | Between major sections |

---

## Border Radius

| Token | px | Use |
|-------|----|-----|
| `--r-sm` | 12px | Small icons, tags, chips |
| `--r` | 18px | Buttons, inputs |
| `--r-md` | **24px** | **Default cell radius** |
| `--r-lg` | 32px | Hero cell, large feature cards |
| `--r-xl` | 40px | Special — full-bleed showcases |
| `--r-full` | 9999px | Pills, toggle tracks, circular icons |

**Rule:** Cells are 24px. Always. Don't mix radii within a single bento — the rhythmic uniformity of corners is what makes the composition feel "Apple" rather than "Tailwind cards".

---

## Motion & Easing

| Token | Value | Use |
|-------|-------|-----|
| `--ease` | `cubic-bezier(0.4, 0, 0.2, 1)` | Color, opacity, shadow transitions |
| `--spring` | `cubic-bezier(0.32, 0.72, 0, 1)` | **Apple's spring.** Transform, scale, hover lifts |
| Cell hover | 320ms spring + `translateY(-2px)` | Every cell |
| Button hover | 180ms spring + `scale(1.02)` | Primary buttons |
| Button press | 180ms spring + `scale(0.97)` | All buttons |
| Toggle thumb | 320ms spring | iOS switch |
| Focus halo | 180ms ease | Input focus |

**Motion philosophy:** Quiet, springy, optical. Cells lift slightly on hover. Buttons scale by 2%. Toggle thumbs snap. Nothing bounces theatrically — Apple's spring is `(0.32, 0.72, 0, 1)`, not the bouncy `(0.34, 1.56, 0.64, 1)` of neumorphism.

---

## Component Snippets

### Primary button (iOS pill)

```css
.btn-primary {
  background: var(--ac);
  color: #fff;
  border: none;
  border-radius: 9999px;          /* always pill */
  padding: 0.625rem 1.25rem;
  font-family: var(--f);
  font-size: 0.9375rem;
  font-weight: 500;
  letter-spacing: -0.011em;
  cursor: pointer;
  transition: background 0.2s var(--ease),
              transform 0.18s var(--spring);
}
.btn-primary:hover  { background: var(--ac-hi);     transform: scale(1.02); }
.btn-primary:active { background: var(--ac-active); transform: scale(0.97); }
```

### Secondary / Ghost / Destructive

```css
.btn-secondary {
  background: var(--surface-1); color: var(--t1);
  border: var(--border);
  /* same radius, padding, font as primary */
}
.btn-ghost {
  background: transparent; color: var(--ac);
}
.btn-ghost:hover { background: rgba(0,113,227,0.08); }

.btn-destructive {
  background: var(--surface-red); color: #fff;
}
```

### Form input (with Apple's focus halo)

```css
.inp {
  background: var(--surface-1);
  color: var(--t1);
  font-family: var(--f);
  font-size: 0.9375rem;
  letter-spacing: -0.011em;
  padding: 0.625rem 0.875rem;
  border: 1px solid rgba(0,0,0,0.1);
  border-radius: var(--r);                 /* 18px */
  outline: none;
  transition: border-color 0.18s var(--ease),
              box-shadow   0.18s var(--ease);
}
.inp:focus {
  border-color: var(--ac);
  box-shadow: 0 0 0 4px rgba(0,113,227,0.18);   /* THE halo */
}
```

The 4px iOS-blue translucent halo is the most-recognized Apple focus signal. Keep it.

### Round iOS checkbox

```css
.ck-circle {
  width: 22px; height: 22px;
  border-radius: 50%;
  border: 1.5px solid rgba(0,0,0,0.18);
  background: var(--surface-1);
}
input:checked + .ck-circle {
  background: var(--ac);
  border-color: var(--ac);
}
```

### iOS toggle switch (51×31 — exact iOS dimensions)

```css
.tgl-track {
  width: 51px; height: 31px;
  background: rgba(120,120,128,0.16);
  border-radius: 9999px;
  transition: background 0.28s var(--ease);
}
.tgl-thumb {
  position: absolute; top: 2px; left: 2px;
  width: 27px; height: 27px;
  border-radius: 50%; background: #fff;
  box-shadow: 0 3px 8px rgba(0,0,0,0.15);
  transition: transform 0.32s var(--spring);
}
input:checked ~ .tgl-track { background: var(--surface-green); }
input:checked ~ .tgl-track .tgl-thumb { transform: translateX(20px); }
```

iOS toggles are **green** when on (not the page accent). This is one of the very few cases the page's iOS-blue accent rule is broken — and it's broken intentionally because that's the iOS pattern.

### Range slider (gradient-filled track)

```css
.rng {
  -webkit-appearance: none;
  width: 100%; height: 4px;
  background: rgba(0,0,0,0.08);
  border-radius: 9999px;
  cursor: pointer;
}
.rng::-webkit-slider-runnable-track {
  height: 4px;
  background: linear-gradient(to right,
    var(--ac) 0%, var(--ac) var(--p, 30%),
    rgba(0,0,0,0.08) var(--p, 30%), rgba(0,0,0,0.08) 100%);
  border-radius: 9999px;
}
.rng::-webkit-slider-thumb {
  -webkit-appearance: none;
  width: 14px; height: 14px;
  border-radius: 50%;
  background: #fff;
  box-shadow: 0 2px 6px rgba(0,0,0,0.18);
  margin-top: -5px;
}
```

(The `--p` CSS variable is updated from JS to recolor the track on input.)

---

## Light + Dark Mode

The bento aesthetic flips beautifully — same grid, same spans, same radius — surface tokens swap.

```css
/* Dark mode bento */
:root.dark, [data-theme="dark"] {
  --bg:        #000000;
  --surface-1: #1d1d1f;
  --surface-3: #2c2c2e;
  --t1:        #f5f5f7;
  --t2:        #aeaeb2;
  --t3:        #6c6c70;
  --border:    1px solid rgba(255,255,255,0.08);
  /* iOS color fills stay the same — they were calibrated to work on both */
}
```

Apple's iPhone 15 Pro page uses dark-mode bento as its primary visualization layer (see "Titanium" and "A17 Pro" sections). Both modes are equally important.

---

## Guiding Principles

**1. Layout IS the aesthetic.**  
The composition does the work. Don't add gradients, glows, frosted glass, or material treatments to compensate. A clean white card on white background, with one cell turned dark and one cell filled blue, IS a complete bento — the mosaic of cell types and spans is what creates visual interest.

**2. One accent. Always iOS blue.**  
`#0071e3` is for: buttons, links, focus rings, mono kickers, the spec callout bar, and the active state of any tab. Other system colors (orange/pink/green) appear *only* as fill-cell backgrounds. Never as text on white. Never as a second button color.

**3. Vary the spans.**  
A bento with 8 equal cells is a Tailwind grid, not a bento. Always include at least one 2×2, one 2×1, and several 1×1 — the rhythm of varied spans is the signature. If all your cells are the same size, you're missing the style.

**4. Tracking is the language.**  
−0.045em on display, −0.022em on heading, −0.011em on body. Without these tracks, the type doesn't read as Apple — it reads as generic SF Pro. The tracking rule is non-negotiable.

**5. Generous radius, near-zero borders.**  
24px corners. 1px solid rgba(0,0,0,0.06) borders — barely visible. The cell shape is what reads, not its outline. Increasing the border opacity above 0.08 destroys the look.

**6. Mix at least 4 of the 6 cell types.**  
A bento with 5 stat cells = a stat dashboard. A bento with 5 quotes = a testimonials page. A bento mixes stat + feature + quote + fill + chart — the *variety* of content surfaces is what makes it feel like an iPhone marketing page.

---

## Do's

- **DO** use a 4-column, 180px-row grid as the base. Drop to 2 columns at ≤900px.
- **DO** vary cell spans (1×1, 1×2, 2×1, 2×2). At least one large hero cell per bento.
- **DO** use SF Pro Display with **negative tracking** on every heading.
- **DO** put one fill-color cell per bento for visual punctuation.
- **DO** use the 4px iOS-blue focus halo on every input and focusable element.
- **DO** keep cell padding at 24px. Less feels cramped, more wastes the cell.
- **DO** give cells a 320ms spring `translateY(-2px)` on hover. The lift is what makes them feel touchable.

---

## Don'ts

- **DON'T** use a symmetric grid. If every cell is the same size, you've left bento and entered Tailwind cards.
- **DON'T** use heavy borders. Anything above `rgba(0,0,0,0.08)` reads as outlined cards, not bento.
- **DON'T** use a second accent color for buttons or links. iOS blue or nothing.
- **DON'T** use a serif typeface anywhere. Bento is a SF Pro / Inter aesthetic only.
- **DON'T** use small radius (≤16px). The generous 24px is what makes cells feel like widgets, not panels.
- **DON'T** fill every cell with a color. Most cells should be plain white — the colored fills are *punctuation*, not the composition.
- **DON'T** forget the mono kicker. Each section needs an `01 · COLORS` style label in iOS blue, +0.08em uppercase, above the heading.

---

## Anti-Patterns to Reject Immediately

If any AI-generated output includes these, reject it and re-prompt:

- **Symmetric 3×3 or 4×4 equal-cell grid** — that's a Tailwind grid. Bento *requires* varied spans.
- **`border-radius: 8px` or `12px` on cells** — too small. Cells are 24px.
- **Multiple accent colors used as buttons** — only iOS blue.
- **`box-shadow: 0 1px 3px ...` chrome on every cell** — bento is borderless+hairline, not Material elevation.
- **Heading without negative letter-spacing** — feels generic, not Apple.
- **Body text at 16px instead of 17px** — small but real difference.
- **Serif typeface** — wrong family entirely.
- **A "header" outside the grid + cells inside** — the heading should sit above the bento, but the *largest cell IS the headline cell* on hero bentos.
- **Frosted glass / glassmorphism on cells** — that's a different style; bento cells are opaque.

---

## AI Prompting Guidance

Use this block to instruct any AI coding agent to reproduce this style:

```
Build in Bento Box style (Apple iOS 16+ widget grid → landing page layout language):

LAYOUT
- Use CSS Grid: 4 columns × 180px rows, 12px gap
- Each section is its own bento — render typography/buttons/forms as bento compositions, not inline stacks
- Vary spans: include at least one 2×2, one 2×1, and several 1×1 cells per bento
- Drop to 2 columns at ≤900px and 1 column at ≤560px

CELLS
- Background: #ffffff (light) or #1d1d1f (dark cell)
- Border: 1px solid rgba(0,0,0,0.06) — hairline only
- Border-radius: 24px (default) — never less
- Padding: 1.5rem (24px)
- Hover: translateY(-2px) + box-shadow 0 10px 28px rgba(0,0,0,0.06), 320ms cubic-bezier(0.32,0.72,0,1)

CELL TYPES (use 4+ per composition)
- Stat: huge SF Pro Display 700 number at 5rem, -0.045em tracking, small label below
- Quote: iOS-blue open quote glyph, italic SF Pro Display 500 at 1.375rem -0.022em, mono attribution
- Fill: solid Apple system color (blue/purple/orange/green/pink/teal) with white name + hex
- Feature: tinted icon top-left → SF Pro Display 600 title 1.25rem -0.022em → 13px description
- Chart: small SVG sparkline paired with stat
- CTA: iOS-blue-filled cell, white centered text

COLORS
- Background: #f5f5f7 (Apple marketing off-white)
- Cards: #ffffff or #1d1d1f
- ONE accent: iOS blue #0071e3 — buttons, links, focus, mono kickers
- iOS system colors (#5856d6 #ff9500 #34c759 #ff2d55 #5ac8fa #ffd60a) only as cell fills
- Never use 2 accents as buttons; never use system colors as text on white

TYPOGRAPHY
- SF Pro Display (headings) / SF Pro Text (body) / SF Mono (kickers)
- Body 17px, weight 400, letter-spacing -0.011em
- Headings 700 weight, letter-spacing -0.045em on display, -0.022em on H2/H3, -0.011em on body
- Mono kickers: SF Mono, 11px, weight 500, letter-spacing 0.08em, UPPERCASE, color iOS blue
- No serifs

BUTTONS
- Pill shape (border-radius: 9999px)
- Primary: background #0071e3, white text, padding 0.625rem 1.25rem, weight 500
- Hover: background #0077ed, transform scale(1.02), 180ms spring
- Active: background #006edb, transform scale(0.97)
- Secondary: white pill with 1px hairline border, t1 text
- Ghost: transparent, iOS blue text, hover tinted bg
- Destructive: iOS red #ff3b30 pill

FORMS
- Inputs: white surface, 1px rgba(0,0,0,0.1) border, 18px radius
- Focus: border #0071e3 + box-shadow 0 0 0 4px rgba(0,113,227,0.18) — Apple's focus halo
- Round (50%) checkboxes, iOS blue when checked
- iOS toggle: 51×31 pill, green (#34c759) on, white thumb 27×27, 320ms spring

ANCHOR PHRASES (use these to lock the aesthetic)
- "iPhone 15 Pro marketing page"
- "Apple iOS 16 Home Screen widget grid"
- "asymmetric modular bento composition"
- "SF Pro tight tracking, generous radius, hairline borders"
- "one accent — iOS blue — across the entire page"
```

---

## References

- **Apple iPhone 15 Pro page** — `apple.com/iphone-15-pro/` — the canonical reference
- **Linear** — `linear.app` — bento marketing applied to a software product
- **Raycast** — `raycast.com` — dark-mode bento done well
- **Vercel** — `vercel.com` — bento with subtle gradients
- **OpenAI** — `openai.com` — bento with editorial restraint
- **Apple Watch Series 10 page** — current best-in-class dark-mode bento
