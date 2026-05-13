# Glassmorphism Style Guide
**UI Styles Library — Version 2.0**  
Category: Layered · Year of origin: 2010s (popularized 2020–2021)

---

## Personality

**Five words:** Luminous. Translucent. Atmospheric. Ethereal. Futuristic.

**Voice of this style:** "Every surface is a pane of frosted glass suspended over a deep-space gradient. You don't look at the interface — you look through it. Depth is refracted light, not painted shadow. The world beneath the glass is always visible, always breathing."

**Use when:** Building immersive apps, dashboards, music players, OS-level interfaces, spatial/AR-adjacent UIs, landing pages, and any surface where the background gradient IS the product. Best when only a few high-priority elements exist per screen — glass shines when it has room to breathe.

**Do NOT use when:**
- Dense information layouts (data tables, email threads, documentation)
- Environments where `backdrop-filter` degrades GPU performance (low-end mobile, battery-sensitive PWAs)
- Light-background designs — the blur requires a vivid gradient or imagery behind it to read correctly
- Accessibility-critical contexts without carefully tested contrast ratios

---

## Quick Start — Copy & Paste

```css
:root {
  /* ── Background (must be fixed) ─────── */
  --bg-grad: linear-gradient(135deg, #1a1a2e 0%, #302b63 55%, #7c3aed 100%);

  /* ── Glass material ─────────────────── */
  --glass:      rgba(255,255,255,0.10);
  --glass-hi:   rgba(255,255,255,0.18);
  --glass-btn:  rgba(255,255,255,0.15);

  /* ── Blur recipe ────────────────────── */
  --blur:       blur(40px) saturate(180%);

  /* ── Borders ────────────────────────── */
  --border:     1px solid rgba(255,255,255,0.18);
  --border-2:   1px solid rgba(255,255,255,0.08);

  /* ── Text ──────────────────────────── */
  --t1:   #ffffff;
  --t2:   rgba(255,255,255,0.70);
  --t3:   rgba(255,255,255,0.40);

  /* ── Accent ─────────────────────────── */
  --ac:      #74b9ff;
  --ac-glow: rgba(116,185,255,0.45);
  --ac-hi:   #a8d8ff;

  /* ── Semantic ──────────────────────── */
  --ok:   #55efc4;
  --err:  #fd79a8;
  --warn: #fdcb6e;

  /* ── Shape ─────────────────────────── */
  --r-sm:   10px;
  --r:      16px;
  --r-md:   20px;
  --r-lg:   28px;
  --r-full: 9999px;

  /* ── Motion ────────────────────────── */
  --ease:     cubic-bezier(0.4, 0, 0.2, 1);
  --spring:   cubic-bezier(0.34, 1.56, 0.64, 1);
  --ease-out: cubic-bezier(0, 0, 0.2, 1);

  /* ── Typography ─────────────────────── */
  --f: 'Inter', system-ui, sans-serif;
}

body {
  font-family: var(--f);
  background: var(--bg-grad);
  background-attachment: fixed;   /* gradient stays as you scroll */
  min-height: 100vh;
  color: var(--t1);
  -webkit-font-smoothing: antialiased;
}

/* ── The glass material — apply to ALL surfaces ── */
.glass {
  background: var(--glass);
  backdrop-filter: var(--blur);
  -webkit-backdrop-filter: var(--blur);
  border: var(--border);
  border-radius: var(--r-md);
}
```

---

## Color Tokens

| Token | Value | Role |
|-------|-------|------|
| `--bg-grad` | `linear-gradient(135deg, #1a1a2e 0%, #302b63 55%, #7c3aed 100%)` | **The fixed background.** Never changes. The gradient lives here; glass panels reveal it. |
| `--glass` | `rgba(255,255,255,0.10)` | Standard glass fill — all panels, cards, nav, forms |
| `--glass-hi` | `rgba(255,255,255,0.18)` | Elevated/hovered glass |
| `--glass-btn` | `rgba(255,255,255,0.15)` | Secondary button fill |
| `--border` | `1px solid rgba(255,255,255,0.18)` | Standard luminous hairline |
| `--border-2` | `1px solid rgba(255,255,255,0.08)` | Subtle / inner borders |
| `--t1` | `#ffffff` | Primary text |
| `--t2` | `rgba(255,255,255,0.70)` | Secondary / body text |
| `--t3` | `rgba(255,255,255,0.40)` | Tertiary / placeholders / labels |
| `--ac` | `#74b9ff` | Accent — reserved for **interactive and active states** |
| `--ac-glow` | `rgba(116,185,255,0.45)` | Accent glow (box-shadow, text-shadow) |
| `--ac-hi` | `#a8d8ff` | Accent hover / lighter shade |
| `--ok` | `#55efc4` | Success state |
| `--err` | `#fd79a8` | Error / destructive state |
| `--warn` | `#fdcb6e` | Warning state |

**Critical rule:** The background gradient is the soul of glassmorphism. If you remove the fixed background, the blur becomes invisible and the entire aesthetic collapses. `background-attachment: fixed` on the body is required.

---

## Glass System

The depth language of glassmorphism. Instead of shadow offsets, depth is expressed through **blur radius, opacity level, and border luminosity**.

### Blur Levels

| Level | `backdrop-filter` | Use on |
|-------|-------------------|--------|
| Subtle | `blur(12px) saturate(120%)` | Tooltips, badges, inline chips |
| Medium | `blur(24px) saturate(150%)` | Small cards, dropdowns, popovers |
| Standard | `blur(40px) saturate(180%)` | All primary panels, nav, forms |
| Deep | `blur(60px) saturate(200%)` | Modals, hero cards, focus surfaces |

### Opacity Levels

| Name | Value | Use on |
|------|-------|--------|
| Ghost | `rgba(255,255,255,0.05)` | Very subtle backgrounds, input track |
| Glass | `rgba(255,255,255,0.10)` | **Standard** — all panels and cards |
| Glass Hi | `rgba(255,255,255,0.18)` | Hover state, elevated elements |
| Glass Btn | `rgba(255,255,255,0.15)` | Interactive buttons at rest |
| Input | `rgba(255,255,255,0.07)` | Form inputs (recessed pocket) |
| Overlay | `rgba(26,26,46,0.65)` | Dark nav bars, overlaid chrome |

### State → Glass Mapping

```
Card rest        → glass(0.10) + blur(40px) + border(0.18)
Card hover       → glass(0.10) + translateY(-4px) + shadow deepen
Panel            → glass(0.10) + blur(40px) + border(0.18) + shadow(0 8px 32px rgba(0,0,0,0.3))
Input rest       → rgba(0.07) + border(0.08) + inset-shadow
Input focus      → border: 1px solid var(--ac) + box-shadow: 0 0 0 3px var(--ac-glow)
Btn secondary    → glass(0.15) + border(0.18) + backdrop-filter
Btn primary      → background: var(--ac) + box-shadow: 0 4px 20px var(--ac-glow)
Btn press        → opacity: 0.8 + scale(0.96)
Toggle off       → rgba(0.10) + border(0.15)
Toggle on        → rgba(116,185,255,0.25) + border(ac) + glow
Active nav tab   → rgba(116,185,255,0.18) + 0 0 16px var(--ac-glow)
```

---

## Typography

**Typeface:** Inter (Google Fonts)  
**Import:** `https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap`

**Why Inter:** Inter's neutral, geometric letterforms disappear behind the glass — the type is a window, not a wall. Rounded or serif faces compete with the material texture. Inter's optical sizing and tabular numerics are also practical for data-dense glass UIs.

| Level | Size | Weight | Letter-spacing | Line-height | Use |
|-------|------|--------|----------------|-------------|-----|
| Display | 48px | 800 | −0.03em | 1.1 | Hero headlines |
| H1 | 36px | 700 | −0.025em | 1.15 | Page titles |
| H2 | 28px | 700 | −0.02em | 1.2 | Section headers |
| H3 | 22px | 600 | −0.01em | 1.25 | Card titles |
| H4 | 18px | 600 | 0 | 1.3 | Sub-sections |
| Body LG | 17px | 400 | 0 | 1.6 | Lead paragraphs |
| Body | 16px | 400 | 0 | 1.55 | Standard copy |
| Body SM | 14px | 400 | 0 | 1.5 | Secondary copy |
| Caption | 12px | 500 | +0.06em | — | Labels, metadata (uppercase) |

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
| `--r-sm` | 10px | Small controls (checkboxes) |
| `--r` | 16px | Buttons, inputs, tags |
| `--r-md` | 20px | Medium cards |
| `--r-lg` | 28px | Large cards, panels, modals |
| `--r-full` | 9999px | Pills, toggles, circular buttons |

**Rule:** Larger radius softens the glass — smaller radius sharpens it. Primary panels use `--r-lg` (28px). Interactive controls use `--r` (16px). The radius consistency signals craftsmanship; mixed values shatter the atmospheric coherence.

---

## Motion & Easing

| Token | Value | Use |
|-------|-------|-----|
| `--ease` | `cubic-bezier(0.4, 0, 0.2, 1)` | All standard transitions |
| `--spring` | `cubic-bezier(0.34, 1.56, 0.64, 1)` | Toggle thumb, bouncing elements |
| `--ease-out` | `cubic-bezier(0, 0, 0.2, 1)` | Scroll reveals, panel entrances |
| Card hover lift | 300ms ease | `transform: translateY(-4px)` |
| Button press | 120ms ease | `opacity: 0.8; scale(0.96)` |
| Glow transitions | 200ms ease | `box-shadow` changes |
| Toggle thumb | 280ms spring | Satisfying snap to active |
| Scroll reveal | 550ms ease-out | Opacity 0→1 + translateY(24px→0) |

**Motion philosophy:** Glass panels feel weightless — they don't have mass. Transitions should be swift and smooth, not heavy. The exception is the toggle spring (280ms with overshoot) which provides tactile satisfaction in an otherwise intangible material.

---

## Component Snippets

### Glass Button (Secondary)

```css
.btn {
  background: rgba(255,255,255,0.15);
  backdrop-filter: blur(20px) saturate(150%);
  -webkit-backdrop-filter: blur(20px) saturate(150%);
  border: 1px solid rgba(255,255,255,0.18);
  border-radius: var(--r);
  padding: 0.75rem 1.75rem;
  font-family: var(--f);
  font-size: 0.9375rem;
  font-weight: 600;
  color: #ffffff;
  cursor: pointer;
  transition: background 200ms var(--ease), box-shadow 200ms var(--ease);
}
.btn:hover:not(:disabled) {
  background: rgba(255,255,255,0.22);
  box-shadow: 0 4px 20px rgba(0,0,0,0.25);
}
.btn:active:not(:disabled) {
  opacity: 0.8;
  transform: scale(0.96);
}
.btn:disabled { opacity: 0.28; cursor: not-allowed; }
```

### Primary Button (Accent Glow)

```css
.btn-primary {
  background: var(--ac);       /* #74b9ff */
  color: #fff;
  border: none;
  border-radius: var(--r-full);
  padding: 0.75rem 1.75rem;
  font-weight: 600;
  box-shadow: 0 4px 20px var(--ac-glow);
  transition: box-shadow 200ms var(--ease), background 200ms var(--ease);
}
.btn-primary:hover:not(:disabled) {
  background: var(--ac-hi);
  box-shadow: 0 8px 32px var(--ac-glow), 0 0 0 1px var(--ac);
}
.btn-primary:active:not(:disabled) {
  opacity: 0.8;
  transform: scale(0.96);
  box-shadow: 0 2px 10px var(--ac-glow);
}
```

### Glass Input

```css
.input {
  background: rgba(255,255,255,0.07);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border: 1px solid rgba(255,255,255,0.08);
  border-radius: var(--r);
  padding: 0.75rem 1rem;
  font-family: var(--f);
  font-size: 0.9375rem;
  font-weight: 400;
  color: #ffffff;
  outline: none;
  width: 100%;
  box-shadow: inset 0 2px 6px rgba(0,0,0,0.18);
  transition: border-color 200ms var(--ease), box-shadow 200ms var(--ease);
}
.input::placeholder { color: rgba(255,255,255,0.35); }
.input:focus {
  border: 1px solid var(--ac);
  box-shadow: 0 0 0 3px var(--ac-glow), inset 0 2px 6px rgba(0,0,0,0.18);
}
```

### Glass Card

```css
.card {
  background: rgba(255,255,255,0.10);
  backdrop-filter: blur(40px) saturate(180%);
  -webkit-backdrop-filter: blur(40px) saturate(180%);
  border: 1px solid rgba(255,255,255,0.18);
  border-radius: var(--r-lg);
  overflow: hidden;
  box-shadow: 0 8px 32px rgba(0,0,0,0.30), 0 0 0 1px rgba(255,255,255,0.08);
  transition: transform 300ms var(--ease), box-shadow 300ms var(--ease);
}
.card:hover {
  transform: translateY(-4px);
  box-shadow: 0 16px 48px rgba(0,0,0,0.40), 0 0 0 1px rgba(255,255,255,0.14);
}
```

### Glass Toggle

```css
.toggle-track {
  display: block;
  width: 52px; height: 28px;
  background: rgba(255,255,255,0.10);
  border: 1px solid rgba(255,255,255,0.15);
  border-radius: 9999px;
  position: relative;
  cursor: pointer;
  transition: background 280ms var(--ease), border-color 280ms var(--ease),
              box-shadow 280ms var(--ease);
}
.toggle-thumb {
  position: absolute;
  top: 3px; left: 3px;
  width: 22px; height: 22px;
  border-radius: 50%;
  background: rgba(255,255,255,0.85);
  box-shadow: 0 2px 8px rgba(0,0,0,0.30);
  transition: transform 280ms var(--spring),
              background 280ms var(--ease),
              box-shadow 280ms var(--ease);
}
/* Checked state */
input:checked + .toggle-track {
  background: rgba(116,185,255,0.25);
  border-color: rgba(116,185,255,0.55);
  box-shadow: 0 0 12px var(--ac-glow);
}
input:checked + .toggle-track .toggle-thumb {
  transform: translateX(24px);
  background: var(--ac);
  box-shadow: 0 0 12px var(--ac-glow), 0 2px 8px rgba(0,0,0,0.2);
}
```

### Range Slider

```css
.slider {
  -webkit-appearance: none;
  width: 100%; height: 8px;
  border-radius: 9999px;
  background: rgba(255,255,255,0.10);
  border: 1px solid rgba(255,255,255,0.10);
  box-shadow: inset 0 1px 4px rgba(0,0,0,0.25);
  outline: none;
  cursor: pointer;
}
.slider::-webkit-slider-thumb {
  -webkit-appearance: none;
  width: 22px; height: 22px;
  border-radius: 50%;
  background: var(--ac);
  box-shadow: 0 0 14px var(--ac-glow), 0 2px 6px rgba(0,0,0,0.3);
  cursor: pointer;
  transition: transform 120ms, box-shadow 120ms;
}
.slider::-webkit-slider-thumb:hover {
  transform: scale(1.12);
  box-shadow: 0 0 22px var(--ac-glow);
}
```

---

## Guiding Principles

**1. The gradient is the material, not the surface.**  
The frosted glass only exists because the gradient exists beneath it. `background-attachment: fixed` is non-negotiable. Without a vivid background showing through, blur renders invisible — you just get a faint white box with no atmosphere.

**2. Translucency is depth, not decoration.**  
Every `rgba` opacity value is a depth decision. More opaque = closer to the viewer. Less opaque = receding into the gradient. Think of it as a z-axis expressed in alpha.

**3. The luminous hairline border is structural.**  
`border: 1px solid rgba(255,255,255,0.18)` is not subtle decoration — it is what makes a glass panel readable as a distinct pane. Remove it and panels dissolve into each other. Never increase it above 0.22 or it becomes a thick white border that destroys the material illusion.

**4. Accent is the one solid point in a translucent world.**  
`#74b9ff` and its glow are the only fully opaque, fully saturated elements in the interface. They draw the eye to interactive states. If you put accent color anywhere other than active/interactive states, you've lost your only contrast anchor.

**5. Performance is a design constraint.**  
`backdrop-filter: blur(40px)` is GPU-expensive. If you stack more than 6–8 blurred layers on screen simultaneously, you will drop frames on mid-range hardware. Use it intentionally — not on every div.

---

## Do's

- **DO** always set `background-attachment: fixed` on the body. The gradient must be static while content scrolls past it.
- **DO** test glass panels against both the lightest and darkest region of your gradient — text contrast varies significantly across the background.
- **DO** add `0 0 0 3px var(--ac-glow)` as the focus ring replacement. A standard 2px outline reads poorly against translucent panels.

---

## Don'ts

- **DON'T** use a solid background color. Glass without a gradient behind it is just a semi-transparent rectangle — you lose the entire aesthetic.
- **DON'T** use `backdrop-filter` on more than ~8 elements simultaneously. GPU cost stacks; profile on a real mid-range device before shipping.
- **DON'T** remove the border entirely. `border: none` makes glass panels invisible at low opacity. The hairline border is structural to legibility.
- **DON'T** use text below `rgba(255,255,255,0.55)` for any body copy. At lower opacities, WCAG contrast requirements cannot be met against variable gradient backgrounds.
- **DON'T** use drop shadows with heavy `rgba(0,0,0,X)` values. Glass shadows should be subtle — `0 8px 32px rgba(0,0,0,0.30)` is already at the maximum. Harsh shadows break the weightlessness of the material.
- **DON'T** mix glassmorphism with neumorphism or flat design within the same screen. Glass requires a dark, vivid backdrop; the other styles conflict fundamentally.

---

## Anti-Patterns to Reject Immediately

If any AI-generated output includes these, reject it and re-prompt:

- `background: white` or `background: #f0f0f0` — solid light surfaces kill the glass effect
- `backdrop-filter: blur(2px)` — too subtle to register as glass; minimum practical blur is 16px
- `border: 2px solid rgba(255,255,255,0.5)` or brighter — this is a visible thick border, not a hairline; never exceed 1px / 0.22 opacity
- `box-shadow: 0 4px 8px rgba(0,0,0,0.8)` — harsh dark shadows destroy the floating glass illusion
- `color: rgba(255,255,255,0.30)` for body text — fails WCAG AA on most gradient regions
- Glass panels with `border-radius: 0` or `border-radius: 4px` — too sharp; minimum 10px for any glass surface
- `transition: all 0.3s ease` — always name the property explicitly and use `var(--ease)`
- Accent color (`#74b9ff`) used as a background fill on non-interactive, non-active elements

---

## AI Prompting Guidance

Use this block to instruct any AI coding agent to reproduce this style:

```
Build in Glassmorphism style:
- Fixed gradient background: linear-gradient(135deg, #1a1a2e 0%, #302b63 55%, #7c3aed 100%)
  with background-attachment: fixed on body — REQUIRED
- All surfaces: background rgba(255,255,255,0.10), backdrop-filter blur(40px) saturate(180%),
  -webkit-backdrop-filter same, border 1px solid rgba(255,255,255,0.18)
- Text: primary #ffffff, secondary rgba(255,255,255,0.70), tertiary rgba(255,255,255,0.40)
- Accent #74b9ff — only for active/interactive states and focus rings
  Accent glow: box-shadow 0 0 Xpx rgba(116,185,255,0.45)
- Primary buttons: background var(--ac), border-radius 9999px, box-shadow 0 4px 20px var(--ac-glow)
  hover: expand glow, active: opacity 0.8 + scale(0.96)
- Secondary buttons: glass material (rgba 0.15, blur, border 0.18)
- Inputs: rgba(255,255,255,0.07), border rgba(0.08), inset shadow; focus: border var(--ac) + glow ring
- Cards: rgba(0.10) glass + box-shadow 0 8px 32px rgba(0,0,0,0.3)
  hover: translateY(-4px), deeper shadow
- Toggles: glass track, white thumb at rest; on active: track rgba(116,185,255,0.25) + thumb var(--ac) + glow
- Slider track: glass groove (rgba 0.10 + inset shadow); thumb: var(--ac) + glow
- Radius: 10px sm, 16px default, 20px md, 28px lg, 9999px pills
- Font: Inter (neutral, disappears into glass)
- NEVER: solid backgrounds, no backdrop-filter, border > 1px, harsh dark shadows
```
