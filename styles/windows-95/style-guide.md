# Windows 95 · Style Guide

**Personality:** Beveled. Teal. Precise. Nostalgic. Microsoft.

---

## Identity

Windows 95 is the design language that shipped 400 million desktops between 1995–2001. It is defined by one mechanical trick — a 4-shadow bevel system that creates the illusion of physical depth on flat 2D screens. There are no gradients (except the title bar), no transparency, no softness, no curves. Everything is hard-edged, gray, and precise.

This is not retro decoration. It is a complete, coherent design system built under extreme constraints: 256-color displays, CRT monitors, low resolution, no GPU. Every decision was load-bearing.

---

## Design Tokens

```css
:root {
  --desktop:   #008080;   /* teal desktop */
  --chrome:    #c0c0c0;   /* Windows gray — the universal surface */
  --chrome-hi: #ffffff;   /* highlight face (top-left bevel) */
  --chrome-lo: #808080;   /* shadow face (inner bottom-right bevel) */
  --chrome-dk: #000000;   /* dark shadow (outer bottom-right bevel) */
  --navy:      #000080;   /* title bar gradient start */
  --navy-hi:   #1084d0;   /* title bar gradient end */
  --t1:        #000000;   /* primary text */
  --t2:        #333333;   /* secondary text */
  --t-inv:     #ffffff;   /* inverse text (on navy title bars) */
  --ac:        #000080;   /* accent / interactive blue */
  --ac-hi:     #1084d0;
  --f:         'MS Sans Serif', 'Arial', sans-serif;
  --f-px:      'Courier New', monospace;

  /* THE BEVEL SYSTEM — derive all depth from these */
  --bevel-out: inset -1px -1px 0 var(--chrome-dk),
               inset  1px  1px 0 var(--chrome-hi),
               inset -2px -2px 0 var(--chrome-lo),
               inset  2px  2px 0 var(--chrome);

  --bevel-in:  inset  1px  1px 0 var(--chrome-dk),
               inset -1px -1px 0 var(--chrome-hi),
               inset  2px  2px 0 var(--chrome-lo),
               inset -2px -2px 0 var(--chrome);
}

/* ENFORCE ZERO CURVES — non-negotiable */
*, *::before, *::after { border-radius: 0 !important; }

body {
  background: var(--desktop);   /* teal everywhere */
  font-family: var(--f);
  font-size: 11px;               /* 8pt at 96dpi */
  color: var(--t1);
}
```

---

## The Bevel System — The One Trick

The entire Windows 95 UI is derived from four inset box-shadow values. Swap their axis position to flip between raised and sunken.

### Raised (buttons, panels, window frames, dialog borders)
```
white  → top + left (outer edge highlight)
chrome → top + left (inner edge, 2px)
gray   → bottom + right (inner edge, 2px)
black  → bottom + right (outer edge)
```
```css
box-shadow: inset -1px -1px 0 #000000,   /* black  · outer BR corner */
            inset  1px  1px 0 #ffffff,   /* white  · outer TL corner */
            inset -2px -2px 0 #808080,   /* gray   · inner BR */
            inset  2px  2px 0 #c0c0c0;  /* chrome · inner TL */
```

### Sunken (inputs, inset panels, active/pressed states)
```
black  → top + left (outer edge shadow)
gray   → top + left (inner edge, 2px)
chrome → bottom + right (inner edge, 2px)
white  → bottom + right (outer edge highlight)
```
```css
box-shadow: inset  1px  1px 0 #000000,  /* black  · inner TL corner */
            inset -1px -1px 0 #ffffff,  /* white  · inner BR corner */
            inset  2px  2px 0 #808080,  /* gray   · inner TL */
            inset -2px -2px 0 #c0c0c0; /* chrome · inner BR */
```

### The mental model
- **Light source is top-left**. The TL face is always bright; the BR face is always dark.
- **Raised** = light TL, dark BR. The element pops toward you.
- **Sunken** = dark TL, light BR. The element recedes away from you.
- **Press state** = swap `bevel-out` for `bevel-in`. That's it. No color change.

---

## Window Chrome Recipe

Every window, dialog, and card follows this exact structure:

```html
<div class="win95-window">
  <!-- 1. Window border: bevel-out, padding: 2px -->

  <div class="win95-titlebar">
    <!-- Navy gradient, 18px tall, white bold 11px text -->
    <!-- Icon · Title text (left) | Min □ Max ✕ (right) -->
    <div class="win95-title-text">🗔 Window Title</div>
    <div class="win95-win-btns">
      <button>─</button>   <!-- minimize: horizontal bar -->
      <button>□</button>   <!-- maximize: square outline -->
      <button>✕</button>   <!-- close: × -->
    </div>
  </div>

  <div class="win95-menubar">
    <!-- 11px, bevel-out separator line at bottom -->
    <span>File</span><span>Edit</span><span>View</span><span>Help</span>
  </div>

  <div class="win95-content">
    <!-- Main window content -->
  </div>

  <div class="win95-statusbar">
    <!-- Multiple bevel-in panes at bottom -->
    <div class="win95-status-pane">Ready</div>
    <div class="win95-status-pane">128 objects</div>
  </div>
</div>
```

### CSS for window chrome
```css
.win95-window {
  background: #c0c0c0;
  box-shadow: var(--bevel-out);
  padding: 2px;  /* space for bevel border */
}
.win95-titlebar {
  background: linear-gradient(to right, #000080 0%, #1084d0 100%);
  height: 18px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 2px 2px 2px 4px;
}
.win95-title-text {
  color: #ffffff;
  font-weight: bold;
  font-size: 11px;
  display: flex;
  align-items: center;
  gap: 4px;
}
.win95-win-btn {
  width: 16px;
  height: 14px;
  background: #c0c0c0;
  box-shadow: var(--bevel-out);
  border: none;
  font-size: 8px;
  cursor: pointer;
}
.win95-win-btn:active { box-shadow: var(--bevel-in); }
```

---

## Taskbar Implementation

```html
<div class="taskbar">
  <!-- Start button: bevel-out, bold, Windows logo -->
  <button class="start-btn">
    <span>⊞</span> <strong>Start</strong>
  </button>

  <!-- Vertical separator -->
  <div class="taskbar-sep"></div>

  <!-- Active program buttons -->
  <div class="taskbar-items">
    <button class="tb-item active">🖥️ My Document</button>
    <button class="tb-item">📁 Explorer</button>
  </div>

  <!-- System tray (right) -->
  <div class="taskbar-tray">
    <span>🌐</span>
    <span>🔊</span>
    <span class="tb-clock" id="tb-clock">9:14 PM</span>
  </div>
</div>
```

```css
.taskbar {
  position: fixed;
  bottom: 0; left: 0; right: 0;
  height: 28px;
  background: #c0c0c0;
  border-top: 1px solid #000;
  box-shadow: inset 0 1px 0 #ffffff;
  display: flex;
  align-items: center;
  gap: 2px;
  padding: 2px;
  z-index: 200;
}
.start-btn {
  height: 22px;
  padding: 2px 8px;
  font-weight: bold;
  box-shadow: var(--bevel-out);
}
.tb-item {
  height: 22px;
  box-shadow: var(--bevel-out);
  max-width: 160px;
  overflow: hidden;
  white-space: nowrap;
}
.tb-item.active { box-shadow: var(--bevel-in); }  /* pressed = active */
.taskbar-tray {
  box-shadow: var(--bevel-in);
  padding: 2px 6px;
  height: 22px;
}
```

```js
// Live clock
function updateClock() {
  document.getElementById('tb-clock').textContent =
    new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });
}
updateClock();
setInterval(updateClock, 5000);
```

---

## Component Recipes

### Button
```css
.win95-btn {
  background: #c0c0c0;
  box-shadow: var(--bevel-out);
  border: none;
  padding: 4px 10px;
  font-family: 'MS Sans Serif', Arial, sans-serif;
  font-size: 11px;
  min-width: 75px;     /* Win95 standard button width */
  cursor: pointer;
}
.win95-btn:active { box-shadow: var(--bevel-in); }
.win95-btn:disabled { color: #808080; }

/* Default button (the one triggered by Enter) */
.win95-btn-primary {
  outline: 1px dotted #000;
  outline-offset: -4px;
}
```

### Text Input
```css
.win95-input {
  background: white;
  box-shadow: var(--bevel-in);    /* sunken = "a hole you type into" */
  border: none;
  padding: 2px 4px;
  font-family: 'MS Sans Serif', Arial, sans-serif;
  font-size: 11px;
  outline: none;
}
.win95-input:focus {
  outline: 1px dotted #000;
  outline-offset: -3px;
}
```

### Select / Combobox
A white bevel-in input with a separate bevel-out arrow button attached to the right:
```html
<div style="position:relative;display:inline-flex">
  <select style="background:white;box-shadow:var(--bevel-in);padding-right:20px;appearance:none">…</select>
  <div style="position:absolute;right:0;top:0;bottom:0;width:17px;background:#c0c0c0;box-shadow:var(--bevel-out);display:flex;align-items:center;justify-content:center;font-size:7px">▼</div>
</div>
```

### Checkbox (Win95 style)
```css
/* 13×13 bevel-in white square, ✓ appears on checked */
.win95-chk-box {
  width: 13px;
  height: 13px;
  background: white;
  box-shadow: var(--bevel-in);
  display: flex;
  align-items: center;
  justify-content: center;
}
/* Pair with hidden <input type="checkbox"> and show .chk-mark on :checked */
input:checked + .win95-chk-box .chk-mark { opacity: 1; }
```

### Radio Button
Same as checkbox but `border-radius: 50%` (the one exception to the zero-radius rule).

### Progress Bar (chunky blocks)
```css
.win95-progress-outer {
  height: 18px;
  background: #c0c0c0;
  box-shadow: var(--bevel-in);
  padding: 2px;
}
.win95-progress-inner {
  height: 100%;
  /* CRITICAL: repeating blocks, not a smooth fill */
  background: repeating-linear-gradient(
    90deg,
    #000080 0px, #000080 14px,    /* navy block */
    #c0c0c0 14px, #c0c0c0 16px   /* chrome gap */
  );
}
```

### Slider
```css
/* Track = bevel-in channel (4px tall) */
/* Thumb = bevel-out widget (11px × 20px) */
input[type=range]::-webkit-slider-runnable-track {
  height: 4px;
  background: white;
  box-shadow: var(--bevel-in);
}
input[type=range]::-webkit-slider-thumb {
  -webkit-appearance: none;
  width: 11px;
  height: 20px;
  background: #c0c0c0;
  box-shadow: var(--bevel-out);
  margin-top: -8px;
}
```

### Scrollbar-style Toggle
Win95 has no toggle component. Simulate one with a scrollbar-style thumb:
```html
<div class="win95-toggle" role="switch" aria-checked="true">
  <div class="win95-toggle-thumb"></div>
</div>
```
```css
.win95-toggle {
  width: 72px; height: 16px;
  background: white;
  box-shadow: var(--bevel-in);
  position: relative;
  cursor: pointer;
}
.win95-toggle-thumb {
  width: 16px; height: 14px;
  background: #c0c0c0;
  box-shadow: var(--bevel-out);
  position: absolute; top: 1px; left: 1px;
  transition: left 0.12s;
}
.win95-toggle[aria-checked="true"] .win95-toggle-thumb { left: 55px; }
```

### Groupbox (form section header)
```css
/* Outer box with bevel-out, title floats above top border */
.win95-groupbox {
  box-shadow: var(--bevel-out);
  padding: 10px 8px 8px;
  position: relative;
}
.win95-groupbox-label {
  position: absolute;
  top: -7px; left: 8px;
  background: #c0c0c0;   /* matches parent chrome */
  padding: 0 3px;
  font-weight: bold;
}
```

---

## Typography

| Role | Font | Size | Weight | Notes |
|------|------|------|--------|-------|
| Title bar | MS Sans Serif | 8pt (11px) | Bold | White on navy gradient |
| Menu bar | MS Sans Serif | 8pt (11px) | Regular | Hover = navy bg + white text |
| Dialog body | MS Sans Serif | 8pt (11px) | Regular | — |
| Bold label | MS Sans Serif | 8pt (11px) | Bold | Field labels |
| Button | MS Sans Serif | 8pt (11px) | Regular | Inside bevel-out button |
| Status bar | MS Sans Serif | 8pt (11px) | Regular | Gray, bevel-in panes |
| Monospace | Courier New | 10pt (12px) | Regular | File paths, code, LCD |

**Rules:**
- Maximum font size in UI: ~14pt (dialog title only). Body never exceeds 11px.
- No font size variation for emphasis — use **bold** instead.
- No letter-spacing. No line-height beyond 1.4.
- Never use a sans-serif with large x-height or rounded terminals.

---

## Explorer Navigation Pattern

Win95's navigation system is the prototype for every file browser since:

1. **Toolbar**: Icon + text buttons. `bevel-out` at rest → `bevel-in` on press.
2. **Address bar**: `bevel-in` input + `bevel-out` Go button.
3. **Split pane**: Left = tree (folders), right = files. Both bevel-in white areas.
4. **Selection**: Navy background (#000080) + white text. No highlight color.
5. **Status bar**: Bottom panes showing selection count and total.

---

## Anti-Patterns

These will immediately break the Win95 illusion:

| ❌ Wrong | ✅ Correct |
|----------|-----------|
| `border-radius: 4px` | `border-radius: 0 !important` |
| `box-shadow: 0 2px 8px rgba(0,0,0,0.2)` | `box-shadow: var(--bevel-out)` |
| Smooth progress fill | Chunky `repeating-linear-gradient` blocks |
| `transition: all 0.3s ease` on buttons | No transition — instant press feel |
| Large fonts (18px+) | Maximum 11px for body, 13px for titles |
| Drop shadows on windows | Windows float on desktop with bevel-out only |
| Blue/purple/teal accent colors | #000080 navy for selections only |
| Rounded checkboxes/radio with fill | Square/circle bevel-in with thin ✓ mark |

---

## AI Prompting Guidance

Use this style guide with any AI code generator. Key phrases that enforce Win95 accuracy:

### Core constraints
```
"Windows 95 design system. Zero border-radius anywhere.
All depth via 4-value inset box-shadow bevel system only.
--bevel-out for raised elements, --bevel-in for sunken inputs.
Background #c0c0c0 chrome, #008080 teal desktop.
Font: MS Sans Serif or Arial at 11px. Nothing larger than 13px."
```

### For buttons
```
"Win95 button: background #c0c0c0, box-shadow var(--bevel-out), min-width 75px.
On :active swap to box-shadow var(--bevel-in). No color change. No animation."
```

### For progress bars
```
"Chunky block progress bar. Use repeating-linear-gradient(90deg,
#000080 0px, #000080 14px, #c0c0c0 14px, #c0c0c0 16px).
NOT a smooth fill. Block size 14px wide, 2px gap."
```

### For windows/dialogs
```
"Win95 window: background #c0c0c0, box-shadow bevel-out, padding 2px.
Title bar: linear-gradient(to right, #000080, #1084d0), height 18px.
Title text: white bold 11px. Control buttons: 16×14px bevel-out gray squares."
```

### For the taskbar
```
"Win95 taskbar: fixed bottom, height 28px, background #c0c0c0.
Start button: bevel-out with ⊞ logo. Active window: bevel-in (pressed).
System tray: bevel-in pane. Clock: updates via new Date().toLocaleTimeString()."
```

---

## Historical Context

- **Released**: August 24, 1995
- **Display target**: 640×480 to 1024×768, 256-color SVGA, CRT monitors
- **Font rendering**: Bitmap (no antialiasing at 96dpi)
- **RAM**: 4MB minimum, 8MB recommended
- **Designed by**: Microsoft UE (User Education) team, influenced by the Chicago project
- **Successor**: Windows XP (2001) — introduced Luna theme with soft gradients
- **Legacy**: The bevel system influenced every GUI toolkit through 2001 and remains instantly recognizable

---

*Style guide version 1.0 · Windows 95 · UI Styles Gallery · MyClaw/seaMYK*
