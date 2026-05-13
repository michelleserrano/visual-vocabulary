# Liquid Glass Style Guide
**UI Styles Library — Version 2.0**
Category: Spatial · Year of origin: WWDC 2025 (Apple iOS 26 / macOS Tahoe / visionOS 3)

---

## Personality

**Five words:** Refractive. Apple. Light-bending. Translucent-with-thickness. WWDC25.

**Voice of this style:** "The interface is a sheet of optical-grade glass laid over the world. It bends the light beneath it. It catches a sheen across its top edge. It pools highlight at its bottom rim. The glass has a thickness — measurable in the inset shadow you can feel even if you can't quite see it. This is not Glassmorphism. This is the material Apple shipped to a billion devices in fall 2025."

**Use when:** Building consumer-facing iOS / macOS / visionOS-adjacent surfaces, marketing pages for premium hardware, AR / spatial UIs, music and media apps, system-level chrome that needs to sit over rich content. Best when there is *something interesting beneath the glass*: imagery, gradient, video, scrolling content, an environment.

**Do NOT use when:**
- Dense data tools (spreadsheets, dashboards, IDEs) — Liquid Glass eats contrast and the focal energy belongs to the data.
- Backgrounds that are flat color or near-white — there is nothing for the glass to refract; the material collapses to "white box with shadow."
- Performance-constrained surfaces (low-end Android, embedded WebViews, battery-critical PWAs). The 4-layer shadow + saturate + brightness is GPU-expensive. Profile early.
- Brand contexts that want to feel anti-establishment, raw, or non-Apple. Liquid Glass *is* the Apple voice; using it elsewhere reads as derivative.

---

## Quick Start — Copy & Paste

```css
:root {
  /* ── Background — must be content-rich ───────── */
  --bg-grad: linear-gradient(135deg, #ffd6c2 0%, #d4a7f7 30%, #6ab5ff 65%, #5cd5d5 100%);
  --bg:      #f0f4fa;

  /* ── Text — deep readable on glass ───────────── */
  --t1:      #1e3a5f;
  --t2:      rgba(30,58,95,0.7);
  --t3:      rgba(30,58,95,0.45);
  --t4:      rgba(30,58,95,0.22);
  --t-inv:   #ffffff;

  /* ── Accent — Apple system palette ───────────── */
  --ac:        #0071e3;     /* iOS blue */
  --ac-hi:     #2196ff;
  --ac-glow:   rgba(0,113,227,0.4);
  --ac-purple: #a020f0;
  --ac-pink:   #ff6b9d;
  --ac-green:  #34c759;
  --ac-red:    #ff453a;
  --ac-orange: #ff9f0a;

  /* ── The Liquid Glass material — signature ───── */
  --glass-fill:    rgba(255,255,255,0.18);
  --glass-fill-2:  rgba(255,255,255,0.28);
  --glass-fill-3:  rgba(255,255,255,0.42);
  --glass-edge:    1px solid rgba(255,255,255,0.4);
  --glass-edge-hi: 1px solid rgba(255,255,255,0.65);

  /* ── Shape ───────────────────────────────────── */
  --r-sm:   12px;
  --r:      18px;
  --r-md:   24px;
  --r-lg:   32px;
  --r-full: 9999px;

  /* ── Type ────────────────────────────────────── */
  --f-display: -apple-system, BlinkMacSystemFont, 'SF Pro Display', 'Inter', system-ui, sans-serif;
  --f:         -apple-system, BlinkMacSystemFont, 'SF Pro Text', 'Inter', system-ui, sans-serif;
  --f-mono:    ui-monospace, 'SF Mono', 'JetBrains Mono', Menlo, monospace;

  /* ── Motion ──────────────────────────────────── */
  --ease:     cubic-bezier(0.4, 0, 0.2, 1);
  --spring:   cubic-bezier(0.32, 0.72, 0, 1);   /* Apple's signature spring */
  --ease-out: cubic-bezier(0, 0, 0.2, 1);
}

body {
  font-family: var(--f);
  background: var(--bg-grad);
  background-attachment: fixed;
  min-height: 100vh;
  color: var(--t1);
  letter-spacing: -0.011em;
  -webkit-font-smoothing: antialiased;
}
```

---

## THE LIQUID GLASS RECIPE — Apply to every glass surface

This is the defining material. Every panel, card, button, input, and tile carries this same recipe at its core. Discipline here is the difference between Liquid Glass and something that merely resembles it.

```css
.lq-glass {
  position: relative;
  background: var(--glass-fill);
  backdrop-filter: blur(20px) saturate(180%) brightness(1.05);
  -webkit-backdrop-filter: blur(20px) saturate(180%) brightness(1.05);
  border: var(--glass-edge);
  border-radius: var(--r-md);
  /* The 4-layer shadow that creates liquid glass thickness */
  box-shadow:
    0 1px 0 rgba(255,255,255,0.5) inset,         /* (1) top edge highlight   */
    0 -1px 0 rgba(30,58,95,0.06) inset,          /* (2) bottom edge depth    */
    0 0 0 0.5px rgba(255,255,255,0.25) inset,    /* (3) inner ring           */
    0 8px 32px rgba(30,58,95,0.12),              /* (4) drop shadow          */
    0 2px 8px rgba(30,58,95,0.08);               /* (4b) close drop shadow   */
  overflow: hidden;
  isolation: isolate;
}

/* The specular highlight overlay — gives glass its WET look */
.lq-glass::before {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(135deg,
    rgba(255,255,255,0.45) 0%,
    rgba(255,255,255,0.10) 30%,
    transparent           50%,
    transparent           70%,
    rgba(255,255,255,0.08) 100%);
  pointer-events: none;
  border-radius: inherit;
  transition: transform 0.6s var(--ease), opacity 0.4s var(--ease);
}

/* The refractive bottom edge — "liquid pooling" highlight */
.lq-glass::after {
  content: '';
  position: absolute;
  inset: 0;
  border-radius: inherit;
  background: linear-gradient(180deg,
    transparent           0%,
    transparent           70%,
    rgba(255,255,255,0.10) 90%,
    rgba(255,255,255,0.20) 100%);
  pointer-events: none;
}
```

**KEY DIFFERENTIATOR FROM GLASSMORPHISM** — read this twice:

| What | Glassmorphism | Liquid Glass |
|------|---------------|--------------|
| Backdrop filter | `blur(40px)` only | `blur(20px) saturate(180%) brightness(1.05)` — three filters, not one |
| Border | One hairline (`1px solid rgba(255,255,255,0.18)`) | Hairline + inner 0.5px ring + top edge highlight + bottom edge depth |
| Shadow | One soft drop shadow | **4 layers**: top inset, bottom inset, inner ring, drop |
| Top sheen | None | `::before` gradient — the diagonal specular highlight |
| Bottom rim | None | `::after` gradient — the liquid pooling at the bottom |
| Behavior on hover | Lift + brighter shadow | Lift + brighter shadow + **specular sweep animation** |
| Mental model | Frosted glass pane | Optical glass slab with measurable thickness |

If your output omits the `saturate(180%)`, the `brightness(1.05)`, the `::before`, or any of the 4 shadow layers, it is not Liquid Glass. Reject and re-prompt.

---

## Animated Specular Sweep (Hover)

```css
.lq-glass.interactive {
  transition: transform 0.4s var(--spring), box-shadow 0.4s var(--ease);
  cursor: pointer;
}
.lq-glass.interactive:hover {
  transform: translateY(-2px) scale(1.005);
  box-shadow:
    0 1px 0 rgba(255,255,255,0.6) inset,
    0 -1px 0 rgba(30,58,95,0.08) inset,
    0 0 0 0.5px rgba(255,255,255,0.4) inset,
    0 16px 48px rgba(30,58,95,0.18),
    0 4px 12px rgba(30,58,95,0.10);
}
.lq-glass.interactive:hover::before {
  transform: translateX(8%) translateY(-4%);
  opacity: 1.2;
}
```

The sweep is the single most "Apple" interaction in this style. It is what tells the eye that the material is alive — that light is moving across its surface, not just rendering statically. Always include it on hoverable glass surfaces.

---

## iOS Blue-Tinted Button (Primary)

The primary button is just the lq-glass recipe with the white fill swapped for `rgba(0,113,227,0.85)` and the shadow drop tinted blue.

```css
.btn-p {
  color: #fff;
  background: rgba(0,113,227,0.85);
  backdrop-filter: blur(16px) saturate(180%);
  -webkit-backdrop-filter: blur(16px) saturate(180%);
  border: 1px solid rgba(255,255,255,0.35);
  box-shadow:
    0 1px 0 rgba(255,255,255,0.5) inset,
    0 -1px 0 rgba(0,40,100,0.18) inset,
    0 0 0 0.5px rgba(255,255,255,0.2) inset,
    0 8px 24px rgba(0,113,227,0.4),
    0 2px 6px rgba(0,113,227,0.22);
  transition: transform 0.3s var(--spring), box-shadow 0.3s var(--ease), background 0.3s var(--ease);
}
.btn-p:hover {
  background: rgba(33,150,255,0.92);
  transform: translateY(-1px);
  box-shadow:
    0 1px 0 rgba(255,255,255,0.6) inset,
    0 -1px 0 rgba(0,40,100,0.22) inset,
    0 0 0 0.5px rgba(255,255,255,0.3) inset,
    0 14px 36px rgba(0,113,227,0.5),
    0 4px 10px rgba(0,113,227,0.28);
}
.btn-p:active { transform: scale(0.97); }
```

For the destructive variant, replace `0,113,227` with `255,69,58` (Apple red `#ff453a`). For success, use `52,199,89` (`#34c759`).

---

## iOS Focus Halo

This single recipe is the most recognizable input focus state in modern Apple software. Reproduce it exactly — the sizes are not arbitrary.

```css
.inp:focus {
  background: rgba(255,255,255,0.45);
  border: 1px solid rgba(0,113,227,0.7);
  box-shadow:
    0 0 0 4px rgba(0,113,227,0.20),     /* halo ring */
    0 0 12px rgba(0,113,227,0.40),      /* outer glow */
    0 1px 0 rgba(255,255,255,0.60) inset,
    inset 0 2px 6px rgba(30,58,95,0.06);
}
```

The halo (`0 0 0 4px rgba(0,113,227,0.20)`) is what reads as "iOS." The outer glow blur (`12px`) is what reads as "Liquid Glass." Together they're unmistakable.

---

## Color Tokens

| Token | Value | Role |
|-------|-------|------|
| `--bg-grad` | `linear-gradient(135deg, #ffd6c2, #d4a7f7, #6ab5ff, #5cd5d5)` | The fixed refractable background. Required. |
| `--glass-fill` | `rgba(255,255,255,0.18)` | Standard glass fill — most surfaces |
| `--glass-fill-2` | `rgba(255,255,255,0.28)` | Elevated surfaces — panels, callouts, secondary buttons |
| `--glass-fill-3` | `rgba(255,255,255,0.42)` | Hover state, focused inputs, brightest elements |
| `--glass-edge` | `1px solid rgba(255,255,255,0.4)` | Standard luminous hairline |
| `--glass-edge-hi` | `1px solid rgba(255,255,255,0.65)` | Focused / emphasized edge |
| `--t1` | `#1e3a5f` | Primary text — deep navy reads sharply on light glass |
| `--t2` | `rgba(30,58,95,0.7)` | Body / secondary text |
| `--t3` | `rgba(30,58,95,0.45)` | Tertiary / placeholders |
| `--t4` | `rgba(30,58,95,0.22)` | Hairlines, separators |
| `--ac` | `#0071e3` | iOS blue — interactive states only |
| `--ac-hi` | `#2196ff` | Accent hover lift |
| `--ac-glow` | `rgba(0,113,227,0.4)` | Glow halo for focus, active controls |
| `--ac-green` | `#34c759` | Success / on toggles (iOS native) |
| `--ac-red` | `#ff453a` | Destructive / error (iOS native) |
| `--ac-orange` | `#ff9f0a` | Warning (iOS native) |

**Critical rule:** Liquid Glass needs a *content-rich background*. A flat color or single-stop gradient kills the material because there is nothing for `saturate(180%)` to amplify. Always pair with a multi-stop gradient + 1–3 large blurred orbs in the corners. The orbs are part of the system, not decoration.

---

## Glass Material System

Five blur recipes for five surface roles. Every glass surface in the demo uses one of these — never invent a new one mid-design.

| Role | Backdrop filter | Fill | Use on |
|------|-----------------|------|--------|
| Subtle | `blur(14px) saturate(160%)` | `rgba(255,255,255,0.22)` | Inline tags, chips, search bars |
| Standard | `blur(20px) saturate(180%) brightness(1.05)` | `rgba(255,255,255,0.18)` | All cards, callouts, default panels |
| Elevated | `blur(24px) saturate(180%) brightness(1.05)` | `rgba(255,255,255,0.28)` | Form panels, large cards, hero widgets |
| Sticky chrome | `blur(28px) saturate(200%) brightness(1.08)` | `rgba(255,255,255,0.28–0.32)` | Sticky nav, modals, floating bars |
| Tinted (active) | `blur(16px) saturate(180%)` over `rgba(0,113,227,0.85)` | — | Primary buttons, active toggle, selected nav |

---

## Typography

**Typeface:** SF Pro Display (headings) + SF Pro Text (body) + SF Mono (numerics, kickers). Inter is the cross-platform fallback.

**Import (fallback for non-Apple systems):**
```html
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
```

**Tight tracking is structural.** Apple's voice lives in the negative letter-spacing — it is not a stylistic flourish, it is the literal sound of the brand.

| Level | Size | Weight | Letter-spacing | Line-height |
|-------|------|--------|----------------|-------------|
| Display | 48–96px | 700 | **−0.04em** | 0.95 |
| H1 | 36px | 700 | −0.035em | 1.10 |
| H2 | 28px | 600 | −0.028em | 1.15 |
| H3 | 22px | 600 | −0.022em | 1.20 |
| H4 | 18px | 600 | −0.018em | 1.30 |
| Body Lg | 17px | 400 | −0.012em | 1.55 |
| Body | 16px | 400 | **−0.011em** | 1.50 |
| Body Sm | 14px | 400 | −0.005em | 1.50 |
| Caption | 12px | 500 | +0.06em | UPPERCASE · MONO |

**Why SF Pro:** It is the operating system. Liquid Glass is the operating system's material. Substituting any other typeface breaks the union — a humanist sans (Inter, Helvetica) reads as "Apple-adjacent"; a geometric (Geist, DM Sans) reads as "Vercel-adjacent"; a rounded face reads as Material Design. Use SF Pro on Apple systems via `-apple-system`; fall back to Inter elsewhere.

---

## Apple Spring Timing

```css
--spring: cubic-bezier(0.32, 0.72, 0, 1);
```

This is the curve Apple uses for sheet presentations, toggle thumbs, and the sliding pill in segmented controls. **Use it for:**
- Card hover lifts
- Button press release
- Toggle thumb travel
- Slider thumb scaling
- Sliding active indicators in nav bars
- Modal entrances and exits

Use the standard ease (`cubic-bezier(0.4, 0, 0.2, 1)`) for non-spatial transitions: opacity, color, shadow shifts.

| Token | Value | Use |
|-------|-------|-----|
| `--ease` | `cubic-bezier(0.4, 0, 0.2, 1)` | Color, opacity, shadow |
| `--spring` | `cubic-bezier(0.32, 0.72, 0, 1)` | Position, scale, transform |
| `--ease-out` | `cubic-bezier(0, 0, 0.2, 1)` | Scroll reveals, panel entrances |

| Interaction | Duration | Curve |
|-------------|----------|-------|
| Button hover lift | 300ms | spring |
| Specular sweep | 600ms | ease |
| Card hover | 400ms | spring |
| Toggle thumb travel | 360ms | spring |
| Slider thumb scale | 150ms | ease |
| Focus halo appear | 250ms | ease |
| Sliding pill (nav) | 500ms | spring |
| Scroll reveal | 700ms | ease-out |

---

## Border Radius

| Token | Value | Use |
|-------|-------|-----|
| `--r-sm` | 12px | Checkboxes, small chips |
| `--r` | 18px | Buttons, inputs |
| `--r-md` | 24px | Cards, callouts, default panels |
| `--r-lg` | 32px | Large panels, modals, form panels |
| `--r-full` | 9999px | Pills, toggles, circular buttons, segmented controls |

Apple's WWDC25 system biases toward *larger radii than you think*. A 16px corner reads as iOS 12. A 24–32px corner reads as iOS 26. When in doubt, round up.

---

## Spacing Scale

Same Apple 8px-based rhythm as the rest of the gallery:

| Step | px | rem |
|------|----|-----|
| 1 | 4 | 0.25 |
| 2 | 8 | 0.5 |
| 3 | 12 | 0.75 |
| 4 | 16 | 1 |
| 5 | 20 | 1.25 |
| 6 | 24 | 1.5 |
| 8 | 32 | 2 |
| 10 | 40 | 2.5 |
| 12 | 48 | 3 |

---

## Component Snippets

### Glass Card

```css
.card-lq {
  border-radius: var(--r-lg);
  overflow: hidden;
  background: var(--glass-fill-2);
  backdrop-filter: blur(22px) saturate(180%) brightness(1.05);
  -webkit-backdrop-filter: blur(22px) saturate(180%) brightness(1.05);
  border: var(--glass-edge);
  box-shadow:
    0 1px 0 rgba(255,255,255,0.55) inset,
    0 -1px 0 rgba(30,58,95,0.06) inset,
    0 0 0 0.5px rgba(255,255,255,0.3) inset,
    0 10px 36px rgba(30,58,95,0.14),
    0 2px 8px rgba(30,58,95,0.06);
  position: relative;
  isolation: isolate;
  transition: transform 0.4s var(--spring), box-shadow 0.4s var(--ease);
}
.card-lq:hover {
  transform: translateY(-4px);
  box-shadow:
    0 1px 0 rgba(255,255,255,0.6) inset,
    0 -1px 0 rgba(30,58,95,0.08) inset,
    0 0 0 0.5px rgba(255,255,255,0.4) inset,
    0 20px 56px rgba(30,58,95,0.22),
    0 4px 12px rgba(30,58,95,0.10);
}
```

The card thumbnails are **rich gradient surfaces** — warm sunset, cool ocean, vivid aurora. Without color beneath the glass, the saturate boost has nothing to work with.

### iOS Toggle (Pill)

```css
.tgl-track {
  display: block;
  width: 51px; height: 31px;
  border-radius: 9999px;
  background: rgba(120,120,128,0.32);
  border: 1px solid rgba(255,255,255,0.30);
  box-shadow:
    0 1px 0 rgba(255,255,255,0.4) inset,
    inset 0 1px 3px rgba(30,58,95,0.12);
  position: relative;
  transition: background 0.3s var(--ease), border-color 0.3s var(--ease);
}
.tgl-thumb {
  position: absolute;
  top: 2px; left: 2px;
  width: 25px; height: 25px;
  border-radius: 50%;
  background: linear-gradient(180deg, #ffffff 0%, #f4f7fb 100%);
  box-shadow:
    0 1px 0 rgba(255,255,255,0.9) inset,
    0 -1px 0 rgba(30,58,95,0.06) inset,
    0 3px 8px rgba(30,58,95,0.18),
    0 1px 2px rgba(30,58,95,0.10);
  transition: transform 0.36s var(--spring);
}
input:checked + .tgl-track {
  background: rgba(52,199,89,0.92);  /* iOS green */
  box-shadow:
    0 1px 0 rgba(255,255,255,0.5) inset,
    0 0 16px rgba(52,199,89,0.4);
}
input:checked + .tgl-track .tgl-thumb { transform: translateX(20px); }
```

Note: iOS toggles use **green**, not blue, when active. This is a system convention. Use blue only on toggles that explicitly mean "iOS blue switch" (rare).

### Slider with Filled Track

```css
.rng {
  -webkit-appearance: none;
  flex: 1; height: 6px;
  border-radius: 9999px;
  /* The track fills with iOS blue glass up to the value */
  background: linear-gradient(to right,
    rgba(0,113,227,0.85) 0%,
    rgba(0,113,227,0.85) var(--p, 50%),
    rgba(30,58,95,0.18) var(--p, 50%),
    rgba(30,58,95,0.18) 100%);
  box-shadow: inset 0 1px 2px rgba(30,58,95,0.12);
  outline: none; cursor: pointer;
  transition: height 0.15s var(--ease);
}
.rng:hover { height: 8px; }
.rng::-webkit-slider-thumb {
  -webkit-appearance: none;
  width: 22px; height: 22px;
  border-radius: 50%;
  background: linear-gradient(180deg, #ffffff 0%, #f4f7fb 100%);
  border: 1px solid rgba(255,255,255,0.5);
  box-shadow:
    0 1px 0 rgba(255,255,255,0.9) inset,
    0 0 0 0.5px rgba(0,113,227,0.5),
    0 4px 12px rgba(30,58,95,0.22),
    0 0 16px var(--ac-glow);
  cursor: pointer; transition: transform 0.15s var(--ease);
}
.rng::-webkit-slider-thumb:hover { transform: scale(1.15); }
```

The thumb is a **floating glass orb** — strong inset highlight on top, accent halo glow around the edge. Update the `--p` CSS variable on `input` events to repaint the fill.

### Sticky Glass Nav

```css
.topnav {
  position: sticky;
  top: 0;
  z-index: 100;
  margin: 12px 16px 0;
  height: 60px;
  padding: 0 1.25rem;
  border-radius: var(--r-md);
  background: rgba(255,255,255,0.28);
  backdrop-filter: blur(28px) saturate(200%) brightness(1.08);
  -webkit-backdrop-filter: blur(28px) saturate(200%) brightness(1.08);
  border: 1px solid rgba(255,255,255,0.5);
  box-shadow:
    0 1px 0 rgba(255,255,255,0.6) inset,
    0 -1px 0 rgba(30,58,95,0.06) inset,
    0 0 0 0.5px rgba(255,255,255,0.3) inset,
    0 12px 36px rgba(30,58,95,0.14),
    0 2px 8px rgba(30,58,95,0.08);
}
```

Note: sticky chrome runs **higher blur (28px)** and **higher brightness (1.08)** than standard glass — it should feel slightly more present than the rest of the surface.

### Sliding Pill Bottom Nav

```css
.lq-navbar {
  position: relative;
  margin: 0 1rem 1rem;
  padding: 0.5rem;
  border-radius: 9999px;
  display: flex;
  background: rgba(255,255,255,0.32);
  backdrop-filter: blur(20px) saturate(180%) brightness(1.05);
  border: 1px solid rgba(255,255,255,0.5);
  box-shadow: 0 1px 0 rgba(255,255,255,0.55) inset, 0 8px 24px rgba(30,58,95,0.12);
}
.ni-pill {
  position: absolute;
  background: rgba(0,113,227,0.85);
  border: 1px solid rgba(255,255,255,0.35);
  border-radius: 9999px;
  box-shadow:
    0 1px 0 rgba(255,255,255,0.5) inset,
    0 4px 14px var(--ac-glow);
  transition: left 0.5s var(--spring), width 0.5s var(--spring);
}
```

The pill's `left` and `width` are set in JavaScript on click. The 500ms spring transition is what makes the slide feel like a real Apple control.

---

## Background Architecture

The body background is the sole place where the gradient lives. **Two layers** are required:

```css
body {
  background: linear-gradient(135deg, #ffd6c2 0%, #d4a7f7 30%, #6ab5ff 65%, #5cd5d5 100%);
  background-attachment: fixed;
  min-height: 100vh;
}

/* Atmospheric blur orbs — extra content for the glass to refract */
body::before {
  content: '';
  position: fixed;
  width: 520px; height: 520px;
  top: -160px; left: -120px;
  background: radial-gradient(circle, #ff8fb0 0%, #ffa08a 40%, transparent 70%);
  filter: blur(80px);
  border-radius: 50%;
  opacity: 0.85;
  pointer-events: none;
  z-index: 0;
}
body::after {
  content: '';
  position: fixed;
  width: 600px; height: 600px;
  bottom: -200px; right: -200px;
  background: radial-gradient(circle, #5b9bff 0%, #7ee0ff 45%, transparent 70%);
  filter: blur(80px);
  border-radius: 50%;
  opacity: 0.85;
  pointer-events: none;
  z-index: 0;
}
```

Add 1–2 additional `.bg-orb` divs positioned mid-page for visual movement. The orbs are not decoration — they are *content for the glass to bend*. Without them, large glass surfaces in the middle of the page look flat and dead.

---

## Guiding Principles

**1. The 4-layer shadow is non-negotiable.**
Top edge highlight + bottom edge depth + inner ring + drop shadow. Together they signal *thickness*. A single drop shadow gives you Glassmorphism. Four layers give you Liquid Glass.

**2. Saturate(180%) + brightness(1.05) are the fingerprint.**
The blur is just the medium — the saturate boost amplifies the refracted color so the glass feels "alive," and the brightness adds the wet sheen. Together, they're what designers point at and say "yes, that's WWDC."

**3. Tracking is voice.**
−0.04em on display, −0.011em on body. Apple's typographic voice lives in the negative letter-spacing as much as in SF Pro itself. Loose tracking instantly reads as not-Apple.

**4. The specular highlight has personality.**
A static `::before` looks great. An animated `::before` that sweeps on hover is what makes the material feel like a real Apple component. Always include the sweep on interactive surfaces.

**5. iOS blue is the only fully saturated point.**
Everything else is translucent and tonal. The accent — `#0071e3` — appears only on interactive states and active controls. Used elsewhere, it loses its meaning as the focal anchor.

**6. The background is part of the system.**
Liquid Glass on a flat color is a contradiction in terms. The gradient + orbs aren't decorative — they are the medium being refracted. Treat them with the same care you treat the glass itself.

---

## Do's

- **DO** layer `backdrop-filter: blur(20px) saturate(180%) brightness(1.05)` on every primary glass surface. All three filters, every time.
- **DO** include all 4 shadow layers — top inset, bottom inset, inner ring, drop. Set them as a single `box-shadow` declaration.
- **DO** use SF Pro Display (or Inter as fallback) at tight tracking: −0.04em on display, −0.011em on body.
- **DO** animate the `::before` specular on hover. The sweep is what makes the material feel real.
- **DO** use the iOS focus halo: `0 0 0 4px rgba(0,113,227,0.20) + 0 0 12px rgba(0,113,227,0.40)`.
- **DO** use Apple's spring `cubic-bezier(0.32, 0.72, 0, 1)` for transforms (slide, scale, lift).
- **DO** use iOS green (`#34c759`) for active toggles, not iOS blue.
- **DO** add 1–3 large blurred orbs as background content for the glass to refract.
- **DO** test glass surfaces against multiple regions of the gradient — light areas vs dark areas show very different material behavior.

---

## Don'ts

- **DON'T** ship a single-layer `box-shadow`. The 4-layer system is what signals thickness. One shadow looks like a flat card with a border-radius.
- **DON'T** omit `saturate()` and `brightness()` from `backdrop-filter`. A pure blur gives you Glassmorphism, not Liquid Glass — the material reads as flat frost, not optical glass.
- **DON'T** use a flat background color. There is nothing for the saturate to amplify. The glass collapses to "white box with shadow."
- **DON'T** use thick borders. The hairline (`1px solid rgba(255,255,255,0.4)`) plus the inner 0.5px ring are structural. A 2px border looks like a debug outline.
- **DON'T** use sharp corners. Liquid Glass needs the 18–32px radius range. Below 12px the material reads as harsh and engineered, not soft and optical.
- **DON'T** use `transition: all`. Always name properties: `transform`, `box-shadow`, `background`, `opacity`. `all` triggers expensive interpolations on properties you didn't intend (and is part of why Glassmorphism implementations feel sluggish).
- **DON'T** use accent color for non-interactive elements. iOS blue means "you can touch this." Bleeding it onto static elements destroys the affordance signal.
- **DON'T** set the body `background` without `background-attachment: fixed`. The gradient must remain stationary as content scrolls past, otherwise the refraction shifts in ways that look broken.
- **DON'T** overload the page with glass. 6–10 glass surfaces visible at once is the practical maximum on mid-range hardware. Each one stacks GPU cost.

---

## Anti-Patterns to Reject Immediately

If any AI-generated output includes these, reject and re-prompt:

| Anti-pattern | What it produces | Fix |
|--------------|------------------|-----|
| `backdrop-filter: blur(20px)` only | Flat Glassmorphism | Add `saturate(180%) brightness(1.05)` |
| `box-shadow: 0 4px 12px rgba(0,0,0,0.1)` only | Generic card | Add 3 inset layers + 2nd drop shadow |
| `border-radius: 8px` on a panel | Engineered, not Apple | Use 24–32px |
| No `::before` overlay on glass | Material feels static and dry | Add diagonal specular gradient |
| `font-family: Helvetica` or `font-family: Roboto` | Wrong system voice | `-apple-system, BlinkMacSystemFont, SF Pro Display, Inter` |
| `letter-spacing: 0` on display headings | Soft / non-Apple | `letter-spacing: -0.04em` |
| Flat hex background (`background: #f5f5f7`) | Dead glass | Multi-stop gradient + orbs |
| `transition: all 0.3s ease` | Sluggish, expensive | Name properties; use `var(--ease)` or `var(--spring)` |
| Active toggle in `#0071e3` | iOS blue toggle (rare) | Use `#34c759` (iOS green) |
| `border: 2px solid #ffffff` | Reads as debug outline | `1px solid rgba(255,255,255,0.4)` |
| Active nav tab with no glow | Looks unfinished | Tinted glass pill + accent glow |
| Square focus outline (`outline: 2px solid blue`) | Generic browser default | iOS halo: `0 0 0 4px rgba(0,113,227,0.20) + 0 0 12px rgba(0,113,227,0.40)` |

---

## AI Prompting Guidance

Use this block to instruct any AI coding agent to reproduce this style. The anchor phrases are intentional — say "WWDC 2025 Liquid Glass," not "frosted glass" or "glassmorphism."

```
Build in WWDC 2025 Liquid Glass style — Apple's iOS 26 / macOS Tahoe / visionOS 3 material:

BACKGROUND (required):
- Body: linear-gradient(135deg, #ffd6c2 0%, #d4a7f7 30%, #6ab5ff 65%, #5cd5d5 100%)
  with background-attachment: fixed
- Add 2-3 large blurred orbs in body::before, body::after, and a .bg-orb div
  (radial-gradients, ~500px wide, blur(80px), positioned in corners)
- This is non-negotiable — Liquid Glass requires content beneath to refract

LIQUID GLASS RECIPE — apply to every glass surface:
- background: rgba(255,255,255,0.18)
- backdrop-filter: blur(20px) saturate(180%) brightness(1.05) — ALL THREE filters
- border: 1px solid rgba(255,255,255,0.4)
- The 4-layer shadow (single box-shadow declaration):
    0 1px 0 rgba(255,255,255,0.5) inset,         (top edge highlight)
    0 -1px 0 rgba(30,58,95,0.06) inset,          (bottom edge depth)
    0 0 0 0.5px rgba(255,255,255,0.25) inset,    (inner ring)
    0 8px 32px rgba(30,58,95,0.12),              (drop shadow)
    0 2px 8px rgba(30,58,95,0.08)                (close drop)
- ::before pseudo: linear-gradient(135deg, rgba(255,255,255,0.45) 0%, rgba(255,255,255,0.10) 30%, transparent 50%, transparent 70%, rgba(255,255,255,0.08) 100%) — the specular highlight
- ::after pseudo: linear-gradient(180deg, transparent 70%, rgba(255,255,255,0.10) 90%, rgba(255,255,255,0.20) 100%) — the bottom liquid pooling
- On hover: translateY(-2px) + scale(1.005); ::before transforms translateX(8%) translateY(-4%); shadow deepens

PRIMARY BUTTONS (iOS blue glass):
- background: rgba(0,113,227,0.85), backdrop-filter: blur(16px) saturate(180%)
- Same 4-layer shadow but tinted: 0 8px 24px rgba(0,113,227,0.4)
- Hover: bg rgba(33,150,255,0.92), translateY(-1px), deeper accent glow
- Press: scale(0.97)

INPUTS (recessed glass):
- background: rgba(255,255,255,0.32) with extra inset shadow: inset 0 2px 6px rgba(30,58,95,0.08)
- Focus: iOS HALO — 0 0 0 4px rgba(0,113,227,0.20) + 0 0 12px rgba(0,113,227,0.40)
  + border: 1px solid rgba(0,113,227,0.7)

TOGGLES (iOS pill):
- Track 51×31px, rounded full, gray glass at rest
- ON state: rgba(52,199,89,0.92) — iOS green, not blue
- White thumb 25×25 with strong inset highlight + drop shadow
- Spring: cubic-bezier(0.32, 0.72, 0, 1), 360ms

SLIDERS:
- Filled track up to value: linear-gradient(to right, rgba(0,113,227,0.85) 0%, rgba(0,113,227,0.85) var(--p), rgba(30,58,95,0.18) var(--p), rgba(30,58,95,0.18) 100%)
- Thumb: floating glass orb with iOS blue accent halo glow

CARDS:
- Same lq-glass recipe, border-radius 32px
- Thumbnails are RICH GRADIENT SURFACES (warm sunset, cool ocean, vivid aurora) — not solid colors
- Hover: translateY(-4px) + spring + brighter specular sweep

NAV:
- Sticky top bar: same recipe but blur(28px) saturate(200%) brightness(1.08), brighter
- Bottom tab bar: glass pill that slides via cubic-bezier(0.32, 0.72, 0, 1)
- Active tab: tinted iOS blue glass pill with accent glow

TYPE:
- Heading: -apple-system, BlinkMacSystemFont, 'SF Pro Display', 'Inter', system-ui, sans-serif
- Display 48-96px / 700 / letter-spacing -0.04em
- Body 16px / 400 / letter-spacing -0.011em
- Mono kicker: SF Mono / 12px / 500 / +0.06em UPPERCASE / iOS blue color

MOTION:
- --spring: cubic-bezier(0.32, 0.72, 0, 1) for transforms
- --ease: cubic-bezier(0.4, 0, 0.2, 1) for color/opacity
- 300-400ms hover lifts, 360ms toggle, 500ms sliding pill, 600ms specular sweep

NEVER:
- Use a flat background color (the saturate has nothing to amplify)
- Use a single-layer box-shadow (must be 4 layers)
- Omit saturate() or brightness() from backdrop-filter
- Use thick borders (>1px) or sharp corners (<12px)
- Use accent color on non-interactive elements
- Use SF Pro at zero or positive letter-spacing
- Use transition: all (always name properties)
- Use iOS blue for active toggle states (use iOS green #34c759)
```

---

## Comparison Table — Liquid Glass vs Glassmorphism

| Dimension | Glassmorphism (2020) | **Liquid Glass (WWDC 2025)** |
|-----------|----------------------|-------------------------------|
| Era | iOS 14-era frosted blur | iOS 26 / macOS Tahoe / visionOS 3 |
| Material model | Frosted glass | Optical glass with measurable thickness |
| Backdrop filter | `blur(40px)` | `blur(20px) saturate(180%) brightness(1.05)` |
| Border | One hairline | Hairline + inner ring + edge highlights |
| Shadow | One drop shadow | **4-layer system** (top, bottom, ring, drop) |
| Top sheen | None | `::before` specular gradient |
| Bottom rim | None | `::after` liquid pooling gradient |
| Hover behavior | Lift + brighter shadow | Lift + brighter shadow + **animated specular sweep** |
| Background | Dark vivid gradient | Light multi-color gradient + atmospheric orbs |
| Text color | White | Deep navy (#1e3a5f) — readable on light glass |
| Active accent | Various (cyan, purple) | Strict iOS blue `#0071e3` |
| Focus state | Glow ring | iOS halo (4px ring + 12px outer glow) |
| Spring curve | Generic ease | Apple spring `cubic-bezier(0.32, 0.72, 0, 1)` |
| Typeface | Inter / Helvetica | SF Pro Display + tight tracking |
| Reads as | "futuristic dashboard" | "an Apple OS surface" |

If your output looks like the left column, you've shipped Glassmorphism. The bar is the right column. The signal is when a designer looks at it and says: *"yes, that's WWDC 2025 Liquid Glass."*
