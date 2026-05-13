# Art Deco · UI Style Guide

**Personality:** Opulent. Geometric. Nocturnal. Symmetrical. Jazz Age.

> "Deco is the architecture of confidence — every line is deliberate, every ornament earns its place."

---

## Identity

Art Deco emerged in the 1920s as a synthesis of modernism and luxury. It rejected the organic curves of Art Nouveau in favor of geometric precision, symmetry, and the glamour of new materials — chrome, lacquer, gold leaf. The Chrysler Building is the canonical reference: dark base, warm gold ornament, mathematical step forms.

For UI: translate this as deep dark backgrounds, a single warm gold accent, hard rectangular geometry, and a typographic duet between an elegant serif and a geometric sans.

---

## Design Tokens

```css
:root {
  /* ── Backgrounds (warm dark scale) ── */
  --bg:        #1a1206;   /* deep near-black, warm brown undertone */
  --s1:        #221808;   /* primary surface */
  --s2:        #2e2010;   /* raised surface / callout background */
  --s3:        #3a2a18;   /* hover surface */

  /* ── Gold system (one metal, all states) ── */
  --gold:      #c8a84b;   /* matte gold — primary accent */
  --gold-hi:   #e8c870;   /* gold hover / highlight */
  --gold-lo:   rgba(200,168,75,0.18);  /* gold tint for fills */

  /* ── Text (cream scale) ── */
  --cream:     #f5e6c8;
  --t1:        #f5e6c8;               /* primary text */
  --t2:        rgba(245,230,200,0.65); /* muted text */
  --t3:        rgba(245,230,200,0.35); /* faint text / labels */
  --t4:        rgba(245,230,200,0.18); /* placeholder / ghost */

  /* ── Borders ── */
  --border:    1px solid rgba(200,168,75,0.22);
  --border-hi: 1px solid rgba(200,168,75,0.5);

  /* ── Geometry: ZERO radius ── */
  --r:         0px;
  --r-sm:      0px;
  --r-md:      0px;
  --r-full:    0px;

  /* ── Typography ── */
  --f-display: 'Cormorant Garamond', Georgia, serif;
  --f:         'Jost', 'Helvetica Neue', sans-serif;
  --f-mono:    'Courier New', monospace;

  /* ── Motion ── */
  --ease:      cubic-bezier(0.4,0,0.2,1);
  --spring:    cubic-bezier(0.34,1.56,0.64,1);

  /* ── Gold glow (use on hover/active only) ── */
  --glow-gold: 0 0 16px rgba(200,168,75,0.4), 0 0 4px rgba(200,168,75,0.6);
}
```

---

## Gold System

Gold in Art Deco is never yellow. It is warm, desaturated, metallic.

| Token | Value | Use |
|-------|-------|-----|
| `--gold` | `#c8a84b` | Default accent: borders, icons, labels, fills |
| `--gold-hi` | `#e8c870` | Hover state for gold elements |
| `--gold-lo` | `rgba(200,168,75,0.18)` | Background tints, hover fills |
| `--glow-gold` | `0 0 16px … 0 0 4px …` | Box-shadow on hover/active for gold elements |
| Border default | `rgba(200,168,75,0.22)` | Resting border — present but subtle |
| Border hi | `rgba(200,168,75,0.5)` | Hover / focus border |

**Rules:**
- Gold is the **only** accent. Never introduce a secondary hue (no blue, no red).
- Gold borders at rest: `0.22` opacity. On hover: `0.5`. On active: `1.0`.
- Gold fills: only for Primary buttons and checked checkboxes.
- Gold glow: only on interactive hover — not on static decorative elements.

---

## Typography Duet

Two typefaces. No substitutions.

### Cormorant Garamond — Display
- **Role:** H1–H3, card titles, player title, form panel title, hero H1
- **Weights used:** 400 (body italic), 500 (subheads), 600 (standard display), 700 (hero italic)
- **Key rules:** Always letter-space slightly (`+0.02em` to `+0.04em`). Italic is correct for hero H1. Never use below 18px.
- **Why:** Cormorant has the proportions of 1920s hotel signage — tall, narrow, luxurious.

```css
/* Display hero */
font-family: var(--f-display);
font-size: clamp(4rem, 10vw, 7rem);
font-weight: 700;
font-style: italic;
letter-spacing: 0.02em;

/* Section H2 */
font-family: var(--f-display);
font-size: 1.375rem;
font-weight: 600;
letter-spacing: 0.04em;
```

### Jost — Body & Labels
- **Role:** All body copy, labels, eyebrows, captions, buttons, nav tabs
- **Weights used:** 300 (body text), 400 (default body), 500 (labels), 600 (eyebrows/buttons), 700 (nav active)
- **Key rules:** Labels always uppercase + `letter-spacing: 0.12em` minimum. Button text: `0.15em`. Captions: `0.18em`.
- **Why:** Jost is a geometric sans with the same mathematical DNA as Deco architecture.

```css
/* Body */
font-family: var(--f);
font-size: 0.9375rem;
font-weight: 300;
line-height: 1.75;

/* Label / eyebrow */
font-family: var(--f);
font-size: 0.5625rem;
font-weight: 500;
letter-spacing: 0.12em;
text-transform: uppercase;
color: var(--t3);
```

---

## Geometric Ornaments

Art Deco uses symmetrical geometric motifs. Implement in CSS — no image dependencies.

```css
/* Diamond ornament for section headers */
.sec-hd::before {
  content: '◆ ◆ ◆';
  display: block;
  font-size: 0.4rem;
  letter-spacing: 0.5em;
  color: var(--gold);
  margin-bottom: 0.625rem;
}

/* Gold horizontal rule — gradient fade */
.gold-rule {
  height: 1px;
  background: linear-gradient(90deg, transparent, var(--gold), transparent);
  margin: 1rem 0;
  border: none;
}

/* Double-line ornament */
.ornament {
  border-top: 1px solid var(--gold);
  border-bottom: 1px solid var(--gold);
  padding: 2px 0;
  margin: 0.5rem 0;
}

/* Progress dot diamond (side nav) */
.prog-dot {
  width: 7px;
  height: 7px;
  background: transparent;
  border: 1px solid rgba(200,168,75,0.4);
  transform: rotate(45deg); /* ZERO border-radius — hard corners */
  border-radius: 0;
}
.prog-dot.active {
  background: var(--gold);
  box-shadow: var(--glow-gold);
}

/* Nested inner border (double-frame motif) */
.framed {
  border: 1px solid var(--gold);
  position: relative;
}
.framed::before {
  content: '';
  position: absolute;
  inset: 5px;
  border: 1px solid rgba(200,168,75,0.2);
}

/* Crosshatch pattern for backgrounds */
.crosshatch {
  background-image:
    repeating-linear-gradient(45deg,  rgba(200,168,75,0.08) 0, rgba(200,168,75,0.08) 1px, transparent 1px, transparent 20px),
    repeating-linear-gradient(-45deg, rgba(200,168,75,0.08) 0, rgba(200,168,75,0.08) 1px, transparent 1px, transparent 20px);
}

/* Grid pattern */
.grid-pattern {
  background-image:
    repeating-linear-gradient(0deg,   rgba(200,168,75,0.06) 0, rgba(200,168,75,0.06) 1px, transparent 1px, transparent 16px),
    repeating-linear-gradient(90deg,  rgba(200,168,75,0.06) 0, rgba(200,168,75,0.06) 1px, transparent 1px, transparent 16px);
}

/* Sunburst / fan gradient */
.sunburst {
  background: radial-gradient(ellipse at 50% 110%, rgba(200,168,75,0.18) 0%, transparent 60%), var(--s2);
}
```

---

## Component Patterns

### Buttons

```css
/* Primary — gold fill */
.btn-p {
  background: var(--gold);
  color: var(--bg);
  border: 1px solid var(--gold);
  border-radius: 0;
  font-family: var(--f);
  font-size: 0.75rem;
  font-weight: 500;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  padding: 0.875rem 2.5rem;
}
.btn-p:hover { background: var(--gold-hi); box-shadow: var(--glow-gold); }
.btn-p:active { transform: translateY(1px); opacity: 0.9; }

/* Secondary — gold border */
.btn-sec {
  background: transparent;
  color: var(--gold);
  border: 1px solid var(--gold);
  /* same font as above */
}
.btn-sec:hover { background: rgba(200,168,75,0.08); }

/* Ghost — cream border */
.btn-ghost {
  background: transparent;
  color: var(--t2);
  border: 1px solid rgba(245,230,200,0.2);
}
```

### Form Inputs

```css
.inp {
  background: var(--s1);
  border: none;
  border-bottom: 1px solid rgba(200,168,75,0.3);
  color: var(--t1);
  font-family: var(--f);
  font-weight: 300;
  padding: 0.75rem 0;
  outline: none;
}
.inp:focus {
  border-bottom-color: var(--gold);
  box-shadow: 0 1px 0 var(--gold);
}
.inp::placeholder { color: var(--t4); }

/* Label */
.label {
  font-family: var(--f);
  font-size: 0.5625rem;
  font-weight: 500;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: var(--t3);
}
```

### Cards

```css
.card-deco {
  background: var(--s1);
  border: 1px solid rgba(200,168,75,0.22);
  /* NO border-radius */
  transition: box-shadow 0.3s, transform 0.3s, border-color 0.3s;
}
.card-deco:hover {
  box-shadow: var(--glow-gold);
  transform: translateY(-2px);
  border-color: var(--gold);
}
/* Primary card top accent */
.card-primary { border-top: 3px solid var(--gold); }
```

### Toggles (rectangular)

```css
.tgl-track {
  width: 44px; height: 22px;
  background: transparent;
  border: 1px solid var(--gold);
  /* border-radius: 0 — hard geometry */
}
.tgl-thumb {
  width: 16px; height: 16px;
  background: var(--t3);
  /* no border-radius */
  transition: transform 0.28s var(--spring), background 0.28s;
}
.tgl-in:checked ~ .tgl-track { background: rgba(200,168,75,0.15); }
.tgl-in:checked ~ .tgl-track .tgl-thumb {
  transform: translateX(22px);
  background: var(--cream);
}
```

### Checkboxes (diamond squares)

```css
.chk-box {
  width: 18px; height: 18px;
  border: 1px solid var(--gold);
  /* border-radius: 0 */
}
.chk-in:checked + .chk-box { background: var(--gold); }
/* Checkmark: cream on gold, square linecap */
```

### Navigation Tabs

```css
.tab-btn {
  font-family: var(--f);
  font-size: 0.5rem;
  font-weight: 500;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  color: var(--t3);
  border-right: 1px solid rgba(200,168,75,0.18); /* gold separator */
}
.tab-btn.tab-on { color: var(--gold); }
.tab-btn.tab-on::after {
  content: '';
  position: absolute;
  bottom: 0; left: 0; right: 0;
  height: 2px;
  background: var(--gold);
}
```

---

## Layout Rules

| Rule | Value |
|------|-------|
| Max page width | 900px, centered |
| Section gap | `margin-top: 5rem` |
| Border radius | **0px everywhere** — this is non-negotiable |
| Ghost section number | Cormorant Roman numeral, `opacity: 0.05`, `color: --gold`, `font-size: 7rem` |
| Section divider | `border-bottom: 1px solid rgba(200,168,75,0.2)` |
| Spec callout | `background: --s2`, `border-left: 2px solid --gold`, chevron `›` icon |

---

## AI Prompting Guidance

When prompting an AI to generate Art Deco UI, use these anchor phrases:

```
Art Deco UI, dark warm background #1a1206, matte gold #c8a84b accent only,
Cormorant Garamond serif display + Jost geometric sans body,
zero border-radius — every corner is hard geometry,
gold border at 22% opacity resting, 50% on hover, full on active,
uppercase Jost labels 10px 500 weight letter-spacing 0.12em,
card hover: box-shadow gold glow translateY(-2px),
no secondary accent colors, black depth / gold light / cream text only,
forms use bottom-border-only input with gold focus underline,
progress dots are rotated 45deg squares (diamonds) not circles,
rectangular toggles not pill-shaped,
section headers decorated with '◆ ◆ ◆' ornament in gold 0.4rem,
gold horizontal rules: linear-gradient(90deg, transparent, gold, transparent)
```

**Anti-patterns to explicitly exclude:**
- `border-radius` in any form
- Blue, purple, or any non-gold accent
- Drop shadows (use gold glow only)
- Gradients on backgrounds (flat dark only)
- Rounded toggles or pill buttons
- Light background variants
- Emoji in content (use geometric symbols: ◆ ▪ › ♩ ♜)

---

## Reference Inspirations

| Building / Object | Deco Principle |
|------------------|----------------|
| Chrysler Building, NYC | Stepped geometry, chrome eagle gargoyles, warm metal |
| Radio City Music Hall | Symmetry, fan motifs, gold leaf |
| Packard automobile interiors | Cream + dark wood + chrome |
| 1930s hotel menus | Uppercase geometric sans + serif display |
| RCA Victor radio console | Dark cabinet, gold dial, rectangular controls |

---

*Art Deco UI Style Guide · Generated for the UI Styles Gallery*
