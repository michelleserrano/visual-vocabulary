# Kawaii Pastel — Style Guide
**Personality: Gentle. Sparkly. Rounded. Pastel. Unconditionally Friendly.**

---

## What is Kawaii?

**Kawaii (かわいい)** is the Japanese aesthetic of cuteness — not childishness, but *deliberate softness*. Every design decision asks: *does this feel safe and welcoming?* If a color could appear on a traffic sign, it's wrong. If an element could appear on a Sanrio character's outfit, it's right.

Design principles, in order of importance:
1. **Nothing should feel hard** — no sharp corners, no saturated colors, no aggressive shadows
2. **Everything should feel cared for** — sparkle decorations, soft glows, heart motifs
3. **Motion should feel alive** — wobble, bounce, float, not just fade

---

## Design Tokens

```css
:root {
  /* Backgrounds */
  --bg:      #fff0f7;   /* sakura-white — primary surface */
  --s1:      #ffe8f3;   /* petal soft — secondary surface */
  --s2:      #ffd8ed;   /* petal deep — tertiary, pressed states */

  /* Text */
  --t1:      #5a3a5a;   /* plum ink — primary text */
  --t2:      #8a5a8a;   /* muted plum — secondary text, labels */
  --t3:      rgba(90,58,90,0.5);   /* hints, metadata */
  --t4:      rgba(90,58,90,0.25);  /* placeholder text */

  /* Kawaii Pastel Palette */
  --sakura:  #ffb3d1;   /* cherry blossom pink — PRIMARY authority color */
  --lavender:#c8b3ff;   /* soft purple — secondary */
  --mint:    #b3ffd9;   /* fresh mint — tertiary */
  --peach:   #ffc8a0;   /* warm peach — warm accent */
  --sky:     #b3d9ff;   /* baby blue — calm accent */
  --lemon:   #fff3b3;   /* soft yellow — gentle attention */

  /* Semantic aliases */
  --ac:      var(--sakura);
  --ac-lo:   rgba(255,179,209,0.25);

  /* Radius system — max roundness at every level */
  --r-sm:    16px;   /* small elements: tags, badges */
  --r:       24px;   /* inputs, dropdowns */
  --r-md:    32px;   /* medium cards, modals */
  --r-lg:    48px;   /* large cards, panels */
  --r-full:  9999px; /* pills, circles — most buttons use this */

  /* Typography */
  --f:       'Nunito', system-ui, sans-serif;
  --f-disp:  'Nunito', sans-serif;

  /* Motion */
  --ease:    cubic-bezier(0.4, 0, 0.2, 1);
  --spring:  cubic-bezier(0.34, 1.56, 0.64, 1);  /* bouncy, overshoots slightly */

  /* Shadow system */
  --sh-soft: 0 4px 16px rgba(255,179,209,0.2);
  --sh-glow: 0 0 20px rgba(255,179,209,0.35);
  --sh-card: 0 4px 20px rgba(255,179,209,0.15), 0 1px 4px rgba(255,179,209,0.1);
  --sh-card-h: 0 8px 32px rgba(255,179,209,0.25), 0 2px 8px rgba(255,179,209,0.15);
}
```

---

## Typography

**One font: Nunito.** Its rounded terminals mirror every rounded corner. Never use a geometric or condensed typeface.

```html
<link href="https://fonts.googleapis.com/css2?family=Nunito:ital,wght@0,400;0,600;0,700;0,800;0,900;1,400&display=swap" rel="stylesheet">
```

| Role     | Size   | Weight | Notes                          |
|----------|--------|--------|--------------------------------|
| Display  | 48px   | 900    | Hero headlines                 |
| H1       | 36px   | 800    | Section titles                 |
| H2       | 28px   | 700    |                                |
| H3       | 22px   | 700    |                                |
| H4       | 18px   | 600    |                                |
| Body Lg  | 17px   | 400    | Intro paragraphs, lh 1.7       |
| Body     | 16px   | 400    | Default text, lh 1.55          |
| Body Sm  | 14px   | 400    | Secondary text                 |
| Caption  | 12px   | 700    | Labels, metadata, UC +0.06em   |

Add emoji and symbols to headings: `🌸 ✦ ♡ ✿ ★` — they are structural decoration, not ornamentation.

---

## Color Rules

**Always pastel. Never saturated. Never dark.**

- Check every color by imagining it on soft fabric, not a screen. If it looks like it belongs in a stationery shop, it's correct.
- `--sakura` (#ffb3d1) is the primary authority color. Use it for primary buttons, active states, highlights.
- Text color is `--t1` (#5a3a5a) — a soft plum-black, not a harsh charcoal.
- Never use pure black (#000) or pure white (#fff) in large areas. Background is always `--bg`.

---

## Sparkle Animation System

The ✦ sparkle is the kawaii signature. Use it as a decoration on cards, inputs, and nav elements.

```css
/* Core twinkle — slow, subtle scale + rotate */
@keyframes twinkle {
  0%, 100% { opacity: 0.4; transform: scale(0.8) rotate(0deg); }
  50%       { opacity: 1;   transform: scale(1.1) rotate(15deg); }
}

/* Apply to card sparkle decorators */
.kawaii-card::before {
  content: '✦';
  position: absolute;
  top: 10px; right: 14px;
  font-size: 0.8rem;
  animation: twinkle 2s ease-in-out infinite;
  pointer-events: none;
}

/* Stagger delays for multiple sparkles */
.card:nth-child(1)::before { animation-delay: 0s;   color: var(--lavender); }
.card:nth-child(2)::before { animation-delay: 0.7s; color: var(--mint); }
.card:nth-child(3)::before { animation-delay: 1.4s; color: var(--peach); }
```

**Click sparkle burst** — appear on user interaction, then remove:
```js
function sparkle(x, y) {
  const el = document.createElement('span');
  el.textContent = '✦';
  el.style.cssText = `
    position:fixed; left:${x}px; top:${y}px;
    pointer-events:none; font-size:1.25rem;
    color:var(--sakura); z-index:9999;
    animation:sparkleAppear 0.5s ease forwards;
  `;
  document.body.appendChild(el);
  setTimeout(() => el.remove(), 600);
}
@keyframes sparkleAppear {
  0%   { opacity: 0; transform: scale(0) rotate(-30deg); }
  60%  { opacity: 1; transform: scale(1.2) rotate(10deg); }
  100% { opacity: 1; transform: scale(1) rotate(0deg); }
}
```

---

## Heart Decoration Placement

Float hearts and sparkles in the background of sections. Use `position: absolute` decorators with `pointer-events: none` so they never interfere.

```css
.heart-float {
  position: absolute;
  font-size: 0.75rem;
  color: var(--sakura);
  opacity: 0.5;
  animation: floatHeart 4s ease-in-out infinite;
  pointer-events: none;
  user-select: none;
}

@keyframes floatHeart {
  0%, 100% { transform: translateY(0) rotate(-10deg);  opacity: 0.4; }
  50%       { transform: translateY(-8px) rotate(10deg); opacity: 0.7; }
}
```

**Placement template per section:**
```html
<span class="heart-float" style="top:10%;left:5%;animation-delay:0s">♡</span>
<span class="heart-float" style="top:20%;right:8%;animation-delay:1s;color:var(--lavender)">✦</span>
<span class="heart-float" style="bottom:15%;left:10%;animation-delay:2s;color:var(--mint)">★</span>
```

Use symbols from this set: `♡ ✦ ★ ✿ ⭐ 🌸` — rotate through pastel colors.

---

## Wobble Hover Recipe

Every interactive element in kawaii should express its interactivity through motion, not just color change.

```css
@keyframes wobble {
  0%   { transform: rotate(0deg); }
  15%  { transform: rotate(-3deg); }
  30%  { transform: rotate(3deg); }
  45%  { transform: rotate(-2deg); }
  60%  { transform: rotate(2deg); }
  75%  { transform: rotate(-1deg); }
  90%  { transform: rotate(1deg); }
  100% { transform: rotate(0deg); }
}

/* Apply on hover — use this on buttons, cards, nav items */
.btn:hover:not(:disabled) {
  animation: wobble 0.5s ease;
  transform: scale(1.04);
}
```

**Spring curve for position transitions:**
```css
--spring: cubic-bezier(0.34, 1.56, 0.64, 1);
/* Overshoots by ~15%, then settles — gives "alive" feel */
```

---

## Emoji Integration

Emoji are structural in kawaii design, not decoration. Use them:
- **In headings**: `🌸 Color Palette` — gives each section a personality
- **In card thumbnails**: replace abstract icons with large emoji at 3–4rem
- **In nav icons**: emoji replace SVG icons for warmth
- **In section labels/pills**: `🌸` beside the number
- **In form labels**: before field names to signal friendliness
- **As floating decorators**: hearts, stars, flowers scattered at low opacity

**Approved emoji set for kawaii:**
```
🌸 Cherry blossom (primary — sakura)
💜 Purple heart (lavender)
🌿 Herb/leaf (mint)
🍑 Peach
☁️ Cloud (sky)
⭐ Star
💌 Love letter
♡ Heart (Unicode — preferred over ❤️ for subtlety)
✦ Four-pointed star (Unicode — signature sparkle)
✿ Flower (Unicode — soft floral)
★ Black star (Unicode — slightly more formal)
🎵 Music note
🌟 Glowing star
```

---

## Component Recipes

### Button
```css
.btn {
  border: none;
  border-radius: var(--r-full);   /* pill shape — always */
  padding: 0.75rem 1.875rem;
  font-family: var(--f); font-weight: 700;
  transition: transform 0.2s var(--spring), box-shadow 0.2s;
}
.btn-sakura {
  background: var(--sakura); color: #fff;
  box-shadow: 0 4px 16px rgba(255,179,209,0.35);
}
.btn-sakura:hover { animation: wobble 0.5s ease; transform: scale(1.04); }
.btn-sakura:active { transform: scale(0.96); }
```

### Input
```css
.inp {
  background: #fff;
  border: none;
  border-radius: var(--r);   /* 24px — always rounded */
  box-shadow: 0 2px 12px rgba(255,179,209,0.15), inset 0 1px 4px rgba(255,179,209,0.1);
  padding: 0.875rem 1.25rem;
  font-family: var(--f); font-weight: 500;
}
.inp:focus {
  box-shadow: 0 0 0 3px rgba(255,179,209,0.3), 0 2px 12px rgba(255,179,209,0.15);
  outline: none;
}
```

### Checkbox
```css
.chk-box {
  width: 24px; height: 24px;
  border-radius: 50%;               /* full circle — never square */
  border: 2px solid var(--sakura);
  background: #fff;
  display: flex; align-items: center; justify-content: center;
  font-size: 0.75rem; color: transparent;
}
input:checked + .chk-box {
  background: var(--sakura); color: #fff;
  transform: scale(1.1);
  animation: bounceIn 0.35s var(--spring);
}
/* Checkmark character: ♡ (not ✓) */
```

### Card
```css
.card {
  background: #fff;
  border: none;                    /* never a hard border */
  border-radius: var(--r-lg);      /* 48px */
  box-shadow: var(--sh-card);
  position: relative;
  transition: transform 0.3s var(--spring), box-shadow 0.3s;
}
.card:hover {
  transform: translateY(-4px) scale(1.01);
  box-shadow: var(--sh-card-h);
}
.card::before {
  content: '✦';
  position: absolute; top: 10px; right: 14px;
  color: var(--lavender); font-size: 0.8rem;
  animation: twinkle 2s ease-in-out infinite;
}
```

---

## Anti-Patterns

| Wrong | Right |
|-------|-------|
| Sharp corners (`border-radius: 4px`) | Max roundness (`var(--r-full)`) |
| Saturated colors (`#ff0066`) | Pastel colors (`#ffb3d1`) |
| Hard borders (`border: 1px solid #ccc`) | Shadow-only (`box-shadow`) |
| Dark text on dark bg | Plum text on sakura-white bg |
| Abrupt transitions (0ms) | Spring transitions (spring curve) |
| SVG icons without personality | Emoji or Unicode symbols |
| Pure black (#000) text | `--t1` (#5a3a5a) plum ink |
| Grid without breathing room | Padding at every level (`var(--r-lg)`) |
| Flat card headers | Pastel gradient headers |
| Generic checkmarks (✓) | Heart checkmarks (♡) |

---

## AI Prompting Guidance

Use these phrases when prompting AI to generate kawaii-style UI:

**Style context:**
> "Design in kawaii pastel style: soft sakura-white background (#fff0f7), Nunito font, max border-radius (pill shapes everywhere), no hard borders, shadow-only depth, pastel palette (sakura #ffb3d1, lavender #c8b3ff, mint #b3ffd9). Add ✦ sparkle decorators and floating ♡ hearts."

**Motion context:**
> "Hover states use a wobble animation (subtle rotation ±3deg over 500ms) plus scale(1.04). Spring easing: cubic-bezier(0.34,1.56,0.64,1). Checkboxes bounce in with scale animation on check."

**Color guardrail:**
> "Keep all colors in the pastel range. Test: if you could imagine the color on a Sanrio character's clothing, it's correct. Never use pure black, dark grays, or saturated hues."

**Decoration context:**
> "Scatter floating ♡ ✦ ★ ✿ symbols as absolute-positioned, pointer-events:none decorators with floatHeart animation (4s ease-in-out, translateY -8px at 50%). Use low opacity (0.4–0.7). Each section gets 3–4 of these."

---

## Accessibility Notes

- Text contrast: `--t1` (#5a3a5a) on `--bg` (#fff0f7) = 4.6:1 ✓ (WCAG AA)
- Interactive elements must have visible focus rings (sakura glow: `0 0 0 3px rgba(255,179,209,0.3)`)
- Animations respect `prefers-reduced-motion` — wrap all keyframes in `@media (prefers-reduced-motion: no-preference)` or use the reset pattern
- Emoji in headings need `aria-hidden="true"` or be wrapped in `<span>` with appropriate labeling
- Checkbox and toggle labels must be programmatically associated (use `<label>` wrapping pattern)
