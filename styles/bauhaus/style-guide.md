# Bauhaus · Style Guide

**Personality:** Functional. Primary. Geometric. Bold. Educational.

**Origin:** Dessau, Germany · 1919–1933  
**Founders:** Walter Gropius (director), Kandinsky (theory), Herbert Bayer (typography)  
**Manifesto:** _"The ultimate aim of all creative activity is building."_ Form follows function. Art and industry unified.

---

## Core Principles

1. **Form follows function** — no ornament that doesn't serve the object
2. **Only three primary colors** — red, blue, yellow. And black and white. Nothing else.
3. **Every form reduces to three shapes** — circle, triangle, square
4. **Typography: bold, condensed, impactful** — Herbert Bayer's universal type
5. **No radius** — except for circles, which are intentional geometric statements
6. **Offset shadow system** — `box-shadow: 4px 4px 0 #1a1a1a` gives dimensionality on hover

---

## Design Tokens

```css
:root {
  --bg:      #fafafa;   /* off-white paper — Bauhaus used off-white */
  --s1:      #f0f0f0;
  --s2:      #e0e0e0;
  --t1:      #1a1a1a;   /* near-black */
  --t2:      #4a4a4a;
  --t3:      #8a8a8a;
  --red:     #e8261d;   /* primary red */
  --blue:    #1a4a8a;   /* primary blue */
  --yellow:  #f7c600;   /* primary yellow */
  --black:   #1a1a1a;
  --r:       0px;       /* no radius — ever */
  --r-circle: 50%;      /* only for intentional circles */
  --f:       'Oswald', 'Helvetica Neue', Helvetica, sans-serif;
  --f-body:  'IBM Plex Sans', 'Helvetica Neue', sans-serif;
  --ease:    cubic-bezier(0.4, 0, 0.2, 1);
  --spring:  cubic-bezier(0.34, 1.56, 0.64, 1);
}
```

---

## The Three-Shape Theory (Kandinsky)

Wassily Kandinsky's foundational teaching at the Bauhaus. Every visual element reduces to three geometric primitives. Each shape has inherent psychological meaning:

| Shape | Meaning | Color Pairing | Use |
|-------|---------|---------------|-----|
| **Circle** | Spiritual, eternal, continuous | Blue | Play buttons, avatars, infinite concepts |
| **Triangle** | Dynamic, tension, aggression | Yellow | Arrows, direction, urgency |
| **Square** | Stable, earthly, reliable | Red | Stop buttons, containers, reliable UI |

**The rule:** When a UI element needs to communicate meaning, choose the shape that carries it. A play button is a circle (continuous, infinite). A stop is a square (stable, final). A "next" arrow is triangular (directional).

---

## Primary Color Rules

**Rule:** Only these five values: red `#e8261d`, blue `#1a4a8a`, yellow `#f7c600`, black `#1a1a1a`, white `#ffffff`. No tints. No mixes in final output. No gradients (except the slider fill trick which is technical, not design).

| Color | Hex | Role | Shape pairing |
|-------|-----|------|---------------|
| Red | `#e8261d` | Primary action, urgency, primary | Square |
| Blue | `#1a4a8a` | Secondary, depth, spiritual | Circle |
| Yellow | `#f7c600` | Tertiary, light, dynamic | Triangle |
| Black | `#1a1a1a` | Structure, borders, type | — |
| White | `#ffffff` | Surface, space, canvas | — |

**Meaning of color assignment in UI:**
- Red button = primary action (submit, confirm, the most important)
- Blue button = secondary action
- Yellow button = tertiary / informational
- Black outlines = structural, always present (no hairlines, use 2px solid)

---

## Typography

### Display: Oswald

Condensed geometric sans-serif. Industrial. Bold. Structural.

```css
/* Display */
font-family: 'Oswald', 'Helvetica Neue', Helvetica, sans-serif;
font-weight: 700;
font-size: 3rem–9rem;
text-transform: uppercase;
letter-spacing: 0.02em;
line-height: 0.9;

/* Headings */
font-weight: 600;
text-transform: uppercase;
letter-spacing: 0.05–0.1em;

/* Labels / Captions */
font-weight: 500;
font-size: 0.625–0.75rem;
text-transform: uppercase;
letter-spacing: 0.12–0.2em;
```

### Body: IBM Plex Sans

```css
font-family: 'IBM Plex Sans', 'Helvetica Neue', sans-serif;
font-weight: 400;
font-size: 0.875rem–1rem;
line-height: 1.6–1.7;
/* No uppercase, no heavy tracking */
```

### Google Fonts import

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Oswald:wght@300;400;500;600;700&family=IBM+Plex+Sans:ital,wght@0,300;0,400;0,500;0,600;1,400&display=swap" rel="stylesheet">
```

---

## Component Specs

### Buttons

```css
/* Base */
padding: 0.875rem 2rem;
font-family: var(--f);        /* Oswald */
font-size: 0.9375rem;
font-weight: 600;
text-transform: uppercase;
letter-spacing: 0.1em;
border: none;
border-radius: 0;             /* no radius */

/* Primary (red) */
background: var(--red);
color: white;

/* Hover */
background: #c01810;
box-shadow: 4px 4px 0 var(--black);

/* Active / pressed */
transform: translate(4px, 4px);
box-shadow: none;

/* Secondary (blue) */
background: var(--blue);
color: white;

/* Tertiary (yellow) */
background: var(--yellow);
color: var(--black);

/* Ghost */
background: transparent;
border: 2px solid var(--black);
color: var(--black);
/* hover: background fills black, text turns white */
```

### Form Inputs

```css
/* Input base — bottom line only */
border: none;
border-bottom: 2px solid var(--black);
background: transparent;
padding: 0.75rem 0;
font-family: 'IBM Plex Sans';
outline: none;

/* Focus */
border-bottom-color: var(--red);

/* Label */
font-family: 'Oswald';
font-size: 0.6875rem;
font-weight: 500;
letter-spacing: 0.12em;
text-transform: uppercase;
color: var(--t2);

/* Checkbox: checked state */
background: var(--red);
border-color: var(--red);
/* checkmark: white SVG stroke */

/* Toggle track */
width: 48px; height: 24px;
border: 2px solid var(--black);
background: white;
/* checked: background: var(--red); border-color: var(--red) */
/* thumb: black square → slides right, turns white */
```

### Cards

```css
/* Card container */
background: white;
border: 2px solid var(--black);
border-radius: 0;

/* Top color bar (4px) */
/* primary card: background: var(--red) */
/* secondary: var(--blue) */
/* tertiary: var(--yellow) */

/* Hover */
box-shadow: 5px 5px 0 var(--black);
transform: translate(-2px, -2px);

/* Card thumb: solid color (red/blue/yellow) + white shape overlay */
/* Red thumb: white circle (rgba(255,255,255,0.28)) */
/* Blue thumb: white triangle */
/* Yellow thumb: white square */
```

### Navigation Bar

```css
/* Container */
background: white;
border-top: 2px solid var(--black);
/* tabs separated by 1px solid var(--s2) */

/* Tab labels */
font-family: 'Oswald';
font-size: 0.5–0.6rem;
font-weight: 600;
letter-spacing: 0.1em;
text-transform: uppercase;

/* Active tab */
color: var(--red);
/* ::before pseudo: height 3px, background var(--red), top 0 */

/* Inactive */
color: var(--t3);
```

### Music Player Controls

```css
/* Play — circle (spiritual / continuous) */
border-radius: 50%;
background: var(--red);
width: 50px; height: 50px;

/* Stop — square (stable / decisive) */
border-radius: 0;
background: var(--black);
width: 34px; height: 34px;

/* Skip forward/back — rectangle (directional) */
border-radius: 0;
width: 36px; height: 26px;

/* Slider fill (JS-driven) */
background: linear-gradient(to right, var(--red) 0%, var(--red) N%, var(--s2) N%, var(--s2) 100%);

/* Slider thumb */
width: 14px; height: 14px;
background: var(--black);
border-radius: 0; /* square thumb */
```

---

## The Offset Shadow System

The signature hover effect in Bauhaus UI. Creates physical dimensionality without gradients.

```css
/* Hover state */
box-shadow: 4px 4px 0 var(--black);
/* Optional: translate the element up-left to exaggerate */
transform: translate(-2px, -2px);

/* Active / pressed state — shadow collapses */
transform: translate(4px, 4px);
box-shadow: none;
```

**Why it works:** The offset shadow in one direction creates the illusion that the element is sitting on a surface. When "pressed," it shifts into the shadow — physically receding. No blur, no spread. Just the geometric offset.

---

## Progress / Side Navigation Dots

Alternate shapes to reinforce the Bauhaus three-shape theory:

| Dot index | Shape | Active color |
|-----------|-------|-------------|
| 0, 3, 6 | Circle (`border-radius: 50%`) | Red |
| 1, 4, 7 | Square (`border-radius: 0`) | Blue |
| 2, 5 | Triangle (CSS border trick) | Yellow |

```css
/* Triangle CSS trick */
.tri {
  width: 0; height: 0;
  background: transparent;
  border-left: 5px solid transparent;
  border-right: 5px solid transparent;
  border-bottom: 9px solid #8a8a8a; /* inactive */
}
.tri.active {
  border-bottom-color: #f7c600; /* yellow when active */
}
```

---

## Section Ghost Numbers

```css
.sec-ghost {
  font-family: 'Oswald';
  font-size: 7rem;
  font-weight: 900;
  color: rgba(0, 0, 0, 0.04); /* barely visible */
  position: absolute;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
  pointer-events: none;
  user-select: none;
}
```

---

## What Not to Do

- **No border-radius** on rectangles. Ever. Use `border-radius: 0` explicitly.
- **No tints or mixes** — `#e87d7d` (tinted red) is not Bauhaus. Use `#e8261d` or `white`.
- **No gradients** (except technical slider fills).
- **No shadows with blur** — use offset solid `box-shadow: Npx Npx 0 color` only.
- **No decorative icons** — icons must be geometric (circle, square, line, triangle). No metaphoric illustration.
- **No italic** in headings — Oswald is always upright. IBM Plex Sans italic only for emphasis in long-form text.
- **No neutral colors** — no grays as primary surfaces. Gray (`#f0f0f0`) is only for spec callouts and section backgrounds.

---

## AI Prompting Guidance

### System prompt fragment for Bauhaus style

```
You are designing in the Bauhaus style (Dessau, 1919–1933).

Color: Only use #e8261d (red), #1a4a8a (blue), #f7c600 (yellow), #1a1a1a (black), #ffffff (white), #fafafa (off-white background). No tints, no gradients, no color mixing in final output.

Shapes: Every UI element reduces to circle, triangle, or square. No organic shapes, no curves except intentional circles. border-radius: 0 on all rectangular elements.

Typography: 'Oswald' for all headings, labels, nav items — always uppercase, always with letter-spacing. 'IBM Plex Sans' for body text — lowercase, functional.

Interaction: Hover state reveals offset box-shadow: 4px 4px 0 #1a1a1a. Active/pressed state: element translates 4px right-down and shadow collapses. This is the primary feedback system.

No drop shadows, no blur, no glow, no glassmorphism, no gradients. Only geometric flat forms.
```

### Few-shot prompt examples

**Prompt:** "Create a Bauhaus-style card component"  
**Key constraints to enforce:** `border: 2px solid black`, 4px top color bar (red/blue/yellow), solid color thumbnail with white shape overlay, hover: `box-shadow: 5px 5px 0 black; transform: translate(-2px,-2px)`, no border-radius, Oswald heading uppercase.

**Prompt:** "Design a Bauhaus form"  
**Key constraints:** Only bottom border on inputs (`border-bottom: 2px solid black`), no box backgrounds, Oswald labels uppercase with tracking, red bottom border on focus, checkbox = black square → red fill on check.

**Prompt:** "Build a Bauhaus music player"  
**Key constraints:** Play = red circle, Stop = black square, Skip = black rectangle. All three shapes, each with correct Bauhaus meaning. Slider thumb = black square. Progress fill = red.

---

## Historical Context

The Bauhaus (1919–1933) was founded by Walter Gropius in Weimar, Germany, later moving to Dessau. It brought together artists, craftspeople, and architects to unify fine art with applied design.

**Key figures and their influence on UI:**
- **Walter Gropius** — systematic thinking, modular grids
- **Wassily Kandinsky** — color-shape theory (blue/circle, yellow/triangle, red/square)
- **Herbert Bayer** — universal type (the precursor to Oswald/geometric sans)
- **László Moholy-Nagy** — light, photography, industrial materials, transparency
- **Marcel Breuer** — tubular steel furniture (the original "material honest" design)
- **Paul Klee** — compositional theory, color relationships

The Nazi regime closed the school in 1933. Its faculty dispersed globally — many to the US — seeding modernism in Chicago, Cambridge, and New York. The Bauhaus continues to influence Swiss design, the International Style, IBM design, and contemporary design systems.
