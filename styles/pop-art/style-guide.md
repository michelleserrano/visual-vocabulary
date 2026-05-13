# Pop Art UI Style Guide

**Personality: Loud. Halftone. Comic. Cultural. Ironic.**

Roy Lichtenstein as a web designer. Andy Warhol as a product manager. Everything is PRODUCT. Every label is an advertisement. The border is thick because Lichtenstein's border was thick. The shadow is sharp because comic book printers couldn't afford blur.

---

## Design Tokens

```css
:root {
  --bg:    #f7e500;    /* Warhol yellow — loud, pop-culture loud */
  --bg-alt:#f5f5f5;    /* white for card interiors */
  --t1:    #000000;    /* pure black — Lichtenstein's outline */
  --t2:    #1a1a1a;
  --t3:    #555555;
  --red:   #e8261d;    /* pop red — Coca-Cola, fire trucks, urgency */
  --blue:  #003087;    /* pop blue — Pepsi, sky, authority */
  --cyan:  #00b4d8;    /* comic book highlight — lens flares */
  --pink:  #ff69b4;    /* Warhol pink — Marilyn, glamour, irony */
  --green: #00a651;    /* money green — dollar bills, envy */
  --ac:    #e8261d;    /* red is primary accent */
  --r:     0px;        /* NO radius — comic book has hard edges */
  --f-disp: 'Bangers', Impact, 'Arial Black', sans-serif;
  --f:     'Comic Neue', 'Arial', sans-serif;
  --ease:  cubic-bezier(0.4,0,0.2,1);
  /* Core shadow system — no blur, all offset */
  --border:      3px solid #000;
  --shadow:      5px 5px 0 #000;
  --shadow-hover:8px 8px 0 #000;
  --shadow-press:2px 2px 0 #000;
  --shadow-lg:   7px 7px 0 #000;
}
/* HARD RULE: no border-radius anywhere */
*, *::before, *::after { border-radius: 0 !important; }
```

---

## Google Fonts

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Bangers&family=Comic+Neue:ital,wght@0,300;0,400;0,700;1,400&display=swap" rel="stylesheet">
```

---

## Halftone Dot Patterns (5 variations)

Ben-Day dots are THE signature of Pop Art. Invented by Benjamin Day in 1879 as a cheap mechanical printing process, Lichtenstein elevated them into fine art. Every background can have them.

```css
/* 1. Black dots — general use, low opacity */
.halftone-bg {
  background-image: radial-gradient(circle, rgba(0,0,0,0.18) 25%, transparent 25%);
  background-size: 6px 6px;
}

/* 2. Red dots — card headers, danger panels */
.halftone-red {
  background-image: radial-gradient(circle, rgba(232,38,29,0.28) 25%, transparent 25%);
  background-size: 5px 5px;
}

/* 3. Blue dots — blue surfaces, authority panels */
.halftone-blue {
  background-image: radial-gradient(circle, rgba(0,48,135,0.22) 25%, transparent 25%);
  background-size: 6px 6px;
}

/* 4. Yellow dots — white surfaces to add warmth */
.halftone-yellow {
  background-image: radial-gradient(circle, rgba(247,229,0,0.5) 25%, transparent 25%);
  background-size: 5px 5px;
}

/* 5. Pink dots — Warhol surfaces, glamour sections */
.halftone-pink {
  background-image: radial-gradient(circle, rgba(255,105,180,0.35) 25%, transparent 25%);
  background-size: 5px 5px;
}

/* Dense dots — large headers, hero backgrounds */
.halftone-dense {
  background-image: radial-gradient(circle, rgba(0,0,0,0.15) 35%, transparent 35%);
  background-size: 4px 4px;
}
```

### Usage guidelines
- Card headers: always use a halftone pattern over the solid color
- Spec callouts: `halftone-yellow` over white background
- Hero sections: `halftone-bg` at reduced opacity
- Never use halftones on body text areas — it kills legibility
- Combine with `position: relative; overflow: hidden` container

---

## Offset Shadow System

The comic book panel shadow is what makes everything look like it was screen-printed and cut out.

```css
/* The rule: box-shadow with NO blur, full color, offset */
.panel-sm  { box-shadow: 3px 3px 0 #000; }
.panel-md  { box-shadow: 5px 5px 0 #000; }   /* default */
.panel-lg  { box-shadow: 7px 7px 0 #000; }
.panel-xl  { box-shadow: 10px 10px 0 #000; }

/* Hover state — always grow the shadow AND translate element */
.panel-hover:hover {
  box-shadow: 8px 8px 0 #000;
  transform: translate(-2px, -2px);  /* shifts element to grow shadow */
  transition: box-shadow 0.1s, transform 0.1s;
}

/* Press state — collapse the shadow */
.panel-press:active {
  box-shadow: 2px 2px 0 #000;
  transform: translate(3px, 3px);
}

/* Colored shadows — for colored elements */
.panel-red   { box-shadow: 5px 5px 0 var(--red); }
.panel-blue  { box-shadow: 5px 5px 0 var(--blue); }
.panel-pink  { box-shadow: 5px 5px 0 var(--pink); }

/* NEVER use: blur, spread, inset for the main pop shadow */
/* WRONG: box-shadow: 0 4px 16px rgba(0,0,0,0.2); */
/* RIGHT: box-shadow: 5px 5px 0 #000;              */
```

---

## Speech Bubble CSS

Lichtenstein's speech bubbles are the most recognizable element of Pop Art UI.

```css
/* Rectangular speech bubble — pointing down-left */
.speech-bubble {
  position: relative;
  background: white;
  border: 3px solid black;
  padding: 12px 16px;
  display: inline-block;
}
.speech-bubble::after {   /* outer triangle (black) */
  content: '';
  position: absolute;
  bottom: -18px;
  left: 22px;
  border: 9px solid transparent;
  border-top-color: #000;
}
.speech-bubble::before {  /* inner triangle (white fill) */
  content: '';
  position: absolute;
  bottom: -12px;
  left: 24px;
  border: 7px solid transparent;
  border-top-color: white;
  z-index: 1;
}

/* Thought bubble variant */
.thought-bubble {
  position: relative;
  background: white;
  border: 3px solid black;
  padding: 12px 16px;
}
.thought-bubble::after {
  content: '• • •';
  position: absolute;
  bottom: -24px;
  left: 16px;
  font-size: 0.5rem;
  color: black;
  letter-spacing: 2px;
}

/* Exclamatory bubble — Bangers font, red text */
.shout-bubble {
  background: var(--bg);
  border: 3px solid black;
  padding: 8px 16px;
  font-family: var(--f-disp);
  font-size: 1.5rem;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: var(--red);
  transform: rotate(-4deg);
  box-shadow: 3px 3px 0 black;
  display: inline-block;
}
```

---

## Typography System

```css
/* Display — Bangers, LOUD, uppercase */
.text-display {
  font-family: 'Bangers', Impact, sans-serif;
  font-size: clamp(3rem, 10vw, 6rem);
  letter-spacing: 0.1em;
  text-transform: uppercase;
  line-height: 0.95;
  -webkit-text-stroke: 2px #000;  /* Lichtenstein outline on large text */
}

/* Headings — all Bangers */
h1 { font-family: 'Bangers'; font-size: 2.5rem; letter-spacing: 0.08em; text-transform: uppercase; }
h2 { font-family: 'Bangers'; font-size: 2rem;   letter-spacing: 0.08em; text-transform: uppercase; }
h3 { font-family: 'Bangers'; font-size: 1.5rem; letter-spacing: 0.07em; text-transform: uppercase; }
h4 { font-family: 'Bangers'; font-size: 1.25rem;letter-spacing: 0.06em; text-transform: uppercase; }

/* Body — Comic Neue */
body { font-family: 'Comic Neue', Arial, sans-serif; font-size: 1rem; line-height: 1.55; }

/* Metadata — Bangers, small */
.meta { font-family: 'Bangers'; font-size: 0.75rem; letter-spacing: 0.1em; text-transform: uppercase; }
```

---

## Button System

```css
.btn {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.7rem 1.6rem;
  background: var(--red);
  color: white;
  border: 3px solid #000;
  box-shadow: 5px 5px 0 #000;
  font-family: 'Bangers', sans-serif;
  font-size: 1rem;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  cursor: pointer;
  transition: box-shadow 0.1s, transform 0.1s;
}
.btn:hover {
  box-shadow: 8px 8px 0 #000;
  transform: translate(-2px, -2px);
}
.btn:active {
  box-shadow: 2px 2px 0 #000;
  transform: translate(3px, 3px);
}
.btn:disabled { opacity: 0.35; cursor: not-allowed; box-shadow: none; }

/* Color variants */
.btn-blue  { background: var(--blue); }
.btn-pink  { background: var(--pink); }
.btn-white { background: white; color: #000; }
.btn-black { background: #000; color: var(--bg); }
```

---

## Form Inputs

```css
/* Text input */
.inp {
  background: white;
  border: 3px solid #000;
  padding: 0.75rem 1rem;
  font-family: 'Comic Neue', sans-serif;
  font-size: 0.9375rem;
  color: #000;
  box-shadow: 3px 3px 0 #000;
  outline: none;
  width: 100%;
}
.inp:focus { border-color: var(--red); box-shadow: 4px 4px 0 var(--red); }

/* Label — always Bangers, uppercase */
.label {
  font-family: 'Bangers', sans-serif;
  font-size: 0.875rem;
  letter-spacing: 0.1em;
  text-transform: uppercase;
}

/* Checkbox — 26px, red when checked */
.chk-box {
  width: 26px; height: 26px;
  background: white;
  border: 3px solid #000;
  box-shadow: 3px 3px 0 #000;
}
input:checked + .chk-box { background: var(--red); }

/* Toggle — rectangular, red when on */
.tgl-track {
  width: 56px; height: 26px;
  background: white;
  border: 3px solid #000;
  box-shadow: 3px 3px 0 #000;
}
input:checked ~ .tgl-track { background: var(--red); }
.tgl-thumb {
  width: 17px; height: 17px;
  background: #000;
  position: absolute;
  top: 3px; left: 3px;
}
input:checked ~ .tgl-track .tgl-thumb {
  transform: translateX(28px);
  background: white;
}
```

---

## Card System

```css
.card {
  background: white;
  border: 3px solid #000;
  box-shadow: 7px 7px 0 #000;
  overflow: hidden;
  transition: box-shadow 0.1s, transform 0.1s;
}
.card:hover {
  box-shadow: 10px 10px 0 #000;
  transform: translate(-3px, -3px);
}

/* Card header — halftone + solid color */
.card-header {
  height: 130px;
  background: var(--red);
  background-image: radial-gradient(circle, rgba(0,0,0,0.18) 25%, transparent 25%);
  background-size: 6px 6px;
  border-bottom: 3px solid #000;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* Card title — Bangers, uppercase */
.card-title {
  font-family: 'Bangers', sans-serif;
  font-size: 1.25rem;
  letter-spacing: 0.06em;
  text-transform: uppercase;
}

/* Card action button */
.card-cta {
  background: #000;
  color: var(--bg);
  border: none;
  padding: 0.35rem 0.875rem;
  font-family: 'Bangers', sans-serif;
  font-size: 0.75rem;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  cursor: pointer;
}
.card-cta:hover { background: var(--red); }
```

---

## Range Sliders

```css
.rng {
  -webkit-appearance: none;
  height: 12px;
  background: white;
  border: 3px solid #000;
  outline: none;
  cursor: pointer;
}
.rng::-webkit-slider-thumb {
  -webkit-appearance: none;
  width: 24px; height: 24px;
  background: var(--red);
  border: 3px solid white;
  outline: 3px solid #000;
  cursor: pointer;
}
/* Hover: change thumb color */
.rng::-webkit-slider-thumb:hover { background: var(--blue); }
```

---

## Bottom Navigation

```css
.pop-navbar {
  display: flex;
  border-top: 3px solid #000;
  background: white;
}
.nav-item {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 0.75rem 0.5rem;
  border-right: 2px solid #000;
  cursor: pointer;
  font-family: 'Bangers', sans-serif;
  font-size: 0.6rem;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  background: none;
  border-bottom: none;
  transition: background 0.1s;
}
.nav-item:last-child { border-right: none; }
.nav-item:hover { background: var(--bg); }
.nav-item.active { background: var(--red); color: white; }
```

---

## Action Words

Pop Art UI must have action words. Rotate them slightly. Make them LOUD.

```css
.action-word {
  display: inline-block;
  font-family: 'Bangers', sans-serif;
  font-size: 0.875rem;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: white;
  background: var(--blue);
  border: 2px solid #000;
  padding: 0.15rem 0.5rem;
  transform: rotate(-3deg);
  box-shadow: 2px 2px 0 #000;
}
/* Variants */
.aw-red  { background: var(--red); transform: rotate(-4deg); }
.aw-pink { background: var(--pink); transform: rotate(2deg); }
.aw-cyan { background: var(--cyan); color: #000; transform: rotate(-2deg); }
```

**The canon:** POW! · ZAP! · BAM! · KA-POW! · WHAM! · ZOK! · BLAM! · SPLAT! · CRUNCH!

---

## Starburst Shape

```css
.starburst {
  clip-path: polygon(
    50% 0%, 61% 20%, 79% 9%, 78% 30%, 100% 29%,
    87% 46%, 100% 63%, 78% 62%, 79% 83%, 61% 72%,
    50% 91%, 39% 72%, 21% 83%, 22% 62%, 0% 63%,
    13% 46%, 0% 29%, 22% 30%, 21% 9%, 39% 20%
  );
  background: var(--red);
  color: white;
  font-family: 'Bangers', sans-serif;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 80px; height: 80px;
  text-align: center;
  text-transform: uppercase;
  letter-spacing: 0.06em;
}
```

---

## AI Prompting Guidance

Use these prompts to generate Pop Art UI with AI tools:

**Component generation:**
> "Design a [button/card/form] in Roy Lichtenstein Pop Art style. Use: thick black borders (3px solid #000), offset box-shadow with no blur (5px 5px 0 #000), primary colors (red #e8261d, blue #003087, yellow #f7e500), Bangers font for all labels and headings, zero border-radius on all elements, halftone dot pattern (radial-gradient dots) on background areas."

**Visual description:**
> "Pop Art UI aesthetic: Ben-Day halftone dots, primary color palette, thick black Lichtenstein outlines, comic book panel layout, exclamatory Bangers typography, offset 2D shadow instead of blur. Inspired by Andy Warhol and Roy Lichtenstein, 1960s."

**Style enforcement:**
> "MUST follow these rules: 1) No border-radius on anything 2) All shadows are 'X px X px 0 #000' format — no blur 3) Bangers font for headings, Comic Neue for body 4) All interactive elements have visible 3px black border 5) Hover state grows the offset shadow and translates element opposite direction"

**Color guidance:**
> "Pop Art color rules: Background is Warhol yellow (#f7e500). Primary action color is red (#e8261d). Text is pure black (#000). Secondary: blue (#003087), pink (#ff69b4), cyan (#00b4d8). White is used for card/panel interiors. Every color boundary has a 3px black border."

---

## Anti-Patterns

**Never do these:**

```css
/* ✗ WRONG — soft shadow kills the pop effect */
box-shadow: 0 4px 24px rgba(0,0,0,0.15);

/* ✓ RIGHT — hard offset, no blur */
box-shadow: 5px 5px 0 #000;

/* ✗ WRONG — rounded corners are completely off-brand */
border-radius: 8px;

/* ✓ RIGHT — square. always. */
border-radius: 0;

/* ✗ WRONG — gradient fills are neumorphism, not pop */
background: linear-gradient(135deg, #e8261d, #ff69b4);

/* ✓ RIGHT — flat solid colors only */
background: var(--red);

/* ✗ WRONG — subtle/muted colors are anti-pop */
color: rgba(232, 38, 29, 0.6);

/* ✓ RIGHT — full saturation. always. */
color: var(--red);

/* ✗ WRONG — serif fonts are intellectual, not pop */
font-family: 'Georgia', serif;

/* ✓ RIGHT — comic fonts only */
font-family: 'Bangers', sans-serif;
```

---

## Historical Reference

| Artist | Contribution | UI Equivalent |
|--------|-------------|---------------|
| Roy Lichtenstein | Thick black outlines, Ben-Day dots, primary colors | `border: 3px solid #000`, halftone backgrounds |
| Andy Warhol | Repetition, flat color, product as art | Consistent color fills, no gradients |
| James Rosenquist | Fragmented billboard imagery | Card grid = panel grid |
| Jasper Johns | Flat iconic imagery | Bold icons, no decoration |

**Color palette sources:**
- Coca-Cola red → `var(--red)` #e8261d
- Pepsi blue → `var(--blue)` #003087
- Campbell's yellow → `var(--bg)` #f7e500
- Marilyn lips → `var(--pink)` #ff69b4

---

*"In the future, everyone will be famous for 15 minutes." — Andy Warhol*

*Pop Art UI is the same deal. Every button is famous. Every card is a poster. Design accordingly.*
