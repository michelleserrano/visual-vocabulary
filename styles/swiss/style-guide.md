# Swiss International · Style Guide
**Personality:** Objective. Mathematical. Systematic. Grid-first. Typography-forward.
**Voice:** The grid is the message. Helvetica is the voice. Red is the only punctuation.

---

## What This Style Is

The International Typographic Style — born in Switzerland and Germany in the 1950s — is not an aesthetic. It is a philosophy: that visual communication should be as clear and objective as possible. Every decision must be justified. Every element must earn its position.

Key practitioners: Josef Müller-Brockmann, Emil Ruder, Armin Hofmann, Max Bill.
Key publications: *Neue Grafik* (1958–65), *Grid Systems in Graphic Design* (1961), *Typographie* (Emil Ruder, 1967).

---

## Design Tokens

```css
:root {
  --bg:       #f5f5f5;   /* Page background */
  --white:    #ffffff;   /* Surfaces, cards, inputs */
  --t1:       #1a1a1a;   /* Primary text, borders */
  --t2:       #4a4a4a;   /* Secondary text */
  --t3:       #888888;   /* Captions, placeholders, meta */
  --ac:       #e8261d;   /* THE ONE COLOR — use sparingly */
  --r:        0px;       /* Zero radius everywhere */
  --f:        Helvetica, 'Helvetica Neue', Arial, sans-serif;
  --f-mono:   'Courier New', monospace;
  --sp4:  4px;  --sp8:  8px;  --sp12: 12px; --sp16: 16px;
  --sp24: 24px; --sp32: 32px; --sp48: 48px; --sp64: 64px;
}
```

**The rule:** All measurements must be multiples of 8. No 5px, no 13px, no 20px. If a value is not on the 8px grid, it is wrong.

---

## Baseline Grid

The baseline grid is not decorative — it is the structural skeleton of every layout.

- **Grid unit:** 8px
- **Body line-height:** 24px (3 units)
- **Heading line-height:** calculated per size to land on a grid line
- **Section spacing:** multiples of 8 only (32, 48, 64)
- **Column gutter:** 24px or 32px (never odd values)

Every text element should sit on a baseline. Every spacer should respect the unit. If two elements feel disconnected, the fix is almost always to align them to the grid.

---

## Color

Swiss design uses color as **information**, not decoration. The full palette:

| Token     | Hex       | Usage |
|-----------|-----------|-------|
| `--bg`    | `#f5f5f5` | Page background |
| `--white` | `#ffffff` | Cards, form panels, nav |
| `--t1`    | `#1a1a1a` | Body text, borders, buttons |
| `--t2`    | `#4a4a4a` | Secondary text, labels |
| `--t3`    | `#888888` | Captions, placeholders, metadata |
| `--ac`    | `#e8261d` | Primary card border, active states, CTA fill, focus indicators, progress fill, red hover state |

**The red rule:** Use `--ac` in no more than 2–3 locations per screen. If it appears everywhere, it is stripped of meaning. If it appears nowhere, something is missing.

---

## Typography Hierarchy

| Level     | Size    | Weight | Tracking  | Leading | Transforms |
|-----------|---------|--------|-----------|---------|------------|
| Display   | 48px    | 700    | −0.04em   | 1.00    | —          |
| H1        | 36px    | 700    | −0.03em   | 1.10    | —          |
| H2        | 28px    | 700    | −0.025em  | 1.15    | —          |
| H3        | 22px    | 700    | −0.02em   | 1.20    | —          |
| H4        | 18px    | 700    | −0.01em   | 1.30    | —          |
| Body Lg   | 16px    | 400    | 0         | 1.65    | —          |
| Body      | 14px    | 400    | 0         | 1.60    | —          |
| Body Sm   | 13px    | 400    | 0         | 1.55    | —          |
| Caption   | 10px    | 700    | +0.12em   | 1.50    | UPPERCASE  |
| Label     | 9px     | 700    | +0.14em   | 1.50    | UPPERCASE  |
| Micro     | 8px     | 700    | +0.18em   | 1.50    | UPPERCASE  |

**The typeface rule:** Helvetica — period. If Helvetica is unavailable, use Helvetica Neue, then Arial. Never use a geometric, humanist, or display typeface in Swiss-style work.

**Alignment rule:** Always flush left, ragged right. Never centered (except display numerals). Never fully justified — the uneven rag is the breath of the text.

---

## Layout Principles

### The Asymmetric Grid
Swiss design uses **asymmetric** column layouts. A 3-column or 5-column grid creates inherent visual tension — the left column is narrower (for labels/numbers), the right is wider (for content). This is not an accident; it is the structure made visible.

### Whitespace Is Structure
Empty space is not wasted space. Every gap between elements has a purpose. Generous margins create visual rest and allow the eye to read individual elements as distinct objects.

### Horizontal Rules
The `1px solid #1a1a1a` line is the most important element in this style after typography. It separates, organizes, and establishes hierarchy. Use it:
- As section dividers
- Under headings
- As card separators
- Between form fields (not boxes around them)

### Ghost Numbers
Large ghost numerals (`opacity: 0.04`) appear behind section headings. They reference the Swiss tradition of visible grid scaffolding — the structure underlying the composition.

---

## Component Rules

### Buttons
- Primary: red fill, white text, uppercase, 0.1em tracking
- Secondary: 1px black border, no fill, same type treatment
- All buttons: `padding: 0.75rem 2rem`, no radius, no shadow, no gradient
- Hover primary: `#c01810` (darker red)
- Hover secondary: black fill, white text (invert)
- Active: `transform: translateY(1px)` — a 1px drop, nothing more

### Form Inputs
- Only a bottom border (`border-bottom: 1px solid #888`)
- No box, no fill, no visual container
- Focus: `border-bottom: 2px solid var(--ac)` — the red arrives precisely where it is needed
- Labels: uppercase, 9px, 0.14em tracking, above the field

### Cards
- White background on gray page
- Top border: 4px solid (red for primary, black for others)
- No shadow at rest
- Hover: red top border + subtle `box-shadow: 0 4px 16px rgba(0,0,0,0.08)`
- Content is entirely typographic

### Navigation
- Uppercase Helvetica labels in a horizontal row
- Active: 3px red bottom border — that is the entire state indicator
- No icons, no fills, no backgrounds

### Checkboxes & Radios
- 20px square (not round) for both checkboxes AND radios
- 1px border
- Checked: black fill (not red — red is reserved for interactive UI state)

### Toggles
- Horizontal bar, 48×20px
- Active: `var(--ac)` fill
- Thumb: 14×14px white square

---

## What to Avoid

| Do NOT | Reason |
|--------|--------|
| Use border-radius | Rounds are ornament, not function |
| Use drop shadows | Shadow implies depth; Swiss design is flat |
| Use gradients | A surface is one color, not a range |
| Use multiple typefaces | Helvetica is sufficient |
| Use multiple colors | Red is already your accent |
| Center-align body text | The flush-left rag is typographic breath |
| Use decorative icons | Icons must be functional or absent |
| Pad every element with the same spacing | Rhythm requires contrast, not uniformity |

---

## AI Prompting Guidance

When prompting an AI to generate Swiss International–style UI, use this vocabulary:

### Affirmative prompts (what to ask for)
```
"Swiss International Typographic Style"
"Helvetica-based, grid-first layout"
"asymmetric column grid with left-aligned content"
"one accent color — red #e8261d — used sparingly"
"1px horizontal rules between sections"
"uppercase small caps labels above underline-only inputs"
"flat, no shadow, no radius, no gradient"
"ghost section numbers at 8rem, opacity 0.04"
"flush-left ragged-right typography throughout"
"red left border (4px) on active or primary elements"
"cards with top border only, no drop shadow"
"toggles using a horizontal bar, red when active"
"square checkboxes and radio buttons"
"progress bar as 1px line with red fill"
"navigation labels as uppercase Helvetica text, red 3px underline for active state"
```

### Negative prompts (what to rule out)
```
"no border-radius, not even 1px"
"no box-shadow"
"no gradients"
"no Google Fonts"
"no pill buttons"
"no circular checkboxes or radio buttons"
"no centered text"
"no decorative emoji or icons"
"no multiple accent colors"
```

### Complete style prompt template
```
Build a UI in Swiss International Typographic Style (Zurich, 1950s).
Typeface: Helvetica / 'Helvetica Neue' / Arial. No other fonts.
Colors: background #f5f5f5, white surfaces, text #1a1a1a, secondary #4a4a4a, 
        captions #888888, single accent red #e8261d used sparingly.
Layout: 8px baseline grid, asymmetric, flush-left alignment throughout.
No border-radius (enforce with * { border-radius: 0 !important }).
No box-shadow. No gradients. No decorative elements.
Headings: 700 weight, tight negative tracking, uppercase.
Section structure: ghost numbers (8rem, opacity 0.04) + red left border (4px).
Buttons: uppercase, 0.1em tracking, primary=red fill, secondary=1px black outline.
Inputs: underline only (no box), focus = 2px red underline.
Cards: white, top border 4px (red for primary, black for others), no shadow.
Navigation: uppercase text row, active = 3px red bottom underline.
```

---

## Historical Reference

| Year | Work | Designer |
|------|------|----------|
| 1957 | Helvetica typeface released | Max Miedinger |
| 1958 | *Neue Grafik* magazine founded | Lohse, Müller-Brockmann, Neuburg, Vivarelli |
| 1961 | First international typography exhibition | Various |
| 1961 | *Gestaltungsprobleme des Grafikers* | Josef Müller-Brockmann |
| 1967 | *Typographie* | Emil Ruder |
| 1981 | *Grid Systems in Graphic Design* | Josef Müller-Brockmann |

---

*This style guide is part of the UI Styles Gallery — a reference library of historically significant design systems implemented as interactive demos.*
