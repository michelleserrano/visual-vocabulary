# Y2K Chrome · Style Guide

**Personality:** Iridescent. Bubbly. Optimistic. Holographic. Soft.

> Windows Aero meets Lisa Frank meets early iTunes visualizer. Everything shimmers. Nothing is flat. Joy is mandatory.

---

## Design Philosophy

Y2K Chrome is the design language of millennium optimism — surfaces that catch light like CDs, buttons that beg to be pressed, gradients that can't decide what color they want to be. The aesthetic sits at the intersection of early 2000s OS chrome (Windows XP, macOS Aqua), Lisa Frank's rainbow maximalism, and the pastel internet of the late 90s.

**Three laws:**
1. No matte surfaces. Every element must shimmer.
2. Maximum roundness. Square corners are banned.
3. The shine overlay `::before` must be present on every elevated element.

---

## Design Tokens

```css
:root {
  /* Backgrounds */
  --bg-grad:    linear-gradient(135deg, #d4f1ff 0%, #e8c8ff 50%, #ffd4f0 100%);
  --surface:    rgba(255,255,255,0.78);
  --surface-2:  rgba(255,255,255,0.55);

  /* Chrome patterns */
  --chrome:     linear-gradient(135deg, rgba(255,255,255,0.92), rgba(200,220,255,0.72));
  --iridescent: conic-gradient(from 180deg, #ff77e9 0%, #b3b3ff 25%, #74d4ff 50%, #a8f0c8 75%, #ff77e9 100%);

  /* Borders */
  --border:     1px solid rgba(255,255,255,0.85);
  --border-col: rgba(180,180,255,0.4);

  /* Text */
  --t1:    #3a3a8c;   /* primary — deep periwinkle blue */
  --t2:    #6060a8;   /* muted */
  --t3:    #9090c8;   /* faint */

  /* Accent palette */
  --ac:    #ff77e9;   /* hot pink — primary action */
  --ac2:   #7b7bff;  /* periwinkle — secondary */
  --ac3:   #74d4ff;  /* baby blue — tertiary */

  /* Status */
  --ok:    #a8f0c8;  /* mint green */
  --err:   #ff8fa8;  /* blush */
  --warn:  #ffe8a0;  /* soft yellow */

  /* Radius scale */
  --r-sm:  14px;
  --r:     20px;
  --r-md:  28px;
  --r-lg:  40px;
  --r-full: 9999px;

  /* Easing */
  --ease:   cubic-bezier(0.4,0,0.2,1);
  --spring: cubic-bezier(0.34,1.56,0.64,1);

  /* Typography */
  --f: 'Fredoka', system-ui, sans-serif;

  /* Chrome shine overlay — apply to all elevated elements */
  --shine: linear-gradient(135deg, rgba(255,255,255,0.6) 0%, rgba(255,255,255,0) 60%);
}
```

---

## Chrome Shine Pattern

The single most important Y2K technique. Every elevated surface gets a `::before` pseudo-element with `--shine`:

```css
.elevated-element {
  position: relative;
  overflow: hidden;
}
.elevated-element::before {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(135deg, rgba(255,255,255,0.6) 0%, rgba(255,255,255,0) 60%);
  pointer-events: none;
  z-index: 1; /* above background, below content */
}
```

Apply to: cards, buttons, form panels, nav bars, hero widgets, player, swatches — everything that has a surface.

---

## Iridescent Gradient System

### Static iridescent
```css
background: conic-gradient(from 180deg, #ff77e9 0%, #b3b3ff 25%, #74d4ff 50%, #a8f0c8 75%, #ff77e9 100%);
```

### Animated holographic
```css
@keyframes holo {
  0%   { filter: hue-rotate(0deg); }
  100% { filter: hue-rotate(360deg); }
}
.holo {
  background: conic-gradient(from 180deg, #ff77e9 0%, #b3b3ff 25%, #74d4ff 50%, #a8f0c8 75%, #ff77e9 100%);
  animation: holo 6s linear infinite;
}
```

### Gradient text
```css
.gradient-text {
  background: linear-gradient(135deg, #3a3a8c 0%, #7b7bff 40%, #ff77e9 80%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}
```

### Primary gradient (buttons, CTAs)
```css
background: linear-gradient(135deg, #ff77e9, #b3b3ff);
```

### Progress/slider gradient
```css
background: linear-gradient(90deg, #ff77e9, #b3b3ff, #74d4ff);
```

---

## Typography

**Font:** Fredoka (Google Fonts)
```html
<link href="https://fonts.googleapis.com/css2?family=Fredoka:wght@300;400;500;600;700&display=swap" rel="stylesheet">
```

| Role      | Size  | Weight | Notes                            |
|-----------|-------|--------|----------------------------------|
| Display   | 48px  | 700    | Gradient text on hero headings   |
| H1        | 36px  | 600    |                                  |
| H2        | 28px  | 600    |                                  |
| H3        | 22px  | 500    |                                  |
| H4        | 18px  | 500    |                                  |
| Body Lg   | 17px  | 400    | lh 1.6                           |
| Body      | 16px  | 400    | lh 1.55                          |
| Body Sm   | 14px  | 400    | lh 1.5                           |
| Caption   | 12px  | 500    | +0.06em, uppercase               |

**Never use:** condensed typefaces, high-contrast serifs, geometric grotesques. The rounded letterform is structural to the aesthetic.

---

## Component Recipes

### Button — Primary
```css
.btn-primary {
  background: linear-gradient(135deg, #ff77e9, #b3b3ff);
  color: white;
  border: 1px solid rgba(255,255,255,0.6);
  border-radius: 9999px;
  box-shadow: 0 6px 24px rgba(255,119,233,0.4), inset 0 1px 0 rgba(255,255,255,0.5);
  position: relative;
  overflow: hidden;
  /* + ::before shine */
}
.btn-primary:hover { box-shadow: 0 8px 32px rgba(255,119,233,0.55); transform: translateY(-2px); }
.btn-primary:active { transform: translateY(1px); box-shadow: 0 4px 16px rgba(255,119,233,0.4); }
```

### Button — Secondary (Chrome)
```css
.btn-secondary {
  background: rgba(255,255,255,0.78);
  color: #3a3a8c;
  border: 1px solid rgba(180,180,255,0.4);
  border-radius: 9999px;
  box-shadow: 0 4px 16px rgba(0,0,0,0.08), inset 0 1px 0 rgba(255,255,255,0.7);
  position: relative;
  overflow: hidden;
  /* + ::before shine */
}
```

### Form Input
```css
.input {
  background: rgba(255,255,255,0.78);
  border: 1px solid rgba(180,180,255,0.3);
  border-radius: 20px;
  box-shadow: inset 0 2px 8px rgba(100,100,200,0.06);
}
.input:focus {
  border-color: #ff77e9;
  box-shadow: 0 0 0 3px rgba(255,119,233,0.2), inset 0 2px 8px rgba(100,100,200,0.06);
}
```

### Card
```css
.card {
  background: rgba(255,255,255,0.78);
  border: 1px solid rgba(255,255,255,0.8);
  border-radius: 40px;
  box-shadow: 0 8px 32px rgba(150,100,200,0.15), inset 0 1px 0 rgba(255,255,255,0.7);
  position: relative;
  overflow: hidden;
  /* + ::before shine */
}
.card:hover { transform: translateY(-6px); box-shadow: 0 16px 48px rgba(150,100,200,0.22), inset 0 1px 0 rgba(255,255,255,0.7); }
```

### Toggle
```css
.toggle-track {
  background: rgba(180,180,255,0.2);
  border-radius: 9999px;
  transition: background 0.28s;
}
.toggle-track[aria-checked="true"] {
  background: linear-gradient(135deg, #ff77e9, #b3b3ff);
}
.toggle-thumb {
  background: white;
  border-radius: 50%;
  box-shadow: 0 2px 8px rgba(150,100,200,0.2);
  transition: transform 0.3s cubic-bezier(0.34,1.56,0.64,1);
}
```

### Checkbox (circular)
```css
.checkbox {
  border-radius: 50%; /* Y2K: circles, not squares */
  border: 2px solid rgba(180,180,255,0.4);
}
.checkbox:checked {
  background: linear-gradient(135deg, #ff77e9, #b3b3ff);
  border-color: transparent;
}
```

### Section pill label
```css
.sec-pill {
  background: linear-gradient(135deg, #ff77e9, #b3b3ff);
  color: white;
  border-radius: 9999px;
  box-shadow: 0 3px 10px rgba(255,119,233,0.3);
  position: relative;
  overflow: hidden;
  /* + ::before shine */
}
```

---

## Color Decisions

| Token | Hex / Value | Use |
|-------|-------------|-----|
| `--ac` hot pink | `#ff77e9` | Primary CTA, active state, focus ring color |
| `--ac2` periwinkle | `#7b7bff` | Secondary accents, pill badges, hover tints |
| `--ac3` baby blue | `#74d4ff` | Tertiary, gradient endpoints, cool accents |
| `--ok` mint | `#a8f0c8` | Success states |
| `--err` blush | `#ff8fa8` | Error states (soft — not alarming) |
| `--t1` deep periwinkle | `#3a3a8c` | All primary text |
| `--surface` | `rgba(255,255,255,.78)` | Card/panel backgrounds |
| `--surface-2` | `rgba(255,255,255,.55)` | Nested panels, items inside cards |

**Section ghost numbers:** `color: rgba(123,123,255,0.06)` — barely visible, just a hint of depth.

---

## Body & Background

```css
body {
  background: linear-gradient(135deg, #d4f1ff 0%, #e8c8ff 50%, #ffd4f0 100%);
  background-attachment: fixed; /* crucial — gradient stays fixed while content scrolls */
  color: #3a3a8c;
  font-family: 'Fredoka', system-ui, sans-serif;
}
```

`background-attachment: fixed` is what makes the gradient feel like a light-field behind the UI — not a static image that scrolls with it.

---

## Shadow System

Y2K doesn't use neumorphic dual shadows. It uses:

| Role | Value |
|------|-------|
| Card at rest | `0 8px 32px rgba(150,100,200,0.15)` |
| Card hover | `0 16px 48px rgba(150,100,200,0.22)` |
| Button primary | `0 6px 24px rgba(255,119,233,0.4)` |
| Button primary hover | `0 8px 32px rgba(255,119,233,0.55)` |
| Button secondary | `0 4px 16px rgba(0,0,0,0.08)` |
| Inset top highlight | `inset 0 1px 0 rgba(255,255,255,0.7)` (add to all cards) |
| Focus ring | `0 0 0 3px rgba(255,119,233,0.2)` |
| Input inset | `inset 0 2px 8px rgba(100,100,200,0.06)` |

---

## Animation Principles

- **Hover lift:** `transform: translateY(-2px)` on buttons, `translateY(-6px)` on cards
- **Spring:** Use `cubic-bezier(0.34,1.56,0.64,1)` for toggle thumbs and nav item hover — slight overshoot is joyful
- **Ease standard:** `cubic-bezier(0.4,0,0.2,1)` for shadows and opacity
- **Holo animation:** `filter: hue-rotate` on iridescent elements, 4–8s duration, linear
- **Pulse glow:** Keyframe alternating box-shadow between two accent colors (useful for player art)
- **Scroll reveal:** `opacity: 0 → 1` + `translateY(24px → 0)` at `threshold: 0.15`

---

## Backdrop Filter Usage

Use `backdrop-filter: blur(...)` on:
- Sticky nav: `blur(20px)` — must have semi-transparent background
- Spec callouts: `blur(10px)` 
- Nav bar: `blur(16px)`
- Search bars: `blur(6–8px)`

Always pair with a semi-transparent background. Never use on fully opaque surfaces — the glass effect requires the background to show through.

---

## AI Prompting Guidance

Use these phrases to get Y2K Chrome UI from any AI system:

**Style prompts:**
- "Y2K chrome aesthetic with iridescent pastel gradients and bubble UI"
- "Windows Aero meets Lisa Frank — frosted glass, pink-to-periwinkle gradients, maximum roundness"
- "Holographic UI with conic gradients, shine overlays, and Fredoka font"
- "Pastel Y2K style: everything glass, nothing square, pink glow on interactive elements"

**Component prompts:**
- Buttons: "gradient pill button with shine overlay and soft pink drop shadow"
- Cards: "frosted glass card with very rounded corners (40px), pastel gradient thumbnail, chrome inset highlight"
- Inputs: "glass input field with periwinkle border, pink focus glow ring"
- Toggles: "super rounded toggle with gradient active track and spring animation"
- Player: "chrome disc player with gradient play button and gradient progress bar"

**Anti-patterns to avoid:**
- Flat fills (no gradients)
- Square or sharp corners
- Dark/neon colors (this is pastel, not cyberpunk)
- Heavy drop shadows (keep them soft and purple-tinted)
- Monochrome UI (everything should have color)
- System fonts (Fredoka is non-negotiable)

---

## Accessibility Notes

Y2K Chrome's pastel palette creates real contrast challenges:

- **Text on glass:** `#3a3a8c` on `rgba(255,255,255,0.78)` achieves WCAG AA for normal text
- **Never:** white text on light gradients — pink buttons with white text pass only at `font-size: 16px+, font-weight: 500+`
- **Focus rings:** Always use `box-shadow: 0 0 0 3px rgba(255,119,233,0.2)` — visible but not jarring
- **Interactive affordance:** The pink accent must carry all interactive signals. Don't rely on subtle tint changes alone.
- **Reduced motion:** Wrap all `animation` and `transition` with `@media (prefers-reduced-motion: reduce)` override

---

## Quick-Reference Cheat Sheet

```
Surface:      rgba(255,255,255,0.78) + border: 1px solid rgba(255,255,255,0.8)
Shine:        ::before { background: linear-gradient(135deg,rgba(255,255,255,.6) 0%,rgba(255,255,255,0) 60%) }
Primary CTA:  linear-gradient(135deg,#ff77e9,#b3b3ff) · shadow: 0 6px 24px rgba(255,119,233,.4)
Focus ring:   box-shadow: 0 0 0 3px rgba(255,119,233,.2)
Hover lift:   transform: translateY(-2px) [buttons] / translateY(-6px) [cards]
Radius:       14 · 20 · 28 · 40 · 9999px
Font:         Fredoka 300–700
Text:         #3a3a8c / #6060a8 / #9090c8
Bg fixed:     linear-gradient(135deg,#d4f1ff,#e8c8ff,#ffd4f0) + background-attachment: fixed
```
