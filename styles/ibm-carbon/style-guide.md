# IBM Carbon Design System
**Personality: Systematic. Dense. IBM. Precise. Enterprise.**

> "Carbon is not a style — it is a specification. Every pixel is intentional. Every decision is documented."

---

## Identity

| Property | Value |
|----------|-------|
| Origin | IBM Design Language, 2016 → Carbon v11 (2022) |
| Theme shown | Gray 100 (darkest) |
| Base surface | `#161616` |
| Grid unit | 8px |
| Typefaces | IBM Plex Mono · IBM Plex Sans · IBM Plex Sans Condensed |
| Accent | `#0f62fe` — IBM Blue 60, exact, no approximations |
| Border-radius | `0px` (zero everywhere, always) |
| Motion curve | `cubic-bezier(0.2, 0, 0.38, 0.9)` (Productive) |

---

## Design Tokens · Gray 100 Theme

```css
:root {
  /* Backgrounds / Layers */
  --bg-ui:    #161616;   /* Gray 100 — base surface */
  --layer-01: #262626;   /* Gray 90 — elevated cards, panels */
  --layer-02: #393939;   /* Gray 80 — inputs, table headers */
  --layer-03: #525252;   /* Gray 70 — hover on layer-02 */
  --bg-hover: #262626;   /* Hover on base surface */

  /* Text */
  --t1: #f4f4f4;          /* Gray 10 — primary text */
  --t2: #c6c6c6;          /* Gray 30 — secondary text */
  --t3: #8d8d8d;          /* Gray 50 — placeholder, helper */
  --t4: #6f6f6f;          /* Gray 60 — disabled, subtle */

  /* The ONE accent */
  --blue:    #0f62fe;     /* IBM Blue 60 — interactive, links, focus */
  --blue-hi: #0050e6;     /* IBM Blue 70 — hover on blue */
  --blue-lo: rgba(15,98,254,0.2); /* Blue with opacity */

  /* Status (use ONLY for status communication) */
  --red:    #fa4d56;      /* Danger / Error */
  --green:  #42be65;      /* Success */
  --yellow: #f1c21b;      /* Warning */

  /* Borders */
  --border:    1px solid #393939;   /* Layer 02 — default border */
  --border-hi: 1px solid #525252;   /* Layer 03 — input border */

  /* Geometry */
  --r: 0px;               /* NO border-radius. Full stop. */
  --r-full: 9999px;       /* Exception: tags/pills only */

  /* Typography */
  --f-mono: 'IBM Plex Mono', 'Courier New', monospace;
  --f-sans: 'IBM Plex Sans', 'Helvetica Neue', sans-serif;
  --f-cond: 'IBM Plex Sans Condensed', sans-serif;

  /* Motion */
  --ease:            cubic-bezier(0.2, 0, 0.38, 0.9);   /* Productive */
  --ease-expressive: cubic-bezier(0.4, 0.14, 0.3, 1);   /* Expressive */
}

/* MANDATORY global reset */
*, *::before, *::after { border-radius: 0 !important; }
body {
  background: var(--bg-ui);
  color: var(--t1);
  font-family: var(--f-sans);
  font-size: 14px;
  line-height: 1.5;
}
```

---

## The 8px Grid — The Law

Carbon's grid is non-negotiable. Every dimension, every spacing value must be a multiple of 4px (minimum) or 8px (preferred).

| Token | Value | Use |
|-------|-------|-----|
| `$spacing-01` | 2px | Never. Micro only. |
| `$spacing-02` | 4px | Tight internal gaps |
| `$spacing-03` | 8px | Base unit |
| `$spacing-04` | 12px | Small gaps |
| `$spacing-05` | 16px | Default padding |
| `$spacing-06` | 24px | Medium gap |
| `$spacing-07` | 32px | Section spacing |
| `$spacing-08` | 40px | Large gap |
| `$spacing-09` | 48px | Section break |
| `$spacing-10` | 64px | Page-level spacing |
| `$spacing-12` | 96px | Hero padding |

**Rule:** If your spacing value is not on this list, it is wrong.

---

## Typography

### IBM Plex — Three Roles, Strict Assignment

```html
<link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:ital,wght@0,300;0,400;0,500;0,600;0,700;1,400&family=IBM+Plex+Sans:ital,wght@0,300;0,400;0,500;0,600;0,700;1,400&family=IBM+Plex+Sans+Condensed:wght@0,300;0,400;0,500;0,600;0,700&display=swap" rel="stylesheet">
```

| Font | Use case | Never use for |
|------|----------|--------------|
| IBM Plex Mono | UI labels, system data, code, field labels, tags, all-caps identifiers | Long prose, headings |
| IBM Plex Sans | Body text, headings, descriptions, buttons, nav | Code, data labels |
| IBM Plex Sans Condensed | Dense tables, sidebar data, compact layouts | Headings, body text |

### Carbon Type Scale

| Role | Size | Weight | Font |
|------|------|--------|------|
| Display | 54px | 300 | Sans |
| Heading 1 | 42px | 300 | Sans |
| Heading 2 | 28px | 400 | Sans |
| Heading 3 | 20px | 600 | Sans |
| Body | 16px | 400 | Sans |
| Body Small | 14px | 400 | Sans |
| Code / Mono | 14px | 400 | Mono |
| Label (uppercase) | 11px | 500 | Mono · 0.08em spacing |

### Label Pattern (everywhere in UI)

```css
.cds-label {
  font-family: 'IBM Plex Mono', monospace;
  font-size: 11px;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  color: var(--t2);
  display: block;
  margin-bottom: 8px; /* 8px grid */
}
```

---

## Button System — Five Types

### Heights (all multiples of 8)

| Size | Height | Padding |
|------|--------|---------|
| Small | 32px | 0 16px |
| Default | 40px | 0 16px |
| Large | 48px | 0 24px |
| Expressive | 64px | 0 32px |

### Button CSS

```css
/* Base — shared by all */
.cds-btn {
  display: inline-flex;
  align-items: center;
  justify-content: space-between;
  gap: 16px;
  height: 40px;
  padding: 0 16px;
  font-family: 'IBM Plex Sans', sans-serif;
  font-size: 14px;
  font-weight: 400;
  border: none;
  cursor: pointer;
  letter-spacing: 0;
  transition: background 0.1s cubic-bezier(0.2, 0, 0.38, 0.9);
}
.cds-btn:focus { outline: 2px solid #0f62fe; outline-offset: -2px; }
.cds-btn:disabled { opacity: 0.25; cursor: not-allowed; }

/* Primary */
.btn-primary { background: #0f62fe; color: #fff; }
.btn-primary:hover { background: #0050e6; }
.btn-primary:active { background: #002d9c; }

/* Secondary */
.btn-secondary { background: #393939; color: #f4f4f4; }
.btn-secondary:hover { background: #474747; }
.btn-secondary:active { background: #525252; }

/* Tertiary (outlined) */
.btn-tertiary { background: transparent; color: #0f62fe; border: 1px solid #0f62fe; }
.btn-tertiary:hover { background: #0f62fe; color: #fff; }

/* Ghost */
.btn-ghost { background: transparent; color: #0f62fe; }
.btn-ghost:hover { background: rgba(15,98,254,0.12); }

/* Danger */
.btn-danger { background: #ba1b23; color: #fff; }
.btn-danger:hover { background: #a2191f; }
.btn-danger:active { background: #750e13; }
```

### Button Decision Guide

| Type | Use when | Do NOT use for |
|------|----------|----------------|
| Primary | One per page/screen — the main action | Multiple actions on same screen |
| Secondary | Supporting action alongside primary | The most important action |
| Tertiary | Low-emphasis alternative | Anything requiring visual weight |
| Ghost | Navigation, inline, toolbar actions | Primary CTAs |
| Danger | Delete, destroy, irreversible | Anything non-destructive |

---

## Carbon State Documentation — All 6 States

Every interactive element must have all states defined:

| State | Visual treatment |
|-------|-----------------|
| Default | Base background, base border |
| Hover | One layer lighter (e.g., Layer 01 → `#2e2e2e`) |
| Focus | `outline: 2px solid #0f62fe; outline-offset: -2px` — ALWAYS inset |
| Active | One layer above hover |
| Disabled | `opacity: 0.25`, `cursor: not-allowed` |
| Selected | Blue left border OR blue fill depending on component |

```css
/* Focus — the exact Carbon focus ring */
:focus-visible {
  outline: 2px solid #0f62fe;
  outline-offset: -2px;
}
/* NEVER use outline-offset: 2px (that's not Carbon) */
/* NEVER use a colored background for focus (that's not Carbon) */
```

---

## Form Inputs

```css
/* Carbon Text Input */
.cds-input {
  height: 40px;
  background: #393939;        /* Layer 02 */
  border: none;
  border-bottom: 1px solid #525252;  /* only bottom border at rest */
  padding: 0 16px;
  font-family: 'IBM Plex Sans', sans-serif;
  font-size: 14px;
  color: #f4f4f4;
  outline: none;
  width: 100%;
  transition: border-color 0.1s;
}
.cds-input:hover { background: #444444; border-bottom-color: #c6c6c6; }
.cds-input:focus { outline: 2px solid #0f62fe; outline-offset: -2px; border-bottom-color: transparent; }
.cds-input.error { outline: 2px solid #fa4d56; outline-offset: -2px; }
.cds-input::placeholder { color: #6f6f6f; }
```

### Label Pattern for Inputs

Labels are always above the field, IBM Plex Mono, uppercase. Never inside the field as a floating label.

---

## Carbon Data Table

The data table is Carbon's signature component. Dense, precise, information-rich.

```css
.cds-data-table { width: 100%; border-collapse: collapse; }

.cds-data-table th {
  background: #393939;           /* Layer 02 */
  color: #c6c6c6;
  font-family: 'IBM Plex Mono', monospace;
  font-size: 11px;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  padding: 8px 16px;             /* 8px grid */
  text-align: left;
  border-bottom: 1px solid #525252;
}

.cds-data-table td {
  padding: 8px 16px;
  border-bottom: 1px solid #393939;
  font-family: 'IBM Plex Mono', monospace;
  font-size: 12px;
  color: #c6c6c6;
}
.cds-data-table tr:hover td { background: rgba(255,255,255,0.04); }
.cds-data-table tr:last-child td { border-bottom: none; }
```

---

## Carbon Motion

IBM Carbon uses two motion categories:

### Productive Motion (default for UI)
```css
/* Fast, precise, no-decoration */
transition: background 100ms cubic-bezier(0.2, 0, 0.38, 0.9);
/* 100ms for micro-interactions */
/* 150ms for simple state changes */
/* 240ms for panels/modals appearing */
```

### Expressive Motion (for high-impact moments)
```css
/* Slower, more character */
transition: transform 400ms cubic-bezier(0.4, 0.14, 0.3, 1);
```

**Rule:** Never use `ease`, `ease-in-out`, or spring physics in Carbon. Those are not the system.

---

## Carbon Inline Notification

```html
<!-- Info notification -->
<div class="cds-notification">
  <span class="notification-icon">ℹ</span>
  <p class="notification-body">
    <strong>Title.</strong> Supporting message text here.
  </p>
</div>
```

```css
.cds-notification {
  display: flex;
  align-items: flex-start;
  gap: 12px;
  background: #262626;         /* Layer 01 */
  border-left: 3px solid #0f62fe;
  padding: 12px 16px;          /* 8px grid */
}
/* Variants: swap border color */
/* Info:    border-color: #0f62fe */
/* Error:   border-color: #fa4d56 */
/* Success: border-color: #42be65 */
/* Warning: border-color: #f1c21b */
```

---

## Carbon Slider

```css
/* 2px track — Carbon precision */
.cds-slider-track {
  height: 2px;
  background: #393939;
  position: relative;
}
.cds-slider-fill { height: 2px; background: #0f62fe; }
input[type="range"]::-webkit-slider-thumb {
  width: 14px; height: 14px;
  border-radius: 50% !important; /* pill exception */
  background: #0f62fe;
  border: none;
}
```

Label beside every slider in IBM Plex Mono. Value displayed right-aligned in IBM Blue.

---

## Color Rules

1. **Background-only palette.** Gray is for backgrounds and borders. Never use gray as an accent or highlight.
2. **One blue.** `#0f62fe`. Never use `#0066cc`, `#1473e6`, or any other blue. Copy-paste the hex.
3. **Status colors are ONLY for status.** Red = error/danger. Yellow = warning. Green = success. Never use them decoratively.
4. **No gradients.** Carbon uses flat color. No gradients, no color blends.
5. **No shadows.** Carbon uses layering (bg → layer-01 → layer-02 → layer-03) for depth. Zero `box-shadow`.

---

## Anti-Patterns

| ❌ Wrong | ✓ Correct |
|---------|----------|
| `border-radius: 4px` | `border-radius: 0` |
| `font-family: 'Roboto'` | `font-family: 'IBM Plex Sans'` |
| `color: #0066cc` | `color: #0f62fe` |
| `box-shadow: 0 2px 8px ...` | Use layer background instead |
| `transition: all 0.3s ease` | `transition: background 100ms cubic-bezier(0.2,0,0.38,0.9)` |
| `outline-offset: 4px` | `outline-offset: -2px` (inset focus) |
| `font-size: 13px` | `font-size: 12px` or `14px` (grid-aligned) |
| Padding `10px 14px` | Padding `8px 16px` (grid units only) |
| `background: #333` | `background: #393939` (layer-02 exact) |
| IBM Blue on any color | IBM Blue on `#161616` or `#262626` only |

---

## AI Prompting Guide

Use these prompts to generate Carbon-accurate UI:

**For components:**
> "Build a Carbon Design System [component] using IBM Plex Mono for labels, IBM Plex Sans for body, background #161616, layer-01 #262626, layer-02 #393939, accent #0f62fe, zero border-radius, 8px grid spacing, 40px default height for interactive elements."

**For full screens:**
> "Design an IBM Carbon Gray 100 theme dashboard. Dense data tables with IBM Plex Mono headers. Blue focus rings inset 2px. No shadows — use background layers for depth. One primary action per screen in #0f62fe."

**For motion:**
> "All transitions use cubic-bezier(0.2, 0, 0.38, 0.9) at 100ms. No spring physics, no ease-in-out."

**Negative prompt (always include):**
> "No border-radius on non-pill elements. No box-shadow. No gradients. No Roboto, Inter, or system-ui. No blue other than #0f62fe. No spacing values outside the 8px grid."

---

## Navigation Pattern

Carbon UI Shell: 48px header. IBM blue logo block left. IBM Plex Mono for title. Navigation items at 40px. Active state: 2px IBM blue bottom border.

```css
.carbon-nav-item { height: 40px; padding: 0 16px; font-family: 'IBM Plex Sans', sans-serif; font-size: 14px; color: #c6c6c6; position: relative; }
.carbon-nav-item::after { content: ''; position: absolute; bottom: 0; left: 0; right: 0; height: 2px; background: #0f62fe; transform: scaleX(0); transition: transform 100ms; }
.carbon-nav-item.active { color: #f4f4f4; }
.carbon-nav-item.active::after { transform: scaleX(1); }
```

---

## Quick Reference Card

```
Colors:   #161616 · #262626 · #393939 · #525252 · #0f62fe
Text:     #f4f4f4 · #c6c6c6 · #8d8d8d · #6f6f6f
Status:   #fa4d56 (err) · #42be65 (ok) · #f1c21b (warn)
Fonts:    IBM Plex Mono (labels) · IBM Plex Sans (body)
Grid:     8 · 16 · 24 · 32 · 40 · 48 · 64 · 96
Heights:  32 · 40 · 48 · 64 (buttons) · 48 (header)
Radius:   0px (always) · 9999px (pills/tags only)
Focus:    outline: 2px solid #0f62fe; outline-offset: -2px
Motion:   cubic-bezier(0.2,0,0.38,0.9) · 100–240ms
Borders:  1px solid #393939 (default) · 1px solid #525252 (elevated)
```
