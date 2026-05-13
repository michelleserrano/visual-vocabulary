# Neubrutalism Style Guide
**Vivid. Chunky. Flat-shadowed. Self-aware. Gen Z.**

> Origin: 2022–present · Digital native aesthetic reacting to polished flat/glassmorphism
> Inspired by old brutalism's structural honesty — but refusing to be ugly about it.

---

## Personality

Neubrutalism takes brutalism's structural rules (thick borders, visible structure, no decoration) and injects Gen Z color energy. It's not trying to look accidental — it's *intentionally awkward* with vivid accents and physical, pressable affordances. The offset black shadow is the signature: sharp as a knife, no blur.

**Three-word pitch:** Structural. Vivid. Physical.

---

## Design Tokens

```css
:root {
  --bg:        #ffffff;   /* clean white — neubrutalism starts from white */
  --s1:        #f8f8f8;
  --t1:        #1a1a1a;   /* near-black text */
  --t2:        #3a3a3a;
  --t3:        #6a6a6a;

  /* Gen Z accent palette — all vivid, all saturated */
  --coral:     #ff6b35;   /* primary · warm coral-orange */
  --teal:      #4ecdc4;   /* secondary · turquoise */
  --lavender:  #a29bfe;   /* tertiary · soft purple */
  --yellow:    #ffe66d;   /* highlight · warm yellow */
  --lime:      #55efc4;   /* alt · mint */
  --black:     #1a1a1a;
  --ac:        var(--coral);

  --r:         4px;       /* very slight radius — not zero, not pill */
  --f:         'Space Grotesk', 'Inter', system-ui, sans-serif;
  --f-disp:    'Space Grotesk', 'Inter', sans-serif;
  --f-mono:    'JetBrains Mono', 'Courier New', monospace;
  --ease:      cubic-bezier(0.4,0,0.2,1);
  --spring:    cubic-bezier(0.34,1.56,0.64,1);

  /* THE neubrutalism shadow — THE signature */
  /* Offset in one direction, NO blur, sharp as a knife */
  --shadow-sm: 3px 3px 0 var(--black);
  --shadow-md: 4px 4px 0 var(--black);
  --shadow-lg: 6px 6px 0 var(--black);
  --shadow-xl: 8px 8px 0 var(--black);
}

body {
  background: var(--bg);
  color: var(--t1);
  font-family: var(--f);
}
```

---

## The `.nb` Pattern (apply to everything)

The only rule that matters: **flat offset shadow + thick black border**. Apply this to every interactive element.

```css
.nb {
  border: 2px solid var(--black);
  box-shadow: var(--shadow-md);          /* 4px 4px 0 #1a1a1a */
  border-radius: var(--r);               /* 4px */
  transition: transform 0.1s, box-shadow 0.1s;
}
.nb:hover {
  transform: translate(-2px, -2px);      /* lifts up-left */
  box-shadow: var(--shadow-lg);          /* 6px 6px 0 #1a1a1a */
}
.nb:active {
  transform: translate(3px, 3px);        /* presses down-right */
  box-shadow: 1px 1px 0 var(--black);    /* shadow disappears = pressed in */
}
```

---

## The Press Effect Recipe

The physical illusion: the element appears to sit above the surface by the shadow offset. When pressed, it translates INTO the surface and the shadow vanishes.

```
Rest:    translate(0,0)       + shadow: 4px 4px 0 black
Hover:   translate(-2px,-2px) + shadow: 6px 6px 0 black   ← shadow grows = rises
Active:  translate(3px, 3px)  + shadow: 1px 1px 0 black   ← shadow shrinks = presses in
```

The translate offset matches the shadow offset direction (bottom-right). Shadow offset + translation = illusion of physical depth.

---

## Color System (5 Accents)

| Token      | Hex       | Use                        |
|------------|-----------|----------------------------|
| `--coral`  | `#ff6b35` | Primary — CTAs, active states, progress |
| `--teal`   | `#4ecdc4` | Secondary — secondary actions, cards   |
| `--lavender`| `#a29bfe`| Tertiary — tertiary actions             |
| `--yellow` | `#ffe66d` | Highlight — callouts, badges, spec tags |
| `--lime`   | `#55efc4` | Alt — success, positive states          |
| `--black`  | `#1a1a1a` | ALL borders and shadows                 |

**Rule:** Cycle through accents per section / per component type. Never use the same accent twice in adjacent contexts. Never soften the black border — it must always be `#1a1a1a`.

---

## Typography Rules

| Scale    | Size   | Weight | Family        | Use                    |
|----------|--------|--------|---------------|------------------------|
| Display  | 48px   | 700    | Space Grotesk | Hero headings          |
| H1       | 36px   | 700    | Space Grotesk | Page titles            |
| H2       | 28px   | 700    | Space Grotesk | Section titles         |
| H3       | 22px   | 600    | Space Grotesk | Card/widget headings   |
| Body     | 16px   | 400    | Space Grotesk | Body copy              |
| Mono     | 15px   | 400    | JetBrains Mono| Code, values, tokens, data labels |

**Rules:**
- Space Grotesk at large sizes must be LARGE — don't go smaller than 20px for display
- Letter-spacing: `-0.04em` on display, `-0.02em` on headings
- JetBrains Mono for anything that looks like a number, code, or data label
- Never use a rounded typeface (not compatible — opposite aesthetic)

---

## Component Recipes

### Button
```css
.btn {
  border: 2px solid var(--black);
  box-shadow: var(--shadow-md);
  border-radius: var(--r);
  background: var(--coral);      /* or any accent */
  color: var(--black);
  font-family: var(--f);
  font-weight: 600;
  padding: 0.75rem 1.75rem;
  transition: transform 0.1s, box-shadow 0.1s;
}
/* + .nb hover/active states */
```

Five flavors: coral (primary), teal (secondary), lavender (tertiary), yellow (highlight), white (ghost).

### Input
```css
.inp {
  background: white;
  border: 2px solid var(--black);
  box-shadow: var(--shadow-sm);
  border-radius: var(--r);
  padding: 0.75rem 1rem;
}
.inp:focus {
  border-color: var(--coral);
  box-shadow: var(--shadow-sm), 0 0 0 3px rgba(255,107,53,0.2);
}
```

### Card
```css
.card {
  background: white;
  border: 2px solid var(--black);
  box-shadow: var(--shadow-lg);
  border-radius: var(--r);
  overflow: hidden;
}
.card-header {
  /* Full-width accent strip */
  background: var(--coral);  /* or teal or lavender — rotate per card */
  border-bottom: 2px solid var(--black);
  height: 108px;
}
/* + .nb hover/active states */
```

### Toggle
```css
.tgl-track {
  width: 56px; height: 30px;
  background: white;
  border: 2px solid var(--black);
  box-shadow: var(--shadow-sm);
  border-radius: 6px;          /* rectangular, not pill */
}
.tgl-thumb {
  width: 20px; height: 20px;
  background: white;
  border: 2px solid var(--black);
  border-radius: 3px;          /* square thumb */
  box-shadow: var(--shadow-sm);
  transition: transform 0.3s cubic-bezier(0.34,1.56,0.64,1);
}
input:checked ~ .tgl-track { background: var(--coral); }
input:checked ~ .tgl-track .tgl-thumb { transform: translateX(24px); }
```

### Checkbox
```css
.chk-box {
  width: 22px; height: 22px;
  background: white;
  border: 2px solid var(--black);
  box-shadow: var(--shadow-sm);
  border-radius: 4px;           /* square */
}
input:checked + .chk-box { background: var(--coral); }
/* checkmark: white SVG stroke */
```

### Slider
```css
/* Track */
input[type=range] {
  -webkit-appearance: none;
  height: 12px;
  background: white;   /* update via JS gradient for fill */
  border: 2px solid var(--black);
  box-shadow: var(--shadow-sm);
  border-radius: 4px;
}
/* Thumb — square */
input[type=range]::-webkit-slider-thumb {
  -webkit-appearance: none;
  width: 24px; height: 24px;
  background: white;
  border: 2px solid var(--black);
  border-radius: 4px;
  box-shadow: var(--shadow-sm);
}
```

For coral fill from left, update via JS:
```js
const pct = ((val - min) / (max - min)) * 100;
el.style.backgroundImage =
  `linear-gradient(to right, #ff6b35 ${pct}%, white ${pct}%)`;
```

### Progress Dots (Square)
```css
.dot {
  width: 8px; height: 8px;
  border-radius: 1px;           /* square */
  border: 2px solid var(--black);
  background: transparent;
}
.dot.active {
  background: var(--coral);     /* cycle through accents per section */
  box-shadow: 2px 2px 0 var(--black);
}
```

### Nav Bar
```css
.navbar { border-top: 2px solid var(--black); box-shadow: 0 -2px 0 var(--black); }
.tab    { border-right: 2px solid var(--black); }
.tab:last-child { border-right: none; }
.tab.active { background: var(--coral); }
```

---

## Spec Callout
```css
.spec-callout {
  background: var(--yellow);   /* always yellow */
  border: 2px solid var(--black);
  box-shadow: var(--shadow-md);
  border-radius: var(--r);
  padding: 1.25rem;
}
```

---

## What to Never Do

| ❌ Don't                          | ✅ Do instead                          |
|----------------------------------|----------------------------------------|
| Box-shadow with blur             | Sharp offset: `4px 4px 0 #1a1a1a`    |
| Pill/rounded border-radius       | 4px radius — slightly rounded only     |
| Soft pastel accents              | Full-saturation: `#ff6b35`, `#4ecdc4` |
| Drop shadows on text             | Strong font weight instead              |
| Gradient fills on buttons        | Flat solid accent color                |
| Subtle 1px borders               | Bold 2px black borders                 |
| Inset / neumorphic shadows       | Outset offset shadow only              |
| Removing borders on hover        | Shadow grows, border stays             |

---

## Google Fonts Import

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300;400;500;600;700&family=JetBrains+Mono:ital,wght@0,400;0,500;1,400&display=swap" rel="stylesheet">
```

---

## AI Prompting Guidance

When asking an AI to generate Neubrutalism UI:

**Include in your prompt:**
```
Use neubrutalism design style (2022 Gen Z aesthetic):
- White background (#ffffff)
- 2px solid #1a1a1a border on every element
- Sharp offset shadow: box-shadow: 4px 4px 0 #1a1a1a (NO blur)
- Hover: transform translate(-2px,-2px) + shadow grows to 6px 6px
- Active: transform translate(3px,3px) + shadow shrinks to 1px 1px
- Font: Space Grotesk 700 for headings, JetBrains Mono for data labels
- Accent colors: #ff6b35 (coral), #4ecdc4 (teal), #a29bfe (lavender), #ffe66d (yellow), #55efc4 (lime)
- border-radius: 4px (not zero, not rounded)
- Spec callouts: yellow background with black border
```

**Key distinction from old Brutalism:**
```
NOT old brutalism (black/white, stark, aggressive)
Neubrutalism = same structural rules BUT with vivid Gen Z colors
Same chunky borders and offset shadows, but FUN and colorful
```

**Negative prompts to include:**
```
No blur in shadows. No gradients. No pill/rounded corners. No soft pastel colors.
No neumorphism inset shadows. No glassmorphism.
```

---

## Accessibility Notes

- Text on coral: `#1a1a1a` text only — never white on coral (fails WCAG AA)
- Text on teal: `#1a1a1a` text only
- Text on lavender: `#1a1a1a` text only  
- Text on yellow: `#1a1a1a` text only
- Focus ring: `outline: 2px solid var(--coral); outline-offset: 3px;`
- Never rely on color alone for state — the border + shadow provide shape affordance
- Disabled state: `opacity: 0.35` — preserves the nb pattern at reduced visibility

---

## Reference

Figma community: search "neubrutalism UI kit"  
Dribble tags: `#neubrutalism`, `#brutalistUI`, `#genzdesign`  
Year: 2022–present  
Key practitioners: Gumroad, Linear (early), many indie SaaS products
