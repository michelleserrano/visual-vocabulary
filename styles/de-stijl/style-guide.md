# De Stijl — UI Style Guide

**Personality:** Absolute. Primary. Gridded. Pure. Neoplastic.

> *"The new plastic idea cannot, therefore, take the form of a natural or concrete representation, although the latter does always indicate the universal to a degree, or at least conceals it within. This new plastic idea will ignore the particulars of appearance, that is to say, natural form and colour. On the contrary, it should find its expression in the abstraction of form and colour, that is to say, in the straight line and the clearly defined primary colour."*
> — Piet Mondrian, 1917

---

## Origin

**De Stijl** (Dutch: "The Style") was founded in Leiden in 1917 by Piet Mondrian, Theo van Doesburg, and Bart van der Leck. Its philosophy — **Neoplasticism** — held that the material world could be expressed through the simplest possible visual language: horizontal and vertical lines, primary colors, black, and white. Nothing more. Everything else was subjective ornamentation to be eliminated.

Van Doesburg introduced diagonals in 1924. Mondrian considered this a betrayal and left the movement. The diagonal was never De Stijl.

Active period: **1917–1931.**

---

## The Five-Value Rule

De Stijl allows exactly **five values**. No exceptions.

| Token      | Hex       | Role          | Notes                                      |
|------------|-----------|---------------|--------------------------------------------|
| `--red`    | `#e8261d` | Primary action | The most charged color. Use sparingly.    |
| `--yellow` | `#f7c600` | Tertiary action | Light — always use black text on yellow. |
| `--blue`   | `#1a4a8a` | Secondary action | Deep, structural blue.                  |
| `--black`  | `#1a1a1a` | Structure      | All lines, borders, text, structural grid. |
| `--white`  | `#f5f5f5` | Silence        | Background, space between things.          |

**No other values exist in this system.** No gray, no tint, no opacity, no mix.

---

## Grid Line System

The 4px black line is the **structural atom** of De Stijl. Every element exists within or between these lines.

```css
--line: 4px solid #1a1a1a;  /* NEVER thinner on structural elements */
```

### How lines work

- **Horizontal lines** divide sections, separate nav from content, delimit form rows
- **Vertical lines** create columns, separate nav items, frame the page
- **Lines define the grid** — color fills the cells
- **Lines never cross diagonally** — this would violate the movement's core principle

### Page as Mondrian painting

```css
/* The nav IS a Mondrian strip at the top */
.topnav {
  background: #f5f5f5;
  border-bottom: 4px solid #1a1a1a;
}

/* Left red stripe on nav = color accent within the top strip */
.tnav-stripe {
  width: 8px;
  background: #e8261d;
  border-right: 2px solid #1a1a1a;
}

/* The page content area has vertical borders */
.page {
  border-left: 4px solid #1a1a1a;
  border-right: 4px solid #1a1a1a;
}

/* Each section begins with a horizontal line */
.sec {
  border-top: 4px solid #1a1a1a;
}
```

---

## Typography

| Role    | Font          | Weight | Size      | Case      | Tracking |
|---------|---------------|--------|-----------|-----------|----------|
| Display | Oswald        | 700    | 48–96px   | Uppercase | −0.02em  |
| H1      | Oswald        | 600    | 36px      | Uppercase | 0        |
| H2      | Oswald        | 500    | 26px      | Uppercase | +0.04em  |
| H3      | Oswald        | 400    | 20px      | Uppercase | +0.06em  |
| Body    | Helvetica Neue| 400    | 16px      | Sentence  | 0        |
| Small   | Helvetica Neue| 400    | 14px      | Sentence  | 0        |
| Caption | Oswald        | 500    | 11px      | Uppercase | +0.14em  |
| Label   | Oswald        | 500    | 10–11px   | Uppercase | +0.12em  |
| Code    | Courier New   | 700    | 12–13px   | —         | 0        |

**Oswald** is used for display and labels because its condensed, vertical proportions echo the vertical lines of the De Stijl grid. It carries authority without ornament.

**Helvetica Neue** for body text because De Stijl's typography was functional, not expressive. The neutrality of Helvetica is a feature.

```html
<link href="https://fonts.googleapis.com/css2?family=Oswald:wght@300;400;500;600;700&display=swap" rel="stylesheet">
```

---

## Color Blocks

Primary colors appear as **solid fill blocks** — never tints, never gradients, never mixed.

```css
/* Correct */
background: #e8261d;  /* pure red */
background: #1a4a8a;  /* pure blue */
background: #f7c600;  /* pure yellow */

/* Wrong */
background: rgba(232, 38, 29, 0.5);  /* ✗ tint */
background: linear-gradient(...);    /* ✗ gradient */
background: #d44f3a;                 /* ✗ mix */
```

Color blocks are used for:
- Card header strips / thumbnail compositions
- Button fills
- Progress dot fills (active state)
- Section number badges
- Decorative Mondrian compositions
- Nav active indicators (8px square)

---

## Components

### Buttons

```css
.btn {
  font-family: 'Oswald', sans-serif;
  font-size: 0.8125rem;
  font-weight: 600;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  border-radius: 0 !important;        /* ABSOLUTE ZERO */
  border: 2px solid #1a1a1a;
  box-shadow: 4px 4px 0 #1a1a1a;     /* offset shadow — the only depth allowed */
  transition: box-shadow 0.12s, transform 0.1s;
}

/* Hover: shadow expands, button lifts */
.btn:hover {
  box-shadow: 6px 6px 0 #1a1a1a;
  transform: translate(-2px, -2px);
}

/* Press: shadow collapses, button stamps down */
.btn:active {
  box-shadow: 2px 2px 0 #1a1a1a;
  transform: translate(2px, 2px);
}

/* Variants */
.btn-red    { background: #e8261d; color: #f5f5f5; }
.btn-blue   { background: #1a4a8a; color: #f5f5f5; }
.btn-yellow { background: #f7c600; color: #1a1a1a; }  /* yellow needs black text */
.btn-ghost  { background: #f5f5f5; color: #1a1a1a; }
```

### Form Inputs

```css
.inp {
  background: #f5f5f5;
  border: 2px solid #1a1a1a;
  border-radius: 0 !important;
  padding: 0.75rem 1rem;
  font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
  font-size: 0.9375rem;
  outline: none;
  transition: border-color 0.12s;
}

.inp:focus {
  border-color: #e8261d;  /* red focus — the only color that changes on focus */
}

/* Labels are Oswald, uppercase */
.label {
  font-family: 'Oswald', sans-serif;
  font-size: 0.625rem;
  font-weight: 500;
  letter-spacing: 0.14em;
  text-transform: uppercase;
}
```

### Checkboxes

```css
.chk-box {
  width: 20px;
  height: 20px;
  background: #f5f5f5;
  border: 2px solid #1a1a1a;
  /* border-radius: 0 !important — always square */
}

/* Checked: fill with red, white checkmark */
.chk-in:checked + .chk-box {
  background: #e8261d;
}
```

### Toggles

```css
.tgl-track {
  width: 48px;
  height: 22px;
  background: #f5f5f5;
  border: 2px solid #1a1a1a;
  /* border-radius: 0 !important — rectangles only, no pill shape */
}

.tgl-thumb {
  width: 14px;
  height: 14px;
  background: #1a1a1a;
  /* no border-radius — square thumb */
  transition: transform 0.2s;
}

.tgl-in:checked ~ .tgl-track { background: #e8261d; }
.tgl-in:checked ~ .tgl-track .tgl-thumb {
  transform: translateX(26px);
  background: #f5f5f5;
}
```

### Cards

```css
.card {
  border: 4px solid #1a1a1a;
  background: #f5f5f5;
  /* no box-shadow at rest — De Stijl is flat */
}

.card:hover {
  box-shadow: 5px 5px 0 #1a1a1a;   /* offset shadow on hover — physical presence */
  transform: translate(-3px, -3px);
}

/* Card thumbnail is a Mondrian composition, not an image */
.card-thumb {
  height: 148px;
  border-bottom: 4px solid #1a1a1a;
  display: grid; /* mini Mondrian grid */
}
```

### Mini Mondrian Compositions

Build card thumbnails as CSS grid-based Mondrian paintings. Use 4px spacer columns/rows for black lines:

```html
<!-- 3×3 Mondrian: columns [3fr, 4px, 2fr], rows [2fr, 4px, 1fr] -->
<div style="display:grid;
            grid-template-columns:3fr 4px 2fr;
            grid-template-rows:2fr 4px 1fr;
            width:100%;height:100%">
  <div style="background:#e8261d"></div>   <!-- top-left: red -->
  <div style="background:#1a1a1a"></div>   <!-- vertical line -->
  <div style="background:#f5f5f5"></div>   <!-- top-right: white -->
  <div style="background:#1a1a1a"></div>   <!-- horizontal line C1 -->
  <div style="background:#1a1a1a"></div>   <!-- horizontal line intersection -->
  <div style="background:#1a1a1a"></div>   <!-- horizontal line C3 -->
  <div style="background:#f5f5f5"></div>   <!-- bottom-left: white -->
  <div style="background:#1a1a1a"></div>   <!-- vertical line -->
  <div style="background:#1a4a8a"></div>   <!-- bottom-right: blue -->
</div>
```

Each composition should be unique. Vary the proportions (3fr/2fr, 1fr/2fr/1fr, etc.) and the color placement. The key constraints:
- Black dividers are always exactly 4px (or 3px for very small compositions)
- Color blocks are always pure primary (#e8261d, #1a4a8a, #f7c600) or white (#f5f5f5)
- The overall composition must be asymmetric but visually balanced

### Progress Dots (Side Navigation)

```css
.prog-dot {
  width: 8px;
  height: 8px;
  background: #f5f5f5;
  border: 2px solid #1a1a1a;
  /* border-radius: 0 !important — squares, never circles */
}

/* Active: fill with rotating primary colors */
.a-red    { background: #e8261d; }
.a-blue   { background: #1a4a8a; }
.a-yellow { background: #f7c600; }
```

### Navigation Bar

```css
.navbar {
  border-top: 4px solid #1a1a1a;
  background: #f5f5f5;
}

.nav-item {
  border-right: 2px solid #1a1a1a;  /* vertical separator */
}

/* Active indicator: single colored square above label */
.ni-indicator {
  width: 8px;
  height: 8px;
  background: #e8261d;  /* red for primary active state */
}
```

---

## Global Reset

```css
/* Apply at root — this is non-negotiable */
*, *::before, *::after {
  border-radius: 0 !important;  /* ABSOLUTE ZERO — no curves anywhere */
}

:root {
  --bg:     #f5f5f5;
  --t1:     #1a1a1a;
  --red:    #e8261d;
  --blue:   #1a4a8a;
  --yellow: #f7c600;
  --black:  #1a1a1a;
  --white:  #f5f5f5;
  --line:   4px solid #1a1a1a;
  --f:      'Helvetica Neue', Helvetica, Arial, sans-serif;
  --f-disp: 'Oswald', 'Helvetica Neue', sans-serif;
  --ease:   cubic-bezier(0.4, 0, 0.2, 1);
}

body {
  background: var(--bg);
  color: var(--t1);
  font-family: var(--f);
}
```

---

## Anti-Patterns

These violate De Stijl and must never appear:

| Anti-Pattern            | Why it's wrong                                            |
|-------------------------|-----------------------------------------------------------|
| `border-radius > 0`     | De Stijl uses only rectangles. Curves are expressionism. |
| Gray (`#888`, `#ccc`)   | Gray does not exist in the palette. Use black at reduced opacity only for metadata, sparingly. |
| `box-shadow` with blur  | Blurred shadows suggest softness. Only sharp offset shadows (e.g., `4px 4px 0`) are allowed. |
| `linear-gradient`       | No gradients. Color is pure and flat.                     |
| Diagonal lines          | Van Doesburg introduced diagonals in 1924 and was expelled. No diagonals. |
| Mixed colors (`#c44a3a`) | Only exact primaries. No mixing, no deviation.           |
| Circular elements       | No circles, no ellipses, no rounded avatars or icons.    |
| Italic text             | De Stijl typography is upright, structural, never expressive. |
| Serif typefaces         | Only Oswald (display) and Helvetica Neue (body).         |
| Decorative drop shadows | `box-shadow: 0 4px 16px rgba(0,0,0,0.15)` — no. Only offset, no blur. |
| Opacity < 0.3 on color blocks | If a color appears, it appears at full strength.  |

---

## AI Prompting Guidance

When prompting AI to generate De Stijl UI:

**Effective prompts:**
- "De Stijl style. Primary colors only: #e8261d, #1a4a8a, #f7c600, #1a1a1a, #f5f5f5. Zero border-radius. 4px black structural borders. Oswald font, uppercase. Offset box-shadow only."
- "Mondrian Neoplasticism UI. No curves, no diagonals, no gray. Every border is 4px solid #1a1a1a. Buttons have 4px offset shadow."
- "Recreate Broadway Boogie Woogie as a [component name]. CSS grid with 4px black line dividers. Pure primary color fills."

**Phrases that prevent drift:**
- "No border-radius, ever, not even 1px"
- "No circular elements — use squares"
- "No gradients — solid color fills only"
- "No diagonal lines — horizontal and vertical only"
- "The only depth allowed is a sharp offset box-shadow: 4px 4px 0 #1a1a1a"
- "Only these 5 values: #e8261d, #f7c600, #1a4a8a, #1a1a1a, #f5f5f5"

**Reference works to cite:**
- Mondrian, "Composition II in Red, Blue, and Yellow" (1930)
- Mondrian, "Broadway Boogie Woogie" (1942–43)
- Rietveld, "Red and Blue Chair" (1919)
- Rietveld, "Rietveld Schröder House" (1924)
- Van Doesburg, "De Stijl" journal covers (1917–1931)

---

## Accessibility Notes

- Yellow (`#f7c600`) on white fails WCAG AA. **Always pair yellow backgrounds with black text.**
- Red (`#e8261d`) on white passes WCAG AA at large text sizes (18px+). For small text, use on dark backgrounds.
- Blue (`#1a4a8a`) on white passes WCAG AA at all sizes.
- Black on white is maximum contrast (21:1).
- Focus states: use `outline: 2px solid #e8261d` — keeping the color vocabulary consistent.
- The square-only rule means no circular avatar images. Use color-filled squares as avatars/indicators.

---

## Design Principles Summary

1. **Grid is everything.** The page is a Mondrian painting. Every element is a cell.
2. **Lines define structure.** 4px black lines are not decoration — they are architecture.
3. **Color has meaning.** Red = primary action. Blue = secondary. Yellow = tertiary. These are not arbitrary.
4. **Asymmetry with equilibrium.** Compositions are never symmetric, but always visually balanced.
5. **Nothing decorative.** If an element doesn't carry meaning in the grid, remove it.
6. **Absolute constraints enable creativity.** The restrictions are the system. Working within them is the skill.
