# TRON Legacy · Style Guide

**Personality:** Luminous. Digital. Monochromatic. Circuit-board. Atmospheric.

A design language derived entirely from the visual language of *TRON: Legacy* (2010). Every surface is dark. Every edge is illuminated. There is one color. It glows.

---

## Core Principle

> The entire visual language comes from **ONE color at different opacity levels.**
>
> `#00e5ff` at 95% is a title. At 55% it's body text. At 28% it's a placeholder. At 12% it's a fill. At 5% it's a background wash. The grid is built from a single wavelength — everything else is how much darkness you allow through.

Never introduce a second hue. The monochromatic constraint is what creates the atmosphere. The moment you add purple or blue as a variant, the Grid collapses.

---

## Design Tokens

```css
:root {
  /* Backgrounds — layers of dark */
  --bg:       #060a0f;          /* void — deepest layer */
  --s1:       #0a1628;          /* surface */
  --s2:       #0d1f2d;          /* elevated surface */
  --s3:       #112235;          /* top surface */

  /* The One Color */
  --ac:       #00e5ff;          /* THE color — cyan only */
  --ac-dim:   rgba(0,229,255,0.12);
  --ac-mid:   rgba(0,229,255,0.35);
  --ac-glo:   rgba(0,229,255,0.55);

  /* Text — all the same color, different density */
  --t1:       rgba(0,229,255,0.95);  /* primary text */
  --t1-solid: #00e5ff;
  --t2:       rgba(0,229,255,0.55);  /* secondary text */
  --t3:       rgba(0,229,255,0.28);  /* muted / placeholder */

  /* Status — the only colors besides cyan */
  --ok:       #39ff14;          /* neon green — success */
  --err:      #ff2d55;          /* red — error / alert */
  --warn:     #ffcc00;          /* yellow — caution */

  /* Radius — sharp geometry only */
  --r:        2px;
  --r-sm:     1px;
  --r-md:     4px;
  --r-full:   9999px;           /* progress bars only */

  /* Type */
  --f:        'Share Tech Mono', 'JetBrains Mono', 'Courier New', monospace;

  /* Easing */
  --ease:     cubic-bezier(0.4,0,0.2,1);
  --ease-out: cubic-bezier(0,0,0.2,1);

  /* Borders */
  --border:     1px solid rgba(0,229,255,0.35);
  --border-glo: 1px solid #00e5ff;
}
```

---

## Glow System

The entire depth system is expressed through `box-shadow`. No drop shadows, no gradients. Light radiates outward.

| Token       | Value                                                                                    | Use case                        |
|-------------|------------------------------------------------------------------------------------------|----------------------------------|
| `--glow-xs` | `0 0 6px rgba(0,229,255,0.4)`                                                           | Subtle presence — borders, labels |
| `--glow-sm` | `0 0 10px rgba(0,229,255,0.5), 0 0 4px rgba(0,229,255,0.8)`                            | Interactive elements at rest      |
| `--glow-md` | `0 0 16px rgba(0,229,255,0.55), 0 0 6px rgba(0,229,255,0.9)`                           | Hover states, active indicators   |
| `--glow-lg` | `0 0 28px rgba(0,229,255,0.6), 0 0 10px rgba(0,229,255,1), 0 0 2px rgba(0,229,255,1)` | Primary button hover, max energy  |

**Rule:** Each level adds one more value. The outermost layer is ambient (large radius, lower opacity). The innermost is the flash (tight radius, full opacity). Layering three values creates the illusion of a physical light source.

---

## Circuit Grid Background

Applied to `body` and optionally to dark section backgrounds:

```css
body {
  background-color: #060a0f;
  background-image:
    linear-gradient(rgba(0,229,255,0.05) 1px, transparent 1px),
    linear-gradient(90deg, rgba(0,229,255,0.05) 1px, transparent 1px);
  background-size: 24px 24px;
}
```

The grid is always present. It is never a decoration — it is the structure of the world. Keep opacity at 0.04–0.06. Higher than 0.08 looks noisy; lower than 0.03 disappears on most displays.

---

## Typography

**Typeface:** `Share Tech Mono` (Google Fonts) — designed for digital display panels.

Fallback stack: `'JetBrains Mono', 'Courier New', monospace`

| Role       | Size     | Letter-spacing | Case      | Effect            |
|------------|----------|----------------|-----------|-------------------|
| Display    | 48–88px  | +0.08em        | UPPERCASE | `text-shadow: var(--glow-md)` |
| H1         | 36px     | +0.06em        | UPPERCASE | `text-shadow: var(--glow-sm)` |
| H2–H4      | 22–28px  | +0.04–0.05em   | Title     | no glow           |
| Body Lg    | 15px     | +0.03em        | normal    | `color: var(--t2)` |
| Body       | 14px     | +0.02em        | normal    | `color: var(--t2)` |
| Label / Cap| 10px     | +0.12–0.18em   | UPPERCASE | `color: var(--t3)` |

**Rule:** Section headings are always `text-transform: uppercase; letter-spacing: 0.06em`. Labels are uppercase at small sizes. Body text is mixed case — data streams don't need to shout.

---

## Component Specifications

### Buttons

```css
/* Primary */
.btn-p {
  background: transparent;
  border: 1px solid var(--ac);
  color: var(--ac);
  text-shadow: var(--glow-xs);
  box-shadow: var(--glow-sm), inset 0 0 20px rgba(0,229,255,0.05);
  text-transform: uppercase;
  letter-spacing: 0.1em;
}
.btn-p:hover {
  box-shadow: var(--glow-lg), inset 0 0 30px rgba(0,229,255,0.1);
  text-shadow: var(--glow-md);
}
.btn-p:active {
  background: rgba(0,229,255,0.15);
  box-shadow: var(--glow-sm);
}

/* Secondary */
.btn {
  background: transparent;
  border: 1px solid rgba(0,229,255,0.25);
  color: var(--t2);
}
.btn:hover {
  border-color: var(--ac);
  color: var(--ac);
  box-shadow: var(--glow-xs);
}
```

**Mental model:** The button is the edge of a light conduit. At rest: a faint boundary. On hover: the conduit activates. On press: energy fills the interior.

### Form Inputs

```css
.inp {
  background: rgba(0,229,255,0.03);
  border: 1px solid rgba(0,229,255,0.2);
  color: var(--t1);
  font-family: var(--f);
  padding: 0.75rem 1rem;
}
.inp::placeholder { color: var(--t3); }
.inp:focus {
  border-color: var(--ac);
  box-shadow: var(--glow-sm), inset 0 0 20px rgba(0,229,255,0.03);
  outline: none;
}
```

**Mental model:** Inputs are recessed data slots in the grid surface. The border is dim until you interact — then the panel illuminates around the entry point.

### Cards

```css
.card {
  background: var(--s1);
  border: 1px solid rgba(0,229,255,0.2);
  box-shadow: var(--glow-xs);
  position: relative;
  overflow: hidden;
}
/* Cyan top accent — marks the card as an active data panel */
.card::before {
  content: '';
  position: absolute;
  top: 0; left: 0; right: 0;
  height: 2px;
  background: var(--ac);
  box-shadow: var(--glow-sm);
}
.card:hover {
  border-color: var(--ac);
  box-shadow: var(--glow-md);
}
```

**Rule:** Every card has the 2px cyan top bar. This is the visual signal that distinguishes a card from a background surface. It is non-negotiable.

### Toggles

- Track: dark background, `border: 1px solid rgba(0,229,255,0.25)`
- Thumb at rest: `background: rgba(0,229,255,0.3)`, dim border
- Track active: `border-color: var(--ac)`, `box-shadow: var(--glow-xs)`
- Thumb active: `background: var(--ac)`, `box-shadow: var(--glow-sm)`, translates 24px

### Progress Dots (side nav)

```css
.prog-dot {
  width: 6px; height: 6px;
  border-radius: 0;              /* square, not round */
  background: transparent;
  border: 1px solid rgba(0,229,255,0.3);
}
.prog-dot.active {
  background: var(--ac);
  box-shadow: var(--glow-sm);
  border-color: var(--ac);
}
```

**Note:** Squares, not circles. The grid is rectilinear. Round dots belong to other aesthetics.

---

## Scanline Atmosphere

A subtle scanline overlay completes the CRT/monitor feel:

```css
body::after {
  content: '';
  position: fixed;
  inset: 0;
  pointer-events: none;
  z-index: 9999;
  background: repeating-linear-gradient(
    0deg,
    transparent,
    transparent 2px,
    rgba(0,0,0,0.03) 2px,
    rgba(0,0,0,0.03) 4px
  );
}
```

Keep opacity at `0.03`. Higher than `0.05` becomes distracting. The goal is subliminal texture, not retro camp.

---

## Layout Rules

- **Max content width:** 900px, centered
- **Section spacing:** `margin-top: 5rem`
- **All section headings:** `text-transform: uppercase; letter-spacing: 0.06em; text-shadow: var(--glow-sm)`
- **Ghost section numbers:** `color: rgba(0,229,255,0.04)` — exist as watermarks, not UI
- **Section dividers:** `border-bottom: 1px solid rgba(0,229,255,0.15)` — dim, not decorative

---

## Anti-Patterns

| ❌ Don't | ✓ Do instead |
|---------|-------------|
| Use rounded corners > 4px | Keep radius ≤ 4px; squares define the grid |
| Add a second accent color | Use status colors only for err/warn/ok states |
| Use a non-monospace font for any UI text | Enforce `--f` everywhere |
| Add gradients to backgrounds | Use flat dark backgrounds + circuit grid |
| Increase glow beyond `--glow-lg` | More glow reduces contrast, not increases it |
| Use white text | All text is cyan at varying opacity |
| Add box-shadow `inset` for depth | Inset shadows are neumorphism — not TRON |

---

## AI Prompting Guidance

When prompting an AI to generate in this style:

```
Design in TRON Legacy style:
- Background #060a0f with a 24px cyan grid overlay at 5% opacity
- Single accent color: #00e5ff (cyan). No other colors except status (#39ff14 ok, #ff2d55 err)
- All borders: 1px solid rgba(0,229,255,0.2) at rest, rgba(0,229,255,1) on focus/hover
- Glow effects via box-shadow only: 3 layers (ambient 28px, mid 10px, flash 2px)
- Font: Share Tech Mono monospace everywhere
- All labels: uppercase, letter-spacing 0.1em+
- No rounded corners (max-radius: 4px)
- No fills on interactive elements — borders and glow only
- Cards: 2px solid cyan top border, dark body
- Scanline overlay: repeating horizontal lines at 3% opacity
```

---

## Reference

- **Film:** TRON: Legacy (2010), dir. Joseph Kosinski
- **Production design:** Darren Gilford
- **Grid concept:** The Grid is a virtual world made of light — every surface is dark matter, every edge is a photon. The UI should feel like you are *inside the computer*, not looking at a screen.
- **Typeface:** [Share Tech Mono](https://fonts.google.com/specimen/Share+Tech+Mono) — Google Fonts, free for commercial use
