# Material You (MD3) Style Guide

**Personality: Adaptive. Expressive. Tonal. System-thinking. Dynamic.**

Material You is the evolution of Material Design launched by Google in 2021 (shipping Android 12). It introduced dynamic color — the ability for the system palette to derive from a user's wallpaper — and a comprehensive tonal role system that replaces the flat color slots of MD2. Every design decision in MD3 is intentional, specified, and measurable.

---

## Philosophy

| Principle | What it means in practice |
|-----------|--------------------------|
| **Adaptive** | Color derives from the user's wallpaper via the HCT color space — the interface changes with the person |
| **Expressive** | Shape, motion, and color are used boldly — not timidly — to create personality |
| **Tonal** | Hierarchy is expressed through tonal relationships (lighter/darker of the same hue), not arbitrary contrasting colors |
| **System-thinking** | Every token is part of a system. Nothing is a one-off. If you're hardcoding a hex, you're fighting the system |
| **Dynamic** | The palette responds. Theming is not a skin — it's a behavior |

---

## Color System — 24 Roles

MD3's color system is built on **role pairs**: every foreground/background pairing is pre-defined in the spec. The seed color generates an entire palette via the **HCT (Hue, Chroma, Tone)** color space — a perceptually uniform model that guarantees contrast and visual harmony.

### Core palette roles

| Token | Value | Usage |
|-------|-------|-------|
| `--md-primary` | `#6750a4` | Primary actions, key UI elements, active states |
| `--md-on-primary` | `#ffffff` | Text/icons on primary-colored surfaces |
| `--md-primary-container` | `#eaddff` | Filled tonal buttons, selected chips, FABs |
| `--md-on-primary-container` | `#21005d` | Text/icons on primary-container surfaces |
| `--md-secondary` | `#625b71` | Supporting elements, less prominent components |
| `--md-on-secondary` | `#ffffff` | Text/icons on secondary-colored surfaces |
| `--md-secondary-container` | `#e8def8` | Nav indicator pills, selected filter chips |
| `--md-on-secondary-container` | `#1d192b` | Text/icons on secondary-container surfaces |
| `--md-tertiary` | `#7d5260` | Contrasting accents, complementary components |
| `--md-on-tertiary` | `#ffffff` | Text/icons on tertiary-colored surfaces |
| `--md-tertiary-container` | `#ffd8e4` | Highlights, complementary tonal containers |
| `--md-on-tertiary-container` | `#31111d` | Text/icons on tertiary-container surfaces |
| `--md-error` | `#b3261e` | Error states, destructive actions |
| `--md-error-container` | `#f9dedc` | Error message backgrounds |
| `--md-surface` | `#fffbfe` | Default background, card surfaces |
| `--md-surface-var` | `#e7e0ec` | Alternative containers, filled card BG, nav bar BG |
| `--md-outline` | `#79747e` | Input borders (rest state), dividers |
| `--md-outline-var` | `#cac4d0` | Subtle dividers, card outlines |

### Tonal surface shorthands

| Token | Value | Usage |
|-------|-------|-------|
| `--md-tonal-1` | `#f3eeff` | Surface + ~5% primary tint — elevated card BG, spec callouts |
| `--md-tonal-2` | `#ede8fd` | Surface + ~8% primary tint — deeper tonal containers |

### The pairing rule

> **Never pair a color with an arbitrary foreground.** Always use the pre-defined `on-*` pair.
> - `primary` → `on-primary`
> - `primary-container` → `on-primary-container`
> - `secondary-container` → `on-secondary-container`
> - etc.

---

## Shape Scale

MD3 uses six named shape tokens. Shape is as expressive as color — the full-rounded `r-full` is used for buttons and chips to signal interactivity; the `r-lg` (28px) signals prominent containers.

| Token | Value | Used on |
|-------|-------|---------|
| `--r-xs` | `4px` | Extra Small — text field borders, dense chips |
| `--r-sm` | `8px` | Small — cards (compact), snackbars, search bar fill |
| `--r` | `12px` | Medium — icon containers, player art |
| `--r-md` | `16px` | Large — cards, dialogs, bottom sheets, player panels |
| `--r-lg` | `28px` | Extra Large — prominent cards (previously used, now MD3 prefers r-md for cards) |
| `--r-full` | `9999px` | Full — all buttons, all chips, all pills, progress bars |

---

## Type Scale

MD3 specifies 15 type roles in 5 categories. Each has a fixed weight — **never substitute boldness for role**. Size, not weight, creates hierarchy.

| Role | Size | Weight | Tracking | Usage |
|------|------|--------|----------|-------|
| Display Large | 57px | 400 | 0 | Hero text, landing pages |
| Display Medium | 45px | 400 | 0 | Feature headings |
| Display Small | 36px | 400 | 0 | Section headers |
| Headline Large | 32px | 400 | 0 | Page titles |
| Headline Medium | 28px | 400 | 0 | Dialog titles, screen headings |
| Headline Small | 24px | 400 | 0 | Card titles |
| Title Large | 22px | 400 | 0 | Navigation titles, drawer headers |
| Title Medium | 16px | 500 | +0.009em | List headers, prominent subtitles |
| Title Small | 14px | 500 | +0.006em | Compact list headers |
| Body Large | 16px | 400 | +0.031em | Primary reading text |
| Body Medium | 14px | 400 | +0.016em | Secondary descriptions, metadata |
| Body Small | 12px | 400 | +0.033em | Captions, helper text |
| Label Large | 14px | 500 | +0.006em | Button text, tab labels |
| Label Medium | 12px | 500 | +0.031em | Nav bar labels, chip text |
| Label Small | 11px | 500 | +0.031em | Overlines, badge text, tooltips |

**Font stack:** `'Google Sans', system-ui, sans-serif`

---

## Elevation System

MD3 elevation is **tonal + shadow**, not shadow alone. At Elevation 1, a surface receives a 5% primary color tint *plus* a subtle drop shadow. This is why the tonal tokens (`--md-tonal-1`, `--md-tonal-2`) exist.

| Level | Shadow | Tonal surface | Used on |
|-------|--------|---------------|---------|
| 0 | none | `--md-surface` (#fffbfe) | Flat surfaces, filled cards |
| 1 | `--elev-1` | `--md-tonal-1` (#f3eeff) | Elevated cards, nav bar, filled buttons |
| 2 | `--elev-2` | `--md-tonal-2` (#ede8fd) | Hover state of Elevation 1 components |
| 3 | `--elev-3` | deeper tint | FABs, menus, tooltips |

```css
--elev-1: 0 1px 2px rgba(0,0,0,0.3), 0 1px 3px 1px rgba(0,0,0,0.15);
--elev-2: 0 1px 2px rgba(0,0,0,0.3), 0 2px 6px 2px rgba(0,0,0,0.15);
--elev-3: 0 4px 8px 3px rgba(0,0,0,0.15), 0 1px 3px rgba(0,0,0,0.3);
```

---

## Button Types — Usage Guide

MD3 has five button types. Use them in strict order of emphasis — **never use two of the same high-emphasis type on the same surface**.

| Type | Emphasis | Background | When to use |
|------|----------|-----------|-------------|
| **Filled** | Highest | `--md-primary` | The single most important action on a screen. One per screen if possible. Save, Submit, Create |
| **Filled Tonal** | High | `--md-primary-container` | Important secondary actions. Paired with Filled for dialog pairs (Save / Cancel) |
| **Outlined** | Medium | transparent | Alternative actions that need more visibility than Text. Filter, Customize |
| **Text** | Low | transparent | Least important actions. Third-option in a group. Learn more, Skip |
| **FAB** | Contextual | `--md-primary-container` | The primary task of a screen. Always visible. New message, Compose, Add |

### Button specifications

```css
/* All buttons share: */
border-radius: var(--r-full);
height: 40px;
padding: 0 24px;
font-size: 14px;
font-weight: 500;
letter-spacing: 0.006em;

/* FAB: */
height: 56px;
width: 56px;
border-radius: var(--r-md); /* 16px — NOT full-rounded */
box-shadow: var(--elev-3);
```

### State layers

All interactive components use **state layers** — a colored overlay applied on top of the component surface at a defined opacity.

| State | Primary button overlay | Secondary button overlay |
|-------|----------------------|------------------------|
| Hover | `rgba(255,255,255,0.08)` | `rgba(103,80,164,0.08)` |
| Pressed | `rgba(255,255,255,0.12)` | `rgba(103,80,164,0.12)` |
| Disabled | `opacity: 0.38` | `opacity: 0.38` |

---

## Forms — Outlined Text Field

The MD3 Outlined Text Field's signature behavior: **the label IS the placeholder**. It floats to sit on the border when the field is focused or filled.

```css
/* Rest state: label centered vertically */
.fl-label {
  position: absolute;
  left: 12px;
  top: 50%;
  transform: translateY(-50%);
  font-size: 1rem;       /* 16px */
  color: var(--md-outline);
  background: var(--md-surface); /* hides the border behind it */
  padding: 0;
  transition: all 0.2s cubic-bezier(0.2, 0, 0, 1);
}

/* Floated state: on focus or when filled */
.fl-input:focus + .fl-label,
.fl-input:not(:placeholder-shown) + .fl-label {
  top: 0;
  transform: translateY(-50%);
  font-size: 0.75rem;    /* 12px */
  color: var(--md-primary);
  padding: 0 4px;
}

/* Focus: thicker border */
.fl-input:focus {
  border: 2px solid var(--md-primary);
}
```

**Key implementation detail:** The input must have `placeholder=" "` (a space) so that `:not(:placeholder-shown)` works when the field has a value.

---

## Navigation Bar

MD3's Navigation Bar uses **indicator pills** — not underlines, not background fills on the entire item.

```
Active item anatomy:
┌────────────────────────────────────────┐
│  [  64×32px pill in secondary-cont ]  │
│           [icon — 24px]               │
│        label · 12px · 500w            │
└────────────────────────────────────────┘
```

```css
/* Pill */
.md-nav-indicator {
  width: 64px;
  height: 32px;
  border-radius: 9999px;
  background: transparent; /* → var(--md-secondary-container) when active */
  transition: background 0.25s cubic-bezier(0.05, 0.7, 0.1, 1);
}

/* Active state */
.md-nav-item.active .md-nav-indicator { background: var(--md-secondary-container); }
.md-nav-item.active .md-nav-lbl       { color: var(--md-on-secondary-container); font-weight: 700; }
```

**Nav bar specs:**
- Height: 80px
- Background: `--md-surface-var`
- 3–5 destinations (never more than 5)
- All icons 24px
- Labels always visible (never hide on desktop)

---

## Cards — Three Types

| Type | Background | Shadow | Border | Use case |
|------|-----------|--------|--------|----------|
| Elevated | `--md-tonal-1` | `--elev-1` (hover: `--elev-2`) | none | Interactive content; articles, product tiles |
| Filled | `--md-surface-var` | none | none | Static groupings, scan-first content |
| Outlined | `--md-surface` | none | `1px --md-outline-var` | Containers, forms, settings panels |

All cards: `border-radius: var(--r-md)` (16px).

---

## Motion

MD3 specifies four easing curves. Use them by intent — not interchangeably.

| Curve | CSS | Intent |
|-------|-----|--------|
| Standard | `cubic-bezier(0.2, 0, 0, 1)` | Elements moving across a surface at consistent speed |
| Emphasized Decelerate | `cubic-bezier(0.05, 0.7, 0.1, 1)` | Elements entering the screen — fast start, soft landing |
| Emphasized Accelerate | `cubic-bezier(0.3, 0, 1, 1)` | Elements leaving the screen — slow start, fast exit |
| Linear | `cubic-bezier(0, 0, 1, 1)` | Color changes, opacity — never for spatial movement |

**Duration guidelines:**
- Small components (buttons, chips): 100–200ms
- Medium components (cards, dialogs appearing): 250–350ms  
- Large transitions (full-screen): 400–500ms

---

## Ripple Effect

Every interactive surface in MD3 shows a ripple on touch/click. This is the Material signature.

```css
.ripple {
  position: absolute;
  border-radius: 50%;
  pointer-events: none;
  animation: ripple-expand 0.55s cubic-bezier(0.2, 0, 0, 1) forwards;
  transform: scale(0);
}
/* On primary (dark) bg: */
.md-btn-filled .ripple { background: rgba(255, 255, 255, 0.28); }
/* On light bg: */
.md-btn-tonal .ripple, .md-btn-outlined .ripple { background: rgba(103, 80, 164, 0.12); }

@keyframes ripple-expand {
  from { transform: scale(0); opacity: 0.9; }
  to   { transform: scale(2.6); opacity: 0; }
}
```

---

## MD3 Switch — Specifications

The Switch is one of MD3's most precisely specified components.

```
Off state:                    On state:
┌──────────────────────┐      ┌──────────────────────┐
│ ──────────────────── │      │ ──────────────────── │
│ ○  track: surface-var│      │         ● track: pri │
└──────────────────────┘      └──────────────────────┘
 52px wide × 32px tall         thumb slides right
 2px border: --md-outline      thumb: 16px → 24px
 thumb: 16px, --md-outline     thumb: white (on-primary)
```

```css
.tgl-track { width: 52px; height: 32px; border-radius: 9999px; border: 2px solid var(--md-outline); }
.tgl-thumb { width: 16px; height: 16px; border-radius: 50%; background: var(--md-outline); left: 6px; }

/* Checked: */
.tgl-in:checked ~ .tgl-track { background: var(--md-primary); border-color: var(--md-primary); }
.tgl-in:checked ~ .tgl-track .tgl-thumb { background: white; width: 24px; height: 24px; left: 22px; }
```

---

## Sliders — Two-Tone Track

MD3 sliders use a two-tone track: **active portion in primary, inactive in surface-variant**.

```css
.md-slider {
  background: linear-gradient(
    to right,
    var(--md-primary) var(--pct),
    var(--md-surface-var) var(--pct)
  );
}
/* Update --pct via JS on input events */
```

Thumb: 20px, `background: var(--md-primary)`, subtle `box-shadow`.  
Track height: **4px** (not 6px or 8px — precision matters in MD3).

---

## CSS Token Reference

```css
:root {
  /* Color roles */
  --md-bg:          #fffbfe;
  --md-surface:     #fffbfe;
  --md-surface-var: #e7e0ec;
  --md-tonal-1:     #f3eeff;
  --md-tonal-2:     #ede8fd;
  --md-primary:     #6750a4;
  --md-on-primary:  #ffffff;
  --md-primary-container: #eaddff;
  --md-on-primary-container: #21005d;
  --md-secondary:   #625b71;
  --md-on-secondary: #ffffff;
  --md-secondary-container: #e8def8;
  --md-on-secondary-container: #1d192b;
  --md-tertiary:    #7d5260;
  --md-on-tertiary: #ffffff;
  --md-tertiary-container: #ffd8e4;
  --md-on-tertiary-container: #31111d;
  --md-error:       #b3261e;
  --md-error-container: #f9dedc;
  --md-outline:     #79747e;
  --md-outline-var: #cac4d0;
  /* Elevation */
  --elev-1: 0 1px 2px rgba(0,0,0,0.3), 0 1px 3px 1px rgba(0,0,0,0.15);
  --elev-2: 0 1px 2px rgba(0,0,0,0.3), 0 2px 6px 2px rgba(0,0,0,0.15);
  --elev-3: 0 4px 8px 3px rgba(0,0,0,0.15), 0 1px 3px rgba(0,0,0,0.3);
  /* Shape */
  --r-xs: 4px; --r-sm: 8px; --r: 12px; --r-md: 16px; --r-lg: 28px; --r-full: 9999px;
  /* Motion */
  --ease:      cubic-bezier(0.2, 0, 0, 1);
  --ease-damp: cubic-bezier(0.05, 0.7, 0.1, 1);
  --ease-acc:  cubic-bezier(0.3, 0, 1, 1);
  /* Typography */
  --f: 'Google Sans', system-ui, sans-serif;
}
```

---

## AI Prompting Guide

Use these prompts to generate accurate MD3 designs with AI coding tools.

### Generating a new component

```
Build a Material You (MD3) [component name] using the MD3 color token system.
Use --md-primary for active/brand elements, --md-primary-container for
tonal containers, and --md-secondary-container for selected states (like nav pills).
All interactive elements need ripple effects. Shape: border-radius uses
--r-full for buttons/chips, --r-md (16px) for cards/panels.
Elevation uses tonal surface + shadow, not shadow alone.
Font: 'Google Sans', system-ui. Never hardcode hex values — use the tokens.
```

### Requesting button variants

```
Generate all 5 MD3 button types: Filled (--md-primary bg), Filled Tonal
(--md-primary-container bg), Outlined (transparent bg, --md-outline border,
--md-primary text), Text (transparent, --md-primary text), and FAB
(--md-primary-container bg, --elev-3 shadow, 56×56px, border-radius: 16px).
Include hover state layers: rgba(255,255,255,0.08) on primary, rgba(103,80,164,0.08) on light.
```

### Requesting a floating label input

```
Create an MD3 Outlined Text Field with floating label. The label starts
vertically centered (top: 50%, transform: translateY(-50%), font-size: 16px,
color: --md-outline). On :focus or :not(:placeholder-shown), it floats to
top: 0, transform: translateY(-50%), font-size: 12px, color: --md-primary,
padding: 0 4px, background: --md-surface (to cover the border).
Border: 1px --md-outline at rest, 2px --md-primary on focus.
Input must have placeholder=" " for the CSS selector to work.
```

### Requesting dark mode

```
Apply MD3 dark theme. Swap: primary → #d0bcff, on-primary → #381e72,
primary-container → #4f378b, on-primary-container → #eaddff,
surface → #1c1b1f, surface-var → #49454f, outline → #938f99.
All roles follow the same pair structure — just darker tone values.
```

### Requesting dynamic theming

```
This is a Material You dynamic theming demo. Show how changing the seed color
from purple (#6750a4) to teal changes all color roles proportionally via HCT.
The hue rotates while chroma and tone relationships stay constant.
The component should re-render with new tokens without structural changes.
```

---

## Anti-Patterns to Avoid

| ❌ Don't | ✅ Do instead |
|---------|-------------|
| Use arbitrary hex colors | Always map to a `--md-*` token |
| Put two Filled buttons in one action area | Use Filled + Tonal pair |
| Use font-weight 700+ for any MD3 type role | Max is 500 (Medium) |
| Use underlines for active nav items | Use indicator pills (64×32px, secondary-container) |
| Use drop-shadow alone for elevation | Combine tonal surface + shadow |
| Use border-radius 8px on buttons | Buttons are always `--r-full` (fully rounded) |
| Use `#000000` for body text | Use `rgba(0,0,0,0.87)` for primary text |
| Skip the ripple on interactive elements | Every tap/click in MD3 gets a ripple |
| Make FABs with `border-radius: 50%` | FABs use `--r-md` (16px), not circles |
| Use the same color for a card's hover state | Elevation change = tonal shift + shadow increase |

---

*Material Design 3 specification: [m3.material.io](https://m3.material.io)*  
*HCT color paper: [Dynamic Color — Material Design](https://material.io/blog/science-of-color-design)*
