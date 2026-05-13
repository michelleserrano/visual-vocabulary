# Dieter Rams · Braun Industrial Design
## UI Style Guide

**Personality:** Restrained. Mathematical. Honest. Function-first. Timeless.

**Voice:** If it can be removed and the function remains, remove it.

---

## The 10 Principles as CSS

Dieter Rams defined good design through ten principles. Each one maps directly to a CSS decision.

| Principle | CSS implication |
|-----------|----------------|
| 1. Innovative | Only use what's needed. No decorative elements. |
| 2. Makes a product useful | Function determines form. Typography as hierarchy. |
| 3. Aesthetic | Mathematical spacing. Everything in proportion. |
| 4. Makes a product understandable | Labels on every control. No icon-only navigation. |
| 5. Unobtrusive | The UI disappears. Background and element differ by 3–6% brightness only. |
| 6. Honest | No fake materials. No gradients pretending to be depth. |
| 7. Long-lasting | No trends. No skeuomorphism. No decoration that dates. |
| 8. Thorough | Every detail considered. 4px grid. Consistent radius (2px). |
| 9. Environmentally friendly | Nothing wasted — not pixels, not whitespace, not contrast. |
| 10. As little design as possible | The last thing you add is the first thing you should question. |

---

## Design Tokens

```css
:root {
  /* Surfaces — warm off-white, differentiated by tone only */
  --bg:      #f5f2ed;   /* Page background */
  --s1:      #ede9e2;   /* Elevated surface (cards, panels) */
  --s2:      #e5e0d8;   /* Deep card surface */
  --s3:      #ddd8cf;   /* Deepest surface (input backgrounds on dark) */

  /* Text — near-black to ghost, never pure black */
  --t1:      #1c1c1c;   /* Primary — headlines, body */
  --t2:      #5a5a5a;   /* Secondary — descriptions */
  --t3:      #9a9a9a;   /* Faint — metadata, captions */
  --t4:      #c0bcb5;   /* Ghost — labels, borders, placeholders */

  /* The singular accent */
  --ac:      #c8a84b;   /* Braun matte gold — appears ONCE per component */
  --ac-dark: #a8882e;   /* Gold hover/active state */
  --ac-lo:   rgba(200,168,75,0.18); /* Gold focus ring, ghost tint */

  /* Semantic */
  --ok:      #4a8c5a;   /* Muted green */
  --err:     #8c3a3a;   /* Muted red */
  --warn:    var(--ac); /* Warning IS gold — caution IS the accent */

  /* Borders — barely there */
  --border:    1px solid rgba(0,0,0,0.08);
  --border-2:  1px solid rgba(0,0,0,0.14);

  /* Shape — functional geometry, not decorative */
  --r:      2px;     /* Default — buttons, inputs */
  --r-sm:   1px;     /* Micro — internal elements */
  --r-md:   4px;     /* Cards, panels */
  --r-lg:   6px;     /* Player, large containers */
  --r-full: 9999px;  /* Toggles only */

  /* Shadow — barely perceptible */
  --sh-sm: 0 1px 3px rgba(0,0,0,0.07), 0 0 0 1px rgba(0,0,0,0.04);
  --sh-md: 0 2px 8px rgba(0,0,0,0.09), 0 0 0 1px rgba(0,0,0,0.04);
  --sh-lg: 0 4px 16px rgba(0,0,0,0.10), 0 0 0 1px rgba(0,0,0,0.04);

  /* Type */
  --f:      'Helvetica Neue', Helvetica, Arial, sans-serif;
  --ease:   cubic-bezier(0.4,0,0.2,1);
}

body {
  background: var(--bg);
  font-family: var(--f);
  color: var(--t1);
  letter-spacing: 0.01em; /* Braun's printing had precise letterspacing */
}
```

---

## Typography

**Font:** Helvetica Neue — system font. The choice IS the philosophy.

No Google Fonts. No web fonts. The typeface was already there.

```css
/* Weights: 400 (body) and 500 (emphasis) ONLY. Never 600, 700, or 800. */

.display { font-size: 2.75rem;   font-weight: 500; letter-spacing: -0.025em; }
.h1      { font-size: 2.125rem;  font-weight: 500; letter-spacing: -0.02em; }
.h2      { font-size: 1.625rem;  font-weight: 500; letter-spacing: -0.015em; }
.h3      { font-size: 1.25rem;   font-weight: 500; letter-spacing: -0.01em; }
.h4      { font-size: 1.0625rem; font-weight: 500; }
.body-lg { font-size: 1rem;      font-weight: 400; line-height: 1.7; }
.body    { font-size: 0.9375rem; font-weight: 400; line-height: 1.65; }
.body-sm { font-size: 0.8125rem; font-weight: 400; line-height: 1.6; }
.caption { font-size: 0.6875rem; font-weight: 500; letter-spacing: 0.12em; text-transform: uppercase; }
```

**Rules:**
- Letter-spacing: `0.01em` on body copy (open, never tight)
- Headings: `-0.01em` to `-0.025em` (tight, not cramped)
- Labels: NOT uppercase — Braun does not shout
- Captions and metadata only: uppercase with `0.12em` tracking

---

## Color Usage

**The three roles:**

1. **Off-white** (`--bg` to `--s3`) — all surfaces. Four values, all warm grey.
2. **Near-black** (`--t1` to `--t4`) — all text. Four values from solid to ghost.
3. **Matte gold** (`--ac`) — the singular accent. One instance per component.

**The gold rule:** Gold appears ONCE per component, at the point of highest significance:
- Primary button: use `--t1` (dark), not gold
- Gold button: the key CTA action — used sparingly, never twice on the same screen
- Toggle active state: gold track
- Focus ring: `--ac-lo` (18% opacity)
- Active navigation underline: 2px gold line
- Card primary indicator: 4px gold strip at top of first card only
- Slider fill: gold from left edge to thumb position
- Section ghost numbers: `rgba(200,168,75,0.06)` — barely there, gold tint

---

## Components

### Buttons

```css
/* Primary — near-black on off-white. Maximum contrast. */
.btn-primary {
  background: #1c1c1c;
  color: #f5f2ed;
  border: none;
  border-radius: 2px;
  padding: 0.75rem 1.75rem;
  font-family: var(--f);
  font-size: 0.875rem;
  font-weight: 500;
  letter-spacing: 0.01em;
}
.btn-primary:hover { background: #2a2a2a; box-shadow: var(--sh-sm); }
.btn-primary:active { transform: translateY(1px); opacity: 0.92; }

/* Gold CTA — secondary, used once */
.btn-gold {
  background: var(--ac);
  color: #fff;
  border: none;
  border-radius: 2px;
}
.btn-gold:hover { background: var(--ac-dark); }

/* Ghost — tertiary */
.btn-ghost {
  background: transparent;
  color: var(--t2);
  border: var(--border-2);
  border-radius: 2px;
}
.btn-ghost:hover { background: var(--s1); color: var(--t1); }
```

**Anti-patterns:**
- ❌ Pill shapes (`border-radius: 9999px`) — not Braun
- ❌ Bold labels — font-weight 500 is the maximum for buttons
- ❌ Gradient fills — never
- ❌ Two gold buttons on the same screen — the gold must be singular

---

### Form Inputs

```css
.input {
  background: var(--bg);         /* Same as page — barely visible at rest */
  border: var(--border-2);
  border-radius: 2px;
  padding: 0.75rem;
  font-family: var(--f);
  font-size: 0.9375rem;
  font-weight: 400;
  color: var(--t1);
  letter-spacing: 0.01em;
}
.input:focus {
  border-color: var(--ac);
  box-shadow: 0 0 0 3px var(--ac-lo);
  outline: none;
}

/* Checkbox — square, dark fill */
.checkbox:checked {
  background: var(--t1);  /* Near-black — not gold */
  border-color: var(--t1);
}

/* Toggle — gold track only when on */
.toggle:checked ~ .track {
  background: var(--ac);
  border-color: var(--ac-dark);
}
```

**Labels:** `font-weight: 500; color: var(--t2);` — NOT uppercase, NOT bold

---

### Cards

```css
.card {
  background: var(--s1);   /* 3% brighter than --s2, darker than --bg */
  border: var(--border);
  border-radius: 4px;
  box-shadow: var(--sh-sm);
}
.card:hover { box-shadow: var(--sh-md); }

/* Gold strip — primary card only, once per group */
.card-primary::before {
  content: '';
  display: block;
  height: 4px;
  background: var(--ac);
}

/* All other cards */
.card-secondary::before {
  content: '';
  display: block;
  height: 4px;
  background: var(--t4);  /* Ghost — barely visible */
}

/* Thumbnails: solid color ONLY */
.card-thumb { background: #d4cfc8; } /* Warm grey — no gradients */
```

---

### Sliders

```css
.slider {
  -webkit-appearance: none;
  height: 4px;
  border: var(--border);
  border-radius: 0;  /* Linear instruments have no radius */
  background: linear-gradient(
    to right,
    var(--ac) 0%,
    var(--ac) var(--pct),
    var(--s2) var(--pct),
    var(--s2) 100%
  );
}

.slider::-webkit-slider-thumb {
  -webkit-appearance: none;
  width: 18px; height: 18px;
  border-radius: 50%;
  background: var(--bg);
  border: var(--border-2);
  box-shadow: var(--sh-sm);
}

.slider:active::-webkit-slider-thumb {
  box-shadow: 0 0 0 3px var(--ac-lo), var(--sh-sm);
}
```

---

### Navigation Bar

Text only. No icons.

```css
.nav-item {
  font-family: var(--f);
  font-size: 0.6875rem;
  font-weight: 500;
  color: var(--t4);
  letter-spacing: 0.02em;
  padding: 0.875rem;
  position: relative;
}

/* Active: single gold underline */
.nav-item.active {
  color: var(--ac);
}
.nav-item.active::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 20%; right: 20%;
  height: 2px;
  background: var(--ac);
}
```

---

## Spacing System

4px grid. All major spacing values are multiples of 4.

| Token | Value | Use |
|-------|-------|-----|
| `4px` | `0.25rem` | Micro gaps, icon margins |
| `8px` | `0.5rem` | Tight groups |
| `12px` | `0.75rem` | Inline spacing |
| `16px` | `1rem` | Standard gap |
| `20px` | `1.25rem` | Section padding (small) |
| `24px` | `1.5rem` | Card padding, row spacing |
| `28px` | `1.75rem` | Form spacing |
| `32px` | `2rem` | Component padding |
| `48px` | `3rem` | Section margin (small) |
| `80px` | `5rem` | Section margin (large) |

---

## Anti-Patterns

These are the mistakes that break the Braun aesthetic:

| ❌ Anti-pattern | ✅ Correct |
|----------------|-----------|
| Gradient fills anywhere | Solid colors only |
| `font-weight: 700` or `900` | Max weight is 500 |
| Uppercase labels | Mixed case, functional |
| Pill-shaped buttons | 2px radius, rectangular |
| Multiple gold elements per screen | Gold appears once |
| Decorative icons in nav | Text labels only |
| Drop shadows with color | Monochrome shadows only |
| Multiple accent colors | One accent: `--ac` |
| Large border-radius on containers | Max 6px for containers |
| Emojis or decorative characters | SVG or nothing |
| Hover: changing colors dramatically | Hover: tone shift (+1 step) |
| Primary button is gold | Primary button is dark (`--t1`) |

---

## AI Prompting Guidance

When generating components in this style, prompt with:

```
Design in Dieter Rams / Braun industrial style:
- Font: Helvetica Neue system font, weight 400 (body) and 500 (emphasis) ONLY
- Colors: warm off-white background (#f5f2ed), near-black text (#1c1c1c), one gold accent (#c8a84b)
- The gold accent appears ONCE per component, at the most important action
- Border-radius: 2px for inputs/buttons, 4px for cards, 6px max
- No gradients anywhere — solid colors and tone shifts only
- Spacing: 4px grid, mathematical and consistent
- Borders: hairline (1px solid rgba(0,0,0,0.08) or 0.14)
- If you're adding something for visual interest rather than function, remove it
- The primary button is dark (#1c1c1c) on light background — NOT gold
- No pill shapes, no rounded corners above 6px, no heavy shadows
- Labels are NOT uppercase — Braun does not shout
```

**The test:** Look at each element and ask: "Does this exist because it makes the product work better, or because it looks interesting?" If the answer is the latter, remove it.

---

## Influences

- **Braun T3 Taschenradio** (1958) — scale, labeled controls, restrained proportion
- **Braun ET 44 Calculator** (1977) — grid layout, every button deliberate
- **Braun Regie 350** — receiver form language, horizontal bands, functional layout
- **Braun LE 1** (1959) — minimal enclosure, visible function

The white space in a Braun product is as designed as the elements. Empty space is not emptiness — it is precision.

---

*Dieter Rams, 1976: "Good design is as little design as possible. Less, but better — because it concentrates on the essential aspects, and the products are not burdened with non-essentials."*
