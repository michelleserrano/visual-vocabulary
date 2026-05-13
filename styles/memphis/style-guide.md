# Memphis Group · Style Guide

**Personality:** Loud. Joyful. Geometric. Provocative. Anti-harmonious.

The Memphis Group (founded by Ettore Sottsass in Milan, 1981) weaponized "bad" design into high art. Anti-functionalism was the point. Pattern against pattern, pink vs. teal, orange interrupting both. The composition is the chaos — and the chaos is always deliberate.

---

## Design Tokens

```css
:root {
  /* ── Color ───────────────────────── */
  --bg:      #f7e642;   /* Memphis Yellow — the background IS the color */
  --bg2:     #f0da20;   /* Deep Yellow */
  --pink:    #e84c9c;   /* Primary accent — fights everything */
  --teal:    #2ebdef;   /* Secondary accent — fights pink */
  --orange:  #f97316;   /* Tertiary accent — interrupts both */
  --black:   #1a1a1a;   /* The ground — borders, shadows, text */
  --white:   #ffffff;   /* Card surface, input backgrounds */
  --t1:      #1a1a1a;
  --t2:      #2a2a2a;
  --t3:      #4a4a4a;
  --ac:      #e84c9c;   /* --pink alias */
  --ac2:     #2ebdef;   /* --teal alias */
  --ac3:     #f97316;   /* --orange alias */

  /* ── Shape ───────────────────────── */
  --r:       0px;       /* Memphis is geometric: mostly 0 radius */
  --r-pill:  100px;     /* Occasional pill shape for tonal contrast */

  /* ── Typography ──────────────────── */
  --f-disp:  'Black Han Sans', 'Arial Black', Impact, sans-serif;
  --f-body:  'Space Mono', 'Courier New', monospace;

  /* ── Motion ──────────────────────── */
  --ease:    cubic-bezier(0.4, 0, 0.2, 1);
  --spring:  cubic-bezier(0.34, 1.56, 0.64, 1);

  /* ── Offset Shadow System ────────── */
  --sh-sm:   3px 3px 0 #1a1a1a;
  --sh-md:   4px 4px 0 #1a1a1a;
  --sh-lg:   6px 6px 0 #1a1a1a;
  --sh-xl:   9px 9px 0 #1a1a1a;
}
```

---

## The Offset Shadow System

Memphis's dimensional language is **not** a blur shadow. It is an exact, directional offset with zero blur — like a printed cut-out placed on the page.

```
┌─────────────────────┐
│                     │
│   Elevated Surface  │
│                     │
└─────────────────────┘
                       ████  ← 6px solid offset (bottom + right), no blur
```

| Token | Value | Usage |
|-------|-------|-------|
| `--sh-sm` | `3px 3px 0 black` | Small chips, tags, badges |
| `--sh-md` | `4px 4px 0 black` | Buttons (resting), input focus |
| `--sh-lg` | `6px 6px 0 black` | Cards, panels, players |
| `--sh-xl` | `9px 9px 0 black` | Cards on hover, hero items |

**Rule:** Every elevated element uses the same black ground offset. Color never changes, only the size.

### Button interaction physics

```
Default:  box-shadow: 4px 4px 0 black; transform: none;
Hover:    box-shadow: 6px 6px 0 black; transform: translate(-2px, -2px);
Pressed:  box-shadow: 2px 2px 0 black; transform: translate(2px, 2px);
```

The button appears to physically float up on hover and compress down on press. The transform compensates so the shadow grows/shrinks from the same visual anchor point.

---

## Typography

### Google Fonts import

```html
<link href="https://fonts.googleapis.com/css2?family=Black+Han+Sans&family=Space+Mono:ital,wght@0,400;0,700;1,400&display=swap" rel="stylesheet">
```

### Two fonts, deliberate tension

| Font | Role | Character |
|------|------|-----------|
| **Black Han Sans** | Display, headings, labels, UI text | Bold, compressed, Korean-style boldness. Always uppercase. Loud. |
| **Space Mono** | Body text, data, inputs, placeholders | Monospaced, ironic, mechanical. The typewriter as commentary. |

### Typescale

| Step | Family | Size | Notes |
|------|--------|------|-------|
| Display | Black Han Sans | 48px | Uppercase, letter-spacing 0.03em |
| H1 | Black Han Sans | 36px | Uppercase always |
| H2 | Black Han Sans | 26px | Uppercase |
| H3 | Black Han Sans | 20px | Uppercase, pink color |
| Body Bold | Space Mono | 17px | 700 weight |
| Body Lg | Space Mono | 15px | lh 1.65 |
| Body | Space Mono | 14px | lh 1.6 |
| Body Sm | Space Mono | 12px | lh 1.55 |
| Caption | Black Han Sans | 9.6px | Uppercase, teal color |

---

## Component Specs

### Buttons

```css
/* Base */
.btn {
  border: 3px solid #1a1a1a;
  padding: 0.75rem 1.75rem;
  font-family: var(--f-disp);
  letter-spacing: 0.05em;
  text-transform: uppercase;
  box-shadow: var(--sh-md);
  transition: transform 0.12s, box-shadow 0.12s;
}

/* Hover */
.btn:hover {
  transform: translate(-2px, -2px);
  box-shadow: var(--sh-lg);
}

/* Active */
.btn:active {
  transform: translate(2px, 2px);
  box-shadow: var(--sh-sm);
}

/* Primary — pink */
.btn-primary { background: #e84c9c; color: white; }

/* Secondary — teal */
.btn-secondary { background: #2ebdef; color: #1a1a1a; }

/* Tertiary — orange pill (only time border-radius appears) */
.btn-tertiary { background: #f97316; color: white; border-radius: 100px; }

/* Outlined */
.btn-outlined { background: transparent; color: #1a1a1a; }
```

### Form Inputs

```css
.input {
  background: white;
  border: 3px solid #1a1a1a;
  padding: 0.75rem 1rem;
  font-family: 'Space Mono', monospace;
  outline: none;
}

.input:focus {
  border-color: #e84c9c;   /* pink */
  box-shadow: 4px 4px 0 #1a1a1a;
}

label {
  font-family: var(--f-disp);
  font-size: 0.6875rem;
  letter-spacing: 0.1em;
  text-transform: uppercase;
}
```

### Checkboxes

```css
.checkbox {
  width: 24px;
  height: 24px;
  border: 3px solid #1a1a1a;
  border-radius: 0;          /* never round */
  background: white;
}

.checkbox:checked {
  background: #e84c9c;       /* pink fill */
}
```

### Toggles

```css
/* Rectangular track, white square thumb */
.toggle-track {
  width: 56px;
  height: 28px;
  background: white;
  border: 3px solid #1a1a1a;
  position: relative;
}

.toggle-thumb {
  width: 18px;
  height: 18px;
  background: #1a1a1a;
  transition: transform 0.22s, background 0.22s;
}

/* Active */
.toggle-thumb-active {
  transform: translateX(28px);
  background: #e84c9c;
}
```

### Cards

```css
.card {
  background: white;
  border: 3px solid #1a1a1a;
  box-shadow: 6px 6px 0 #1a1a1a;
  transition: transform 0.15s, box-shadow 0.15s;
}

.card:hover {
  transform: translate(-3px, -3px);
  box-shadow: 9px 9px 0 #1a1a1a;
}

.card-header {
  height: 8px;
  background: #e84c9c;   /* or teal or orange */
}
```

### Progress / Slider tracks

```css
/* White track, no radius, black border */
input[type="range"] {
  height: 10px;
  background: white;
  border: 3px solid #1a1a1a;
  -webkit-appearance: none;
}

/* Square thumb, pink, black border */
input[type="range"]::-webkit-slider-thumb {
  -webkit-appearance: none;
  width: 22px;
  height: 22px;
  background: #e84c9c;
  border: 3px solid #1a1a1a;
  border-radius: 0;
}
```

---

## Geometric Decoration System

Every section gets at least one decorative geometric shape. These are non-interactive background elements that reinforce the Memphis visual language.

### Rules

1. Use `position: absolute` with `z-index: 0` (content sits above at z-index 1)
2. Colors: `--pink`, `--teal`, or `--orange` at 10–25% opacity
3. Mix circles (border-radius 50%) and rectangles (border-radius 0)
4. Size range: 30px–120px
5. Place at edges or corners, never center-stage
6. Never add borders to deco shapes (the border is for UI elements only)

### Example decoration pattern

```css
/* Circle deco */
.deco-circle {
  position: absolute;
  width: 80px;
  height: 80px;
  border-radius: 50%;
  background: #e84c9c;
  opacity: 0.12;
  right: -20px;
  top: 20px;
  pointer-events: none;
}

/* Rectangle deco */
.deco-rect {
  position: absolute;
  width: 40px;
  height: 40px;
  background: #2ebdef;
  opacity: 0.2;
  right: 60px;
  top: 10px;
  pointer-events: none;
}
```

### Spec callout decoration

Every `.spec-callout` gets an overlapping pink + teal circle pair (via `::before` / `::after`) in the upper-right corner. This is the single most recognizable Memphis UI detail.

```css
.spec-callout::before {
  content: '';
  position: absolute;
  width: 64px;
  height: 64px;
  border-radius: 50%;
  background: #e84c9c;
  opacity: 0.15;
  right: -16px;
  top: -16px;
}

.spec-callout::after {
  content: '';
  position: absolute;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  background: #2ebdef;
  opacity: 0.18;
  right: 24px;
  bottom: -12px;
}
```

---

## Progress / Side Navigation Dots

Memphis progress dots are small circles (exception to the no-radius rule) with:

- Size: 12×12px, `border-radius: 50%`
- Border: `2px solid black`
- Inactive: yellow (--bg) fill
- Active: filled with alternating pink / teal / orange

```
dot[1]: pink
dot[2]: teal
dot[3]: orange
dot[4]: pink  (repeat)
...
```

---

## Sticky Nav

```css
.topnav {
  background: var(--bg);          /* yellow */
  border-bottom: 3px solid black;
  height: 56px;
}

.tnav-title {
  font-family: var(--f-disp);
  text-transform: uppercase;
  letter-spacing: 0.04em;
}

/* Download button — pink with offset shadow */
.tnav-dl {
  background: var(--pink);
  color: white;
  border: 3px solid black;
  box-shadow: 3px 3px 0 black;
  font-family: var(--f-disp);
  text-transform: uppercase;
}
```

---

## Navigation Bar

| State | Treatment |
|-------|-----------|
| Inactive | Black icon on white, no fill |
| Hover | Yellow (--bg) background |
| Active | Pink background, white icon + label |

Separation between tabs: `border-right: 1px solid rgba(26,26,26,0.15)`. The active inversion is total — pink floods the full tab cell.

---

## The Memphis Color Rules

| Principle | Rule |
|-----------|------|
| Yellow is air | `--bg` (#f7e642) is the only background. It is the canvas. |
| Pink leads | All primary interactive elements are pink. |
| Teal replies | Secondary elements, data accents, icon fills. |
| Orange interrupts | Tertiary, notifications, highlights that need to cut through. |
| Black grounds | All borders, all offset shadows, all text. Never grey for borders. |
| White surfaces | Cards, inputs, callouts. White is the relief from yellow. |
| No harmony | Pink and teal are intentionally placed near each other. This is correct. |

---

## AI Prompting Guidance

Use these prompts to generate Memphis-accurate assets and components.

### For UI generation

> "Memphis Group design aesthetic, 1981 Milan postmodern. Yellow background (#f7e642), pink (#e84c9c), teal (#2ebdef), orange (#f97316) accent colors. Bold 3px black borders on every element. Offset box-shadow (6px 6px 0 black, no blur). Black Han Sans for display type, uppercase. Space Mono for body text. No gradient, no drop shadows. Geometric shapes as decoration. Anti-harmonious color combinations. Ettore Sottsass aesthetic."

### For illustration/pattern

> "Memphis Group pattern, 1980s postmodern Italian design. Geometric shapes: circles, triangles, zigzags, squiggles, dots. Colors: hot pink, cyan, orange, yellow, black, white. High contrast, clashing colors, bold outlines. Flat, no shadows on the pattern shapes themselves. Repeat tile. Bacterio pattern influence. Sottsass, Mendini, De Lucchi style."

### For photography direction

> "Memphis Group object design, Ettore Sottsass 1981. Laminate surface, bold color blocking, terrazzo texture, primary color geometry. Studio product photography on white or yellow background. Bold, exuberant, anti-minimalist."

### Anti-patterns to avoid

- ❌ Gradients (Memphis is flat color + borders)
- ❌ Blur shadows (the offset shadow must have 0 blur)
- ❌ Rounded corners on cards/inputs/buttons (0px radius only; pills are the rare exception)
- ❌ Neutral grey borders (always #1a1a1a black)
- ❌ Muted/desaturated color palette (the colors must be vivid and clashing)
- ❌ Centered, symmetrical layouts (Memphis favors deliberate asymmetry)
- ❌ Serifs or humanist sans-serifs (Black Han Sans + Space Mono only)

---

## Quick Reference: What makes it Memphis

| Element | Memphis Treatment |
|---------|------------------|
| Background | #f7e642 yellow — loud, not neutral |
| Borders | 3px solid #1a1a1a, always |
| Shadow | 4–9px offset, 0 blur, black |
| Border radius | 0px (geometric), 100px (pill, rare) |
| Primary accent | #e84c9c pink |
| Secondary accent | #2ebdef teal |
| Tertiary accent | #f97316 orange |
| Display font | Black Han Sans, uppercase |
| Body font | Space Mono |
| Button hover | float up: translate(-2px,-2px), shadow grows |
| Button press | sink down: translate(2px,2px), shadow shrinks |
| Card hover | translate(-3px,-3px), shadow → 9px |
| Active nav tab | full pink background inversion |
| Decoration | Circles + rectangles, 10–25% opacity, at edges |

---

*Memphis Group Style Guide · Generated for UI Styles Gallery · May 2026*
