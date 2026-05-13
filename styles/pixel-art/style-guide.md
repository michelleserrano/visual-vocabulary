# 8-Bit Pixel Art · Style Guide

**Personality:** Pixelated. Constrained. Retro-gaming. Step-animated. Chunky.

---

## Overview

A design language born from 4 colors and 8×8 pixel grids. Every aesthetic choice is a constraint inherited from 1980s hardware: the Game Boy's LCD, the NES's 2C02 PPU. When the hardware defines the aesthetic, the constraint becomes the craft.

**When to use:** Retro-gaming apps, developer tools, chiptune music players, game UIs, hackathon demos, anything that benefits from a playful, nostalgic, and opinionated visual identity.

**When NOT to use:** B2B SaaS dashboards, healthcare, finance, any product requiring WCAG AA contrast on body text (GB palette struggles at body weight).

---

## Design Tokens

```css
:root {
  /* Game Boy 4-color palette */
  --gb-1: #0f380f;  /* darkest — background */
  --gb-2: #306230;  /* dark — surfaces, borders */
  --gb-3: #8bac0f;  /* light — secondary text, mid elements */
  --gb-4: #9bbc0f;  /* lightest — primary accent, headings */

  /* Semantic aliases */
  --bg:    #0f380f;
  --s1:    #1a4a1a;          /* elevated surface */
  --s2:    #306230;          /* border / separator */
  --light: #9bbc0f;          /* primary accent */
  --lt2:   #8bac0f;          /* secondary accent */
  --t1:    #9bbc0f;          /* text primary */
  --t2:    rgba(155,188,15,0.7);   /* text secondary */
  --t3:    rgba(155,188,15,0.4);   /* text muted */

  /* Typography */
  --f:      'Press Start 2P', monospace;  /* headings, UI chrome, labels */
  --f-body: 'VT323', monospace;           /* body text, data readouts */

  /* ZERO border-radius. Always. No exceptions. */
  --r: 0px;
}

/* Force zero radius everywhere */
*, *::before, *::after {
  border-radius: 0 !important;
  image-rendering: pixelated;
  image-rendering: crisp-edges;
}
```

---

## The Pixel Border System

The single most important technique. **Never use CSS `border` for decorative borders** — use `box-shadow` instead. This allows corner cutouts that give the chipped-pixel notch characteristic of 8-bit UI elements.

```css
/* ── Full pixel border with corner cutouts ── */
.pixel-border {
  box-shadow:
    /* 4 sides */
    -2px  0    0 0 var(--light),
     2px  0    0 0 var(--light),
     0   -2px  0 0 var(--light),
     0    2px  0 0 var(--light),
    /* corner cutouts — match the background color */
    -2px -2px  0 0 var(--bg),
     2px -2px  0 0 var(--bg),
    -2px  2px  0 0 var(--bg),
     2px  2px  0 0 var(--bg);
}

/* ── Dim variant (inactive state) ── */
.pixel-border-dim {
  box-shadow:
    -2px  0    0 0 var(--s2),
     2px  0    0 0 var(--s2),
     0   -2px  0 0 var(--s2),
     0    2px  0 0 var(--s2),
    -2px -2px  0 0 var(--bg),
     2px -2px  0 0 var(--bg),
    -2px  2px  0 0 var(--bg),
     2px  2px  0 0 var(--bg);
}

/* ── Inset pixel border (for inputs, sunken panels) ── */
.pixel-border-inset {
  box-shadow:
    inset -2px  0    0 0 var(--s2),
    inset  2px  0    0 0 var(--s2),
    inset  0   -2px  0 0 var(--s2),
    inset  0    2px  0 0 var(--s2);
}
.pixel-border-inset:focus {
  box-shadow:
    inset -2px  0    0 0 var(--light),
    inset  2px  0    0 0 var(--light),
    inset  0   -2px  0 0 var(--light),
    inset  0    2px  0 0 var(--light);
}
```

**Corner cutout color must match the parent background.** When a bordered element sits on `--s1` instead of `--bg`, update the cutout color to `--s1`.

---

## Step Animation Recipe

**All animations must use `steps()`.** Never use `ease`, `ease-in-out`, or `cubic-bezier`. Every motion should feel like it's running at 8–12fps.

```css
/* ── Blinking cursor ── */
@keyframes pixel-blink {
  0%,  49% { opacity: 1; }
  50%, 100% { opacity: 0; }
}
.cursor::after {
  content: '█';
  animation: pixel-blink steps(1) 0.7s infinite;
  color: var(--light);
  margin-left: 3px;
}

/* ── Button press (2-frame) ── */
@keyframes pixel-press {
  0%   { transform: translate(0, 0); }
  50%  { transform: translate(2px, 2px); }
  100% { transform: translate(0, 0); }
}
.btn:active {
  animation: pixel-press steps(2) 0.12s;
}

/* ── Hover blink (primary button) ── */
@keyframes pixel-hover-pulse {
  0%, 100% { background: var(--light); color: var(--bg); }
  50%       { background: var(--lt2);  color: var(--bg); }
}
.btn-primary:hover {
  animation: pixel-hover-pulse steps(1) 0.4s infinite;
}

/* ── Toggle thumb (3-step snap) ── */
.tgl-thumb {
  transition: transform 0.15s steps(3), background 0.1s steps(1);
}

/* ── Scroll reveal (4-step appear) ── */
.sec {
  opacity: 0;
  transform: translateY(16px);
  transition: opacity 0.4s steps(4), transform 0.4s steps(4);
}
.sec.visible { opacity: 1; transform: translateY(0); }

/* ── Game Boy power-on ── */
@keyframes gb-poweron {
  0%   { transform: scaleY(0.02); opacity: 0; }
  40%  { transform: scaleY(0.02); opacity: 1; }
  70%  { transform: scaleY(1.02); opacity: 1; }
  100% { transform: scaleY(1);    opacity: 1; }
}
```

---

## Dithering Patterns

Dithering is the pixel art technique for creating perceived mid-tones. Use `repeating-linear-gradient` at 45° with 4px tile size.

```css
/* ── Transition zone between gb-1 and gb-2 ── */
.dither-1-2 {
  background: repeating-linear-gradient(
    45deg,
    var(--gb-1) 0px, var(--gb-1) 4px,
    var(--gb-2) 4px, var(--gb-2) 8px
  );
}

/* ── Transition zone between gb-2 and gb-3 ── */
.dither-2-3 {
  background: repeating-linear-gradient(
    45deg,
    var(--gb-2) 0px, var(--gb-2) 4px,
    var(--gb-3) 4px, var(--gb-3) 8px
  );
}

/* ── Pixel progress bar (discrete blocks) ── */
.pixel-progress-fill {
  background: repeating-linear-gradient(
    90deg,
    var(--gb-1) 0px,  var(--gb-1) 10px,
    var(--gb-2) 10px, var(--gb-2) 12px
  );
  transition: width 0.1s steps(10);
}

/* ── Dungeon floor grid ── */
.dungeon-grid {
  background-image:
    repeating-linear-gradient(0deg, transparent, transparent 11px, var(--gb-1) 11px, var(--gb-1) 12px),
    repeating-linear-gradient(90deg, transparent, transparent 11px, var(--gb-1) 11px, var(--gb-1) 12px);
  background-color: var(--gb-2);
}
```

---

## Typography Rules

| Context | Font | Size | Notes |
|---|---|---|---|
| Display / Hero | Press Start 2P | 24–80px | Letter-spacing: 0.04em |
| Section heading | Press Start 2P | 16px | Max 1 line, overflow ellipsis |
| Subheading | Press Start 2P | 12–14px | |
| UI label / button | Press Start 2P | 7–10px | Minimum readable: 7px |
| Body text | VT323 | 18–22px | Line-height: 1.4–1.6 |
| Data readout | VT323 | 20–36px | Score counters, timers |
| Caption | Press Start 2P | 6–7px | Letter-spacing: 0.06em |

**Google Fonts import:**
```html
<link href="https://fonts.googleapis.com/css2?family=Press+Start+2P&family=VT323:wght@400&display=swap" rel="stylesheet">
```

**Disable font smoothing** — pixel fonts must NOT be antialiased:
```css
body {
  -webkit-font-smoothing: none;
  font-smooth: never;
}
```

---

## 4-Color Constraint Rules

1. **Only 4 hex values exist:** `#0f380f` `#306230` `#8bac0f` `#9bbc0f`
2. Never introduce a 5th color — not even for error states or hover effects
3. Error → use `--gb-1` (darkest, inversion)
4. Success → use `--light` (already the "positive" register)
5. Depth comes from dithering between adjacent palette values, never from gradients
6. Transparency (`rgba`) is allowed only for text opacity values, not fills

---

## CSS Pixel Sprite Technique

Draw pixel art directly in CSS using `box-shadow` on a 1×1px element. Each shadow tuple is `x-offset y-offset 0 0 color`.

```css
/* 1×1 anchor — place anywhere */
.sprite {
  position: relative;
  width: 1px;
  height: 1px;
}

/* Example: 5×5 pixel diamond ♦ */
.sprite-diamond {
  box-shadow:
    /* Row 1 */
    2px 0 0 0 var(--light),
    /* Row 2 */
    1px 1px 0 0 var(--light),
    2px 1px 0 0 var(--light),
    3px 1px 0 0 var(--light),
    /* Row 3 */
    0 2px 0 0 var(--light),
    1px 2px 0 0 var(--light),
    2px 2px 0 0 var(--light),
    3px 2px 0 0 var(--light),
    4px 2px 0 0 var(--light),
    /* Row 4 */
    1px 3px 0 0 var(--light),
    2px 3px 0 0 var(--light),
    3px 3px 0 0 var(--light),
    /* Row 5 */
    2px 4px 0 0 var(--light);
}
```

Scale by setting `transform: scale(4)` — `image-rendering: pixelated` keeps it crisp.

---

## CRT Scanline Effect

Apply to Game Boy screens and display panels for the LCD feel:

```css
.gb-screen {
  background: var(--gb-3);
  position: relative;
  overflow: hidden;
}
.gb-screen::after {
  content: '';
  position: absolute;
  inset: 0;
  background: repeating-linear-gradient(
    0deg,
    transparent       0px, transparent       3px,
    rgba(15,56,15,0.12) 3px, rgba(15,56,15,0.12) 4px
  );
  pointer-events: none;
  z-index: 1;
}
```

---

## Component Checklist

Before shipping any component in this style, verify:

- [ ] `border-radius: 0` on every element (enforced globally with `!important`)
- [ ] All borders are via `box-shadow`, not CSS `border`
- [ ] All animations use `steps()` timing — no `ease` or `cubic-bezier`
- [ ] Only the 4 GB palette colors appear in fills (alpha is OK for text)
- [ ] Press Start 2P at minimum 7px (anything smaller becomes unreadable pixels)
- [ ] `image-rendering: pixelated` on all elements
- [ ] Interactive elements have pixel-press (translate 2px/2px) on `:active`
- [ ] Blinking cursor on text inputs (`:focus ~ ::after` with `pixel-blink`)
- [ ] Toggle thumb uses `steps(3)` for discrete snap movement
- [ ] Card top border is 4px solid `--light` (cartridge label stripe)

---

## AI Prompting Guidance

When prompting an AI to build in this style, lead with constraints:

```
Build a [component] in 8-bit pixel art style:
- Background: #0f380f (Game Boy darkest green)
- Only 4 colors: #0f380f #306230 #8bac0f #9bbc0f
- Font: Press Start 2P (headings/UI), VT323 (body)
- ZERO border-radius everywhere (border-radius: 0 !important)
- Borders via box-shadow with corner cutouts, NOT CSS border
- All animations must use steps() timing function only
- image-rendering: pixelated on all elements
- Active/press state: translate(2px, 2px) with steps(2)
```

**Anti-patterns to reject from AI output:**
- `border-radius` on any element
- `ease`, `ease-in-out`, or `cubic-bezier` in any transition or animation
- Colors outside the 4-value palette
- Smooth gradients (dithered patterns only)
- CSS `border` for pixel borders
- Font weights other than 400 for both fonts (neither has weight variants)

---

## Reference Implementations

| Element | Key technique |
|---|---|
| Pixel border | `box-shadow` 4-side + corner cutout |
| Progress bar | `repeating-linear-gradient(90deg)` blocks |
| Dithering | `repeating-linear-gradient(45deg)` 4px tiles |
| CRT screen | `repeating-linear-gradient(0deg)` 4px scanlines |
| Blinking cursor | `steps(1) 0.7s infinite` |
| Button press | `steps(2) 0.12s` + translate(2px,2px) |
| Toggle snap | `steps(3) 0.15s` |
| Scroll reveal | `steps(4) 0.4s` on opacity + translateY |
| GB power-on | `steps(3) 0.6s` scaleY(0.02) → scaleY(1) |

---

*Inspired by Nintendo Game Boy (1989), NES (1983), and the constraint-driven craft of early pixel artists.*
