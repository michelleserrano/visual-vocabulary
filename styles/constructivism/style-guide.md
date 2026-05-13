# Soviet Constructivism — Style Guide

**Personality:** Agitational. Geometric. Diagonal. Revolutionary. Typographic.

Soviet Constructivism (1920–1935) was art as political weapon. Rodchenko, El Lissitzky, Varvara Stepanova believed design had a duty: to serve the revolution, to agitate, to mobilize. There was no neutral form. Every color, every line, every typeface was a statement.

Applied to UI, Constructivism creates interfaces that demand attention. They do not suggest — they command.

---

## Design Tokens

```css
:root {
  --bg:     #f5f0e8;   /* aged paper — constructivist posters were on newsprint */
  --paper2: #ede8d8;   /* secondary surface — slightly darker newsprint */
  --t1:     #1a1a1a;   /* near-black text */
  --t2:     #3a3a3a;   /* secondary text */
  --t3:     #6a6a6a;   /* muted / caption text */
  --red:    #d42b2b;   /* revolutionary red — THE primary color */
  --black:  #1a1a1a;   /* structural black */
  --gold:   #f0c030;   /* propaganda yellow — secondary accent */
  --r:      0px;       /* ZERO radius — hard geometry, always */
  --f-disp: 'Oswald', 'Arial Black', Impact, sans-serif;
  --f:      'IBM Plex Sans', 'Helvetica Neue', sans-serif;
  --f-mono: 'IBM Plex Mono', 'Courier New', monospace;
  --ease:   cubic-bezier(0.4,0,0.2,1);
}

/* The non-negotiable reset */
*, *::before, *::after { border-radius: 0 !important; }
```

---

## Typography

```
Oswald     — Display, headings, labels, buttons, nav. Always uppercase. 500–700 weight.
IBM Plex   — Body copy, form inputs, descriptions. Sentence or lower case.
IBM Plex Mono — Timestamps, metadata, hex codes, spec values.
```

**The rule:** If it's structural or interactive → Oswald. If it's content → IBM Plex Sans.

### Type Scale

| Level    | Font         | Size   | Weight | Transform  | Tracking |
|----------|-------------|--------|--------|------------|----------|
| Display  | Oswald       | 48px   | 700    | uppercase  | 0.04em   |
| H1       | Oswald       | 36px   | 700    | uppercase  | 0.02em   |
| H2       | Oswald       | 28px   | 600    | uppercase  | 0.02em   |
| H3       | Oswald       | 22px   | 500    | uppercase  | 0.04em   |
| H4       | Oswald       | 18px   | 500    | uppercase  | 0.05em   |
| Body Lg  | IBM Plex     | 17px   | 400    | none       | —        |
| Body     | IBM Plex     | 16px   | 400    | none       | —        |
| Body Sm  | IBM Plex     | 14px   | 400    | none       | —        |
| Mono     | IBM Plex Mono| 12px   | 400    | uppercase  | 0.06em   |

---

## Color System

| Token     | Value     | Ideological Meaning                                          |
|-----------|-----------|--------------------------------------------------------------|
| `--red`   | `#d42b2b` | Revolution. Primary action. Active states. Dominant accent.  |
| `--black` | `#1a1a1a` | Structure. Secondary actions. Typography. Hard borders.      |
| `--gold`  | `#f0c030` | Victory. Tertiary accent. Use sparingly for maximum impact.  |
| `--bg`    | `#f5f0e8` | Aged paper. The default surface — evokes newsprint posters.  |
| `--paper2`| `#ede8d8` | Slightly darker newsprint. Cards, form panels, surfaces.     |

**Color as argument:** In Constructivism, red meant revolution and the working class. When you use `--red`, you are deploying the most politically charged color in 20th-century visual culture. Use it with intention — not for decoration, but for meaning.

---

## Offset Shadow System

The signature Constructivist depth technique — **no blur, pure offset**. Reads like a rubber stamp or letterpress print:

```css
/* Card — default */
box-shadow: 5px 5px 0 var(--red);

/* Card — hover (lift) */
transform: translate(-3px, -3px);
box-shadow: 8px 8px 0 var(--red);

/* Button — default */
box-shadow: 3px 3px 0 var(--black);

/* Button — hover */
transform: translate(-2px, -2px);
box-shadow: 5px 5px 0 var(--black);

/* Button — press */
transform: translate(2px, 2px);
box-shadow: 1px 1px 0 var(--black);

/* Nav/hero widget — large shadow */
box-shadow: 6px 6px 0 var(--black);
```

**Why it works:** The zero-blur shadow creates the illusion of a physical object lifted off the paper surface. Combined with the aged paper background, it evokes letterpress printing — the exact medium Constructivists used for their posters.

---

## Diagonal Bar System

Diagonal bars are the **primary decorative element**. They create dynamic tension and reference the political energy of Constructivist posters — nothing is static, everything is in motion.

```css
.c-diag {
  position: absolute;
  width: 120px;
  height: 4px;
  background: var(--red);
  transform: rotate(-38deg);    /* -38deg is the canonical Constructivist angle */
  transform-origin: left center;
  pointer-events: none;
}
```

**Usage rules:**
- Place at least one diagonal bar per major section
- Never perfectly horizontal or vertical
- Authentic range: -35deg to -42deg
- Stack two bars at slightly offset positions for density
- Vary `width` (80px–200px) and `height` (3px–5px) to create visual rhythm

---

## Borders & Structure

```css
/* Zero radius — always enforced */
*, *::before, *::after { border-radius: 0 !important; }

/* Primary structural border */
border: 2px solid var(--black);

/* Red accent left border — section headings, form inputs */
border-left: 5px solid var(--red);   /* section headings */
border-left: 3px solid var(--red);   /* form inputs */
border-left: 4px solid var(--red);   /* nav titles */

/* Sticky nav bottom border */
border-bottom: 4px solid var(--black);

/* Left stripe — constructivist page signature */
/* 8px wide vertical red stripe on left edge of nav + page */
```

---

## Button Recipe

```css
.btn {
  font-family: 'Oswald', sans-serif;
  font-size: 0.9375rem;
  font-weight: 700;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  padding: 0.875rem 2.5rem;
  border: none;
  cursor: pointer;
  transition: transform 0.12s ease, box-shadow 0.12s ease;
}

/* Primary — Revolutionary Red */
.btn-primary {
  background: #d42b2b;
  color: #fff;
  box-shadow: 3px 3px 0 #1a1a1a;
}
.btn-primary:hover  { transform: translate(-2px,-2px); box-shadow: 5px 5px 0 #1a1a1a; }
.btn-primary:active { transform: translate(2px,2px);  box-shadow: 1px 1px 0 #1a1a1a; }

/* Secondary — Structural Black */
.btn-secondary {
  background: #1a1a1a;
  color: #fff;
  box-shadow: 3px 3px 0 #d42b2b;
}
.btn-secondary:hover  { transform: translate(-2px,-2px); box-shadow: 5px 5px 0 #d42b2b; }
.btn-secondary:active { transform: translate(2px,2px);  box-shadow: 1px 1px 0 #d42b2b; }

/* Yellow — Victory */
.btn-gold {
  background: #f0c030;
  color: #1a1a1a;
  box-shadow: 3px 3px 0 #1a1a1a;
}
```

---

## Form Input Recipe

```css
.inp {
  background: var(--paper2);
  border: none;
  border-bottom: 2px solid var(--black);
  border-left: 3px solid var(--red);
  padding: 0.75rem 1rem;
  font-family: 'IBM Plex Sans', sans-serif;
  font-size: 0.9375rem;
  color: var(--t1);
  outline: none;
  width: 100%;
  transition: border-bottom-color 0.15s;
}
.inp:focus { border-bottom-color: var(--red); }

/* Labels */
.label {
  font-family: 'Oswald', sans-serif;
  font-size: 0.75rem;
  font-weight: 500;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: var(--t2);
}

/* Checkboxes — square, red fill when checked */
.chk-box {
  width: 20px; height: 20px;
  background: var(--bg);
  border: 2px solid var(--black);
}
input:checked + .chk-box { background: var(--red); border-color: var(--red); }

/* Toggles — rectangular, NO round ends */
.tgl-track {
  width: 48px; height: 24px;
  background: var(--t3);
  border: 2px solid var(--black);
}
.tgl-thumb {
  width: 16px; height: 16px;
  background: var(--black);  /* square thumb */
}
input:checked ~ .tgl-track { background: var(--red); }
input:checked ~ .tgl-track .tgl-thumb { transform: translateX(24px); background: #fff; }
```

---

## Card Recipe

```css
.card {
  background: var(--paper2);
  border: 2px solid var(--black);
  box-shadow: 5px 5px 0 var(--red);
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}
.card:hover {
  transform: translate(-3px, -3px);
  box-shadow: 8px 8px 0 var(--red);
}

/* Red header strip — always */
.card-header-strip {
  background: var(--red);
  padding: 0.5rem 1rem;
  font-family: 'Oswald', sans-serif;
  font-size: 0.625rem;
  font-weight: 700;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: #fff;
}

/* Card thumbnail — geometric SVG composition in black, red, gold */
/* No photos. No icons. Only geometry. */
```

---

## Spec Callout

```css
.spec-callout {
  background: var(--paper2);
  border-left: 5px solid var(--red);
  padding: 1rem 1.25rem;
}
.spec-callout-text {
  font-family: 'IBM Plex Sans', sans-serif;
  font-size: 0.875rem;
  line-height: 1.65;
  color: var(--t2);
  font-style: italic;
}
```

---

## Section Heading Pattern

```css
.sec-title {
  font-family: 'Oswald', sans-serif;
  font-size: 1.375rem;
  font-weight: 700;
  letter-spacing: 0.06em;
  text-transform: uppercase;
  color: var(--t1);
  border-left: 5px solid var(--red);
  padding-left: 0.75rem;
}
/* Diagonal red underline bar */
.sec-title::after {
  content: '';
  display: block;
  width: 60px; height: 3px;
  background: var(--red);
  margin-top: 5px;
  transform: rotate(-3deg);
  transform-origin: left center;
}
```

---

## Historical Context

**Key figures:**
- **Alexander Rodchenko** (1891–1956) — Photography, advertising, photomontage. Defined Soviet graphic design.
- **El Lissitzky** (1890–1941) — "Beat the Whites with the Red Wedge" (1920). Architecture, typography, exhibition design.
- **Varvara Stepanova** (1894–1958) — Textile design, theater design, sports clothing.
- **Gustav Klutsis** (1895–1938) — Photomontage, political poster design.

**Key institutions:**
- **Vkhutemas** (1920–1930) — Soviet state art school. The Bauhaus of Constructivism. Produced the core generation of Constructivist designers.
- **LEF** (1923–1929) — Left Front of the Arts. The theoretical journal that defined Constructivist ideology.
- **Proletkult** (1917–1932) — Proletarian cultural organization. Mass audience, agitational design.

**Key works:**
- "Beat the Whites with the Red Wedge" — El Lissitzky, 1920
- "Books" advertisement poster — Rodchenko, 1924
- "The USSR in Construction" magazine — various, 1930–1941
- "Cinema" poster — Rodchenko, 1925

---

## Anti-Patterns

Do NOT do any of the following in Constructivist UI:

| Forbidden | Why |
|-----------|-----|
| Border radius of any kind | Softness is ideologically passive |
| Rounded toggles or pill buttons | Geometry must be hard |
| Gradient backgrounds | The paper is flat and aged |
| Blur-based drop shadows | Only hard offsets — letterpress, not digital |
| Centered, symmetrical layouts | Use diagonal energy and asymmetry |
| Decorative illustrations | Only geometric SVG compositions |
| Rounded fonts (e.g. Nunito) | Use condensed/geometric forms only |
| Lowercase labels and buttons | Uppercase is the collective voice |
| Pastel colors | Only red, black, gold, and aged paper |

---

## AI Prompting Guide

When asking an AI to generate in Soviet Constructivist style:

```
Generate a [UI component] in Soviet Constructivist style (1920s Russian avant-garde):
- Background: aged paper (#f5f0e8), secondary surface (#ede8d8)
- Primary color: revolutionary red (#d42b2b)
- Secondary: structural black (#1a1a1a), gold accent (#f0c030)
- Typography: Oswald (condensed, uppercase, bold) for all labels and headings
- Body text: IBM Plex Sans
- Border radius: ZERO — hard edges everywhere, no exceptions
- Depth: hard offset shadows (e.g. 5px 5px 0 #d42b2b) — no blur
- Decoration: diagonal red bars at -38deg rotation
- Energy: asymmetric, nothing centered gratuitously
- Card art: overlapping geometric shapes (circles, rectangles) in red/black/gold SVG
- Feel: El Lissitzky's "Beat the Whites" if it were a web page
```

**Power phrases:**
- "Hard geometry, zero radius"
- "Agitational typography — uppercase, condensed, demanded"
- "Offset shadow creates physical presence"
- "Diagonal as structural element, not decoration"
- "Red as argument, not accent"
