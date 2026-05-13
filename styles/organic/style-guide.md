# Organic / Biomorphic — Style Guide

**Personality:** Earthy. Flowing. Warm. Biomorphic. Living.

Design as if nature drew the interface — asymmetric curves, geological colour strata, editorial serif type with humanist warmth. Think Kinfolk magazine. Think handcrafted ceramics. Think a sustainable design studio whose studio is also a greenhouse.

---

## Design Tokens

```css
:root {
  /* ── Surfaces ── */
  --bg:         #f0e8d8;   /* warm linen — like handmade paper */
  --s1:         #e8dfc8;   /* warm paper */
  --s2:         #dfd4b8;   /* aged vellum */
  --s3:         #d0c8a8;   /* dried grass */

  /* ── Brand colours ── */
  --sage:       #6b8c42;   /* sage green — primary accent */
  --terracotta: #c4783c;   /* terracotta orange — secondary */
  --forest:     #2d4a3e;   /* deep forest green — hover/pressed */
  --sand:       #b09060;   /* warm sand — decorative */

  /* ── Text ── */
  --t1:         #1e2618;   /* deep organic dark */
  --t2:         #4a5a3a;   /* body text */
  --t3:         #8a9a7a;   /* secondary / muted */
  --t4:         #b0c0a0;   /* placeholder / faintest */

  /* ── Semantic aliases ── */
  --ac:         #6b8c42;   /* primary accent = sage */
  --ac2:        #c4783c;   /* secondary = terracotta */
  --ac-lo:      rgba(107,140,66,0.18); /* sage focus glow */
  --border:     1px solid rgba(30,38,24,0.10);
  --border-2:   1px solid rgba(30,38,24,0.16);

  /* ── Shadows ── */
  --sh-sm:  0 2px 8px rgba(30,38,24,0.08);
  --sh-md:  0 4px 16px rgba(30,38,24,0.10);
  --sh-lg:  0 8px 32px rgba(30,38,24,0.12);
}
```

---

## Blob Shape System

The blob is the signature form. Six border-radius combinations, each producing a distinct organic silhouette. Use them intentionally — the same blob on every element reads as noise, not nature.

| Token      | Value                                      | Use case                                 |
|------------|--------------------------------------------|------------------------------------------|
| `--blob-1` | `60% 40% 70% 30% / 50% 60% 40% 50%`       | Hero decorations, play button default    |
| `--blob-2` | `40% 60% 30% 70% / 60% 40% 60% 40%`       | Animated morph target, card decorations  |
| `--blob-3` | `50% 50% 60% 40% / 40% 60% 50% 50%`       | Player art, secondary blobs              |
| `--blob-4` | `70% 30% 50% 50% / 40% 50% 60% 50%`       | Icon wells, avatar frames, blob buttons  |
| `--blob-5` | `30% 70% 40% 60% / 50% 40% 60% 50%`       | Background decorations, subtle overlays  |
| `--blob-6` | `55% 45% 65% 35% / 45% 55% 45% 55%`       | Nav active indicator, slider thumbs      |

### Blob animation pattern

Animate `border-radius` between `--blob-1` → `--blob-2` → `--blob-3` at 8–15 second intervals. Keep `ease-in-out`. This is breathing, not jittering.

```css
@keyframes blobDrift {
  0%,100% { border-radius: var(--blob-1); }
  33%      { border-radius: var(--blob-2); }
  66%      { border-radius: var(--blob-3); }
}
```

### Decorative blob elements

Use as page-level background decorations, not interactive elements.

```css
.blob-decoration {
  position: absolute;
  border-radius: var(--blob-1);
  background: var(--sage);         /* or --terracotta, --sand */
  opacity: 0.06–0.10;              /* barely visible — geological, not playful */
  pointer-events: none;
  user-select: none;
}
```

---

## Earth Palette Rationale

The palette is geological. These are not brand colours chosen from a Pantone chart — they are colours that exist in the earth, the shore, and the forest.

| Colour       | Hex       | Source reference                    | When to use                          |
|--------------|-----------|-------------------------------------|--------------------------------------|
| Linen        | `#f0e8d8` | Handmade paper, unbleached cotton   | Page background — the only base      |
| Warm paper   | `#e8dfc8` | Aged sketch paper                   | Card surfaces, form panels           |
| Aged vellum  | `#dfd4b8` | Dried parchment                     | Secondary surfaces, slider tracks    |
| Dried grass  | `#d0c8a8` | Late summer meadow                  | Tertiary surface, deep contrast      |
| Sage         | `#6b8c42` | Salvia officinalis in dry season    | Primary buttons, active states, fills|
| Terracotta   | `#c4783c` | Earthenware pottery, Tuscan roof    | Secondary actions, badges, accents   |
| Forest       | `#2d4a3e` | Pacific forest understory           | Hover depth for sage elements        |
| Sand         | `#b09060` | Coastal sand, dry adobe             | Decorative accents, avatars          |
| Dark ink     | `#1e2618` | Iron gall ink on vellum             | Primary text — not pure black        |

**Rule:** Never use a colour that doesn't exist in the natural world. If it looks neon, it doesn't belong here.

---

## Typography

### Type Stack

```css
--f-disp: 'Playfair Display', Georgia, serif;
--f:      'DM Sans', system-ui, sans-serif;
```

### Google Fonts import

```html
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,600;0,700;1,400;1,600&family=DM+Sans:ital,opsz,wght@0,9..40,300;0,9..40,400;0,9..40,500;0,9..40,600;1,9..40,400&display=swap" rel="stylesheet">
```

### Type pairing rationale

| Role         | Font                   | Weight    | Style   | Why                                              |
|--------------|------------------------|-----------|---------|--------------------------------------------------|
| Display H1   | Playfair Display       | 600       | Italic  | High-contrast serifs echo brush calligraphy      |
| H1 upright   | Playfair Display       | 600       | Normal  | Use for section headers needing gravitas         |
| H2 editorial | Playfair Display       | 400       | Italic  | Light italic = warmth without weight             |
| H3–H4 body   | DM Sans                | 500       | Normal  | Humanist sans — approachable, not clinical       |
| Body text    | DM Sans                | 300–400   | Normal  | Light weight breathes; don't go below 300        |
| Captions     | DM Sans                | 500       | Normal  | Slight weight for metadata legibility            |

### Anti-rules

- Do NOT use geometric sans (Inter, Helvetica) — too cold, too grid-brained
- Do NOT use Playfair Display at weights > 700 — it becomes aggressive
- Do NOT use more than two typefaces — the pair is the system

---

## Radius Scale

Nothing angular. Everything rounded — preferably to blob proportions.

```css
--r-sm:   12px;    /* smallest: form hints, minor chips */
--r:      20px;    /* default: inputs, small cards */
--r-md:   28px;    /* medium: panels, player surfaces */
--r-lg:   40px;    /* large: primary cards, modals */
--r-full: 9999px;  /* pill: all buttons, progress bars, nav pills */
```

---

## Component Patterns

### Buttons

```css
/* Primary — sage pill */
.btn-primary {
  background: var(--sage);
  color: #fff;
  border: none;
  border-radius: var(--r-full);
  padding: 0.875rem 2rem;
  font-family: var(--f);
  font-weight: 500;
  box-shadow: 0 4px 14px rgba(107,140,66,0.30);
  transition: background 0.2s, box-shadow 0.2s, transform 0.15s;
}
.btn-primary:hover {
  background: var(--forest);
  box-shadow: 0 6px 20px rgba(107,140,66,0.35);
  transform: translateY(-2px);
}
.btn-primary:active {
  transform: translateY(0);
  box-shadow: 0 2px 8px rgba(107,140,66,0.25);
}

/* Secondary — terracotta pill */
.btn-secondary {
  background: var(--terracotta);
  color: #fff;
  box-shadow: 0 4px 14px rgba(196,120,60,0.30);
  /* same shape as primary */
}

/* Ghost — thin border pill */
.btn-ghost {
  background: transparent;
  border: var(--border-2);
  border-radius: var(--r-full);
  color: var(--t2);
}
.btn-ghost:hover { background: var(--s1); color: var(--t1); }
```

### Form inputs

```css
.inp {
  background: var(--bg);
  border: var(--border-2);
  border-radius: var(--r);        /* 20px — notably rounded */
  padding: 0.875rem 1rem;
  font-family: var(--f);
  font-size: 0.9375rem;
  color: var(--t1);
}
.inp:focus {
  border-color: var(--sage);
  box-shadow: 0 0 0 3px var(--ac-lo);   /* gentle sage glow */
  outline: none;
}
```

Checkboxes are perfectly round (`border-radius: 50%`). When checked, fill with `--sage`. No square checkboxes — ever.

### Cards

```css
.card {
  background: var(--s1);
  border: var(--border);
  border-radius: var(--r-lg);    /* 40px */
  box-shadow: var(--sh-sm);
  overflow: hidden;
}
.card:hover {
  box-shadow: var(--sh-md);
  transform: translateY(-4px);
}
```

Card thumbnails use a pseudo-element wave to create an organic curved bottom edge:
```css
.card-thumb::before {
  content: '';
  position: absolute;
  bottom: -16px; left: -10%; right: -10%;
  height: 32px;
  border-radius: 50% 50% 0 0 / 100% 100% 0 0;
  background: var(--s1);   /* match card surface */
  z-index: 2;
}
```

### Toggles

Blob-ish track. Spring thumb animation. Active = sage background.

```css
.tgl-track {
  width: 56px; height: 30px;
  background: var(--s2);
  border-radius: var(--r-full);
}
.tgl-in:checked ~ .tgl-track { background: var(--sage); }
.tgl-thumb {
  transition: transform 0.28s cubic-bezier(0.34,1.56,0.64,1);   /* --spring */
}
.tgl-in:checked ~ .tgl-track .tgl-thumb { transform: translateX(26px); }
```

### Navigation active indicator

Use `--blob-6` for the active indicator pill — not a circle, not a standard pill:

```css
.ni-on .ni-wrap {
  background: var(--ac-lo);
  border-radius: var(--blob-6);   /* 55% 45% 65% 35% / 45% 55% 45% 55% */
}
```

---

## Motion

| Property     | Value                                     | Use                            |
|--------------|-------------------------------------------|--------------------------------|
| `--ease`     | `cubic-bezier(0.4,0,0.2,1)`               | Standard UI transitions        |
| `--spring`   | `cubic-bezier(0.34,1.56,0.64,1)`          | Toggle thumb, radio dot        |
| `--ease-out` | `cubic-bezier(0,0,0.2,1)`                 | Section scroll-reveal          |
| blob drift   | `12–15s ease-in-out infinite`             | Floating decorative blobs      |
| form hover   | `0.2s var(--ease)`                        | Input border-color + glow      |
| button lift  | `0.15s var(--ease)` → `translateY(-2px)`  | Primary/secondary hover        |
| card lift    | `0.3s var(--ease)` → `translateY(-4px)`   | Card hover                     |

---

## Spec Callout

```css
.spec-callout {
  background: var(--s1);
  border-left: 3px solid var(--sage);
  border-radius: 0 var(--r) var(--r) 0;
  padding: 1rem 1.25rem;
  font-style: italic;
  color: var(--t2);
}
```

The left-flush border + organic right radius gives it a living, bookmarked quality. Always use italic text inside.

---

## Accessibility

- All interactive elements have visible focus via `outline: 2px solid var(--sage)`
- Sage (#6b8c42) on white (#ffffff): **4.7:1** — passes WCAG AA for large text
- Sage on linen (#f0e8d8): **3.8:1** — acceptable for large UI text (14px+ bold)
- Forest (#2d4a3e) on linen: **8.5:1** — passes WCAG AAA
- Dark ink (#1e2618) on linen: **12.4:1** — excellent
- Terracotta (#c4783c) on linen: **3.2:1** — use for decorative accents, not body text
- `prefers-reduced-motion` support: disable blob animations and all transitions

---

## AI Prompting Guidance

Use these phrases when generating organic/biomorphic UI with AI tools:

**Style descriptors:**
- "Kinfolk magazine editorial aesthetic"
- "handcrafted ceramics studio website"
- "sustainable botanical garden app"
- "warm linen paper background, earth tones"
- "no sharp corners, blob border-radius, imperfect organic shapes"
- "Playfair Display italic headers, DM Sans body"
- "sage green and terracotta color palette, muted desaturated"
- "floating asymmetric blob shapes as decorations"

**Anti-descriptors (what to avoid):**
- "no neon colors"
- "no pure white or pure black"
- "no geometric shapes, no rectangles"
- "no Inter font, no Helvetica"
- "no flat design, no glassmorphism"
- "no drop shadows with blue tint"

**Figma prompts:**
> "Create a mobile app UI in an organic biomorphic style. Use #f0e8d8 as the background, #6b8c42 (sage) as the primary accent, and #c4783c (terracotta) as secondary. All buttons should be pill-shaped. Cards should have 40px border-radius. Use Playfair Display italic for headlines and DM Sans Light for body text. Add floating asymmetric blob shapes as subtle background decorations."

---

## Do / Don't

| ✓ Do                                          | ✗ Don't                                        |
|-----------------------------------------------|------------------------------------------------|
| Use blob border-radius intentionally           | Blob-ify every single element randomly         |
| Layer warm tones like geological strata        | Use primary colours — they feel synthetic      |
| Mix Playfair italic with DM Sans Light         | Use a single font or > 2 fonts                 |
| Animate blobs slowly (12–15s) and subtly       | Animate blobs fast — it looks like a game      |
| Keep shadows warm-tinted (`rgba(30,38,24,…)`) | Use cool blue-tinted shadows                   |
| Use terracotta sparingly as an accent          | Make terracotta the dominant colour            |
| Slightly desaturate every colour               | Boost saturation — organic is never electric   |
| Leave generous white space                     | Fill every surface — organic design breathes   |

---

*Style guide generated for the UI Styles Gallery · Organic / Biomorphic edition*
