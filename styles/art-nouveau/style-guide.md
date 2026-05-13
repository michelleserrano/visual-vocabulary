# Art Nouveau — UI Style Guide

**Personality:** Botanical. Sinuous. Ornamental. 1900. Warm.

**Lineage:** Alphonse Mucha's lithographs · Gustav Klimt's gold leaf · Antoni Gaudí's organic stone · Paris and Vienna, 1890–1910.

---

## Design Tokens

```css
:root {
  /* Backgrounds — deep forest, warm not cold */
  --bg:        #1a3a1a;   /* base: deep forest green */
  --s1:        #1e4220;   /* surface raised 1 */
  --s2:        #234825;   /* surface raised 2 */
  --s3:        #2a5530;   /* surface raised 3 */

  /* Type */
  --parchment: #f0e8d0;   /* aged paper — primary text */
  --t1:        #f0e8d0;
  --t2:        rgba(240,232,208,0.65);
  --t3:        rgba(240,232,208,0.38);
  --t4:        rgba(240,232,208,0.18);

  /* Gold — Mucha's gold, matte and earthy */
  --gold:      #c8a84b;
  --gold-hi:   #e8c870;   /* hover state */
  --gold-lo:   rgba(200,168,75,0.2);   /* tinted fills */

  /* Accent palette */
  --peacock:   #006060;   /* peacock teal */
  --rose:      #8b1a3a;   /* deep rose */

  /* Borders */
  --border:    1px solid rgba(200,168,75,0.2);
  --border-hi: 1px solid rgba(200,168,75,0.45);

  /* Radius — organic curves, NOT blobs, NOT right angles */
  --r-sm:   6px;
  --r:      16px;
  --r-md:   24px;
  --r-lg:   40px;
  --r-full: 9999px;

  /* Typography */
  --f-disp:  'Cinzel Decorative', 'Trajan Pro', Georgia, serif;
  --f-body:  'IM Fell English', 'Palatino Linotype', Georgia, serif;
  --f-small: 'Cormorant Garamond', Georgia, serif;

  /* Motion */
  --ease:   cubic-bezier(0.4, 0, 0.2, 1);
  --spring: cubic-bezier(0.34, 1.56, 0.64, 1);

  /* Glow — warm gold candlelight, never electric blue */
  --glow-gold: 0 0 12px rgba(200,168,75,0.3), 0 0 4px rgba(200,168,75,0.45);
}
```

---

## Typeface Pair

| Role | Font | Weight | Style | Use |
|------|------|--------|-------|-----|
| Display / H1–H2 | Cinzel Decorative | 900 / 700 / 400 | Normal | Titles, nav, buttons, labels |
| Body / H3 | IM Fell English | 400 | Italic preferred | Body copy, spec text, descriptions |
| Supporting | Cormorant Garamond | 300–600 | Italic for labels | Form labels, captions, metadata |
| Code / Mono | Courier New | — | — | Token values, timestamps |

**Google Fonts import:**
```html
<link href="https://fonts.googleapis.com/css2?family=Cinzel+Decorative:wght@400;700;900&family=IM+Fell+English:ital@0;1&family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;1,300;1,400;1,600&display=swap" rel="stylesheet">
```

**Why this pair works:**  
Cinzel Decorative is Roman capitals ornamented — the inscribed stone of the classical tradition remixed for the decorative age. IM Fell English italic recalls the 17th-century manuscript — warm, slightly irregular, humanist. Together they are the typography of a Mucha calendar.

---

## Botanical Character Library

These characters are structural punctuation, not emoji. Use them as section ornaments, button prefixes, dividers, and progress markers.

| Character | Name | Use |
|-----------|------|-----|
| `❧` | Aldus leaf / Hedera | Section openers, back links, kickers |
| `✿` | Botanical blossom | Checkboxes, progress dots (active), decorative bullets |
| `❦` | Floral heart | Card ornaments, quotes |
| `✦` | Star / gem | Hero panels, accent ornaments |
| `◆` | Diamond | Progress dots (inactive), list markers |
| `❋` | Six-pointed star | Form ornament, callout icons |
| `✾` | Six-petal flower | Alternate callout, section sub-ornament |
| `◉` | Bullseye | Spec callout icon |
| `❁` | Eight-petal | Rare accent |

**Usage rules:**
- Max 2 ornament characters per visible screen area.
- Always `color: var(--gold)` and `opacity: 0.6–0.85`.
- Never use as interactive affordance without a text label.
- Botanical dividers: `color: var(--gold); letter-spacing: 0.5em; opacity: 0.35;`

---

## Organic Corner System

The alternating corner radius is the Art Nouveau shape signature. Never use uniform rounded corners — that is Material Design, not Art Nouveau.

```css
/* Primary organic card shape — the Mucha frame */
.card-an {
  border-radius: 12px 4px 12px 4px;
}

/* Alternate — more pronounced */
.card-alt {
  border-radius: 4px 16px 4px 16px;
}

/* Form panels — wider asymmetry */
.form-panel {
  border-radius: 4px 16px 4px 16px;
}

/* Swatches — subtle organic */
.swatch {
  border-radius: 8px 2px 8px 2px;
}

/* Large panels */
.player {
  border-radius: 4px 20px 4px 20px;
}

/* Buttons — always pill */
.btn {
  border-radius: var(--r-full);  /* 9999px — organic pill */
}
```

**The rule:** Opposite corners share the same radius. Top-left = bottom-right. Top-right = bottom-left. The shape breathes.

---

## Mucha Palette Rationale

| Token | Hex | Why |
|-------|-----|-----|
| `--bg: #1a3a1a` | Deep forest | Mucha's posters often used deep botanical backgrounds — moss, forest shadow. Warm, not cold. Never pure black. |
| `--gold: #c8a84b` | Matte gold | Klimt's gold is not chrome — it is the gold of illuminated manuscripts, slightly warm and earthy. Not `#FFD700` (too bright). Not `#B8860B` (too brown). |
| `--parchment: #f0e8d0` | Aged paper | Mucha's lithographs were printed on cream stock. Pure white (`#FFFFFF`) would be too harsh against the forest green. |
| `--peacock: #006060` | Peacock feather | The peacock is one of Art Nouveau's primary motifs (see: Whistler's Peacock Room). The teal is deep and saturated, not pastel. |
| `--rose: #8b1a3a` | Deep rose | Mucha's palette included deep rose-mauve for his female figures. Used sparingly as a tertiary accent. |

**What the palette is NOT:**
- Not neon (no `#00FF00` greens)
- Not pastel (no baby blue, powder pink)
- Not monochrome (always use the full botanical range)
- Not primary RGB

---

## Gold Glow

The glow in Art Nouveau is warm candlelight, not electric:

```css
--glow-gold: 0 0 12px rgba(200,168,75,0.3), 0 0 4px rgba(200,168,75,0.45);
```

Apply on:
- Active progress dots
- Primary button hover
- Focused input bottom border
- Player play button hover
- Card hover

Never use blue, purple, or white glow — those belong to cyberpunk and glassmorphism.

---

## Button System

```css
/* Primary — Mucha gold pill */
.btn-p {
  background: var(--gold);
  color: var(--bg);
  border-radius: var(--r-full);
  font-family: var(--f-disp);
  font-size: 0.8125rem;
  letter-spacing: 0.1em;
  box-shadow: 0 4px 16px rgba(200,168,75,0.3);
}
.btn-p:hover {
  background: var(--gold-hi);
  box-shadow: var(--glow-gold), 0 4px 20px rgba(200,168,75,0.35);
  transform: translateY(-2px);
}

/* Peacock secondary */
.btn-pk { background: var(--peacock); color: var(--parchment); }

/* Ghost */
.btn-ghost {
  border: 1px solid rgba(200,168,75,0.3);
  color: var(--t2);
  background: transparent;
}
.btn-ghost:hover {
  border-color: rgba(200,168,75,0.6);
  color: var(--gold);
  background: var(--gold-lo);
}
```

---

## Form Input System

```css
/* Bottom-line underbar — an invitation card */
.inp {
  background: rgba(240,232,208,0.06);
  border: none;
  border-bottom: 1px solid rgba(200,168,75,0.25);
  border-radius: var(--r-sm) var(--r-sm) 0 0;
  font-family: var(--f-body);
  color: var(--t1);
}
.inp:focus {
  border-color: var(--gold);
  box-shadow: 0 2px 0 var(--gold);
  background: rgba(240,232,208,0.09);
}

/* Labels — always italic Cormorant in gold */
.label {
  font-family: 'Cormorant Garamond', serif;
  font-style: italic;
  color: var(--gold);
  font-size: 0.8125rem;
  letter-spacing: 0.05em;
}
```

---

## Card Pattern

```css
.card-an {
  background: var(--s1);
  border: var(--border);          /* 1px solid rgba(200,168,75,0.2) */
  border-radius: 12px 4px 12px 4px;
  transition: border-color 0.3s, box-shadow 0.3s;
}
.card-an:hover {
  border-color: rgba(200,168,75,0.55);
  box-shadow: 0 8px 24px rgba(0,0,0,0.4), var(--glow-gold);
}

/* Decorative line under card image area */
.card-thumb::after {
  content: '';
  position: absolute; bottom: 0; left: 0; right: 0;
  height: 1px;
  background: linear-gradient(to right,
    transparent, rgba(200,168,75,0.5) 30%,
    rgba(200,168,75,0.8) 50%,
    rgba(200,168,75,0.5) 70%, transparent
  );
}
```

---

## Section Header Pattern

```css
/* Gold botanical ornament before heading */
.sec-hd {
  border-bottom: 1px solid rgba(200,168,75,0.18);
  padding-bottom: 1.25rem;
}

/* Circular section number */
.sec-pill {
  width: 28px; height: 28px;
  border-radius: 50%;
  border: 1px solid rgba(200,168,75,0.35);
  color: var(--gold);
  font-family: var(--f-disp);
  font-size: 0.5rem;
}

/* Ghost section number — almost invisible */
.sec-ghost {
  font-family: var(--f-disp);
  font-size: 7rem;
  color: rgba(200,168,75,0.04);   /* 4% opacity — barely there */
  pointer-events: none;
}
```

---

## Vine Decoration Pattern

```css
/* Left vine line on sections */
.sec::before {
  content: '';
  position: absolute;
  left: -1.75rem;
  top: 0; bottom: 0;
  width: 1px;
  background: linear-gradient(
    to bottom,
    transparent,
    rgba(200,168,75,0.15) 20%,
    rgba(200,168,75,0.15) 80%,
    transparent
  );
}

/* Gold gradient underline after H1 */
.hero-h1::after {
  content: '';
  display: block;
  width: 120px;
  height: 2px;
  background: linear-gradient(to right, var(--gold), transparent);
  margin-top: 1rem;
}
```

---

## AI Prompting Guidance

When prompting an AI to generate in Art Nouveau style, use these phrases:

**For visual design:**
> "Art Nouveau, Alphonse Mucha poster aesthetic, deep forest green background (#1a3a1a), matte gold ornaments (#c8a84b), aged parchment text (#f0e8d0), sinuous botanical curves, no hard right angles, organic alternating corner radius, Cinzel Decorative for titles, IM Fell English italic for body text, peacock teal (#006060) accent, warm candlelight glow on gold elements"

**For UI components:**
> "Art Nouveau UI component: forest green (#1a3a1a) background, gold border (rgba(200,168,75,0.2)), organic border-radius alternating 12px/4px, Cinzel Decorative font, gold bottom-line inputs not boxed, pill buttons in Mucha gold, botanical characters (❧ ✿ ❦) as ornaments, no drop shadows — only warm gold glow"

**Anti-patterns to forbid in prompts:**
- ~~"neon colors"~~ → use earthy gold
- ~~"sharp corners"~~ → use organic alternating radius
- ~~"white background"~~ → use deep forest (#1a3a1a)
- ~~"blue accent"~~ → use peacock teal or gold only
- ~~"sans-serif font"~~ → always serif (Cinzel / IM Fell)
- ~~"drop shadows with black"~~ → use warm gold glow only
- ~~"material icons"~~ → use botanical ornament characters

---

## Reference Works

| Artist | Work | Visual Element |
|--------|------|----------------|
| Alphonse Mucha | Les Saisons (1896) | Decorative halos, botanical borders, parchment ground |
| Alphonse Mucha | Job cigarette poster (1896) | Sinuous hair/vine, gold hair ornament |
| Gustav Klimt | The Kiss (1907–08) | Gold geometric ornament on organic figure |
| Gustav Klimt | Portrait of Adele Bloch-Bauer I (1907) | Gold filling negative space |
| Antoni Gaudí | Sagrada Família (1882–) | Stone as organic growth, branching columns |
| Antoni Gaudí | Casa Batlló (1904–06) | Undulating facade, no straight line |
| Hector Guimard | Paris Metro entrances (1900) | Cast iron as vine, organic lettering |
| Émile Gallé | Glass vases | Botanical forms pressed into material |

---

## The Four Rules of Art Nouveau UI

1. **The line curves.** If you catch yourself drawing a right angle — stop. Find the botanical equivalent.
2. **Gold is a line, not a fill.** Use gold as border, underline, ornament. Not as the background of large surfaces.
3. **Nature provides the metaphor.** A card is a picture frame. A button is a medallion. A form is an invitation card.
4. **Ornament is structure.** The botanical character `❧` is not decoration — it is punctuation. The alternating corner radius is not a quirk — it is the signature.
