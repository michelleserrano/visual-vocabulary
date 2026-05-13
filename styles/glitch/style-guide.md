# GLITCH ART — Style Guide
**Corrupted. Chromatic. Monochrome-plus. Erratic. Beautiful-broken.**

> Glitch Art is not a visual style — it is a philosophy. The error is the medium. Breakage, when controlled, is the highest form of intentionality.

---

## Identity

| Property | Value |
|---|---|
| Personality | Corrupted terminal. System breakdown as aesthetic. |
| Distinguish from Cyberpunk | No neon city. No grid. No danger. This is the signal, not the street. |
| Distinguish from Acid | No color overload. Glitch is monochrome-plus: black void + two RGB channels only. |
| Distinguish from Vaporwave | No nostalgia. No pastel. Glitch is now, erratic, and cold. |
| Era feel | Post-internet art, net.art, Rosa Menkman, datamoshing |

---

## Design Tokens

```css
:root {
  --bg:    #000000;   /* true black — errors happen in the void */
  --s1:    #080808;
  --s2:    #101010;
  --s3:    #181818;
  --t1:    #ffffff;
  --t2:    rgba(255,255,255,0.65);
  --t3:    rgba(255,255,255,0.35);
  --t4:    rgba(255,255,255,0.15);
  --red:   #ff0050;   /* RGB: Red channel */
  --cyan:  #00ffd5;   /* RGB: Cyan channel (green+blue) */
  --blue:  #0050ff;   /* Blue channel accent */
  --ac:    var(--red);
  --ac2:   var(--cyan);
  --border: 1px solid rgba(255,255,255,0.1);
  --border-red: 1px solid rgba(255,0,80,0.4);
  --r:    0px;       /* no radius — errors don't round */
  --r-sm: 0px;
  --r-full: 0px;
  --f:    'Share Tech Mono', 'IBM Plex Mono', 'Courier New', monospace;
  --f-disp: 'Share Tech Mono', monospace;
  --ease: cubic-bezier(0.4,0,0.2,1);
  --glitch-dur: 0.3s;
}

*, *::before, *::after { border-radius: 0 !important; }
```

---

## Color Channel Explanation

The two accent colors are not a design palette. They are the **R** and **G+B** planes of an RGB signal physically separating from each other.

| Token | Hex | Role |
|---|---|---|
| `--red` | `#ff0050` | Red channel — primary corruption vector |
| `--cyan` | `#00ffd5` | Cyan (G+B) channel — secondary aberration |
| `--blue` | `#0050ff` | Blue accent — used sparingly |
| Black | `#000000` | The void — where errors appear |
| White | `#ffffff` | Where R + G+B reconstruct at full intensity |

**Key rule:** `mix-blend-mode: screen` on the aberration layers reconstructs white where they overlap. This is the physics of light addition, not a design trick.

---

## Typography

**One typeface. No exceptions.**

```css
font-family: 'Share Tech Mono', 'IBM Plex Mono', 'Courier New', monospace;
```

- `Share Tech Mono` — primary display and body. Thin stroke, terminal feel.
- `IBM Plex Mono 700` — ghost section numbers only. Weight signals structural data, not decoration.
- No geometric sans. No humanist. No display serifs. The system is corrupted — it uses what is available.

**Letter spacing:** Always positive. `0.05em` minimum. Monospace is already spaced; add air to feel like a terminal printout.

**Text transform:** `uppercase` for labels, navigation, buttons, and identifiers. Body copy in sentence case.

---

## Chromatic Aberration — THE Signature Effect

This is the core technique. It creates the illusion of an RGB signal splitting apart.

### CSS Recipe

```css
.glitch-text {
  position: relative;
  color: var(--t1);
  display: inline-block;
}

/* Red channel — offset right, clips a horizontal band */
.glitch-text::before {
  content: attr(data-text);  /* element MUST have data-text="same content" */
  position: absolute;
  top: 0; left: 2px;
  color: var(--red);
  clip-path: polygon(0 0, 100% 0, 100% 5%, 0 5%);
  mix-blend-mode: screen;
  animation: glitch-a 4s infinite;
  pointer-events: none;
}

/* Cyan channel — offset left, clips a different band */
.glitch-text::after {
  content: attr(data-text);
  position: absolute;
  top: 0; left: -2px;
  color: var(--cyan);
  clip-path: polygon(0 0, 100% 0, 100% 3%, 0 3%);
  mix-blend-mode: screen;
  animation: glitch-b 4s infinite 0.15s;
  pointer-events: none;
}

@keyframes glitch-a {
  0%, 88%, 100% {
    transform: translate(0);
    clip-path: polygon(0 0, 100% 0, 100% 5%, 0 5%);
    opacity: 0.7;
  }
  89% { transform: translate(-3px, 1px); clip-path: polygon(0 28%, 100% 28%, 100% 48%, 0 48%); opacity: 1; }
  90% { transform: translate(3px, -1px); clip-path: polygon(0 50%, 100% 50%, 100% 55%, 0 55%); opacity: 0.8; }
  91% { transform: translate(-1px, 2px); clip-path: polygon(0 68%, 100% 68%, 100% 82%, 0 82%); opacity: 1; }
  92% { transform: translate(0); clip-path: polygon(0 0, 100% 0, 100% 5%, 0 5%); opacity: 0.7; }
}

@keyframes glitch-b {
  0%, 86%, 100% {
    transform: translate(0);
    clip-path: polygon(0 0, 100% 0, 100% 3%, 0 3%);
    opacity: 0.6;
  }
  87% { transform: translate(3px, -1px); clip-path: polygon(0 42%, 100% 42%, 100% 62%, 0 62%); opacity: 1; }
  88% { transform: translate(-2px, 2px); clip-path: polygon(0 75%, 100% 75%, 100% 88%, 0 88%); opacity: 0.9; }
  89% { transform: translate(1px, 0); clip-path: polygon(0 0, 100% 0, 100% 3%, 0 3%); opacity: 0.6; }
}
```

**HTML requirement:** Every element using `.glitch-text` needs `data-text` matching its text content:
```html
<h1 class="glitch-text" data-text="GL!TCH">GL!TCH</h1>
```

---

## Scan Tear System

A horizontal band of displacement. Slow-moving, not flickering. The effect is a wound.

```css
.scan-tear {
  position: relative;
  overflow: hidden;
}
.scan-tear::before {
  content: '';
  position: absolute;
  left: 0; right: 0;
  height: 1px;
  background: linear-gradient(90deg,
    transparent 0%,
    rgba(255,0,80,0.6) 30%,
    rgba(0,255,213,0.4) 60%,
    transparent 100%
  );
  z-index: 10;
  mix-blend-mode: screen;
  animation: tear-move 5s steps(1) infinite;
  pointer-events: none;
}

@keyframes tear-move {
  0%   { top: 15%; opacity: 0.5; height: 1px; }
  20%  { top: 62%; opacity: 0.7; height: 2px; }
  40%  { top: 38%; opacity: 0.3; height: 1px; }
  60%  { top: 77%; opacity: 0.6; height: 1px; }
  80%  { top: 25%; opacity: 0.4; height: 2px; }
  100% { top: 15%; opacity: 0.5; height: 1px; }
}
```

**Critical timing:** Use `steps(1)` not `linear`. The tear jumps — it does not slide. It is a frame error, not a motion.

---

## Data Corruption Stripes

Missing pixel rows — the evidence of data loss.

```css
.data-corrupt {
  background-image: repeating-linear-gradient(
    0deg,
    transparent 0px,
    transparent 4px,
    rgba(255,0,80,0.04) 4px,
    rgba(255,0,80,0.04) 5px
  );
}
```

Use on spec callouts, form panels, card thumbnails, and hero panels. The stripe should be nearly invisible at rest — it reads subliminally.

---

## JavaScript Glitch Trigger System

```javascript
function triggerGlitch(el) {
  if (el.classList.contains('glitching')) return;
  el.classList.add('glitching');
  setTimeout(() => el.classList.remove('glitching'), 200 + Math.random() * 300);
}

/* Periodic random glitches on all glitch-text elements */
document.querySelectorAll('.glitch-text').forEach(el => {
  const interval = 2000 + Math.random() * 4000;
  setInterval(() => {
    if (Math.random() > 0.6) triggerGlitch(el);
  }, interval);
});

/* Glitch on hover for interactive elements */
document.querySelectorAll('.btn, .card, .nav-item').forEach(el => {
  el.addEventListener('mouseenter', () => {
    triggerGlitch(el.querySelector('.glitch-text') || el);
  });
});
```

```css
.glitching {
  animation: intense-glitch 0.3s steps(1) forwards !important;
}

@keyframes intense-glitch {
  0%   { transform: translate(0); filter: none; }
  15%  { transform: translate(-4px, 1px); filter: hue-rotate(90deg) brightness(1.3); }
  30%  { transform: translate(4px, -2px); filter: hue-rotate(180deg); }
  45%  { transform: translate(-2px, 3px); filter: hue-rotate(270deg) brightness(0.9); }
  60%  { transform: translate(3px, -1px); filter: hue-rotate(360deg); }
  75%  { transform: translate(-1px, 2px); filter: none; }
  90%  { transform: translate(2px, -1px); }
  100% { transform: translate(0); filter: none; }
}
```

**Timing rule:** 200–500ms total. Long enough to register, short enough to feel like a recovery, not a breakdown.

---

## Component Rules

### Sticky Navigation
- `background: #000000`
- `border-bottom: 1px solid rgba(255,0,80,0.2)`
- Title: chromatic aberration active via `.glitch-text`
- Download button: red border + red text, uppercase monospace
- No shadows, no gradients

### Progress Dots (Side Nav)
- **6×6px squares** — `border-radius: 0 !important`
- `border: 1px solid rgba(255,255,255,0.2)` at rest
- Active: white fill + glitch animation that briefly shows red/cyan offset

### Buttons
- **Primary:** `background: white; color: black; border: 2px solid white`
- **Hover:** text chromatic aberration via `::before`/`::after` + `data-text` attribute
- **Active:** `transform: skew(2deg); background: rgba(255,0,80,0.15); color: var(--red)`
- **Red variant:** `background: var(--red); color: black`
- **Ghost:** `transparent; border: 1px solid rgba(255,255,255,0.25)` → hover: red border, red text
- All buttons: `text-transform: uppercase; letter-spacing: 0.1em`

### Form Inputs
- `background: rgba(255,255,255,0.04); border: 1px solid rgba(255,255,255,0.15)`
- `caret-color: var(--red)`
- Focus: `border-color: var(--red); box-shadow: 0 0 0 1px var(--red), 0 0 10px rgba(255,0,80,0.15)`
- Checkboxes: **`×`** not `✓` — use the mark of error, not confirmation
- Toggles: rectangular track with scanline overlay; red when active; thumb glitches on toggle

### Cards
- `background: var(--s1); border: 1px solid rgba(255,255,255,0.06)`
- Hover: `box-shadow: inset 0 0 0 1px var(--red), inset 1px 0 0 1px var(--cyan)` (chromatic border separation)
- Scan tear appears in card on hover only
- Thumbnail: procedural noise from `repeating-linear-gradient`, not an image

### Spec Callouts
- `background: var(--s2); border-left: 2px solid var(--red)`
- Add `.data-corrupt` class for stripe pattern
- Animated scan tear passes through via `::before`

---

## What Makes Glitch ≠ Other Styles

| Style | Core signal | Color logic | Edge radius |
|---|---|---|---|
| Cyberpunk | Urban danger, neon city | Magenta + cyan, electric purple | Mixed (sharp + pill) |
| Acid | Rave overload, all neons | Maximum saturation, every hue | Pill/round |
| Glitch | Digital error, system failure | **Black + R/G+B channel only** | **Zero — always** |

The distinguishing test: **does it look like a monitor failing to render?** If yes, it's Glitch.

---

## AI Prompting Guidance

When describing this style to an AI system:

> "Glitch art aesthetic. True black background. Chromatic aberration: red (#ff0050) and cyan (#00ffd5) text layers offset by ±2px using clip-path to show horizontal bands, mix-blend-mode: screen. Monospace font only (Share Tech Mono). Hard rectangular edges, no border-radius anywhere. Scan tear animation: a 1px horizontal line that jumps between positions with steps() timing. Data corruption stripes via repeating-linear-gradient. The effect should look like a monitor showing intentional, beautiful errors — not genuinely broken."

**Avoid these AI descriptions:**
- ~~"neon glowing" ~~ → that's Cyberpunk
- ~~"colorful glitch"~~ → that's Acid
- ~~"retro 80s"~~ → that's Synthwave
- ~~"rainbow corruption"~~ → wrong color model

**Correct framing:**
- "RGB signal separation"
- "CRT monitor error"
- "data corruption aesthetic"
- "scan line artifacts"
- "monochrome plus two RGB channels only"

---

## Anti-Patterns

- **No rounded corners** — ever. `border-radius: 0 !important` globally.
- **No gradients for decoration** — gradients only appear as corruption artifacts.
- **No multiple accent colors** — only red + cyan + optional blue. Adding green, yellow, or purple makes it Acid or Cyberpunk.
- **No smooth animations** — use `steps(1)` for tears and frame transitions. Smoothness is a sign the system is working.
- **No chaotic flickering** — controlled timing. The effect recovers. A broken system that recovered is more uncanny than one that is still failing.
- **No drop shadows** — shadows belong to neumorphism and glassmorphism. Glitch has no physics, only signal.

---

## Accessibility Notes

Glitch art has inherent accessibility tensions:
- Chromatic aberration at full intensity can cause issues for users with visual processing disorders
- Always respect `prefers-reduced-motion` — suppress all animations including glitch-text and scan tear
- Ensure sufficient contrast on body text (white on black passes WCAG AAA)
- Use `aria-label` and semantic HTML — the visual corruption is decorative, not structural

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}
```

---

*Glitch Art style guide — seaMYK / Michelle Pujals*
