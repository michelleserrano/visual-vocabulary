# Vaporwave · Style Guide

**Personality:** Dreamy. Nostalgic. Neon. Retrowave. Gradient-saturated.

A digital dreamspace suspended between the 1980s and 1990s. Pink bleeds into purple bleeds into cyan — a sunset glimpsed through a cathode-ray tube. Retrofuturism made neon. Nostalgia made interactive.

---

## Design Tokens

```css
:root {
  /* Backgrounds */
  --bg:      #1a0533;   /* deep void — the space between stars */
  --s1:      #2d1052;   /* surface — elevated panels */
  --s2:      #0f001e;   /* deep surface — navbars, overlays */
  --s3:      rgba(123,47,255,0.2);  /* subtle tint for layering */

  /* Neon spectrum */
  --pink:    #ff6ec7;   /* primary — hot pink, signature color */
  --purple:  #7b2fff;   /* mid — electric violet */
  --cyan:    #00d4ff;   /* secondary — electric blue-cyan */
  --lavender:#b388ff;   /* h3 headings, softer accent */
  --teal:    #00e5cc;   /* green-teal, third card accent */
  --ac:      #ff6ec7;   /* alias — primary action */
  --ac2:     #00d4ff;   /* alias — secondary action */

  /* Text */
  --t1:  #f0e6ff;                    /* primary — near-white with purple cast */
  --t2:  rgba(240,230,255,0.68);     /* muted */
  --t3:  rgba(240,230,255,0.38);     /* faint — labels, hints, placeholders */

  /* Radius */
  --r-sm:   4px;
  --r:      8px;
  --r-md:   12px;
  --r-lg:   16px;
  --r-full: 9999px;

  /* Typography */
  --f-disp: 'Orbitron', sans-serif;        /* display / headers — geometric, futuristic */
  --f:      'Exo 2', system-ui, sans-serif; /* body — angular, condensed */

  /* Easing */
  --ease:   cubic-bezier(0.4, 0, 0.2, 1);
  --spring: cubic-bezier(0.34, 1.56, 0.64, 1);

  /* Glow system */
  --glow-p: 0 0 12px rgba(255,110,199,0.6), 0 0 28px rgba(255,110,199,0.3);  /* pink */
  --glow-c: 0 0 12px rgba(0,212,255,0.6),   0 0 28px rgba(0,212,255,0.3);   /* cyan */
  --glow-v: 0 0 12px rgba(123,47,255,0.6),  0 0 28px rgba(123,47,255,0.3);  /* violet */
}
```

---

## Gradient Text

The single most important visual rule. All display headings use a pink-to-purple-to-cyan gradient applied as a text fill.

```css
.grad-text {
  background: linear-gradient(90deg, #ff6ec7 0%, #7b2fff 50%, #00d4ff 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}
```

Variations:
- **Pink → Purple:** `linear-gradient(90deg, #ff6ec7 0%, #7b2fff 100%)`
- **Purple → Cyan:** `linear-gradient(90deg, #7b2fff 0%, #00d4ff 100%)`
- **Full spectrum:** `linear-gradient(90deg, #ff6ec7 0%, #7b2fff 50%, #00d4ff 100%)`

---

## Perspective Grid

The signature vaporwave visual. Applied as a fixed background element.

```css
.vapor-grid {
  position: fixed;
  bottom: 0; left: 0; right: 0;
  height: 45vh;
  z-index: 0;
  background:
    linear-gradient(rgba(255,110,199,0.15) 1px, transparent 1px),
    linear-gradient(90deg, rgba(255,110,199,0.1) 1px, transparent 1px);
  background-size: 40px 20px;
  transform: perspective(400px) rotateX(30deg);
  transform-origin: bottom center;
  pointer-events: none;
}
```

For card thumbnails (smaller grid):
```css
.card-grid-lines {
  position: absolute; inset: 0;
  background:
    linear-gradient(rgba(255,255,255,0.05) 1px, transparent 1px),
    linear-gradient(90deg, rgba(255,255,255,0.05) 1px, transparent 1px);
  background-size: 20px 12px;
  transform: perspective(100px) rotateX(15deg);
  transform-origin: bottom;
}
```

---

## Glow System

Three glow tokens — pink, cyan, violet — applied via `box-shadow`.

```css
/* Pink glow — primary interactive elements */
box-shadow: 0 0 12px rgba(255,110,199,0.6), 0 0 28px rgba(255,110,199,0.3);

/* Cyan glow — secondary / cool elements */
box-shadow: 0 0 12px rgba(0,212,255,0.6), 0 0 28px rgba(0,212,255,0.3);

/* Violet glow — cards, panels on hover */
box-shadow: 0 0 12px rgba(123,47,255,0.6), 0 0 28px rgba(123,47,255,0.3);

/* Enhanced hover glow (buttons, CTAs) */
box-shadow: 0 0 20px rgba(255,110,199,0.7), 0 0 40px rgba(255,110,199,0.4);
```

---

## Typography

### Font Stack
```html
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;500;600;700;800;900&family=Exo+2:ital,wght@0,300;0,400;0,500;0,600;0,700;0,800;1,400&display=swap" rel="stylesheet">
```

### Scale

| Role     | Font     | Size     | Weight | Notes                         |
|----------|----------|----------|--------|-------------------------------|
| Display  | Orbitron | 48px     | 900    | Gradient text, uppercase      |
| H1       | Orbitron | 36px     | 800    | Gradient text, +0.03em        |
| H2       | Orbitron | 28px     | 700    | Gradient text                 |
| H3       | Orbitron | 22px     | 700    | `--lavender` color            |
| H4       | Orbitron | 18px     | 600    | `--t1` color                  |
| Body Lg  | Exo 2    | 17px     | 400    | lh 1.6, `--t1`                |
| Body     | Exo 2    | 16px     | 400    | lh 1.55, `--t2`               |
| Body Sm  | Exo 2    | 14px     | 400    | lh 1.5                        |
| Caption  | Orbitron | 12px     | 600    | Uppercase, +0.1em, `--cyan`   |

---

## Color Palette

| Token       | Hex       | Usage                              |
|-------------|-----------|-----------------------------------|
| `--bg`      | `#1a0533` | Page background — the void        |
| `--s1`      | `#2d1052` | Cards, panels, elevated surfaces  |
| `--s2`      | `#0f001e` | Deep panels, navbar bg            |
| `--pink`    | `#ff6ec7` | Primary action, borders, glows    |
| `--purple`  | `#7b2fff` | Mid-spectrum, gradient anchor     |
| `--cyan`    | `#00d4ff` | Secondary, cool accents           |
| `--lavender`| `#b388ff` | H3 headings, soft accent          |
| `--teal`    | `#00e5cc` | Third variant accent              |
| `--t1`      | `#f0e6ff` | Primary text                      |
| `--t2`      | `rgba(240,230,255,0.68)` | Muted text         |
| `--t3`      | `rgba(240,230,255,0.38)` | Faint text, labels |

---

## Components

### Sticky Nav
```css
nav {
  background: rgba(26,5,51,0.92);
  backdrop-filter: blur(20px);
  border-bottom: 1px solid rgba(255,110,199,0.2);
}
```
- Title: Orbitron, gradient text
- Download button: `box-shadow: 0 0 0 1px var(--pink)`, pink text, hover adds `--glow-p`

### Buttons

**Primary — gradient pill:**
```css
.btn-primary {
  background: linear-gradient(135deg, #ff6ec7, #7b2fff);
  color: #fff;
  border: none;
  border-radius: 9999px;
  box-shadow: var(--glow-p);
  padding: 0.75rem 1.75rem;
  font-family: 'Exo 2', sans-serif;
  font-weight: 600;
  transition: box-shadow 0.2s, transform 0.12s;
}
.btn-primary:hover {
  box-shadow: 0 0 20px rgba(255,110,199,0.7), 0 0 40px rgba(255,110,199,0.4);
  transform: translateY(-2px);
}
.btn-primary:active { transform: translateY(1px); }
```

**Secondary — ghost with glow:**
```css
.btn-secondary {
  background: rgba(255,110,199,0.05);
  border: 1px solid rgba(255,110,199,0.35);
  color: #ff6ec7;
  border-radius: 8px;
  padding: 0.75rem 1.75rem;
}
.btn-secondary:hover { box-shadow: var(--glow-p); }
```

### Form Inputs
```css
input, textarea, select {
  background: rgba(123,47,255,0.12);
  border: 1px solid rgba(255,110,199,0.2);
  color: #f0e6ff;
  border-radius: 8px;
}
input::placeholder { font-family: 'Courier New', monospace; color: rgba(240,230,255,0.38); }
input:focus { border-color: #ff6ec7; box-shadow: var(--glow-p); }
```

### Cards
```css
.card {
  background: #2d1052;
  border: 1px solid rgba(123,47,255,0.3);
  border-radius: 16px;
  overflow: hidden;
}
.card-header { border-top: 3px solid var(--pink); /* or --cyan or --teal */ }
.card:hover { box-shadow: var(--glow-v); }
```

### Toggles
```css
.toggle-track {
  background: rgba(123,47,255,0.2);
  border: 1px solid rgba(255,110,199,0.2);
  border-radius: 9999px;
}
/* Active state */
input:checked ~ .toggle-track {
  background: linear-gradient(135deg, rgba(255,110,199,0.2), rgba(123,47,255,0.2));
  border-color: #ff6ec7;
  box-shadow: var(--glow-p);
}
input:checked ~ .toggle-track .toggle-thumb {
  background: #ff6ec7;
  box-shadow: var(--glow-p);
}
```

### Progress / Slider Bars
```css
/* Gradient fill overlay technique */
.progress-fill {
  background: linear-gradient(90deg, #ff6ec7, #7b2fff, #00d4ff);
  box-shadow: 0 0 8px rgba(255,110,199,0.5);
  border-radius: 9999px;
}

/* Thumb */
input[type=range]::-webkit-slider-thumb {
  background: #ff6ec7;
  box-shadow: var(--glow-p);
}
```

### Bottom Nav (Mobile)
```css
.navbar {
  background: rgba(15,0,30,0.95);
  border-top: 1px solid rgba(255,110,199,0.15);
}
/* Active tab */
.nav-item.active .icon-wrap {
  background: linear-gradient(135deg, rgba(255,110,199,0.2), rgba(123,47,255,0.2));
  box-shadow: var(--glow-p);
  border-radius: 9999px;
}
.nav-item.active .label { color: #ff6ec7; }
```

---

## Do / Don't

| Do | Don't |
|----|-------|
| Apply gradient text to all display/H1/H2 headings | Use solid colors for display headings |
| Use Orbitron for labels, section numbers, nav items | Use a serif or humanist typeface |
| Let the perspective grid be subtle but visible | Make the grid too dense or too bright |
| Use pink for primary interactive affordance | Use cyan as primary (it's always secondary) |
| Uppercase section labels with wide letter-spacing | Mix too many glow colors on one element |
| Deep dark purple backgrounds | Light or pastel backgrounds |
| Monospace fonts in form placeholders | Use the body font for placeholder text |

---

## AI Prompting Guidance

Use these prompts to generate on-aesthetic vaporwave UI with AI tools:

**For components:**
> "Design a [button/card/form] in vaporwave aesthetic: deep purple background (#1a0533), pink-to-purple gradient (#ff6ec7 → #7b2fff) for primary actions, cyan (#00d4ff) for secondary. Use Orbitron for headings, Exo 2 for body. Add subtle pink neon glow on interactive states. Perspective grid background visible but at 15% opacity."

**For screens:**
> "Vaporwave UI screen: dark purple void background, neon pink and cyan gradient accents, Orbitron typeface, perspective grid at the bottom. All headings use linear-gradient text from hot pink through electric violet to electric cyan. Cards are dark purple panels with glowing gradient top borders. CRT-retro meets synthwave aesthetic."

**For the color feel:**
> "aesthetic.tumblr.com meets a synthwave album cover. The palette is a sunset seen through a cathode-ray tube. Three colors: #ff6ec7 (hot pink), #7b2fff (electric purple), #00d4ff (electric cyan). Deep black-purple void background. All neon elements should glow softly."

**For typography:**
> "Orbitron font with 0.08em letter-spacing, uppercase section labels. Text fills use pink-to-cyan gradients. Monospace in code and placeholder elements. The type should feel like a retrofuturistic operating system."

---

## Scroll Reveal Animation

Sections enter with a fade-up:

```css
.section {
  opacity: 0;
  transform: translateY(24px);
  transition: opacity 0.55s cubic-bezier(0,0,0.2,1),
              transform 0.55s cubic-bezier(0,0,0.2,1);
}
.section.visible {
  opacity: 1;
  transform: translateY(0);
}
```

---

## Accessibility Notes

- Ensure neon text on dark backgrounds meets WCAG AA (4.5:1 for body text)
- `#ff6ec7` on `#1a0533` = ~6.2:1 contrast ✓
- `#00d4ff` on `#1a0533` = ~8.1:1 contrast ✓
- `--t2` (rgba(240,230,255,0.68)) on `#1a0533` ≈ 4.8:1 ✓
- Always use glow as enhancement, not sole focus indicator — pair with border color change
- Use `focus-visible` with `outline: 2px solid var(--pink)` for keyboard navigation
- `prefers-reduced-motion`: disable all animations and transitions at `0.01ms`
