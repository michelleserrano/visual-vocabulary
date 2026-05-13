# Risograph Style Guide
**UI Styles Library — Version 2.0**  
Category: Print revival · Year of origin: 1986 (machine) / 2018+ (digital UI revival)

---

## Personality

**Five words:** Printed. Two-color. Misregistered. Tactile. Crafted.

**Voice of this style:** "Two ink drums, one pass each. The second pass never lands exactly where the first did — and that gap is where the design lives. The third color is the one you didn't ink; it appears where the first two overlap on multiply."

**Use when:** Building zine-style portfolios, indie product brands, editorial UI, music apps, festival sites, anything that wants to feel hand-made and printed rather than computed. Excellent for personality-forward marketing, swag-adjacent UIs, and brand identities that lean editorial.

**Do NOT use when:**
- Dense data UIs (the grain + multiply reduces legibility under load)
- Enterprise tooling, banking, healthcare, or any context that needs an authoritative, neutral voice
- Dark-mode interfaces — the entire system depends on cream paper as the third "color"
- Touch-dense screens with >12 interactive elements per view

---

## Quick Start — Copy & Paste

```css
:root {
  /* ── The paper ─────────────────────── */
  --paper:        #f8f3e8;   /* warm cream — NEVER #fff */
  --paper-shadow: #e8e0c8;   /* toasted paper, for depth */

  /* ── The two inks ──────────────────── */
  --ink-pink:     #ff6b9d;   /* Riso FLUO PINK 32U */
  --ink-teal:     #3aafa9;   /* Riso TEAL 22A */

  /* ── The discovered third color ────── */
  --overprint:    #b85a76;   /* pink × teal on multiply */

  /* ── Type ──────────────────────────── */
  --ink-black:    #1a1a1a;   /* warm black — never #000 */
  --ink-grey:     #4a4640;
  --ink-faint:    #8a8378;

  /* ── Misregistration offset (locked diagonal) ── */
  --reg-x:    3px;
  --reg-y:    3px;
  --reg-x-lg: 4px;   /* buttons, large cards */
  --reg-y-lg: 4px;

  /* ── No shadows. No radii. ─────────── */
  --r-stamp: 2px;     /* maximum corner radius — use sparingly */

  /* ── Motion: print mechanics, not digital easings ── */
  --press: cubic-bezier(0.4, 0, 0.6, 1);   /* short, hard-stop */
  --stamp: steps(2, end);                  /* for stamping marks */
  --dur:   120ms;

  /* ── Type stacks ───────────────────── */
  --f-display: 'Anton', 'Oswald', 'Impact', sans-serif;
  --f-body:    'Lora', 'Crimson Pro', Georgia, serif;
  --f-mono:    'JetBrains Mono', 'Courier New', monospace;
}

body {
  font-family: var(--f-body);
  background: var(--paper);    /* never white */
  color: var(--ink-black);
}
```

Then import the three Google Font families:

```html
<link href="https://fonts.googleapis.com/css2?family=Anton&family=Lora:ital,wght@0,400;0,500;0,600;0,700;1,400&family=JetBrains+Mono:wght@400;500;600;700&display=swap" rel="stylesheet">
```

---

## Color Tokens

| Token | Value | Role |
|-------|-------|------|
| `--paper` | `#f8f3e8` | Page background AND most element fills. NEVER white. |
| `--paper-shadow` | `#e8e0c8` | Subtle depth — focused input fill, disabled buttons |
| `--ink-pink` | `#ff6b9d` | **Riso Fluo Pink 32U** — primary ink, active states, accents |
| `--ink-teal` | `#3aafa9` | **Riso Teal 22A** — secondary ink, misregistered shadow layer |
| `--overprint` | `#b85a76` | The discovered third color — appears where pink × teal multiply |
| `--ink-black` | `#1a1a1a` | Body type and borders — warm black, never `#000` |
| `--ink-grey` | `#4a4640` | Secondary type, muted captions |
| `--ink-faint` | `#8a8378` | Tertiary type, placeholders, disabled state |

**Critical rule:** Use only two colored inks. The overprint is *discovered*, never authored — set both pink and teal layers with `mix-blend-mode: multiply` over cream paper, and #b85a76 appears on its own where they overlap. Reaching for a third ink (yellow, blue, etc.) is leaving the style.

---

## The Six Signature Patterns

These are non-negotiable. Strip any one of them out and you no longer have Risograph.

### 1. Visible grain texture everywhere

Subtle SVG noise filter at ~6–7% opacity, multiplied over every surface.

```css
body::before {
  content: '';
  position: fixed;
  inset: 0;
  pointer-events: none;
  z-index: 999;
  background-image: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' width='240' height='240'><filter id='n'><feTurbulence type='fractalNoise' baseFrequency='0.92' numOctaves='2' stitchTiles='stitch'/><feColorMatrix values='0 0 0 0 0.10  0 0 0 0 0.09  0 0 0 0 0.06  0 0 0 0.85 0'/></filter><rect width='100%25' height='100%25' filter='url(%23n)'/></svg>");
  opacity: 0.07;
  mix-blend-mode: multiply;
}
```

### 2. Intentional misregistration (always 3–4px down-right)

A colored element is offset behind the foreground — as if the second print pass missed by a hair.

```css
.btn {
  background: var(--ink-pink);
  color: var(--paper);
  border: 2px solid var(--ink-black);
  position: relative;
  isolation: isolate;
  mix-blend-mode: multiply;
}
.btn::before {
  content: '';
  position: absolute;
  top: 4px; left: 4px;
  width: 100%; height: 100%;
  background: var(--ink-teal);
  border: 2px solid var(--ink-black);
  z-index: -1;
  mix-blend-mode: multiply;
}
/* Pressed = the misregistration closes back to 0 */
.btn:active::before { top: 0; left: 0; }
```

**Lock the diagonal.** Always down + right (positive x, positive y). Random offsets read as bugs; consistent offsets read as craft.

### 3. Multiply blend mode on colored elements

Pink and teal both set with `mix-blend-mode: multiply` over the cream paper. Where they overlap, the multiply produces `#b85a76` naturally.

```css
.ink-pink { background: var(--ink-pink); mix-blend-mode: multiply; }
.ink-teal { background: var(--ink-teal); mix-blend-mode: multiply; }
/* Where these two overlap on .paper background, you get #b85a76 for free */
```

### 4. Halftone dot patterns

Repeating radial-gradient dots for the "printed" feel — used as backgrounds for tracks, photo fills, type interiors.

```css
.halftone-pink {
  background-image: radial-gradient(circle, var(--ink-pink) 1.4px, transparent 1.9px);
  background-size: 6px 6px;
}
.halftone-teal {
  background-image: radial-gradient(circle, var(--ink-teal) 1.4px, transparent 1.9px);
  background-size: 6px 6px;
}
```

Dot diameter 2.8–4px, spacing 5–7px. Larger = more graphic; smaller = more photographic.

### 5. Two-color rule

Only pink and teal exist as colored inks. Everything else — backgrounds, type, borders, depth — is paper, warm black, or a tone of the two inks. If you find yourself opening the color picker to add a third saturated hue, stop.

```css
/* ✓ Allowed: pink, teal, paper, ink-black, ink-grey, paper-shadow */
/* ✗ Forbidden: any other hue (yellow, blue, green, purple) as a fill */
```

### 6. Registration marks (✛) + cropmarks

Print-shop ephemera that announces "this is a proof, not a webpage."

```css
/* CMYK cropmarks at viewport corners */
.cropmark {
  position: fixed;
  width: 22px; height: 22px;
  pointer-events: none;
  mix-blend-mode: multiply;
  opacity: 0.55;
}
.cropmark::before, .cropmark::after {
  content: '';
  position: absolute;
  background: var(--ink-black);
}
.cropmark::before { left: 0; right: 0; height: 1px; top: 50%; }
.cropmark::after  { top: 0; bottom: 0; width: 1px; left: 50%; }

/* Registration mark — use ✛ or an SVG crosshair-in-circle */
.reg-mark {
  font-family: var(--f-mono);
  color: var(--ink-pink);
  mix-blend-mode: multiply;
}
```

---

## Comparison Tables

### Risograph vs. Memphis Group

| Dimension | Risograph | Memphis Group |
|-----------|-----------|---------------|
| Color count | Strictly 2 inks on paper | 4–6 saturated brights |
| Palette mood | Warm, muted, printed | Loud, dissonant, plastic |
| Surface | Grain + multiply over cream | Flat hard fills on white |
| Shape vocabulary | Rectangles, halftones, crosshatches | Squiggles, terrazzo, geometric riot |
| Texture | Always present (noise, halftone) | Pattern motifs (dots, stripes) but no grain |
| Type | Anton chunky display + serif body | Geometric sans, often Memphis-specific specimens |
| Imperfection | Misregistration *by 3–4px* | Misalignment of *shapes*, not pixels |
| Cultural reference | Print shop, zine, indie press | 80s post-modern furniture, Milan |
| Mood | Quiet craft | Loud rebellion |

### Risograph vs. Brutalist Web

| Dimension | Risograph | Brutalist Web |
|-----------|-----------|---------------|
| Color count | 2 inks on cream | Often monochrome or harsh primaries |
| Imperfection | *Crafted* misregistration | *Default* browser styling, raw HTML |
| Type | Editorial mix (Anton + Lora + Mono) | System fonts, Times, Courier |
| Texture | Grain & halftone — additive craft | None — defaults are the texture |
| Intent | Lovingly hand-made print | Defiantly un-designed |
| Forms | 2px black border, grain inside, no radius | `<input>` with no styling at all |
| Depth | Offset color block (multiplied) | None — flat, raw |
| Audience | Designers, indie brands, editorial | Anti-design statements, hacker culture |

---

## Typography

**Display:** Anton (Google Fonts) — a chunky condensed grotesque that references silkscreen posters.  
**Body:** Lora — a humanist serif with warm proportions; softens the bold display.  
**Mono:** JetBrains Mono — modern monospace for labels, metadata, captions.

**Import:** `https://fonts.googleapis.com/css2?family=Anton&family=Lora:ital,wght@0,400;0,500;0,600;0,700;1,400&family=JetBrains+Mono:wght@400;500;600;700&display=swap`

| Level | Family | Size | Weight | Letter-spacing | Line-height | Use |
|-------|--------|------|--------|----------------|-------------|-----|
| Display | Anton | 64–136px | 400 | +0.005em | 0.88–1.0 | Hero headlines (with misreg) |
| H1 | Anton | 44px | 400 | +0.01em | 1.05 | Page titles |
| H2 | Anton | 32px | 400 | +0.02em | 1.1 | Section headers |
| H3 | Anton | 24px | 400 | +0.02em | 1.15 | Card titles |
| H4 | Lora | 20px | 700 | 0 | 1.3 | Sub-headings, sub-cards |
| Body LG | Lora | 18px | 400 | 0 | 1.65 | Lead paragraphs |
| Body | Lora | 16px | 400 | 0 | 1.6 | Standard copy |
| Body SM | Lora | 14px | 400 | 0 | 1.55 | Secondary copy |
| Caption | JetBrains Mono | 12px | 600 | +0.12em UC | — | Labels, metadata, stamps |

**Typographic rules:**
- All Anton text is `text-transform: uppercase`. The font reads as a poster face.
- Body is **never** Anton. Long-form copy uses Lora exclusively.
- Labels, metadata, time stamps, registration callouts: JetBrains Mono UPPERCASE with +0.10–0.16em letter-spacing.
- Italics carry voice — use Lora italic for hints, captions, and editorial asides.

---

## Spacing Scale

| Step | px | rem | Use |
|------|----|-----|-----|
| 1 | 4px | 0.25rem | Fine adjustments, icon offset |
| 2 | 8px | 0.5rem | Icon-to-label gap |
| 3 | 12px | 0.75rem | Tight padding |
| 4 | 16px | 1rem | Standard padding |
| 5 | 20px | 1.25rem | Card interior padding |
| 6 | 24px | 1.5rem | Section padding |
| 8 | 32px | 2rem | Panel padding |
| 10 | 40px | 2.5rem | Vertical rhythm between blocks |
| 12 | 48px | 3rem | Section gaps |
| 16 | 64px | 4rem | Major hero space |

Generous spacing is structural: cramped layouts collapse the grain + halftone effect into visual noise.

---

## Border Radius

**Default: 0px.** Risograph cannot print smooth curves cleanly. The rectangular silhouette is structural.

| Token | Value | Use |
|-------|-------|-----|
| (default) | 0px | All buttons, cards, inputs, panels |
| `--r-stamp` | 2px | Only on tiny chips/badges, if needed |
| (full) | 50% | Reserved for radio buttons & registration-mark dots |

Any radius above 4px on a box element is a deviation — and almost always wrong.

---

## "Shadows" (There Are None)

Risograph cannot print true black box shadows. Instead, use **offset color blocks** behind elements:

```css
.card {
  background: var(--paper);
  border: 2.5px solid var(--ink-black);
  position: relative;
  isolation: isolate;
}
.card::before {
  content: '';
  position: absolute;
  top: 4px; left: 4px;
  right: -4px; bottom: -4px;
  background: var(--ink-pink);
  border: 2.5px solid var(--ink-black);
  z-index: -1;
  mix-blend-mode: multiply;
  opacity: 0.35;
}
```

| State | Offset | Block opacity |
|-------|--------|---------------|
| Rest | 4px / 4px | 0.30–0.40 |
| Hover | 2px / 2px | 0.35–0.45 |
| Pressed | 0px / 0px | 0.50 (touches the element) |

---

## Motion & Easing

| Token | Value | Use |
|-------|-------|-----|
| `--press` | `cubic-bezier(0.4, 0, 0.6, 1)` | Button presses, card hovers, all UI state changes |
| `--stamp` | `steps(2, end)` | Checkbox mark appearance, stamp animations |
| Duration | 120ms | Default for all state changes |

**Motion philosophy:**
- **No smooth digital easings.** No `ease-in-out`, no `cubic-bezier(0.4, 0, 0.2, 1)` (that's neumorphism's). Risograph motion is *physical* — a stamp landing, a press platen closing.
- **No bounces.** No spring overshoot. The press goes down. It stops. It comes up. That's the entire motion vocabulary.
- **Stepped, not continuous.** VU meters, loading indicators, and decorative animations use `steps(N)` — not smooth keyframes — so they read as mechanical, like a tape deck readout.
- **Animations under 200ms.** Anything longer feels digital, not printed.

---

## Component Snippets

### Primary Button (with misregistered shadow)

```css
.btn-p {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  background: var(--ink-pink);
  color: var(--paper);
  border: 2px solid var(--ink-black);
  padding: 0.7rem 1.6rem;
  font-family: var(--f-mono);
  font-size: 0.8rem;
  font-weight: 700;
  letter-spacing: 0.10em;
  text-transform: uppercase;
  position: relative;
  isolation: isolate;
  mix-blend-mode: multiply;
  cursor: pointer;
  transition: transform 120ms var(--press);
}
.btn-p::before {
  content: '';
  position: absolute;
  top: 4px; left: 4px;
  width: 100%; height: 100%;
  background: var(--ink-teal);
  border: 2px solid var(--ink-black);
  z-index: -1;
  mix-blend-mode: multiply;
  transition: top 120ms var(--press), left 120ms var(--press);
}
.btn-p:hover         { transform: translate(2px, 2px); }
.btn-p:hover::before { top: 2px; left: 2px; }
.btn-p:active         { transform: translate(4px, 4px); }
.btn-p:active::before { top: 0; left: 0; }
```

### Input Field (with grain texture)

```css
.inp {
  background: var(--paper);
  border: 2px solid var(--ink-black);
  padding: 0.7rem 0.9rem;
  font-family: var(--f-body);
  font-size: 0.9375rem;
  color: var(--ink-black);
  outline: none;
  width: 100%;
  /* Grain texture baked into background */
  background-image: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' width='100' height='100'><filter id='n'><feTurbulence type='fractalNoise' baseFrequency='1.0' numOctaves='2' stitchTiles='stitch'/><feColorMatrix values='0 0 0 0 0  0 0 0 0 0  0 0 0 0 0  0 0 0 0.5 0'/></filter><rect width='100%25' height='100%25' filter='url(%23n)' opacity='0.06'/></svg>");
  transition: border-color 120ms var(--press), background-color 120ms var(--press);
}
.inp:focus {
  border-color: var(--ink-pink);
  background-color: var(--paper-shadow);
}
```

### Checkbox (pink ✕ stamp)

```css
.chk-box {
  width: 22px; height: 22px;
  background: var(--paper);
  border: 2px solid var(--ink-black);
  display: flex;
  align-items: center;
  justify-content: center;
}
.chk-mark {
  opacity: 0;
  color: var(--ink-pink);
  mix-blend-mode: multiply;
  transform: rotate(-4deg);     /* hand-stamped tilt */
  transition: opacity 120ms steps(2, end);
}
input:checked + .chk-box .chk-mark { opacity: 1; }
```

### Card (Zine page)

```css
.card-zine {
  background: var(--paper);
  border: 2.5px solid var(--ink-black);
  padding: 1.5rem;
  position: relative;
  isolation: isolate;
  transition: transform 120ms var(--press);
}
.card-zine::before {
  content: '';
  position: absolute;
  top: 4px; left: 4px;
  right: -4px; bottom: -4px;
  background: var(--ink-pink);
  border: 2.5px solid var(--ink-black);
  z-index: -1;
  mix-blend-mode: multiply;
  opacity: 0.35;
}
.card-zine:hover { transform: translate(-2px, -2px); }
```

### Misregistration text helper

```css
.misreg {
  position: relative;
  color: var(--ink-pink);
  mix-blend-mode: multiply;
  display: inline-block;
}
.misreg::before {
  content: attr(data-text);
  position: absolute;
  top: 3px; left: 3px;
  color: var(--ink-teal);
  mix-blend-mode: multiply;
  z-index: -1;
}
```

Usage: `<h1 class="misreg" data-text="RISOGRAPH">RISOGRAPH</h1>`

---

## Guiding Principles

**1. Two colors only. Multiply teaches the third.**  
Pink and teal. That's the ink budget. The third color (#b85a76) emerges where the two overlap on multiply — it's a discovery, not an addition. If you find yourself reaching for yellow, green, or any third saturated hue, you've left the style.

**2. Misregister on purpose. Always down-right. Always 3–4px.**  
The misregistration is the signature. It only feels intentional when it's consistent: every offset on a single page goes in the same direction (down + right) and at the same magnitude. Random offsets read as buggy CSS. Locked offsets read as craft.

**3. Paper is never white.**  
The cream `#f8f3e8` is not background — it's the **third surface** that completes the print. Every pink and teal pixel multiplies with the cream to produce its final color. Drop in `#ffffff` and the entire palette collapses.

**4. Grain is non-optional.**  
The 6–7% noise overlay is what separates a Risograph UI from a flat illustration with offset shadows. Without grain, you have a Memphis poster. With grain, you have a printed page.

**5. Animation = press mechanics.**  
The motion vocabulary is: press platen closes (offset → 0), platen lifts (offset → 4px). No bouncing, no spring, no smooth digital easings. Steps and short hard-stop bezier curves only. The entire UI should feel like operating a duplicator, not a glass touchscreen.

---

## Do's

- **DO** use `mix-blend-mode: multiply` on every colored element. The multiply is what produces the overprint zone and the discovered third color.
- **DO** apply the offset color block at exactly the same diagonal magnitude everywhere on a page (3px or 4px — pick one and stay).
- **DO** put registration marks (✛) at the corners of every card, hero, and major panel.
- **DO** use JetBrains Mono UPPERCASE for every label, badge, time stamp, and metadata field. Mono is the print-shop language.
- **DO** include a colophon at the bottom of the page: machine, month, edition number.

## Don'ts

- **DON'T** use `#ffffff` anywhere. White breaks the multiply formula and the third-color discovery. Always `#f8f3e8`.
- **DON'T** use a third saturated ink color (yellow, blue, purple, green). Two colors total — pink and teal — full stop.
- **DON'T** use `box-shadow` for depth. Risograph can't print black shadows. Use multiplied offset color blocks behind elements instead.
- **DON'T** use `border-radius` above 2px on rectangular elements. The squared silhouette is structural to the print aesthetic.
- **DON'T** use smooth digital easings (`ease-in-out`, default `cubic-bezier(0.4, 0, 0.2, 1)`). Use `steps(2)` for stamps and a short hard-stop bezier for presses. Everything should feel mechanical.

---

## Anti-Patterns to Reject Immediately

If you (or any AI agent) produce any of these, reject and re-prompt:

### Anti-pattern 1 — `box-shadow: 0 4px 12px rgba(0,0,0,0.1)`

A soft drop-shadow is the fingerprint of generic digital UI. Risograph can't print it.

**Fix:** Use an offset color block as a `::before` pseudo-element with `mix-blend-mode: multiply` and 30–40% opacity.

```css
/* ✗ Wrong */
.card { box-shadow: 0 4px 12px rgba(0,0,0,0.1); }

/* ✓ Right */
.card { position: relative; isolation: isolate; }
.card::before {
  content: '';
  position: absolute;
  top: 4px; left: 4px;
  right: -4px; bottom: -4px;
  background: var(--ink-pink);
  z-index: -1;
  mix-blend-mode: multiply;
  opacity: 0.35;
}
```

### Anti-pattern 2 — Pure white background or fills

```css
/* ✗ Wrong */
body { background: #ffffff; }
.card { background: #fff; }

/* ✓ Right */
body { background: var(--paper); /* #f8f3e8 */ }
.card { background: var(--paper); }
```

White is a calibration target on a monitor. Cream paper is the printed surface — and the third pigment that completes the palette. Don't trade the second one in for the first.

### Anti-pattern 3 — Random or symmetrical misregistration

```css
/* ✗ Wrong — random direction */
.btn-1::before { top: -3px; left: 4px; }
.btn-2::before { top: 5px; left: -2px; }

/* ✗ Wrong — symmetrical centered "drop shadow" feel */
.btn::before { top: 3px; left: 0; }
```

Random or symmetrical offsets read as buggy CSS — not as a print mistake — because they violate the print physics. A second pass on a Risograph never lands "above-left" of the first; the paper feeds the same direction every time.

```css
/* ✓ Right — always positive x, positive y, consistent magnitude */
.btn::before    { top: 4px; left: 4px; }
.card::before   { top: 4px; left: 4px; }
.input::before  { top: 3px; left: 3px; }
```

Lock the diagonal. Choose 3px or 4px. Apply it the same way every time.

---

## AI Prompting Guidance

Use this exact block to instruct any AI coding agent to reproduce this style:

```
Build in Risograph style:

ANCHOR PHRASES:
- "Risograph duplicator print"
- "Two-color overprint"
- "Intentional misregistration"
- "Warm pink + teal on cream paper"

PALETTE (locked, do not deviate):
- Paper background: #f8f3e8 (warm cream, NEVER #ffffff)
- Ink 1: #ff6b9d (Riso Fluo Pink 32U)
- Ink 2: #3aafa9 (Riso Teal 22A)
- Discovered third (do not author, let it emerge): #b85a76 where pink × teal multiply
- Text: #1a1a1a (warm black, never #000)

SIGNATURE MOVES (all six required):
1. Grain texture — SVG fractal noise at 6-7% opacity, multiply blend, full page
2. Misregistration — offset second color block 3-4px down-right, always positive x+y, always same magnitude on a page
3. Multiply blend mode — apply mix-blend-mode: multiply to every colored element (pink, teal)
4. Halftone dot patterns — repeating radial-gradient dots, 1.4px circle / 6px spacing
5. No drop shadows — use offset color blocks (::before pseudo-element with multiply)
6. Registration marks (✛) + CMYK cropmarks at corners

TYPE:
- Display: Anton (chunky condensed sans), uppercase, +0.01em tracking
- Body: Lora (warm humanist serif), 16-18px
- Labels: JetBrains Mono UPPERCASE, +0.12em tracking

SHAPE:
- Border-radius: 0 (never above 2px on rectangles)
- Borders: 2px solid #1a1a1a on all containers

MOTION:
- transition: 120ms cubic-bezier(0.4, 0, 0.6, 1) — NO smooth digital easings
- Checkboxes/stamps: steps(2, end)
- No bounce, no spring, no overshoot
- Buttons "press" by closing the misregistration offset from 4px → 0 on :active

EPHEMERA (include at least 3 per layout):
- Edition number stamp ("EDITION 38 / 50")
- Registration marks (✛) at card corners
- "PROOF" diagonal watermark behind hero
- Colophon at footer ("PRINTED ON RISOGRAPH MZ 1090 · MAY 2026")
- Hand-tilted check marks, slightly rotated stickers (2-3deg)

REJECT IF YOU SEE:
- box-shadow with rgba(0,0,0,...)
- background: #ffffff or #fff
- border-radius > 2px on rectangular elements
- A third saturated color beyond pink + teal
- Misregistration in random directions or symmetrical centering
- Smooth easings: ease, ease-in-out, cubic-bezier(0.4, 0, 0.2, 1)
- System fonts where Anton/Lora/JetBrains Mono should be
```

---

## Closing Note

A Risograph print is not "designed and then printed." It is *designed for the act of printing.* The mistake is built in from the start — the second pass is supposed to land 3px off. The grain is supposed to be visible. The third color is supposed to be discovered, not picked.

When you build a UI in this style, you are not building a website. You are pressing an edition. Edition number, paper stock, ink density, registration tolerance — every decision belongs to the press, not to the screen. Treat the browser as a printing surface, and the style will land.

**The mistake is the mark. The mark is the signature.**

✛ ✛ ✛
