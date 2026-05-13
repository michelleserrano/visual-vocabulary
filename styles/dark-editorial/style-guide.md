# Dark Editorial — Style Guide

**Personality:** Premium. Typographic. Sparse. Nocturnal. Confident.

> *The New Yorker at midnight. T Magazine on a screen. Vogue without the noise.*

---

## Identity

Dark Editorial is a luxury interface language. It takes the visual intelligence of prestige print journalism — considered typography, aggressive whitespace, ink-on-paper restraint — and renders it in a true dark environment. Not a dark *mode*. A dark *first* design.

The aesthetic is nocturnal by nature. Every decision serves legibility and confidence, not trend.

---

## Design Tokens

```css
:root {
  /* Surfaces — true black, not dark gray */
  --bg:       #0a0a0a;
  --s1:       #111111;
  --s2:       #181818;
  --s3:       #1e1e1e;

  /* Text — warm off-white, not pure white */
  --t1:       #f0f0ee;                      /* primary */
  --t2:       rgba(240,240,238,0.65);       /* secondary */
  --t3:       rgba(240,240,238,0.35);       /* muted */
  --t4:       rgba(240,240,238,0.18);       /* placeholder */

  /* Gold — editorial punctuation */
  --gold:     #d4af37;
  --gold-lo:  rgba(212,175,55,0.15);

  /* Mid */
  --mid:      #888888;

  /* Borders — hairline, almost invisible */
  --border:   1px solid rgba(240,240,238,0.07);
  --border-hi:1px solid rgba(240,240,238,0.15);

  /* Radius — none or minimal */
  --r:        0px;
  --r-sm:     2px;

  /* Typefaces */
  --f-disp:   'Playfair Display', 'Times New Roman', serif;
  --f:        'Libre Baskerville', Georgia, serif;
  --f-sans:   'Helvetica Neue', Helvetica, sans-serif;

  /* Motion */
  --ease:     cubic-bezier(0.4,0,0.2,1);
  --spring:   cubic-bezier(0.34,1.56,0.64,1);

  /* Shadows */
  --sh-sm:    0 2px 8px rgba(0,0,0,0.4);
  --sh-md:    0 4px 20px rgba(0,0,0,0.5);
}
```

---

## Typography Scale

The typeface *is* the design. Everything else is support.

| Role     | Family            | Size       | Weight | Style  | Line height |
|----------|-------------------|------------|--------|--------|-------------|
| Display  | Playfair Display  | 4.5rem+    | 900    | italic | 1.0         |
| H1       | Playfair Display  | 2.25rem    | 700    | italic | 1.1         |
| H2       | Playfair Display  | 1.5rem     | 700    | italic | 1.2         |
| H3       | Playfair Display  | 1.25rem    | 400    | italic | 1.3         |
| Body Lg  | Libre Baskerville | 1.125rem   | 400    | normal | 1.75        |
| Body     | Libre Baskerville | 1rem       | 400    | normal | 1.7         |
| Body Sm  | Libre Baskerville | 0.875rem   | 400    | normal | 1.65        |
| Label    | Helvetica Neue    | 0.625rem   | 400    | normal | — UC +0.18em|

**Rules:**
- Never use Playfair Display upright in body copy. It is a display face.
- Never use Libre Baskerville at sizes below 13px — it will break.
- Labels are always Helvetica Neue, uppercase, tracked at 0.16–0.20em.
- Display size must be large enough to hold the frame — at minimum 3.5rem.

---

## Drop Cap System

Use for lead paragraphs only — one per screen, maximum. Never in secondary body copy.

```css
.drop-cap::first-letter {
  font-family: var(--f-disp);
  font-size: 4em;
  font-weight: 400;
  float: left;
  line-height: 0.75;
  margin: 0.05em 0.12em 0 0;
  color: var(--gold);
}
```

**Rules:**
- Gold drop cap on true black is the loudest editorial statement available. Use once.
- The cap size of `4em` is calibrated for Playfair Display. Do not reduce it.
- Never apply to secondary or card body copy.

---

## Pull Quote System

The primary spec callout format. Replaces generic callout boxes with an editorial treatment.

```css
.pull-quote {
  border-top: 1px solid var(--gold);
  border-bottom: 1px solid var(--gold);
  padding: 1.5rem 2rem;
  font-family: var(--f-disp);
  font-style: italic;
  font-size: 1.125rem;
  line-height: 1.65;
  color: var(--t1);
  margin-bottom: 2.5rem;
}
```

**Usage:**
- Use for design rationale, spec callouts, key principles.
- Gold border lines are `1px solid var(--gold)` — both top and bottom only. Never side borders.
- Italic Playfair inside the pull quote. Sans-serif inline label optional (`em` tag with uppercase tracking).

---

## Gold Hairline Rules

Gold appears as jewelry, not wallpaper. Rules for its use:

| Context                     | Usage                                                      |
|-----------------------------|------------------------------------------------------------|
| Section heading rule        | 60px × 1px line above label, `opacity: 0.7`               |
| Pull quote borders          | `border-top` and `border-bottom` only                      |
| Card top hairline           | `border-top: 1px solid var(--gold)` — marks premium cards |
| Hero framing lines          | Gradient fade: `rgba(212,175,55,0.5)` center → transparent |
| Drop cap first letter       | `color: var(--gold)` — the only large gold element allowed |
| Focus state                 | `border-bottom: 1px solid var(--gold)` on inputs           |
| Progress indicators         | Active dot/dash, active player progress line               |
| Navigation active tab       | `border-top: 1px solid var(--gold)` on active tab only     |
| Button — secondary          | `border: 1px solid var(--gold)` — for gold CTA variant     |

**What gold is NOT:**
- Not a fill color for backgrounds
- Not a hover glow or box-shadow color
- Not used for text except drop caps and labels at `opacity: 0.7–0.8`
- Never more than 3 gold elements visible simultaneously

---

## Button System

```css
/* Primary — white border, inverts on hover */
.btn {
  background: transparent;
  border: 1px solid var(--t1);
  padding: 0.875rem 2.5rem;
  font-family: var(--f-sans);
  font-size: 0.6875rem;
  font-weight: 400;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: var(--t1);
  border-radius: 0;
}
.btn:hover { background: var(--t1); color: var(--bg); }
.btn:active { opacity: 0.85; }

/* Secondary — gold border */
.btn-sec { border-color: var(--gold); color: var(--gold); }
.btn-sec:hover { background: rgba(212,175,55,0.1); }

/* Ghost */
.btn-ghost { border-color: rgba(240,240,238,0.15); color: var(--t3); }
```

**Rules:**
- No border-radius. Zero. The square corner is the editorial choice.
- Hover inversion (white fill, black text) is the primary affordance signal — it is not subtle.
- Track, letter-spacing at `0.18em` minimum. Buttons that aren't tracked read as body copy.
- Never use a filled button as primary in this system.

---

## Form Input System

```css
/* Editorial input — bottom border only */
.inp {
  background: transparent;
  border: none;
  border-bottom: 1px solid rgba(240,240,238,0.15);
  color: var(--t1);
  font-family: var(--f);
  font-size: 1rem;
  padding: 0.875rem 0;
  outline: none;
  border-radius: 0;
}
.inp::placeholder { color: rgba(240,240,238,0.18); }
.inp:focus { border-bottom-color: var(--gold); }

/* Field label */
.label {
  font-family: var(--f-sans);
  font-size: 0.5625rem;
  font-weight: 400;
  letter-spacing: 0.16em;
  text-transform: uppercase;
  color: var(--t3);
  margin-bottom: 0.625rem;
}
```

**Rules:**
- Bottom border only. No box, no background, no radius.
- Gold focus state is the editor's attention — the only moment gold appears in interaction.
- Labels are always smaller than the input text. The 9px uppercase label is structural.
- Placeholder text at `var(--t4)` — barely visible. The user's input must dominate.

---

## Card System

```css
.card-ed {
  background: var(--s1);
  border-top: 1px solid var(--gold);  /* the premium mark */
  /* no shadow, no outer border except via layout */
}
.card-ed:hover { background: var(--s2); }
```

**Rules:**
- Gold top hairline is the premium mark. No card without it.
- No box-shadow. Depth is achieved through background contrast: `--s1` on `--bg`.
- Card thumbnails are editorial black — dark backgrounds with large ghost type, not photographs. Magazine aesthetic without actual images.
- Card headline always Playfair italic. Category label always uppercase sans, `color: var(--gold)` at low opacity.

---

## Progress Indicators

```css
/* Thin vertical dash — not a circle */
.prog-dot {
  width: 2px;
  height: 16px;
  background: rgba(240,240,238,0.18);
  border: none;
  cursor: pointer;
  transition: background 0.25s, transform 0.25s, height 0.25s;
}
.prog-dot.active {
  background: var(--gold);
  height: 20px;
  transform: scaleY(1.35);
}
```

The editorial progress indicator is a dash, not a dot. It references the column rule — a typographic artifact — not a button.

---

## Slider System

```css
/* 1px track, square gold thumb */
.rng::-webkit-slider-thumb {
  width: 10px;
  height: 10px;
  background: var(--gold);
  border: none;
  border-radius: 0;   /* square — not circular */
}
.rng::-webkit-slider-runnable-track {
  height: 1px;
  background: rgba(240,240,238,0.1);
}
```

Track is 1px. Thumb is 10×10px, square, gold. The fill from left is gold. No glow, no shadow.

---

## Navigation Bar

```css
/* Tab with gold top hairline when active */
.ni::after {
  content: '';
  position: absolute;
  top: 0; left: 0; right: 0;
  height: 1px;
  background: var(--gold);
  opacity: 0;
  transition: opacity 0.2s;
}
.ni.ni-on::after { opacity: 1; }

/* Label */
.ni-lbl {
  font-family: var(--f-sans);
  font-size: 0.4375rem;
  letter-spacing: 0.16em;
  text-transform: uppercase;
  color: var(--t3);
}
.ni.ni-on .ni-lbl { color: var(--gold); }
```

Active tab: gold top hairline, gold label text. No fill, no background change, no indicator dot.

---

## Motion

| Property          | Value                                      |
|-------------------|--------------------------------------------|
| Default ease      | `cubic-bezier(0.4,0,0.2,1)` — 200ms       |
| Spring            | `cubic-bezier(0.34,1.56,0.64,1)` — 280ms  |
| Hover transitions | 150–200ms                                  |
| Section reveal    | 650ms ease, `translateY(20px)` → 0         |
| Toggle thumb      | 280ms spring                               |

**Rules:**
- No bounce on buttons or text elements. Spring is reserved for radio dots and toggle thumbs.
- Section entrance animation is 650ms — deliberately slow and considered.
- No animation should feel playful or energetic. Every transition is deliberate.

---

## AI Prompting Guidance

When describing this style to an AI:

> "Design in the Dark Editorial style: true black background (#0a0a0a), warm off-white text (#f0f0ee), gold (#d4af37) used only as hairlines, borders, and drop caps — never as fill. Primary typeface is Playfair Display italic for headings and display, Libre Baskerville for body text, Helvetica Neue uppercase for labels. No border-radius on interactive elements. Buttons use border-only treatment that inverts on hover. Form inputs use bottom border only with gold focus state. Generous whitespace — the space is as important as the content."

**Style references to include:**
- *The New Yorker* (typographic confidence, restraint)
- *T Magazine* (dark editorial, gold accents)
- *Vogue* (large serif, luxury whitespace)
- *Kinfolk* (editorial minimalism, serif body text)
- *Apartamento* (confident ugliness/restraint combined)

**Anti-patterns — never do these in this system:**
- Rounded corners on buttons or cards
- Gradient fills as backgrounds
- Gold as a button fill color
- Sans-serif headlines
- Bright accent colors (blue, purple, green)
- Drop shadows that imply elevation
- Multiple typefaces beyond the three defined
- Icon-only navigation without text labels
- Centered body text
- Small display type (Display must be 3.5rem+)

---

## Accessibility Notes

- Text contrast: `#f0f0ee` on `#0a0a0a` achieves **16.5:1** — well above AAA (7:1).
- Secondary text `rgba(240,240,238,0.65)` on `#0a0a0a` achieves approximately **10.7:1**.
- Gold `#d4af37` on `#0a0a0a` achieves approximately **8.8:1** — AAA for normal text.
- Always provide `aria-label` on icon-only controls.
- Focus states use `outline: 1px solid var(--gold)` — ensure 3px offset minimum.

---

*Dark Editorial — Vol. XII · Style Guide*
*Crafted for the UI Styles Gallery*
