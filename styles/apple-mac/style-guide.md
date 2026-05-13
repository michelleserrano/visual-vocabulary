# Classic Mac — Style Guide

**Personality:** Nostalgic. Pixel-precise. Grayscale. Beveled. Functional.

> "A computer for the rest of us." — Steve Jobs, 1984
>
> The Classic Mac aesthetic is a design system of pure constraint: one background color, one border color, one type family, and a bevel recipe built from four inset shadows. Every affordance is legible at 72 DPI. Someone who grew up on System 7 should have a visceral nostalgic reaction.

---

## 1. Design Tokens

```css
:root {
  --bg:        #d4d4d4;  /* Classic System gray — the desktop */
  --bg-white:  #ffffff;  /* Content area fill */
  --bg-dark:   #555555;  /* Shadow / dark bevel */
  --bg-darker: #333333;  /* Deep shadow */
  --t1:        #000000;  /* Primary text + borders */
  --t2:        #333333;  /* Secondary text */
  --t3:        #666666;  /* Disabled / caption */
  --t-inv:     #ffffff;  /* Text on inverted/black backgrounds */
  --r:         0px;      /* Classic Mac: NO border radius */
  --r-dialog:  4px;      /* Dialog corners only — rare */

  /* Typography */
  --f:    'Chicago', 'Charcoal', Geneva, Helvetica, system-ui, monospace;
  --f-sm: Geneva, 'Helvetica Neue', Helvetica, system-ui, sans-serif;

  /* Bevel system — see Section 3 */
  --bevel-btn:      inset -1px -1px #000, inset 1px 1px #fff,
                    inset -2px -2px #888, inset 2px 2px #e0e0e0;
  --bevel-btn-down: inset 1px 1px #000, inset -1px -1px #fff,
                    inset 2px 2px #888, inset -2px -2px #e0e0e0;
  --bevel-panel:    inset -1px -1px #888, inset 1px 1px #fff;

  /* Interactions are instant — no easing */
  --ease: steps(1);
}

body {
  font-family: var(--f);
  background: var(--bg);
  color: var(--t1);
  -webkit-font-smoothing: none;  /* Preserve pixel-crisp rendering */
}
```

---

## 2. Color Palette

The Classic Mac palette was 4-bit: **16 shades of gray**. There is no accent color. Black on white is the default — maximum contrast is built in.

| Token | Hex | Role |
|---|---|---|
| `--bg` | `#d4d4d4` | Desktop background — everywhere |
| `--bg-white` | `#ffffff` | Content area (document windows) |
| `--bg-dark` | `#555555` | Shadow, dark bevel edge |
| `--bg-darker` | `#333333` | Deep shadow, drop shadow |
| `--t1` | `#000000` | All borders, primary text |
| `--t2` | `#333333` | Secondary text |
| `--t3` | `#666666` | Disabled, captions |
| `--t-inv` | `#ffffff` | Text on inverted (black) surfaces |
| bevel-dark | `#888888` | Mid bevel (inner-outer dark) |
| bevel-light | `#e0e0e0` | Mid bevel (inner-outer light) |
| titlebar-end | `#bbbbbb` | End of titlebar gradient |
| divider | `#cccccc` | Separator lines in lists |

---

## 3. The Bevel System

The entire 3D depth system is created by **four inset box-shadows**. Light source is top-left.

### Button — raised state
```css
box-shadow:
  inset -1px -1px #000,    /* outer dark edge: bottom + right */
  inset  1px  1px #fff,    /* outer light edge: top + left */
  inset -2px -2px #888,    /* inner dark: bottom + right */
  inset  2px  2px #e0e0e0; /* inner light: top + left */
```

### Button — pressed state (flip all shadows)
```css
box-shadow:
  inset  1px  1px #000,
  inset -1px -1px #fff,
  inset  2px  2px #888,
  inset -2px -2px #e0e0e0;
```

### Default button (dialog accept — double border)
```css
box-shadow:
  inset 0 0 0 2px #000,   /* bold double border */
  inset -1px -1px #000, inset 1px 1px #fff,
  inset -2px -2px #888, inset 2px 2px #e0e0e0;
```

### Panel / inset surface
```css
box-shadow:
  inset -1px -1px #888,
  inset  1px  1px #fff;
```

### Window drop shadow
```css
box-shadow: 2px 2px 0 #888, 3px 3px 0 #555;
```

---

## 4. Window Chrome CSS Recipe

Every window on the desktop uses this chrome:

```css
.mac-window {
  border: 1px solid #000;
  background: #fff;
  box-shadow: 2px 2px 0 #888, 3px 3px 0 #555;
}

.mac-titlebar {
  height: 20px;
  background: linear-gradient(180deg, #fff 0%, #bbb 100%);
  border-bottom: 1px solid #000;
  display: flex;
  align-items: center;
  padding: 0 4px;
  gap: 4px;
  position: relative;
  overflow: hidden;
}

/* Horizontal drag stripes behind the title */
.mac-titlebar::before {
  content: '';
  position: absolute;
  left: 22px; right: 4px; top: 0; bottom: 0;
  background: repeating-linear-gradient(
    180deg,
    transparent 0px, transparent 1px,
    rgba(0,0,0,0.12) 1px, rgba(0,0,0,0.12) 2px
  );
  pointer-events: none;
}

.mac-closebox {
  width: 13px; height: 13px;
  border: 1px solid #000;
  background: #d4d4d4;
  box-shadow: inset -1px -1px #000, inset 1px 1px #fff,
              inset -2px -2px #888, inset 2px 2px #e0e0e0;
  display: flex; align-items: center; justify-content: center;
  cursor: pointer; font-size: 7px;
}
.mac-closebox:hover::after { content: '✕'; }
.mac-closebox:active {
  box-shadow: inset 1px 1px #000, inset -1px -1px #fff,
              inset 2px 2px #888, inset -2px -2px #e0e0e0;
}

/* Title — centered, with a background mask over the stripes */
.mac-title-text {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  font-size: 11px;
  font-weight: bold;
  font-family: Geneva, Helvetica, sans-serif;
  white-space: nowrap;
  z-index: 1;
  background: linear-gradient(180deg, #fff 0%, #bbb 100%);
  padding: 0 6px;
}
```

---

## 5. Typography

```css
/* Display — titles, hero */
.ts-72pt { font-size: 72px; font-family: var(--f); line-height: 1; }
.ts-48pt { font-size: 48px; font-family: var(--f); }
.ts-36pt { font-size: 36px; font-family: var(--f); }
.ts-24pt { font-size: 24px; font-family: var(--f); }

/* UI text — labels, body */
.ts-18pt { font-size: 18px; font-family: var(--f-sm); }
.ts-14pt { font-size: 14px; font-family: var(--f-sm); }
.ts-12pt { font-size: 12px; font-family: var(--f-sm); }  /* standard UI */
.ts-10pt { font-size: 10px; font-family: var(--f-sm); }
.ts-9pt  { font-size:  9px; font-family: var(--f-sm); }  /* smallest legible */
```

**Rules:**
- Disable anti-aliasing with `-webkit-font-smoothing: none`
- `Chicago` for display (large sizes only)
- `Geneva` for all UI labels, body, captions
- Never go below 9pt (9px)
- Bold for all labels and button text

---

## 6. Component Recipes

### Button
```css
.btn {
  background: #d4d4d4;
  border: 1px solid #000;
  box-shadow: inset -1px -1px #000, inset 1px 1px #fff,
              inset -2px -2px #888, inset 2px 2px #e0e0e0;
  padding: 4px 20px;
  font-family: Geneva, Helvetica, sans-serif;
  font-size: 12px;
  font-weight: bold;
  cursor: pointer;
  min-width: 60px;
  transition: none;
}
.btn:active {
  box-shadow: inset 1px 1px #000, inset -1px -1px #fff,
              inset 2px 2px #888, inset -2px -2px #e0e0e0;
}
```

### Text Input
```css
.inp {
  background: #fff;
  border: 1px solid #000;
  box-shadow: inset 1px 1px #888, inset -1px -1px #e0e0e0;
  padding: 4px 6px;
  font-family: Geneva, Helvetica, sans-serif;
  font-size: 12px;
  border-radius: 0;
  outline: none;
}
.inp:focus { outline: 2px solid #000; outline-offset: 1px; }
```

### Checkbox (square, ✓ mark)
```css
.chk-box {
  width: 14px; height: 14px;
  background: #fff;
  border: 1px solid #555;
  display: flex; align-items: center; justify-content: center;
  font-size: 10px;
}
/* Show ✓ when :checked — use the hidden input + adjacent sibling technique */
```

### Radio Button (circle with dot)
```css
.rad-box {
  width: 14px; height: 14px;
  background: #fff;
  border: 1px solid #555;
  border-radius: 50%;
  display: flex; align-items: center; justify-content: center;
}
.rad-dot {
  width: 6px; height: 6px;
  background: #000;
  border-radius: 50%;
  display: none; /* shown when :checked */
}
```

### Popup Menu (Select)
```css
.sel {
  -webkit-appearance: none;
  background: #d4d4d4 url("▾ triangle SVG") no-repeat right 6px center;
  border: 1px solid #000;
  box-shadow: inset -1px -1px #000, inset 1px 1px #fff,
              inset -2px -2px #888, inset 2px 2px #e0e0e0;
  padding: 4px 22px 4px 6px;
  font-family: Geneva, Helvetica, sans-serif;
  font-size: 12px;
  border-radius: 0;
}
```

---

## 7. Mac Menu Bar

```css
.topnav {
  position: sticky; top: 0; z-index: 100;
  background: #fff;
  border-bottom: 1px solid #000;
  height: 20px;
  display: flex; align-items: center;
  padding: 0 8px;
  font-family: Geneva, Helvetica, sans-serif;
  font-size: 12px; font-weight: bold;
  user-select: none;
}
/* Apple logo: &#63743; */
/* Menu items hover: background: #000; color: #fff; */
```

---

## 8. AI Prompting Guidance

Use these tokens when prompting an AI to generate Classic Mac UI:

**Style descriptors:**
- "Apple System 7 / Mac OS 8 era interface"
- "Classic Mac grayscale UI, 1-bit pixel-perfect"
- "Beveled 3D buttons with inset box-shadows, no border radius"
- "Window chrome with gradient titlebar from white to #bbb"
- "Black 1px borders on everything"
- "Chicago font for display, Geneva for body"
- "Gray #d4d4d4 desktop background"

**Anti-patterns to reject:**
- ❌ Rounded corners (except 4px on dialogs)
- ❌ Color (this is grayscale — no blue, no purple, no gradients with color)
- ❌ Smooth transitions or easing (Classic Mac = instant feedback, `steps(1)`)
- ❌ Drop shadows with blur radius (use `0px` blur, hard pixel shadows)
- ❌ Anti-aliased fonts (use `-webkit-font-smoothing: none`)
- ❌ Sans-serif fonts other than Geneva / Helvetica / Chicago

**Example prompt:**
> "Generate a Classic Mac System 7 style dialog box. Gray #d4d4d4 background. 1px solid #000 border. Window chrome with gradient titlebar (white → #bbb). Chicago 12px bold title. Bevel button with four inset box-shadows: inset -1px -1px #000, inset 1px 1px #fff, inset -2px -2px #888, inset 2px 2px #e0e0e0. No border radius. No color. No transitions. Default OK button has double border: inset 0 0 0 2px #000 plus bevel."

---

## 9. Quick Reference

| Property | Value |
|---|---|
| Desktop bg | `#d4d4d4` |
| Content bg | `#ffffff` |
| Borders | `1px solid #000` |
| Button bevel | 4-shadow inset recipe |
| Titlebar | `linear-gradient(180deg, #fff, #bbb)` |
| Title font | Chicago 11px bold |
| Body font | Geneva 12px |
| Interactions | `transition: none` — instant |
| Border radius | `0px` (dialogs: `4px`) |
| Drop shadow | `2px 2px 0 #888, 3px 3px 0 #555` |
| Font smoothing | `-webkit-font-smoothing: none` |

---

*Classic Mac — UI Styles Gallery · seaMYK*
