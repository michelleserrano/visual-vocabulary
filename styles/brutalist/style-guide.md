# Brutalist Web Style Guide
**UI Styles Library — Version 1.0**  
Category: Anti-Design · Year of origin: 1990s web, revival ~2014

---

## Personality

**Five words:** Raw. Confrontational. Honest. Dense. Anti-decorative.

**Voice of this style:** "The interface says what it is. No metaphors, no shadows, no gradients. Every border is a hard truth. The browser's default is not a failure to overcome — it is the starting condition. Decoration is dishonesty."

**Use when:** Building content-first tools, developer utilities, anti-brand statements, Craigslist-tier classified interfaces, zines, portfolios that reject visual conformity, and any context where information density matters more than visual softness. Also excellent for accessibility: black on white at 21:1 is automatically WCAG AAA.

**Do NOT use when:**
- Consumer apps where warmth and approachability are required
- Brand contexts with established visual languages (gradients, curves, illustration)
- Mobile-first experiences where small touch targets need visual softening
- Any context where "friendly" and "inviting" are user experience requirements

---

## Quick Start — Copy & Paste

```css
:root {
  /* ── Palette ────────────────────────── */
  --bg:      #ffffff;    /* page and element background */
  --bg2:     #f0f0f0;    /* offset / hover / subtle fills */

  /* ── Text ──────────────────────────── */
  --t1:      #000000;    /* primary — pure black */
  --t2:      #1a1a1a;    /* body copy */
  --t3:      #555555;    /* muted / placeholders / metadata */

  /* ── Structural color ───────────────── */
  --ac:      #ff2222;    /* accent — active, focus, hover, alert */
  --ac2:     #0000ee;    /* link blue — use for hyperlinks only */
  --yellow:  #ffff00;    /* highlight — use sparingly */

  /* ── Shape — ZERO radius ────────────── */
  --r:       0px;        /* every element is a rectangle */

  /* ── Typography — system only ────────── */
  --f:       Arial, Helvetica, sans-serif;
  --f-mono:  'Courier New', Courier, monospace;
  --f-serif: Georgia, 'Times New Roman', serif;

  /* ── Border weight ──────────────────── */
  --bw:      3px;        /* primary border thickness */

  /* ── Motion ────────────────────────── */
  --ease:    cubic-bezier(0.4, 0, 0.2, 1);
}

/* The one non-negotiable rule */
*, *::before, *::after { border-radius: 0 !important; }

body {
  font-family: var(--f);
  background: var(--bg);
  color: var(--t1);
}
```

---

## Color Tokens

| Token | Value | Role |
|-------|-------|------|
| `--bg` | `#ffffff` | Page and element background |
| `--bg2` | `#f0f0f0` | Offset backgrounds (callouts, inputs at rest, hover) |
| `--t1` | `#000000` | Primary text — pure black |
| `--t2` | `#1a1a1a` | Body copy |
| `--t3` | `#555555` | Muted text / placeholders / labels |
| `--ac` | `#ff2222` | **The only accent.** Active states, focus rings, hover fills, alerts |
| `--ac2` | `#0000ee` | Browser-default link blue — use only on actual hyperlinks |
| `--yellow` | `#ffff00` | Highlight / callout fill — structural, never decorative |

**Critical rule:** Color serves information, not aesthetics. Red = action/active. Yellow = attention. Blue = link. Everything else is black on white.

---

## Border System

Borders are the depth language of brutalism. There are no shadows.

| Use | Value |
|-----|-------|
| Primary border | `3px solid #000` |
| Secondary / divider | `2px solid #000` |
| Fine rule | `1px solid #000` |
| Section header bottom | `3px solid #000` |
| Spec callout left | `4px solid #000` — with `background: #f0f0f0` |
| Card hover shadow | `box-shadow: 4px 4px 0 #000` |
| Nav bottom | `4px solid #000` |

**Rule:** Never use `box-shadow` for depth — only for the offset hover effect on cards (`4px 4px 0 #000`). No blur radius. No spread. No color other than black.

---

## Typography

**Typefaces:** Arial (system), Courier New (system), Georgia (system)  
**External fonts:** None. Do not load them. This is the philosophy.

| Level | Size | Weight | Font | Notes |
|-------|------|--------|------|-------|
| Display | 48px | 900 | Arial | All-caps, tight tracking |
| H1 | 36px | 700 | Arial | — |
| H2 | 28px | 700 | Arial | — |
| H3 | 22px | 700 | Arial | — |
| Body | 16px | 400 | Arial | lh 1.55 |
| Body SM | 14px | 400 | Arial | lh 1.5 |
| Label | 11px | 700 | Courier New | ALL-CAPS, +0.08–0.14em tracking |
| Mono | 14px | 400 | Courier New | Hex values, timestamps, code, IDs |

**Why Arial:** It is the most common system font. It is invisible in the best way — it carries meaning without personality. Using a custom typeface would be a decoration.

---

## Spacing Scale

| Step | px | rem | Use |
|------|----|-----|-----|
| 1 | 4px | 0.25rem | Tight details |
| 2 | 8px | 0.5rem | Icon–label gap |
| 3 | 12px | 0.75rem | Compact padding |
| 4 | 16px | 1rem | Standard padding |
| 5 | 20px | 1.25rem | Card inner padding |
| 6 | 24px | 1.5rem | Section padding |
| 8 | 32px | 2rem | Panel padding |
| 10 | 40px | 2.5rem | Generous vertical rhythm |
| 12 | 48px | 3rem | Section gaps |

---

## Component Snippets

### Primary Button

```css
.btn-primary {
  border: 3px solid #000;
  background: #000;
  color: #fff;
  padding: 0.75rem 1.75rem;
  font-family: Arial, sans-serif;
  font-weight: 700;
  font-size: 0.9375rem;
  text-transform: uppercase;
  letter-spacing: 0.06em;
  cursor: pointer;
  transition: background 0.12s, border-color 0.12s, transform 0.07s;
}
.btn-primary:hover:not(:disabled) {
  background: #ff2222;
  border-color: #ff2222;
}
.btn-primary:active:not(:disabled) { transform: translate(2px, 2px); }
.btn-primary:disabled              { opacity: 0.3; cursor: not-allowed; }
```

### Secondary Button

```css
.btn-secondary {
  border: 3px solid #000;
  background: #fff;
  color: #000;
  /* same padding / font as primary */
}
.btn-secondary:hover:not(:disabled) { background: #000; color: #fff; }
.btn-secondary:active:not(:disabled) { transform: translate(2px, 2px); }
```

### Input Field

```css
.input {
  background: #fff;
  border: 3px solid #000;
  padding: 0.75rem;
  font-family: Arial, sans-serif;
  font-size: 0.9375rem;
  color: #000;
  outline: none;
  width: 100%;
  transition: border-color 0.15s;
}
.input::placeholder { color: #555; }
.input:focus        { border-color: #ff2222; }
```

### Label (all inputs)

```css
.label {
  font-size: 0.6875rem;
  font-weight: 700;
  font-family: 'Courier New', monospace;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  color: #000;
}
```

### Card

```css
.card {
  border: 3px solid #000;
  background: #fff;
  overflow: hidden;
  transition: border-color 0.18s, box-shadow 0.18s;
}
.card:hover {
  border-color: #ff2222;
  box-shadow: 4px 4px 0 #000;  /* hard offset — no blur */
}
.card-rule {
  border: none;
  border-top: 3px solid #000;
  margin: 0.875rem 0;
}
```

### Toggle Switch (rectangle, not pill)

```css
.toggle-track {
  display: block;
  width: 56px; height: 24px;
  background: #fff;
  border: 3px solid #000;
  position: relative;
  cursor: pointer;
  transition: background 0.18s;
}
.toggle-thumb {
  position: absolute;
  top: 2px; left: 2px;
  width: 16px; height: 16px;
  background: #000;
  transition: transform 0.18s cubic-bezier(0.4, 0, 0.2, 1);
  /* border-radius: 0 already — rectangle slides, not pill */
}
input:checked + .toggle-track { background: #000; }
input:checked + .toggle-track .toggle-thumb {
  transform: translateX(32px);
  background: #ff2222;
}
```

### Spec Callout

```css
.spec-callout {
  border-left: 4px solid #000;
  background: #f0f0f0;
  padding: 1rem 1.25rem;
  display: flex;
  align-items: flex-start;
  gap: 0.875rem;
}
```

### Progress Dot (square, not circle)

```css
.prog-dot {
  width: 8px; height: 8px;
  border: 2px solid #000;
  background: transparent;
  cursor: pointer;
  /* border-radius: 0 — squares, not circles */
}
.prog-dot.active { background: #ff2222; border-color: #ff2222; }
```

---

## Guiding Principles

**1. Zero border-radius, always.**  
`border-radius: 0 !important` on `*` is not optional — it is the signature rule of brutalist web. Every softened corner is a lie. Every rounded button is an apology.

**2. Borders carry all depth.**  
No `box-shadow` for depth. No `z-index` theater. A heavier border communicates importance. A `4px solid` border says "primary." A `2px solid` says "secondary." The border system IS the information hierarchy.

**3. Color means something or it means nothing.**  
`#ff2222` (red) appears only on: active states, focus rings, hover fills on primary buttons, error conditions, and accent callouts. Yellow marks attention. Blue marks hyperlinks. Everything else is black on white. If a color doesn't carry meaning, remove it.

**4. System fonts are the philosophy, not a fallback.**  
Loading a custom typeface is a decoration. Arial is invisible — it serves the content without asserting itself. Courier New is legible, monospace, and honest about being machine-readable. These are the right tools.

**5. Information density is a virtue.**  
Brutalism does not require breathing room to function. Content can be dense because the borders provide clear structure. Whitespace is fine; whitespace for softening is unnecessary.

**6. Interactions work, they just look raw.**  
The offset press (`transform: translate(2px, 2px)`) works precisely. The toggle slides correctly. The focus ring is 3px solid red. Brutalism is not broken design — it is honest design. Every interaction must function perfectly; it simply won't look soft doing it.

---

## Do's

- **DO** use `border-radius: 0 !important` on `*` — no exceptions anywhere in the page
- **DO** use `3px solid #000` as the primary border on all interactive elements
- **DO** use `transform: translate(2px, 2px)` for the press state on all buttons
- **DO** set `border-color: #ff2222` on focus — never `outline` with a glow
- **DO** use Courier New for all labels, metadata, hex values, and monospace contexts
- **DO** put a `3px solid #000` horizontal rule between card titles and card body text
- **DO** use `4px 4px 0 #000` (hard offset, no blur) for card hover elevation

---

## Don'ts

- **DON'T** use `border-radius` anywhere. Not 2px, not 4px, not 50%. Zero.
- **DON'T** use `box-shadow` with a blur radius for depth — the 4px card hover is the only exception, and it has no blur
- **DON'T** use `background: linear-gradient` anywhere — fills are flat
- **DON'T** load external fonts — Arial and Courier New are the full type system
- **DON'T** use `rgba(0,0,0,0.X)` colored borders — borders are `solid #000` or `solid var(--ac)` only
- **DON'T** use more than two accent colors (red and yellow). `--ac2` blue is only for actual hyperlinks
- **DON'T** soften interactions with spring easing — `cubic-bezier(0.4, 0, 0.2, 1)` is sufficient
- **DON'T** confuse "brutalist" with "broken" — spacing, hierarchy, and interactions must all work correctly

---

## Anti-Patterns to Reject Immediately

If any AI-generated output includes these, reject it and re-prompt:

- `border-radius: Xpx` on any element — always zero
- `box-shadow: rgba(0,0,0,0.X) Ypx Zpx Wpx` — blurred shadow is forbidden
- `background: linear-gradient(...)` — no gradients
- `font-family: 'Inter'` or any Google Font — system fonts only
- `transition: all 0.3s ease` — always specify the property; use `var(--ease)`
- Red (`#ff2222`) used as a background fill on non-interactive, non-active elements
- Soft placeholder text without a thick border on the input itself
- Toggle switches with rounded ends (use `border-radius: 0 !important`)

---

## AI Prompting Guidance

Use this block to instruct any AI coding agent to reproduce this style:

```
Build in Brutalist Web style:
- Zero border-radius on everything: *, *::before, *::after { border-radius: 0 !important }
- All borders: 3px solid #000 for primary interactive elements, 2px for secondary/dividers
- No box-shadow for depth — only 4px 4px 0 #000 (no blur) for card hover offset
- No gradients, no fills other than #fff, #f0f0f0, #000, #ff2222, #ffff00
- Colors: #ff2222 = active/hover/focus ONLY; #ffff00 = highlight ONLY; #0000ee = hyperlinks ONLY
- Fonts: Arial for body/headings, Courier New for labels/metadata/mono — NO external fonts
- Primary button: border:3px solid #000; background:#000; color:#fff; hover→background:#ff2222
- Secondary button: border:3px solid #000; background:#fff; color:#000; hover→invert
- Press state on all buttons: transform: translate(2px, 2px)
- Focus: border-color: #ff2222 on inputs; outline: 3px solid #ff2222 on buttons
- Labels: all-caps, Courier New, 0.08–0.14em letter-spacing
- Card hover: border-color:#ff2222; box-shadow: 4px 4px 0 #000
- Toggles: rectangles that slide — NOT pills. Track: 56×24px, border:3px solid #000
- Spec callouts: border-left:4px solid #000; background:#f0f0f0
- Progress indicator dots: 8×8px squares with border:2px solid #000; active: background:#ff2222
```
