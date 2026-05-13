# Terminal Mono — Style Guide

**Personality:** Monochromatic. Focused. CRT-warm. Historical. Minimal.

> "The terminal predates the concept of design choices. The hardware decided the font, the color, the radius. We adopt those constraints as intent."

---

## Identity

| Property | Value |
|----------|-------|
| Origin | DEC VT100 / IBM 3270, 1978–1985 |
| Color count | **1** (amber) |
| Typeface | Share Tech Mono |
| Radius | 0px everywhere |
| Glow | Phosphor warm — soft, not aggressive |
| Mood | Focused, calm, productive |
| Anti-mood | Chaotic, decorative, neon rave |

**Key distinction from Acid Graphics:** Acid uses multiple neon colors, glitch effects, and rave energy. Terminal Mono uses a single amber wavelength, no glitch, and the quiet focus of a working mainframe operator.

---

## Design Tokens

```css
:root {
  /* Surfaces */
  --bg:          #0a0800;   /* near-black with amber undertone */
  --s1:          #110f00;   /* panel background */
  --s2:          #1a1600;   /* raised surface */

  /* The one color */
  --amber:       #ffb000;   /* THE color — warm CRT phosphor */
  --amber-hi:    #ffcc44;   /* highlight / excited state */
  --amber-dim:   rgba(255,176,0,0.55);
  --amber-lo:    rgba(255,176,0,0.15);
  --amber-faint: rgba(255,176,0,0.06);

  /* Text hierarchy — opacity only */
  --t1:          rgba(255,176,0,0.92);  /* primary */
  --t2:          rgba(255,176,0,0.55);  /* secondary */
  --t3:          rgba(255,176,0,0.30);  /* muted */

  /* Borders */
  --border:      1px solid rgba(255,176,0,0.2);
  --border-hi:   1px solid rgba(255,176,0,0.5);

  /* Structure */
  --r:           0px;   /* no radius — ever */
  --f:           'Share Tech Mono', 'IBM Plex Mono', 'Courier New', monospace;

  /* Glow — subtle phosphor bloom, NOT acid neon */
  --glow-xs:     0 0 4px rgba(255,176,0,0.3);
  --glow-sm:     0 0 8px rgba(255,176,0,0.35), 0 0 3px rgba(255,176,0,0.5);
  --glow-md:     0 0 12px rgba(255,176,0,0.4), 0 0 5px rgba(255,176,0,0.6);
}
```

---

## CRT Effects

### 1. Scanlines
Add to `body::after`. Subtle — not overwhelming. The lines are 1px dark bands every 2px.

```css
body::after {
  content: '';
  position: fixed;
  inset: 0;
  background: repeating-linear-gradient(
    0deg,
    transparent 0px,
    transparent 1px,
    rgba(0,0,0,0.15) 1px,
    rgba(0,0,0,0.15) 2px
  );
  pointer-events: none;
  z-index: 9999;
}
```

**Tuning:** Increase `rgba(0,0,0,0.15)` → `0.25` for more visible lines. Never exceed `0.35` or the UI becomes unreadable.

### 2. Phosphor Bloom
Apply to all visible text elements. The glow is warm amber, not white. Simulate the phosphor's slight luminance spread.

```css
p, span, h1, h2, h3, h4, h5, h6,
div, label, button, a { 
  text-shadow: 0 0 3px rgba(255,176,0,0.4); 
}
```

**Tuning:** `0 0 3px rgba(255,176,0,0.4)` is baseline. Use `--glow-xs` for interactive focus states, `--glow-sm` on hover, `--glow-md` for primary headings or active states.

### 3. Screen Curvature
Subtle inward shadow on the body simulates the CRT tube's curved glass.

```css
body {
  box-shadow: inset 0 0 100px rgba(0,0,0,0.4);
  min-height: 100vh;
}
```

### 4. Blinking Cursor
Use `.cursor-blink` on headings, input labels, or anywhere a typing cursor is contextually appropriate.

```css
@keyframes blink { 0%,49% { opacity:1; } 50%,100% { opacity:0; } }

.cursor-blink::after {
  content: '█';
  animation: blink 1s step-end infinite;
  margin-left: 1px;
  color: var(--amber);
  text-shadow: var(--glow-sm);
}
```

---

## Typography

**One typeface: Share Tech Mono.** No fallback to proportional fonts.

```html
<link href="https://fonts.googleapis.com/css2?family=Share+Tech+Mono&display=swap" rel="stylesheet">
```

| Scale | Size | Usage |
|-------|------|-------|
| Display | 48px | Hero titles, section names |
| H1 | 36px | Page titles |
| H2 | 28px | Section headings |
| H3 | 22px | Card headings |
| H4 | 18px | Sub-headings |
| Body Lg | 16px | Lead paragraph text |
| Body | 14px | Standard body copy |
| Small | 12px | Metadata, hints |
| Caption | 10px | Labels, uppercase, 0.15em tracking |

**Rules:**
- Headings: `text-transform: uppercase; letter-spacing: 0.15em`
- Body: `letter-spacing: 0.02em` (default on body)
- Labels: `text-transform: uppercase; letter-spacing: 0.12em; font-size: 0.6875rem`
- Never use italic — terminals don't have italic glyphs

---

## Color System

The hierarchy is opacity, not hue. Never introduce a second hue.

```
#FFB000 ─── 1.00 ─── Border highlight, active states
#FFB000 ─── 0.92 ─── Primary text (--t1)
#FFB000 ─── 0.55 ─── Secondary text, dim labels (--t2)
#FFB000 ─── 0.30 ─── Muted text, placeholders (--t3)
#FFB000 ─── 0.20 ─── Default borders
#FFB000 ─── 0.15 ─── Subtle background fills
#FFB000 ─── 0.06 ─── Ghost numbers, faint overlays
#FFB000 ─── 0.03 ─── Input background tint
```

**Contrast:** Amber `#FFB000` on `#0A0800` = **12.5:1**. Passes WCAG AAA.

---

## Components

### Buttons
No gradients, no radius, no icons. The border IS the button.

```css
.btn {
  border: 1px solid var(--amber);
  color: var(--amber);
  background: rgba(255,176,0,0.06);
  font-family: var(--f);
  text-transform: uppercase;
  letter-spacing: 0.12em;
  border-radius: 0;
  text-shadow: var(--glow-xs);
}
.btn:hover {
  background: rgba(255,176,0,0.12);
  box-shadow: var(--glow-sm);
  text-shadow: var(--glow-sm);
}
.btn:active { background: rgba(255,176,0,0.18); }

/* Secondary */
.btn-sec {
  border-color: rgba(255,176,0,0.3);
  color: var(--t2);
  background: transparent;
}
```

Labels format: `[PRIMARY]`, `[CANCEL]`, `[EXECUTE]`, `[HELP]`

### Form Inputs
```css
.inp {
  background: rgba(255,176,0,0.03);
  border: 1px solid rgba(255,176,0,0.2);
  color: var(--t1);
  font-family: var(--f);
  caret-color: var(--amber);
  border-radius: 0;
}
.inp:focus {
  border-color: var(--amber);
  box-shadow: var(--glow-xs);
}
```

### Cards
```css
.card {
  background: var(--s1);
  border: 1px solid rgba(255,176,0,0.15);
}
/* Amber header line */
.card-top-line {
  height: 2px;
  background: var(--amber);
  box-shadow: var(--glow-xs);
}
.card:hover {
  border-color: rgba(255,176,0,0.4);
  box-shadow: var(--glow-xs);
}
```

Card thumbnails use ASCII art — no images, no emojis.

### ASCII Progress Bar
```javascript
function asciiBar(val, max, length = 30) {
  const filled = Math.round((val / max) * length);
  const empty = length - filled;
  return '[' + '█'.repeat(filled) + '░'.repeat(empty) + ']';
}
// Output: [████████████░░░░░░░░░░░░░░░░░░]
```

### Navigation
Active state: `border-bottom: 2px solid var(--amber)` on the nav item.
Separators: `width: 1px; height: 24px; background: rgba(255,176,0,0.12)`

---

## Anti-Patterns

| Don't | Do instead |
|-------|-----------|
| Use `border-radius > 0` | Sharp corners everywhere |
| Add a second color | Vary opacity of amber only |
| Use emoji or icons | ASCII characters: `[*]`, `[?]`, `[✓]`, `[>]` |
| Make glows intense | Keep glow subtle — the mood is calm, not rave |
| Use proportional typeface | Share Tech Mono only |
| Use bold/italic | Monospace has weight only — rely on opacity |
| Overcrowd elements | Terminals have spacious line-height (1.65) |
| Animate aggressively | Slow reveals, 0.55s ease-out |

---

## AI Prompting Guidance

When prompting an AI to generate Terminal Mono UI:

```
Design a [component] in Terminal Mono style:
- Background: #0A0800 (near-black with amber undertone)
- ONE color only: #FFB000 amber, varying opacity for hierarchy
- Font: Share Tech Mono — monospace, uppercase labels, 0.12em letter-spacing
- All borders/cards: sharp corners, border-radius: 0
- Amber phosphor text-shadow: 0 0 3px rgba(255,176,0,0.4) on text
- CRT scanlines overlay: repeating-linear-gradient with rgba(0,0,0,0.15) bands
- Buttons labeled as commands: [EXECUTE], [CANCEL], [HELP]
- Progress shown as ASCII blocks: [████░░░░░░]
- Mood: 1980s mainframe terminal, quiet focus, NOT neon rave
```

**Differentiate from Acid Graphics:**
- Acid: neon multi-color, glitch, chaos → Terminal: single amber, clean, calm
- Acid: `text-shadow: 0 0 20px` (intense) → Terminal: `text-shadow: 0 0 3px` (subtle)
- Acid: rave culture reference → Terminal: computing history reference

---

## Usage Contexts

**Best for:**
- Developer tools and dashboards
- System monitoring interfaces
- Code editors and IDEs
- Command-line adjacent tools
- Retro/vintage-themed applications
- Data terminal readouts
- Security and infrastructure tools

**Avoid for:**
- Consumer social apps (too austere)
- Children's applications
- High-photography content (no image support)
- Brand-heavy interfaces

---

## File Reference

- `demo.html` — Interactive component showcase
- `style-guide.md` — This file

**Google Fonts import:**
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Share+Tech+Mono&display=swap" rel="stylesheet">
```
