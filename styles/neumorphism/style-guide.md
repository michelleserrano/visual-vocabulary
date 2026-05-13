# Neumorphism Style Guide
**UI Styles Library — Version 2.0**  
Category: Tactile · Year of origin: 2019

---

## Personality

**Five words:** Soft. Physical. Monochromatic. Tactile. Meditative.

**Voice of this style:** "Every surface is the same material. Depth is a conversation between two shadows — light and dark — not a change in color. The interface feels pressed from clay, not painted."

**Use when:** Building music players, smart home controls, dashboard widgets, and any focused single-task app where *feeling the UI* matters more than dense information. Avoid for content-rich, data-heavy, or multi-task interfaces — neumorphism does not scale to complexity.

**Do NOT use when:** 
- Low-vision or accessibility-critical contexts (inherently low contrast)
- Interfaces with more than ~8 interactive elements per screen
- Dark-background designs (the shadow formula only works on light, near-gray surfaces)

---

## Quick Start — Copy & Paste

```css
:root {
  /* ── The ONE surface color ─────────── */
  --bg:  #e0e5ec;       /* ALL elements use this background */

  /* ── Shadow sources ────────────────── */
  --sl:  #ffffff;       /* light shadow (top-left) */
  --sd:  #a3b1c6;       /* dark shadow (bottom-right) */

  /* ── Shadow system ─────────────────── */
  --sh-xs:    3px  3px  6px  var(--sd), -3px  -3px  6px  var(--sl);
  --sh-sm:    4px  4px  9px  var(--sd), -4px  -4px  9px  var(--sl);
  --sh-md:    6px  6px  14px var(--sd), -6px  -6px  14px var(--sl);
  --sh-lg:    10px 10px 22px var(--sd), -10px -10px 22px var(--sl);
  --sh-in:    inset 5px  5px  11px var(--sd), inset -5px  -5px  11px var(--sl);
  --sh-in-sm: inset 3px  3px  7px  var(--sd), inset -3px  -3px  7px  var(--sl);

  /* ── Accent (use sparingly — for active/interactive only) ── */
  --ac:    #6c5ce7;
  --ac-lo: rgba(108,92,231,0.28);
  --ac-hi: #5a4bd1;

  /* ── Text ──────────────────────────── */
  --t1: #2d3748;   /* primary text */
  --t2: #718096;   /* secondary */
  --t3: #a0aec0;   /* tertiary / placeholders */

  /* ── Semantic ──────────────────────── */
  --ok:   #00b894;
  --err:  #e17055;
  --warn: #fdcb6e;

  /* ── Shape ─────────────────────────── */
  --r-sm:   8px;
  --r:      12px;
  --r-md:   16px;
  --r-lg:   24px;
  --r-full: 9999px;

  /* ── Motion ────────────────────────── */
  --ease:   cubic-bezier(0.4, 0, 0.2, 1);
  --spring: cubic-bezier(0.34, 1.56, 0.64, 1);
  --dur:    200ms;

  /* ── Typography ────────────────────── */
  --f: 'Nunito', sans-serif;   /* import from Google Fonts */
}

body {
  font-family: var(--f);
  background: var(--bg);    /* page background = element background */
  color: var(--t1);
  -webkit-font-smoothing: antialiased;
}
```

---

## Color Tokens

| Token | Value | Role |
|-------|-------|------|
| `--bg` | `#e0e5ec` | **The one surface.** Background AND all element fills. |
| `--sl` | `#ffffff` | Light shadow source (top-left origin) |
| `--sd` | `#a3b1c6` | Dark shadow source (bottom-right origin) |
| `--ac` | `#6c5ce7` | Accent — reserved for **active/interactive states only** |
| `--ac-lo` | `rgba(108,92,231,0.28)` | Accent shadow for primary buttons |
| `--ac-hi` | `#5a4bd1` | Pressed accent state |
| `--t1` | `#2d3748` | Primary text |
| `--t2` | `#718096` | Secondary / muted text |
| `--t3` | `#a0aec0` | Tertiary / placeholders / labels |
| `--ok` | `#00b894` | Success state |
| `--err` | `#e17055` | Error / destructive state |
| `--warn` | `#fdcb6e` | Warning state |

**Critical rule:** `--bg`, `--sl`, and `--sd` are never changed. If you change the surface color, recalculate all three as a matched trio (lighter for `--sl`, darker+saturated for `--sd`).

---

## Shadow System

The complete depth language. Each name maps to a specific use case:

| Token | Value | Use on |
|-------|-------|--------|
| `--sh-xs` | `3px 3px 6px sd, -3px -3px 6px sl` | Small badges, chips, tiny icons |
| `--sh-sm` | `4px 4px 9px sd, -4px -4px 9px sl` | Medium interactive elements |
| `--sh-md` | `6px 6px 14px sd, -6px -6px 14px sl` | Buttons (default state) |
| `--sh-lg` | `10px 10px 22px sd, -10px -10px 22px sl` | Cards, panels, containers |
| `--sh-in` | `inset 5px 5px 11px sd, inset -5px -5px 11px sl` | Pressed buttons, active inputs |
| `--sh-in-sm` | `inset 3px 3px 7px sd, inset -3px -3px 7px sl` | Input fields at rest, recessed elements |

### State → Shadow Mapping

```
Button default  → --sh-md
Button hover    → --sh-lg
Button pressed  → --sh-in
Input rest      → --sh-in-sm
Input focused   → --sh-in + 0 0 0 2px var(--ac)
Card rest       → --sh-lg
Card hover      → 14px 14px 28px var(--sd), -14px -14px 28px var(--sl)
Toggle thumb    → --sh-sm → (when active) accent shadow
```

---

## Typography

**Typeface:** Nunito (Google Fonts)  
**Import:** `https://fonts.googleapis.com/css2?family=Nunito:wght@300;400;500;600;700;800;900&display=swap`

**Why Nunito:** Rounded terminal strokes mirror the soft, physical material of neumorphism. Geometric or condensed faces feel wrong — they have hard corners the style doesn't.

| Level | Size | Weight | Letter-spacing | Line-height | Use |
|-------|------|--------|----------------|-------------|-----|
| Display | 48px | 900 | −0.03em | 1.1 | Hero headlines |
| H1 | 36px | 800 | −0.025em | 1.15 | Page titles |
| H2 | 28px | 700 | −0.02em | 1.2 | Section headers |
| H3 | 22px | 700 | −0.01em | 1.25 | Card titles |
| H4 | 18px | 600 | 0 | 1.3 | Sub-sections |
| Body LG | 17px | 400 | 0 | 1.6 | Lead paragraphs |
| Body | 16px | 400 | 0 | 1.55 | Standard copy |
| Body SM | 14px | 400 | 0 | 1.5 | Secondary copy |
| Caption | 12px | 600 | +0.06em | — | Labels, metadata (uppercase) |

---

## Spacing Scale

| Step | px | rem | Use |
|------|----|-----|-----|
| 1 | 4px | 0.25rem | Fine-grained adjustments |
| 2 | 8px | 0.5rem | Icon–label gap |
| 3 | 12px | 0.75rem | Tight padding |
| 4 | 16px | 1rem | Standard padding |
| 5 | 20px | 1.25rem | Card inner padding |
| 6 | 24px | 1.5rem | Section padding |
| 8 | 32px | 2rem | Panel padding |
| 10 | 40px | 2.5rem | Large vertical rhythm |
| 12 | 48px | 3rem | Section gaps |

---

## Border Radius

| Token | Value | Use |
|-------|-------|-----|
| `--r-sm` | 8px | Small controls (checkboxes) |
| `--r` | 12px | Buttons, inputs, tags |
| `--r-md` | 16px | Medium cards |
| `--r-lg` | 24px | Large cards, panels, modals |
| `--r-full` | 9999px | Pills, toggles, circular buttons |

**Rule:** Radius scales with the element's surface area. Small element = small radius. Inconsistent radius values immediately break the style's material cohesion.

---

## Motion & Easing

| Token | Value | Use |
|-------|-------|-----|
| `--ease` | `cubic-bezier(0.4, 0, 0.2, 1)` | All shadow transitions (standard) |
| `--spring` | `cubic-bezier(0.34, 1.56, 0.64, 1)` | Toggle thumb, bouncing elements |
| Shadow transitions | 200–250ms | Button states |
| Toggle thumb | 280ms with spring | Satisfying snap |
| Hover shadow | 250ms | Feels physical |

**Motion philosophy:** Transitions simulate mass. When a button is pressed, it *sinks* — the shadow inverts over 200ms. When the toggle activates, the thumb springs with slight overshoot. Nothing is instant; nothing is sluggish.

---

## Component Snippets

### Raised Button (Default)

```css
.btn {
  background: var(--bg);
  box-shadow: var(--sh-md);
  border: none;
  border-radius: var(--r);
  padding: 0.75rem 1.75rem;
  font-family: var(--f);
  font-size: 0.9375rem;
  font-weight: 700;
  color: var(--t1);
  cursor: pointer;
  transition: box-shadow 200ms var(--ease), transform 120ms var(--ease);
}
.btn:hover:not(:disabled)  { box-shadow: var(--sh-lg); }
.btn:active:not(:disabled) { box-shadow: var(--sh-in); transform: scale(0.975); }
.btn:disabled              { opacity: 0.35; box-shadow: none; cursor: not-allowed; }
```

### Primary Button

```css
.btn-primary {
  background: var(--ac);
  color: #fff;
  box-shadow: 6px 6px 14px var(--ac-lo), -6px -6px 14px var(--sl);
}
.btn-primary:hover:not(:disabled) {
  box-shadow: 10px 10px 22px var(--ac-lo), -10px -10px 22px var(--sl);
}
.btn-primary:active:not(:disabled) {
  box-shadow: inset 4px 4px 10px rgba(0,0,0,0.28),
              inset -4px -4px 10px rgba(255,255,255,0.12);
}
```

### Input Field

```css
.input {
  background: var(--bg);
  box-shadow: var(--sh-in-sm);   /* recessed — a hole in the surface */
  border: none;
  border-radius: var(--r);
  padding: 0.75rem 1rem;
  font-family: var(--f);
  font-size: 0.9375rem;
  font-weight: 500;
  color: var(--t1);
  outline: none;
  transition: box-shadow 200ms var(--ease);
}
.input::placeholder { color: var(--t3); }
.input:focus {
  box-shadow: var(--sh-in), 0 0 0 2px var(--ac);
}
```

### Toggle Switch

```css
.toggle-track {
  display: block;
  width: 52px; height: 28px;
  background: var(--bg);
  box-shadow: var(--sh-in-sm);
  border-radius: 9999px;
  position: relative;
  cursor: pointer;
}
.toggle-thumb {
  position: absolute;
  top: 3px; left: 3px;
  width: 22px; height: 22px;
  border-radius: 50%;
  background: var(--bg);
  box-shadow: var(--sh-sm);
  transition: transform 280ms var(--spring),
              background 280ms var(--ease),
              box-shadow 280ms var(--ease);
}
/* Checked state */
input:checked + .toggle-track .toggle-thumb {
  transform: translateX(24px);
  background: var(--ac);
  box-shadow: 3px 3px 7px var(--ac-lo), -2px -2px 5px rgba(255,255,255,0.65);
}
```

### Card

```css
.card {
  background: var(--bg);
  box-shadow: var(--sh-lg);
  border-radius: var(--r-lg);
  overflow: hidden;
  transition: box-shadow 300ms var(--ease);
}
.card:hover {
  box-shadow: 14px 14px 28px var(--sd), -14px -14px 28px var(--sl);
}
```

### Range Slider

```css
.slider {
  -webkit-appearance: none;
  width: 100%; height: 10px;
  border-radius: 9999px;
  background: var(--bg);
  box-shadow: var(--sh-in-sm);
  outline: none;
  cursor: pointer;
}
.slider::-webkit-slider-thumb {
  -webkit-appearance: none;
  width: 26px; height: 26px;
  border-radius: 50%;
  background: var(--ac);
  box-shadow: 4px 4px 8px var(--ac-lo), -3px -3px 7px rgba(255,255,255,0.7);
  cursor: pointer;
  transition: transform 120ms;
}
.slider::-webkit-slider-thumb:hover { transform: scale(1.12); }
```

---

## Guiding Principles

**1. One surface, one color.**  
Every element — button, card, input, background — uses `#e0e5ec`. If you add a gradient, a border, or a different fill, you've left neumorphism. The monochromatic constraint IS the style.

**2. Depth is a shadow equation.**  
Light comes from the top-left. Dark shadow falls bottom-right. The ratio and size of these two values creates all states — raised, pressed, flat, recessed. Master this equation before touching anything else.

**3. Accent color is a signal, not decoration.**  
`--ac` (`#6c5ce7`) appears only on active and interactive states. Nowhere else. It is the only affordance cue; overusing it destroys the contrast signal that makes it work.

**4. The touch response is the experience.**  
Buttons sinking, toggles snapping, sliders gliding — this is what neumorphism is FOR. If the interactions feel laggy, underanimated, or linear, the style fails entirely. Spring easing on toggles is mandatory, not optional.

**5. Know the limits.**  
Low-contrast components are inherently risky for accessibility. The accent must appear on every interactive element's active state, and focus states must use a 2px solid accent ring. If your audience has vision-related needs, supplement neumorphism with additional affordance signals (labels, patterns, high-contrast mode override).

---

## Do's

- **DO** use the shadow system exclusively for all depth communication — never borders, never fills.
- **DO** ensure every interactive element shows the pressed state (`--sh-in`) within 200ms of user input.
- **DO** add the `--ac` 2px focus ring on all focusable elements for keyboard accessibility.

---

## Don'ts

- **DON'T** change the surface color. Not to white, not to a darker gray. `#e0e5ec` or recalculate the full shadow system.
- **DON'T** use more than two accent colors. The entire style's legibility rests on `--ac` being the sole hue signal.
- **DON'T** use sharp corners, hard borders, or gradient fills. If you find yourself adding any of these, you are no longer building neumorphism.
- **DON'T** skip the pressed state animation on buttons. A neumorphic button that doesn't physically depress is a broken neumorphic button.
- **DON'T** use neumorphism for dense UI. It requires generous padding (minimum 12px, ideally 16–24px) and breathing room. Dense information layouts destroy the tactile illusion.

---

## Anti-Patterns to Reject Immediately

If any AI-generated output includes these, reject it and re-prompt:

- `border: 1px solid` — never borders
- `background: linear-gradient` or `background: white` — never non-surface fills
- `box-shadow: rgba(0,0,0,0.X)` (single shadow) — always dual shadow
- `transition: all 0.3s ease` — always specify the property and use `var(--ease)`
- Accent color (`#6c5ce7`) used as a background fill on non-button, non-active elements
- Any corner with `border-radius: 0` or `border-radius: 4px` or less

---

## AI Prompting Guidance

Use this block to instruct any AI coding agent to reproduce this style:

```
Build in Neumorphism style:
- Background AND all element fills: #e0e5ec (one surface only, never changes)
- No borders, no gradients, no fills other than #e0e5ec
- All depth via dual box-shadow: light (#ffffff) top-left, dark (#a3b1c6) bottom-right
- Shadow tokens: xs(3/3/6), sm(4/4/9), md(6/6/14), lg(10/10/22), in(inset 5/5/11), in-sm(inset 3/3/7)
- Buttons: box-shadow md at rest → lg on hover → inset on press, 200ms cubic-bezier(0.4,0,0.2,1)
- Inputs: inset shadow (recessed) at rest, + 2px solid accent on focus
- Toggles: spring animation cubic-bezier(0.34,1.56,0.64,1) 280ms
- Accent color #6c5ce7 only for active/interactive states and focus rings — nowhere else
- Font: Nunito (rounded terminals match the soft material aesthetic)
- Border radius: 8px small, 12px default, 16px medium, 24px large, 9999px pills
```
