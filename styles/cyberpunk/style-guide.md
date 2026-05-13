# Cyberpunk · Style Guide

**Personality:** Urban. Dangerous. Dense. Neon-lit. Dystopian.

> "The future city at night, seen through rain-slicked glass. Where corporations own the sky and the streets own everyone else."

---

## Identity

| Attribute | Value |
|-----------|-------|
| Era | Blade Runner 2049 · Cyberpunk 2077 |
| Mood | Threatening, dense, beautiful in decay |
| Shape language | Angular · clipped corners · no curves |
| Light source | Neon signs from below |
| Texture | Scanlines · noise · chromatic glow |

---

## Design Tokens

```css
:root {
  /* Backgrounds — near-black with blue undertone */
  --bg:     #0a0a0f;   /* void */
  --s1:     #0e0e16;   /* surface */
  --s2:     #14141e;   /* raised */
  --s3:     #1a1a28;   /* elevated */

  /* Neon accents */
  --red:    #ff2d55;   /* danger · primary */
  --yellow: #ffcc00;   /* caution · secondary */
  --purple: #a020f0;   /* vice · tertiary */
  --cyan:   #00d4ff;   /* data · highlight */

  /* Aliases */
  --ac:     #ff2d55;
  --ac2:    #ffcc00;

  /* Text — cool white with purple tint */
  --t1:     #f0e8ff;
  --t2:     rgba(240,232,255,0.65);
  --t3:     rgba(240,232,255,0.35);

  /* Borders */
  --border:    1px solid rgba(255,45,85,0.25);
  --border-hi: 1px solid rgba(255,45,85,0.6);

  /* Radii — angular is the law */
  --r:      2px;
  --r-sm:   0px;
  --r-md:   4px;
  --r-full: 9999px;   /* pills only for extreme contrast */

  /* Typography */
  --f:      'Rajdhani', 'Helvetica Neue', sans-serif;
  --f-disp: 'Bebas Neue', Impact, sans-serif;
  --f-mono: 'Share Tech Mono', 'Courier New', monospace;

  /* Motion */
  --ease:   cubic-bezier(0.4,0,0.2,1);
  --spring: cubic-bezier(0.34,1.56,0.64,1);

  /* Neon glows */
  --glow-r: 0 0 10px rgba(255,45,85,0.6),  0 0 24px rgba(255,45,85,0.3);
  --glow-y: 0 0 10px rgba(255,204,0,0.6),  0 0 24px rgba(255,204,0,0.3);
  --glow-c: 0 0 10px rgba(0,212,255,0.6),  0 0 24px rgba(0,212,255,0.3);
  --glow-p: 0 0 10px rgba(160,32,240,0.6), 0 0 24px rgba(160,32,240,0.3);
}

body {
  background: var(--bg);
  color: var(--t1);
  font-family: var(--f);
}
```

---

## Signature Shape: Clipped Corner

The single most important pattern. Every card, button, panel, and container uses this cut.

```css
/* Standard — use on cards, panels, large containers */
.clip-corner {
  clip-path: polygon(
    0 0,
    calc(100% - 12px) 0,
    100% 12px,
    100% 100%,
    12px 100%,
    0 calc(100% - 12px)
  );
}

/* Small — use on buttons, chips, inputs */
.clip-corner-sm {
  clip-path: polygon(
    0 0,
    calc(100% - 8px) 0,
    100% 8px,
    100% 100%,
    8px 100%,
    0 calc(100% - 8px)
  );
}

/* Large — use on hero panels, major containers */
.clip-corner-lg {
  clip-path: polygon(
    0 0,
    calc(100% - 18px) 0,
    100% 18px,
    100% 100%,
    18px 100%,
    0 calc(100% - 18px)
  );
}
```

**Rule:** Never use `border-radius` on primary UI elements. Circles are for icons and avatars only.

---

## Scanline Overlay

Always-on atmospheric texture. Apply to `body::after`.

```css
body::after {
  content: '';
  position: fixed;
  inset: 0;
  background: repeating-linear-gradient(
    0deg,
    transparent 0px,
    transparent 2px,
    rgba(255,45,85,0.015) 2px,
    rgba(255,45,85,0.015) 4px
  );
  pointer-events: none;
  z-index: 9999;
}
```

---

## Neon Glow System

Four colors. Four semantic meanings. Each has a glow formula.

| Color | Hex | Meaning | Glow |
|-------|-----|---------|------|
| Red | `#ff2d55` | Danger · Execute · Primary | `var(--glow-r)` |
| Yellow | `#ffcc00` | Caution · Warning · Secondary | `var(--glow-y)` |
| Purple | `#a020f0` | Vice · Mystery · Tertiary | `var(--glow-p)` |
| Cyan | `#00d4ff` | Data · Network · Info | `var(--glow-c)` |

**Usage rules:**
- Red: CTAs, active states, borders on primary cards
- Yellow: Top nav bar line, caution buttons, Intel/warning content
- Purple: Deep links, encrypted data, black-market content
- Cyan: Live data feeds, network status, uplink indicators

---

## Typography

Three faces. Three roles. Never mix.

| Face | Use | Notes |
|------|-----|-------|
| **Bebas Neue** | Display, H1, H2, section titles, buttons | Uppercase only. Track at +0.1–0.2em. |
| **Rajdhani** | Body text, H3, H4, UI labels | Weight 400–700. Clean and military. |
| **Share Tech Mono** | Data, captions, code, terminal, form inputs | Color: `var(--cyan)` or `var(--t3)`. Scan-readable. |

```html
<link href="https://fonts.googleapis.com/css2?family=Rajdhani:wght@300;400;500;600;700&family=Bebas+Neue&family=Share+Tech+Mono&display=swap" rel="stylesheet">
```

---

## Components

### Buttons

```css
.btn {
  font-family: var(--f-disp);
  font-size: 1rem;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  clip-path: polygon(0 0, calc(100% - 10px) 0, 100% 10px,
                     100% 100%, 10px 100%, 0 calc(100% - 10px));
  border: 1px solid;
  padding: 0.75rem 1.75rem;
  cursor: pointer;
  transition: box-shadow 0.2s, transform 0.12s;
}

/* Primary — execute */
.btn-p {
  background: var(--red);
  color: #0a0a0f;
  border-color: var(--red);
  box-shadow: var(--glow-r);
}
.btn-p:hover { box-shadow: 0 0 18px rgba(255,45,85,0.9), 0 0 40px rgba(255,45,85,0.4); }

/* Secondary — caution */
.btn-sec {
  background: transparent;
  color: var(--yellow);
  border-color: var(--yellow);
  box-shadow: var(--glow-y);
}

/* Ghost — passive */
.btn-ghost {
  background: transparent;
  color: var(--t2);
  border-color: rgba(240,232,255,0.2);
}
```

### Cards

```css
.card {
  background: var(--s1);
  border: 1px solid rgba(255,45,85,0.15);
  clip-path: polygon(0 0, calc(100% - 14px) 0, 100% 14px,
                     100% 100%, 14px 100%, 0 calc(100% - 14px));
  position: relative;
}

/* Top border glow — always on, half intensity */
.card::before {
  content: '';
  position: absolute;
  top: 0; left: 0; right: 0;
  height: 2px;
  background: var(--red);
  box-shadow: var(--glow-r);
  opacity: 0.5;
  transition: opacity 0.25s;
}

.card:hover {
  border-color: var(--red);
  box-shadow: var(--glow-r);
}
.card:hover::before { opacity: 1; }
```

### Form Inputs

```css
.inp {
  background: rgba(255,45,85,0.05);
  border: 1px solid rgba(255,45,85,0.2);
  font-family: var(--f-mono);
  color: var(--t1);
  caret-color: var(--red);
  border-radius: 0;
  padding: 0.6875rem 1rem;
  outline: none;
  transition: border-color 0.2s, box-shadow 0.2s;
}
.inp:focus {
  border-color: var(--red);
  box-shadow: var(--glow-r), inset 0 0 16px rgba(255,45,85,0.05);
}
```

### Nav Bar

```css
.navbar {
  background: var(--s2);
  border-top: 1px solid rgba(255,204,0,0.3);
  box-shadow: 0 -2px 20px rgba(255,204,0,0.08);
}

/* Yellow gradient scan line */
.navbar::before {
  content: '';
  position: absolute;
  top: 0; left: 0; right: 0; height: 1px;
  background: linear-gradient(
    90deg,
    transparent 0%,
    var(--yellow) 30%,
    var(--red) 70%,
    transparent 100%
  );
}

/* Active item */
.nav-item.active { color: var(--red); }
.nav-item.active .icon { filter: drop-shadow(0 0 6px rgba(255,45,85,0.8)); }
```

---

## Motion Principles

- **Fast and sharp** — transitions 150–250ms. Cyberpunk is not gentle.
- **Scale on hover** — `transform: scale(1.02)` on primary buttons
- **Scale on press** — `transform: scale(0.97)` — never inset/press, just shrink
- **Glow intensification** — primary hover interaction for glowing elements
- **Pulse animations** — status indicators use `opacity: 0.2 → 1` at 1.5–2s

```css
@keyframes pulse-red {
  0%, 100% { opacity: 1; }
  50%       { opacity: 0.2; }
}
.status-dot { animation: pulse-red 1.5s ease-in-out infinite; }
```

---

## Anti-patterns

| ❌ Don't | ✓ Do instead |
|----------|-------------|
| Round corners on cards/buttons | `clip-path` angular cuts |
| Use `border-radius > 4px` on containers | `var(--r-sm)` or `var(--r-md)` max |
| White or light backgrounds | Always dark (`--bg` to `--s3`) |
| Soft drop shadows | Neon glow via `box-shadow` |
| Mix neon colors randomly | Each color has a semantic role |
| Use rounded typefaces | Bebas Neue / Rajdhani / Share Tech Mono only |
| Soft motion / elastic spring | Fast, deliberate, aggressive transitions |
| Clean UI sans context | Add monospace data labels everywhere |

---

## AI Prompting Guide

When prompting AI to generate in this style:

```
Design in the Cyberpunk / Blade Runner 2049 UI aesthetic.

Key requirements:
- Dark near-black backgrounds (#0a0a0f, #0e0e16)  
- Neon red (#ff2d55) as primary accent with glow effect
- Clipped angular corners using clip-path polygon — NO border-radius on cards
- Scanline overlay on body
- Three-font system: Bebas Neue (display/headings), Rajdhani (body), Share Tech Mono (data/captions)
- Red = danger/execute, Yellow = caution, Cyan = data/network, Purple = vice
- All buttons uppercase, Bebas Neue, letter-spacing 0.2em
- Form inputs use Share Tech Mono, red caret, red border on focus
- Cards have subtle red top border that intensifies on hover
- HUD panels with monospace labels and data readouts
- Neon glow: box-shadow 0 0 10px rgba(255,45,85,0.6), 0 0 24px rgba(255,45,85,0.3)
- Dense layout — this is urban UI, pack information in
- Section numbers as ghost Bebas Neue text at rgba opacity
```

---

## Color Quick Reference

```
#0a0a0f  void
#0e0e16  surface
#14141e  raised
#1a1a28  elevated
#ff2d55  red / danger ████
#ffcc00  yellow / caution ████
#a020f0  purple / vice ████
#00d4ff  cyan / data ████
#f0e8ff  text primary
```

---

*Blade Runner 2049 (2017) · Cyberpunk 2077 (2020) · AKIRA (1988)*  
*"The street finds its own uses for things."*
