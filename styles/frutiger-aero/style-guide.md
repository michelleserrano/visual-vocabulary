# Frutiger Aero — Style Guide

**Personality:** Optimistic. Glassy. Nature-inspired. Sky-blue. 2007.

Named after typographer Adrian Frutiger and the Windows Aero glass UI. The defining visual language of the Web 2.0 era — translucent panels, sky-blue gradients, glossy pill buttons, and a genuine belief that technology belonged in nature.

---

## Identity

| Attribute | Value |
|---|---|
| Era | 2004–2012 (peak: 2006–2009) |
| Platform origin | Windows Vista / Windows 7 / Web 2.0 |
| Mood | Optimistic, clean, alive, friendly |
| Key material | Aero glass — translucent, blurred, specular |
| Signature color | Sky blue `#87ceeb` |
| Signature element | Glossy two-tone pill button |
| Font | Segoe UI (Windows) / Myriad Pro (Mac) |

---

## Color Palette

```
--sky:      #87ceeb   // THE defining color — use everywhere
--sky-lt:   #c8e8f8   // pale sky, backgrounds, hover states
--sky-dk:   #1a6bb5   // accent, text headings, borders
--grass:    #4caf50   // nature anchor, secondary actions
--grass-lt: #81c784   // light grass, hover on green
--chrome:   rgba(255,255,255,0.85)  // glass white
--glass-bg: rgba(255,255,255,0.55)  // panel background
--glass-dk: rgba(200,232,248,0.35)  // tinted glass
--t1:       #1a3a5c   // primary text
--t2:       #2a5a8a   // secondary text
--t3:       rgba(26,58,92,0.55)     // muted text
--t4:       rgba(26,58,92,0.3)      // ghost text
--ac:       var(--sky-dk)           // accent
--ac-lo:    rgba(26,107,181,0.18)   // focus ring glow
```

### Page Background

The signature sky-to-nature gradient — always fixed attachment so panels float over it.

```css
body {
  background: linear-gradient(180deg,
    #87ceeb 0%,
    #c8e8f8 40%,
    #e8f4e8 80%,
    #c8e8c0 100%
  );
  background-attachment: fixed;
}
```

---

## Typography

**Font stack:** `'Segoe UI', 'Myriad Pro', 'Frutiger', 'Helvetica Neue', Arial, sans-serif`

No Google Fonts needed — this style uses the system font exactly as Microsoft intended it.

| Level | Size | Weight | Tracking |
|---|---|---|---|
| Display | 48px | 700 | −0.03em |
| H1 | 36px | 600 | −0.025em |
| H2 | 28px | 600 | −0.02em |
| H3 | 22px | 600 | −0.01em |
| H4 | 18px | 500 | — |
| Body Lg | 17px | 400 | — |
| Body | 16px | 400 | — |
| Body Sm | 14px | 400 | — |
| Caption | 12px | 600 | +0.06em UC |

**Rules:**
- Headings: `color: var(--sky-dk)`; text-shadow subtle white below
- Body: `color: var(--t1)` or `var(--t2)`
- Never use a condensed, geometric, or decorative typeface

---

## Aero Glass Panel

The core building block. Three layers in combination:

```css
.aero-panel {
  /* Layer 1: translucent white fill */
  background: rgba(255,255,255,0.6);

  /* Layer 2: backdrop blur */
  backdrop-filter: blur(16px) saturate(140%);
  -webkit-backdrop-filter: blur(16px) saturate(140%);

  /* Layer 3: specular highlights */
  border: 1px solid rgba(255,255,255,0.7);
  border-radius: 18px;
  box-shadow:
    0 4px 24px rgba(26,107,181,0.15),       /* depth shadow */
    inset 0 1px 0 rgba(255,255,255,0.8);    /* specular top edge */
}
```

**Hover state:** increase shadow intensity, optionally lift `translateY(-2px)` or `(-3px)`.

**Glass opacity scale:**
- Panels: `rgba(255,255,255,0.6)` — main panels
- Forms: `rgba(255,255,255,0.65)` — slightly more opaque for readability
- Inputs: `rgba(255,255,255,0.75)` — most opaque for contrast
- Overlays: `rgba(255,255,255,0.35)` — lightest decorative use

---

## Glossy Button

The Web 2.0 signature. The two-stop gradient (light top, dark bottom) + specular inset = water droplet.

```css
.btn-aero {
  /* The two-tone glossy gradient */
  background: linear-gradient(180deg,
    #7ec8f0 0%,
    #5bb8f5 45%,      /* top half: light blue */
    #1a6bb5 50%,      /* hard midpoint transition */
    #2a7ad4 100%      /* bottom half: darker */
  );
  border-radius: 9999px;          /* always pill */
  border: 1px solid #1a5a9a;
  box-shadow:
    0 3px 8px rgba(26,107,181,0.35),          /* drop shadow */
    inset 0 1px 0 rgba(255,255,255,0.45);     /* specular */
  color: white;
  text-shadow: 0 -1px 0 rgba(0,0,50,0.3);    /* text depth */
  padding: 0.6875rem 1.75rem;
  font-weight: 600;
}

.btn-aero:hover {
  box-shadow:
    0 5px 16px rgba(26,107,181,0.45),
    inset 0 1px 0 rgba(255,255,255,0.55);
  filter: brightness(1.06);
}

.btn-aero:active {
  box-shadow:
    0 1px 4px rgba(26,107,181,0.3),
    inset 0 2px 6px rgba(0,0,50,0.25);
  filter: brightness(0.95);
}
```

### Green Secondary Button

Same recipe, grass palette:

```css
background: linear-gradient(180deg,
  #a5d6a7 0%, #81c784 45%,
  #388e3c 50%, #4caf50 100%
);
border: 1px solid #2e7d32;
box-shadow: 0 3px 8px rgba(56,142,60,0.35), inset 0 1px 0 rgba(255,255,255,0.45);
```

### Ghost Button

```css
background: rgba(255,255,255,0.55);
backdrop-filter: blur(12px);
border: 1px solid var(--sky-dk);
color: var(--sky-dk);
box-shadow: 0 2px 8px rgba(26,107,181,0.15), inset 0 1px 0 rgba(255,255,255,0.8);
```

---

## Form Inputs

White glass with sky blue focus — a Vista dialog feel.

```css
.inp {
  background: rgba(255,255,255,0.75);
  border: 1px solid rgba(26,107,181,0.2);
  border-radius: 12px;
  padding: 0.75rem 1rem;
  box-shadow:
    inset 0 1px 4px rgba(26,107,181,0.08),
    inset 0 1px 0 rgba(255,255,255,0.9);    /* specular inside */
  color: var(--t1);
  font-family: var(--f);
}

.inp:focus {
  border-color: var(--sky-dk);
  box-shadow:
    0 0 0 3px rgba(26,107,181,0.18),         /* glow ring */
    inset 0 1px 4px rgba(26,107,181,0.1),
    inset 0 1px 0 rgba(255,255,255,0.9);
}
```

**Checkboxes:** round (`border-radius: 50%`), white glass at rest, glossy sky blue when checked.

**Toggles:** white glass pill track with inset shadow; sky blue gradient track on active; glossy white thumb with drop shadow.

---

## Sliders

Sky-tinted track, glossy white thumb — a water droplet riding a sky channel.

```css
/* Track */
background: rgba(135,206,235,0.3);
border: 1px solid rgba(26,107,181,0.15);
box-shadow: inset 0 1px 3px rgba(26,107,181,0.15);
height: 10px;
border-radius: 9999px;

/* Thumb */
background: linear-gradient(180deg, #ffffff 30%, #e0f0f8 100%);
border: 1px solid rgba(26,107,181,0.3);
box-shadow: 0 2px 8px rgba(26,107,181,0.3), inset 0 1px 0 rgba(255,255,255,1);
border-radius: 50%;
width: 24px; height: 24px;
```

---

## Navigation

**Sticky top nav:**
- `background: rgba(255,255,255,0.75)` + `backdrop-filter: blur(20px)`
- Top border: 4px sky gradient strip — `border-image: linear-gradient(90deg, #87ceeb, #1a6bb5, #4caf50, #87ceeb) 1`
- Title: `color: var(--sky-dk)`, Segoe UI 700
- CTA: glossy sky blue pill button (same as primary button recipe)

**Bottom / tab nav:**
- Bar: `background: rgba(255,255,255,0.7)` + blur
- Active tab: glossy sky pill wrap (same two-tone gradient as primary button)
- Inactive: transparent wrap, `color: var(--t3)` label
- Active label: `color: var(--sky-dk)`

---

## Nature Decorations

Soft cloud shapes in section backgrounds:

```css
.sec::before {
  content: '';
  position: absolute;
  width: 200px; height: 100px;
  border-radius: 50%;
  background: rgba(255,255,255,0.3);
  filter: blur(40px);
  top: -20px; right: 10%;
  pointer-events: none;
}
```

For hero sections, add multiple blurred orbs of `rgba(135,206,235,0.2)` and `rgba(129,199,132,0.15)`.

---

## Section Headings

```css
.sec-hd::after {
  content: '';
  position: absolute;
  bottom: 0; left: 0; right: 0;
  height: 2px;
  background: linear-gradient(90deg, var(--sky-dk), var(--sky), var(--grass-lt));
  opacity: 0.6;
}
```

Section number pill: glossy sky blue (same button gradient, small pill).

Ghost number: `color: rgba(26,107,181,0.05)`, `font-size: 6rem`.

---

## Spec Callout

```css
.spec-callout {
  background: rgba(255,255,255,0.65);
  backdrop-filter: blur(12px);
  border: 1px solid rgba(255,255,255,0.6);
  border-left: 3px solid var(--sky-dk);   /* sky accent strip */
  border-radius: 12px;
  box-shadow:
    0 2px 12px rgba(26,107,181,0.1),
    inset 0 1px 0 rgba(255,255,255,0.8);
}
```

---

## Card Pattern

```css
.card-aero {
  background: rgba(255,255,255,0.6);
  backdrop-filter: blur(16px) saturate(140%);
  border: 1px solid rgba(255,255,255,0.7);
  border-radius: 24px;
  box-shadow:
    0 6px 24px rgba(26,107,181,0.18),
    inset 0 1px 0 rgba(255,255,255,0.9);   /* specular top */
  transition: box-shadow 0.3s, transform 0.3s;
}
.card-aero:hover {
  box-shadow:
    0 12px 40px rgba(26,107,181,0.28),
    inset 0 1px 0 rgba(255,255,255,0.9);
  transform: translateY(-3px);
}
```

Thumbnails use sky + nature gradients:
- Sky: `linear-gradient(135deg, #87ceeb 0%, #c8e8f8 60%, #e8f4e8 100%)`
- Deep sky: `linear-gradient(135deg, #c8e8f8 0%, #87ceeb 50%, #1a6bb5 100%)`
- Nature: `linear-gradient(135deg, #81c784 0%, #c8e8c0 60%, #87ceeb 100%)`

---

## Anti-Patterns

- **No dark backgrounds.** Frutiger Aero is always light. Dark mode destroys the sky metaphor.
- **No flat fills.** Every interactive surface needs at least one gradient or gloss layer.
- **No sharp corners.** Minimum `border-radius: 8px`. Pill radius for buttons always.
- **No heavy box shadows.** Shadows should be soft and blue-tinted (`rgba(26,107,181,...)`) — never pure black.
- **No geometric typefaces.** Segoe UI / Myriad Pro only. No Roboto, no Inter as primary.
- **No saturated primaries.** The sky blue is soft. If it looks like a sports brand, desaturate.
- **No opaque panels.** All panels need `backdrop-filter` + translucency. Opaque = wrong era.

---

## AI Prompting Guidance

Use these phrases when generating Frutiger Aero UI:

```
"Windows Vista Aero glass style, 2007 Web 2.0 aesthetic"
"translucent frosted glass panels, sky blue #87ceeb palette"
"glossy pill buttons with two-tone gradient, specular highlight"
"nature-inspired, sky and grass greens, optimistic technology"
"backdrop-filter blur panels floating over sky gradient background"
"Segoe UI typeface, water droplet aesthetic, digital optimism"
"Windows Media Player 11 chrome style controls"
"frosted glass with inset specular top highlight, soft blue shadow"
```

**One-liner for LLMs:** "Frutiger Aero: glass panels with backdrop-blur over sky-to-green gradient body, Segoe UI, glossy two-tone sky-blue pill buttons with specular highlights, nature-inspired palette."
