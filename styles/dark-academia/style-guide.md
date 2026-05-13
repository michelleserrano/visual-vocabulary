# Dark Academia — Style Guide

> *"The scholar's candlelit study, made digital. Oxford paneling, parchment, tarnished gold, and the warmth of a candle that never goes out."*

**Personality:** Scholarly · Candlelit · Aged · Literary · Oxford

---

## I. Aesthetic Identity

Dark Academia is not a dark *theme*. It is a dark *world* — the world of old universities, dusty bookshelves, ink and parchment. Its reference is not a screen; it is a room. That room is an Oxford library in 1890: oak paneling, leather-bound volumes, a brass lamp burning amber on a mahogany desk.

**The three material anchors:**
- **Dark oak** — the panels, the shelves, the desk itself
- **Parchment** — the page you read and write on
- **Tarnished gold** — candlelight, gilt lettering on spines, worn hardware

Every design decision should be traceable to one of these three materials.

---

## II. Design Tokens

```css
:root {
  /* Backgrounds — oak gradients */
  --bg:        #1a1208;   /* dark oak — Oxford library paneling */
  --s1:        #211808;   /* mahogany */
  --s2:        #2a200e;   /* aged walnut */
  --s3:        #342c1a;   /* old leather */
  --s4:        #3d3020;   /* worn cloth binding */

  /* Ink & parchment */
  --parchment: #d4b896;   /* aged parchment — primary text */
  --gold:      #c8a84b;   /* tarnished gold — accent */
  --amber:     #e8a832;   /* candlelight amber — hover/active warmth */
  --rust:      #8b3a1a;   /* old ink — wax seal, error states */

  /* Text opacity scale */
  --t1:        #d4b896;                    /* full parchment */
  --t2:        rgba(212,184,150,0.65);     /* muted */
  --t3:        rgba(212,184,150,0.35);     /* faint — marginalia */
  --t4:        rgba(212,184,150,0.18);     /* ghost — placeholders */

  /* Accent system */
  --ac:        #c8a84b;
  --ac-lo:     rgba(200,168,75,0.15);

  /* Borders — always gold-tinted */
  --border:    1px solid rgba(200,168,75,0.15);
  --border-hi: 1px solid rgba(200,168,75,0.3);

  /* Radius — very slight; aged, not clinical */
  --r:         4px;
  --r-sm:      2px;
  --r-full:    9999px;

  /* Typography */
  --f-disp:    'Cormorant Garamond', Garamond, Georgia, serif;
  --f-body:    'EB Garamond', Garamond, Georgia, serif;
  --f-small:   'Libre Baskerville', Georgia, serif;

  /* Easing */
  --ease:      cubic-bezier(0.4,0,0.2,1);
  --spring:    cubic-bezier(0.34,1.56,0.64,1);

  /* Candlelight glow — for hover states */
  --glow-amber: 0 0 16px rgba(232,168,50,0.2), 0 0 4px rgba(232,168,50,0.3);

  /* Book shadows — deep and warm */
  --sh-book:   0 2px 8px rgba(0,0,0,0.5), 0 1px 2px rgba(0,0,0,0.4);
  --sh-deep:   0 8px 32px rgba(0,0,0,0.6), 0 2px 8px rgba(0,0,0,0.4);
}
```

---

## III. Typography System

### The Garamond Pair

Dark Academia uses two companion Garamond interpretations:

| Role | Typeface | Weight | Style | Use |
|------|----------|--------|-------|-----|
| Display | Cormorant Garamond | 600–700 | Italic | H1, hero, card titles |
| Heading | Cormorant Garamond | 500–600 | Roman | H2–H4 |
| Body | EB Garamond | 400 | Roman + Italic | All prose |
| Body italic | EB Garamond | 400 | Italic | Placeholders, captions, marginalia |
| Label | Libre Baskerville | 700 | Roman UC | Form labels, eyebrows, small caps |

### Scale

```css
.ts-disp  { font: 700 italic 3rem/1.1 var(--f-disp); }       /* 48px */
.ts-h1    { font: 600 italic 2.25rem/1.15 var(--f-disp); }   /* 36px */
.ts-h2    { font: 600 1.75rem/1.2 var(--f-disp); }           /* 28px */
.ts-h3    { font: 500 italic 1.375rem/1.3 var(--f-disp); }   /* 22px */
.ts-body  { font: 400 1rem/1.75 var(--f-body); }             /* 16px */
.ts-label { font: 700 0.5625rem/1.4 var(--f-small); letter-spacing: 0.1em; text-transform: uppercase; }
```

**Rules:**
- Never use EB Garamond at weights above 600 in UI contexts
- Always italic for display headings — Roman Cormorant reads as headlines, not academia
- Line-height 1.75–1.85 for body text — the reader needs air
- Labels: Libre Baskerville 700, 9–10px, uppercase, +0.1em tracking only

---

## IV. The Candlelight Glow System

The candlelight is the soul of this aesthetic. It must pervade — not overpower.

### Animation

```css
@keyframes flicker {
  0%, 100% { opacity: 0.85; text-shadow: 0 0 6px rgba(232,168,50,0.3); }
  33%       { opacity: 1;    text-shadow: 0 0 12px rgba(232,168,50,0.5); }
  66%       { opacity: 0.9;  text-shadow: 0 0 8px rgba(232,168,50,0.35); }
}

/* Apply to accent text on hover — subtly */
.candlelit:hover {
  animation: flicker 2s ease-in-out infinite;
}
```

### Box-shadow Glow (for interactive elements)

```css
/* Primary button hover, active player controls */
--glow-amber: 0 0 16px rgba(232,168,50,0.2), 0 0 4px rgba(232,168,50,0.3);

/* Pulsing candlelight on focused elements */
@keyframes candle-pulse {
  0%, 100% { box-shadow: var(--glow-amber); }
  50%       { box-shadow: 0 0 24px rgba(232,168,50,0.35), 0 0 8px rgba(232,168,50,0.5); }
}
```

**Rule:** The glow should feel like reflected candlelight, not a neon sign. Keep opacity values ≤ 0.35. If it reads as "glow effect," dim it by half.

---

## V. Academic Marginalia

The marginalia system adds scholarly character to specifications and annotations.

```css
.marginalia {
  font-family: var(--f-body);
  font-style: italic;
  font-size: 0.8125rem;
  color: var(--t3);
  border-left: 1px solid rgba(200,168,75,0.15);
  padding-left: 0.875rem;
  margin-left: 1.5rem;
  margin-top: 0.75rem;
  line-height: 1.6;
}
```

Use for:
- Secondary descriptions on form fields
- Aside notes in spec callouts
- Citation references in interface copy

---

## VI. Spec Callout (Scholarly Footnote)

```css
.spec-callout {
  background: var(--s2);
  border: var(--border);
  border-left: 2px solid var(--gold);
  border-radius: var(--r);
  padding: 1rem 1.25rem 1rem 1.5rem;
  position: relative;
}
/* Footnote label — e.g. "¹ Nota bene" */
.spec-callout::before {
  content: attr(data-fn);
  position: absolute;
  top: -0.6rem; left: 1.25rem;
  font-family: var(--f-disp);
  font-size: 0.75rem;
  font-style: italic;
  color: var(--gold);
  background: var(--s2);
  padding: 0 0.25rem;
  opacity: 0.8;
}
```

Usage: `<div class="spec-callout" data-fn="¹ Nota bene">`

---

## VII. Wax Seal Component

Use as section header decoration, badge, or crest mark.

```css
.wax-seal {
  width: 28px;
  height: 28px;
  background: var(--rust);           /* old wax — #8b3a1a */
  border-radius: 50%;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  font-size: 0.6875rem;
  color: var(--parchment);
  box-shadow: 0 2px 6px rgba(0,0,0,0.5), inset 0 1px 0 rgba(255,255,255,0.08);
}
```

---

## VIII. Interaction States

### Buttons

| Variant | Default | Hover | Active |
|---------|---------|-------|--------|
| Primary | `bg: rgba(200,168,75,0.1)` · gold border | `bg: rgba(200,168,75,0.18)` · amber glow | `bg: rgba(200,168,75,0.25)` |
| Secondary | `bg: transparent` · subtle border | `border-color: rgba(200,168,75,0.4)` · gold text | opacity 0.8 |
| Dark | `bg: var(--s3)` · subtle border | `bg: var(--s4)` · slightly higher border | opacity 0.8 |

### Form Inputs (the writing desk)

```css
.inp {
  background: transparent;
  border: none;
  border-bottom: 1px solid rgba(200,168,75,0.2);  /* the desk surface */
  color: var(--t1);
  font-family: var(--f-body);
  font-style: italic;   /* the pen writes in italic */
  font-size: 1rem;
  padding: 0.625rem 0;
}
.inp:focus {
  border-color: var(--gold);
  box-shadow: 0 1px 0 rgba(200,168,75,0.4);   /* candlelight on the line */
  outline: none;
}
.inp::placeholder { color: var(--t4); font-style: italic; }
```

### Toggles (rectangular, scholarly)

```css
.tgl-track {
  width: 44px; height: 22px;
  background: var(--s3);
  border: var(--border);
  border-radius: var(--r);  /* rectangular, not pill */
}
/* Active state */
.tgl-in:checked ~ .tgl-track {
  border-color: rgba(200,168,75,0.4);
  background: rgba(200,168,75,0.1);
  box-shadow: 0 0 8px rgba(200,168,75,0.15);
}
```

---

## IX. Cards (Book Covers)

Each card is a scholarly volume: dark cloth binding, gold lettering on the cover, deep shadow.

```css
.card {
  background: var(--s1);
  border: var(--border);
  border-radius: var(--r);
  box-shadow: var(--sh-book);
  transition: box-shadow 0.3s, border-color 0.3s;
}
.card:hover {
  box-shadow: var(--sh-deep), 0 0 0 1px rgba(200,168,75,0.15);
  border-color: rgba(200,168,75,0.25);
}
/* Cover thumbnail */
.card-cover {
  background: linear-gradient(145deg, #1e1408, #2d1e0a, #1a1208);
  /* Use different dark palettes for variety — no warm colours */
}
```

---

## X. Latin Kicker Library

Use these as section eyebrows and decorative headers:

| Latin | Meaning | Use |
|-------|---------|-----|
| `De Typographia` | On typography | Typography sections |
| `De Coloribus Pulchritudinem` | On the beauty of colours | Colour sections |
| `De Arte Designandi` | On the art of designing | General design |
| `De Voluminibus` | On volumes / books | Cards, catalogue sections |
| `De Scriptura` | On writing | Form sections |
| `De Actionibus` | On actions | Button sections |
| `De Navigatione` | On navigation | Nav sections |
| `In Tenebris Lucet` | It shines in darkness | Dark/contrast emphasis |
| `Per Vitruvius` | According to Vitruvius | Architecture/structure |
| `Ex Libris` | From the library | Cards, book-related |
| `Nota Bene` | Note well | Callouts, important notes |
| `Quod Erat Faciendum` | Which was to be done | Completed states |

**Format:** `SMALL-CAPS LABEL · Roman Numeral`
Example: `DE TYPOGRAPHIA · II`

---

## XI. Drop Cap (Hero Prose)

```css
.hero-desc::first-letter {
  font-family: var(--f-disp);
  font-size: 3.25em;
  font-weight: 600;
  float: left;
  line-height: 0.75;
  margin-right: 0.1em;
  margin-top: 0.1em;
  color: var(--gold);
}
```

Use on hero body text, long-form reading, and introductory paragraphs.

---

## XII. Background Texture

The body carries a subtle noise texture to evoke aged paper:

```css
body {
  background: var(--bg);
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='300' height='300'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.75' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='300' height='300' filter='url(%23n)' opacity='0.025'/%3E%3C/svg%3E");
}
```

Keep opacity ≤ 0.025. This is subliminal texture — not pattern.

---

## XIII. Section Gold Rule

```css
.sec-hd::after {
  content: '';
  display: block;
  width: 100%;
  height: 1px;
  background: linear-gradient(to right,
    rgba(200,168,75,0.3)   0%,
    rgba(200,168,75,0.08) 60%,
    transparent           100%
  );
}
```

Always left-to-right fade. Never a symmetrical rule — the light source is at the left.

---

## XIV. Google Fonts Import

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,500;0,600;0,700;1,300;1,400;1,600&family=EB+Garamond:ital,wght@0,400;0,500;0,600;0,700;1,400;1,600&family=Libre+Baskerville:ital,wght@0,400;0,700;1,400&display=swap" rel="stylesheet">
```

---

## XV. AI Prompting Guidance

Use these phrases when generating or evaluating Dark Academia UI:

**To generate:**
> "Dark Academia aesthetic. Oxford library in 1890. Dark oak background #1a1208. Tarnished gold accents #c8a84b. Parchment text #d4b896. Cormorant Garamond italic for headings, EB Garamond for body. Candlelight amber glow on hover states. Gold borders — never fills. Latin kicker labels. No cold colours anywhere."

**To check work:**
> "Does this feel like a scholar's study or a tech product? Is every tone warm? Does the typography feel like an old book? Is the gold tarnished or clean? If it looks modern, it's wrong."

**Anti-patterns to avoid:**
- Pure black backgrounds — always warm, never neutral
- Sans-serif typefaces — this is a Garamond-only world
- Blue, green, or neutral accent colours — only gold and amber
- Sharp square borders with no warmth
- High contrast without warmth (WCAG AA is required but must use warm neutrals)
- "Glow" effects at high opacity — amber glow must be whisper-level
- Pill-shaped buttons or toggles — keep them rectangular (var(--r) = 4px)

---

## XVI. Contrast & Accessibility

| Pairing | Ratio | WCAG |
|---------|-------|------|
| `--parchment` on `--bg` (#d4b896 / #1a1208) | ~9.8:1 | AAA |
| `--t2` on `--bg` | ~6.1:1 | AA |
| `--gold` on `--bg` (#c8a84b / #1a1208) | ~5.2:1 | AA |
| `--t3` on `--bg` | ~3.1:1 | AA Large |

**Rule:** All body text uses `--t1` (parchment) — always AAA. Labels and annotations use `--t2` — always AA. Ghost text and placeholders (`--t3`, `--t4`) are decorative only and must never carry essential information.

---

*Est. MDCCCXCV · In tenebris lucet*
