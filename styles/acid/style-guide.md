# Acid Graphics — Design System Style Guide

**Personality:** Dangerous. Neon. Monospace. Glitch. Maximum.

> "Acid is what happens when rave culture meets terminal hacking. Everything burns. Nothing is soft."

---

## Origin & Aesthetic Philosophy

Acid Graphics emerged from the intersection of **early rave culture (1987–1992)** and **hacker terminal aesthetics**. The style takes its name from the Roland TB-303 bass synthesizer — the "acid" machine — whose sound defined Chicago House and the rave movement. Visually, it translates that sonic intensity into light.

The core principle: **black background, neon light**. Every element is a signal. If it doesn't glow, it doesn't exist.

---

## Design Tokens

```css
:root {
  /* Backgrounds */
  --bg:      #000000;   /* absolute void */
  --s1:      #080808;   /* near-black surface */
  --s2:      #111111;   /* elevated surface */

  /* Chromatic palette */
  --green:   #00ff41;   /* Matrix green — primary */
  --magenta: #ff00ff;   /* Rave magenta — warning/danger */
  --yellow:  #ffff00;   /* Caution yellow — attention */
  --cyan:    #00ffff;   /* Signal cyan */
  --red:     #ff0000;   /* Alarm red */

  /* Semantic */
  --ac:      #00ff41;   /* primary accent */
  --ac2:     #ff00ff;   /* secondary accent */
  --ac3:     #ffff00;   /* tertiary accent */

  /* Text hierarchy */
  --t1:      #00ff41;                    /* primary text */
  --t2:      rgba(0,255,65,0.65);        /* secondary text */
  --t3:      rgba(0,255,65,0.35);        /* muted / metadata */

  /* Geometry */
  --r:       0px;   /* ZERO border radius. Always. */

  /* Typography */
  --f:       'Share Tech Mono', 'JetBrains Mono', 'Courier New', monospace;
  --f-disp:  'Impact', 'Arial Black', sans-serif;

  /* Motion */
  --ease:    cubic-bezier(0.4, 0, 0.2, 1);
}
```

---

## Glow System

The glow system is the foundation of Acid Graphics. Each color has a calibrated two-layer glow: a tight inner halo and a diffuse outer halo.

### Glow Recipes

```css
/* Green — primary, most used */
--glow-g: 0 0 8px #00ff41, 0 0 20px rgba(0,255,65,0.5);

/* Magenta — warning/dangerous actions */
--glow-m: 0 0 8px #ff00ff, 0 0 20px rgba(255,0,255,0.5);

/* Yellow — caution/attention */
--glow-y: 0 0 8px #ffff00, 0 0 20px rgba(255,255,0,0.5);

/* Cyan — secondary signal */
--glow-c: 0 0 8px #00ffff, 0 0 20px rgba(0,255,255,0.5);

/* Hover charge — amplified green */
--glow-g-hover: 0 0 16px #00ff41, 0 0 32px rgba(0,255,65,0.4);

/* Extreme — use sparingly for H1/hero moments */
--glow-g-hero: var(--glow-g), 0 0 60px rgba(0,255,65,0.3);
```

### Glow Application Rules

| Element | Glow Token | Notes |
|---------|-----------|-------|
| H1 display text | `--glow-g-hero` | Max 1 per page |
| Section headings | `--glow-g` | Standard |
| Active buttons | `--glow-g` / `--glow-m` / `--glow-y` | Color-matched |
| Hover buttons | `--glow-g-hover` | Amplified on hover |
| Active toggles | `--glow-g` | Track + thumb |
| Active checkboxes | `--glow-g` | Box shadow |
| Focused inputs | `0 0 12px rgba(0,255,65,0.25)` | Softer focus ring |
| Card hover | `--glow-g` | Border switches to full green |
| Player controls | `--glow-g` | Play button always glows |
| Progress bar fill | `--glow-g` | Scanning line of light |
| Slider thumb | `--glow-g` | Square thumb glows |
| Alert badges | `0 0 6px #ff0000, 0 0 12px rgba(255,0,0,0.5)` | Red alarm |

---

## Chromatic Aberration Trick

The signature glitch effect — apply to H1 or hero elements for maximum intensity:

```css
.glitch-text {
  position: relative;
  color: #00ff41;
  text-shadow: var(--glow-g);
}

.glitch-text::before,
.glitch-text::after {
  content: attr(data-text);
  position: absolute;
  inset: 0;
  clip-path: inset(0 0 60% 0);  /* adjust per frame */
}

.glitch-text::before {
  color: #ff00ff;
  transform: translateX(-2px);
  opacity: 0.8;
  animation: glitch-before 3s infinite;
}

.glitch-text::after {
  color: #00ffff;
  transform: translateX(2px);
  opacity: 0.8;
  animation: glitch-after 3s infinite;
}

@keyframes glitch-before {
  0%, 95%, 100% { clip-path: inset(0 0 100% 0); transform: translateX(0); }
  96%  { clip-path: inset(20% 0 60% 0); transform: translateX(-3px); }
  97%  { clip-path: inset(60% 0 20% 0); transform: translateX(2px); }
  98%  { clip-path: inset(0% 0 80% 0);  transform: translateX(-1px); }
}

@keyframes glitch-after {
  0%, 95%, 100% { clip-path: inset(0 0 100% 0); transform: translateX(0); }
  96%  { clip-path: inset(60% 0 20% 0); transform: translateX(3px); }
  97%  { clip-path: inset(20% 0 60% 0); transform: translateX(-2px); }
  98%  { clip-path: inset(80% 0 0% 0);  transform: translateX(1px); }
}
```

Usage: `<h1 class="glitch-text" data-text="ACID">ACID</h1>`

---

## Scanline Overlay

Add a subtle scanline effect to the full page — a CRT screen texture:

```css
body::before {
  content: '';
  position: fixed;
  inset: 0;
  background: repeating-linear-gradient(
    0deg,
    transparent,
    transparent 2px,
    rgba(0,255,65,0.015) 2px,
    rgba(0,255,65,0.015) 4px
  );
  pointer-events: none;
  z-index: 9999;
}
```

**Calibration:** `rgba(0,255,65,0.015)` is the correct intensity. Below 0.01 is invisible. Above 0.03 is distracting. Never use white scanlines.

---

## Typography

### Two Typefaces Only

**Impact** — display, headings
- Maximum visual weight
- Zero letter-spacing or positive: +0.04em
- Always uppercase
- Apply `text-shadow: var(--glow-g)` to H1–H2
- Size range: 22px – 96px+

**Share Tech Mono** (fallback: JetBrains Mono, Courier New)
- Body text, labels, metadata, terminal readouts
- Every character is a data point
- Uppercase with `letter-spacing: 0.1em–0.2em` for labels
- Size range: 10px – 16px

### Never Use
- Any rounded sans-serif (Inter, Nunito, etc.)
- Any serif typeface
- Any geometric sans (Futura, etc.)
- Variable weights — Impact is always max weight, mono is always regular

---

## Component Specs

### Sticky Nav
```css
.topnav {
  background: rgba(0,0,0,0.95);
  border-bottom: 1px solid rgba(0,255,65,0.3);
}
.tnav-title {
  font-family: var(--f-disp);
  text-shadow: var(--glow-g);
}
.tnav-dl {
  border: 1px solid #00ff41;
  color: #00ff41;
  box-shadow: var(--glow-g);
  text-shadow: var(--glow-g);
  background: transparent;
}
```

### Progress Dots (Squares)
```css
.prog-dot {
  width: 6px; height: 6px;
  border-radius: 0;  /* SQUARE — never circle */
  background: transparent;
  border: 1px solid rgba(0,255,65,0.4);
}
.prog-dot.active {
  background: var(--green);
  box-shadow: var(--glow-g);
  border-color: var(--green);
}
```

### Buttons
```css
/* Primary — execute */
.btn-p {
  border: 1px solid #00ff41;
  color: #00ff41;
  background: rgba(0,255,65,0.05);
  box-shadow: var(--glow-g);
  text-shadow: var(--glow-g);
  text-transform: uppercase;
  letter-spacing: 0.12em;
  font-family: var(--f);
  border-radius: 0;
}
.btn-p:hover {
  background: rgba(0,255,65,0.12);
  box-shadow: 0 0 16px #00ff41, 0 0 32px rgba(0,255,65,0.4);
}
.btn-p:active { background: rgba(0,255,65,0.2); }

/* Secondary — warning */
.btn-m {
  border: 1px solid #ff00ff;
  color: #ff00ff;
  background: rgba(255,0,255,0.05);
  box-shadow: var(--glow-m);
  text-shadow: var(--glow-m);
}

/* Tertiary — caution */
.btn-y {
  border: 1px solid #ffff00;
  color: #ffff00;
  background: rgba(255,255,0,0.05);
  box-shadow: var(--glow-y);
  text-shadow: var(--glow-y);
}
```

### Form Inputs
```css
.inp {
  background: rgba(0,255,65,0.03);
  border: 1px solid rgba(0,255,65,0.2);
  color: #00ff41;
  font-family: var(--f);
  caret-color: #00ff41;
  border-radius: 0;
}
.inp:focus {
  border-color: #00ff41;
  box-shadow: 0 0 12px rgba(0,255,65,0.25);
}
.label {
  color: var(--t2);
  font-family: var(--f);
  text-transform: uppercase;
  letter-spacing: 0.15em;
  font-size: 0.5625rem;
}
```

### Checkboxes (Square)
```css
.chk-box {
  width: 18px; height: 18px;
  background: transparent;
  border: 1px solid rgba(0,255,65,0.4);
  border-radius: 0;  /* SQUARE */
}
.chk-in:checked + .chk-box {
  border-color: #00ff41;
  background: rgba(0,255,65,0.15);
  box-shadow: var(--glow-g);
}
```

### Toggles (Rectangular)
```css
.tgl-track {
  width: 48px; height: 22px;
  background: rgba(0,0,0,0.8);
  border: 1px solid rgba(0,255,65,0.3);
  border-radius: 0;  /* RECTANGULAR */
}
.tgl-thumb {
  width: 14px; height: 14px;
  background: rgba(0,255,65,0.3);
  border-radius: 0;  /* SQUARE thumb */
}
.tgl-in:checked ~ .tgl-track {
  border-color: #00ff41;
  box-shadow: var(--glow-g);
}
.tgl-in:checked ~ .tgl-track .tgl-thumb {
  transform: translateX(26px);
  background: #00ff41;
  box-shadow: var(--glow-g);
}
```

### Sliders (Square Thumb)
```css
.rng { border-radius: 0; }  /* flat track */
.rng::-webkit-slider-thumb {
  -webkit-appearance: none;
  width: 12px; height: 12px;
  background: var(--green);
  box-shadow: var(--glow-g);
  border-radius: 0;  /* SQUARE */
  cursor: pointer;
}
```

### Range Fill (JS-updated)
```javascript
function updateRangeFill(el) {
  const pct = ((el.value - el.min) / (el.max - el.min)) * 100;
  el.style.background =
    `linear-gradient(to right, #00ff41 ${pct}%, rgba(0,255,65,0.12) ${pct}%)`;
}
```

---

## AI Prompting Guidance

Use these phrases when prompting an AI to generate Acid Graphics UI:

```
Design in Acid Graphics / rave terminal style:
- Black background (#000), zero border radius, zero softness
- Matrix green (#00ff41) as primary with text-shadow glow
- Magenta (#ff00ff) for warnings, yellow (#ffff00) for caution
- Share Tech Mono for all body/label text, Impact for all headings
- All headings uppercase with letter-spacing +0.04em
- All borders are glowing neon lines, not solid fills
- Buttons: transparent bg, 1px colored border, matching text-shadow
- Every interactive element must have a neon glow on active/hover state
- Scanline overlay via repeating-linear-gradient
- Square/rectangular everything — no circles, no border-radius
```

### Scenario Prompts

**For a login form:**
> "Build an access terminal form in Acid Graphics style. Black background, green monospace labels like `// OPERATOR_ID`, `// AUTH_KEY`. Inputs glow green on focus. Submit button: glowing green border, `AUTHENTICATE` in Impact font."

**For a dashboard card:**
> "Create a system panel card: near-black (#080808) background, 1px green border at 15% opacity, green neon text on hover. Header uses Impact uppercase. Body uses Share Tech Mono. Status indicator is a pulsing green square."

**For a data table:**
> "Design a data readout table: black bg, monospace font, thin 1px green horizontal rules between rows, green header text with glow. Values in bright green, secondary values in 65% green opacity. No border-radius anywhere."

---

## Anti-Patterns

### Never Do

| Anti-pattern | Why it breaks the style |
|---|---|
| `border-radius > 0` | Softness is antithetical to acid. Zero tolerance. |
| Gradients on elements | Acid uses flat color + glow only. No `linear-gradient` on UI elements. |
| Pastel or muted colors | All colors must be maximum saturation. Half-saturation is half-wrong. |
| Serif or rounded fonts | The letterform must feel mechanical. Serifs are organic. |
| Box shadows without glow | Regular drop shadows are neumorphism. Acid only uses glow shadows. |
| White as a primary color | White is for rare maximum-contrast moments only. |
| Smooth gradients as backgrounds | Background is flat black. No vignettes, no gradients. |
| Filled buttons (solid bg) | Buttons are transparent at rest — a border of light, not a filled shape. |
| Disabled as 50% opacity | Disabled should be ~20% opacity — nearly invisible, not halfway. |
| Circles for checkboxes or thumbs | All controls are square/rectangular. Circles feel friendly. Acid is not friendly. |

### Red Flags

If your design has any of these, it's not Acid:
- Something that looks "comfortable" or "approachable"
- A shadow that creates depth without glow
- A font that's "legible" at small sizes in a comfortable way
- A color that's been desaturated "for readability"
- A button that looks "pressable" (3D, rounded, shadow-lifted)

---

## Calibration Reference

The glow intensity spectrum:

```
Too weak:   text-shadow: 0 0 4px rgba(0,255,65,0.3)  → barely visible, flat
Correct:    text-shadow: 0 0 8px #00ff41, 0 0 20px rgba(0,255,65,0.5)  → electric, present
Overdone:   text-shadow: 0 0 20px #00ff41, 0 0 60px rgba(0,255,65,0.9)  → garish, unreadable
```

The goal: **electric, not blinding**. The glow should make text feel like it's lit from within, not like it's causing retinal damage.

---

## Color Semantics

| Color | Semantic | Use case |
|-------|----------|----------|
| Green `#00ff41` | Execute / Online / OK | Primary actions, success states, active elements |
| Magenta `#ff00ff` | Warning / Override | Destructive actions, system warnings |
| Yellow `#ffff00` | Caution / Attention | Alerts, notifications, approaching limits |
| Cyan `#00ffff` | Signal / Ping | Network activity, secondary info |
| Red `#ff0000` | Alarm / Error | Critical failures, badge counters |
| White `#ffffff` | Maximum | Rare highest-contrast moments only |

---

## Versioning

- Style: Acid Graphics v1.0
- Origin: Rave culture + hacker terminal, 1987–1992
- Primary color: Matrix green (#00ff41), sourced from The Matrix (1999) and phosphor monitors
- Font sources: Google Fonts (Share Tech Mono), System (Impact)
