# Skeuomorphic Style Guide
**iOS 6 · OS X Mountain Lion · 2010–2013**

> *Material. Physical. Tactile. Nostalgic. Pre-flat.*

Skeuomorphism is the design language where every UI element imitates a real-world material or object. Leather notebooks, green felt notepads, chrome buttons, brushed aluminum panels. The aesthetic peaked at Apple between 2007–2013 under Scott Forstall, and was replaced by iOS 7's flat design in 2013.

---

## Personality

| Dimension | Expression |
|-----------|------------|
| **Tone** | Physical, tangible, tactile |
| **Era** | 2010–2013 Apple (iOS 6, OS X 10.8) |
| **Metaphor** | The UI is made of real materials |
| **Emotional resonance** | Nostalgia, warmth, craftsmanship |
| **Anti-patterns** | Flat fills, no gradients, abstract color use |

---

## Design Tokens

```css
:root {
  /* Surfaces */
  --bg:         #e8e4dc;   /* linen-like neutral — the desk the UI sits on */
  --linen:      #f5f0e8;   /* page/paper background */
  --felt:       #1a4a2a;   /* green felt (Notes, Passbook) */
  --wood:       #8b5a2b;   /* wooden shelf (iBooks) */

  /* Text */
  --t1:         #1a1208;   /* deep brown-black — ink on paper */
  --t2:         #4a3a28;   /* muted brown */
  --t3:         #8a7a68;   /* faint brown-gray */

  /* iOS accent colors */
  --ac-blue:    #2a7ad4;   /* iOS tint — button, link, selected */
  --ac-green:   #2a8a2a;   /* ON toggle, confirm */
  --ac-red:     #c83030;   /* delete, destructive */

  /* Shadow system */
  --sh-book:    0 6px 16px rgba(0,0,0,0.4), 0 2px 6px rgba(0,0,0,0.3),
                inset 0 1px 0 rgba(255,255,255,0.15);
  --sh-btn:     0 2px 5px rgba(0,0,0,0.4), inset 0 1px 0 rgba(255,255,255,0.35);
  --sh-inset:   inset 0 2px 6px rgba(0,0,0,0.35), inset 0 1px 2px rgba(0,0,0,0.2);

  /* Radius */
  --r:          6px;
  --r-sm:       4px;
  --r-md:       10px;
  --r-lg:       16px;
  --r-full:     9999px;

  /* Typography */
  --f:          'Georgia', serif;         /* editorial, headings, book feel */
  --f-ui:       'Helvetica Neue', Helvetica, sans-serif;  /* UI, labels, body */

  /* Motion */
  --ease:       cubic-bezier(0.4,0,0.2,1);
  --spring:     cubic-bezier(0.34,1.56,0.64,1);  /* toggle thumb spring */
}
```

---

## Material CSS Recipes

### Leather (crosshatch)
The authentic iOS 6 Game Center / Find My Friends leather texture. Two diagonal gradients at ±45° create diamond crosshatch.

```css
.leather {
  background-color: #3a2414;
  background-image:
    repeating-linear-gradient(45deg,  rgba(0,0,0,0.18) 0, rgba(0,0,0,0.18) 1px, transparent 1px, transparent 50%),
    repeating-linear-gradient(-45deg, rgba(0,0,0,0.18) 0, rgba(0,0,0,0.18) 1px, transparent 1px, transparent 50%);
  background-size: 8px 8px;
}

/* Stitching border (dashed pseudo-element inset from edges) */
.leather::after {
  content: '';
  position: absolute;
  inset: 6px;
  border: 1px dashed rgba(210,165,85,0.28);
  border-radius: 6px;
  pointer-events: none;
}
```

### Felt (fabric)
The Notes.app and Passbook green felt. Muted, slightly textured.

```css
.felt {
  background-color: #1a4a2a;
  background-image: repeating-linear-gradient(
    45deg,
    rgba(255,255,255,0.03) 0,
    rgba(255,255,255,0.03) 1px,
    transparent 1px,
    transparent 50%
  );
  background-size: 4px 4px;
}
```

### Chrome / Metal (reflective gradient)
Simulates brushed aluminum or polished chrome via multi-stop gradients.

```css
/* Brushed aluminum (OS X style) */
.metal {
  background: linear-gradient(180deg,
    #d8d8d4 0%,
    #b0b0a8 40%,
    #c0c0b8 100%
  );
}

/* Polished chrome (button style) */
.chrome {
  background: linear-gradient(180deg,
    #ffffff 0%,
    #ebebeb 30%,
    #d4d4d4 65%,
    #c4c4c4 100%
  );
  box-shadow:
    0 2px 6px rgba(0,0,0,0.35),
    inset 0 1px 0 rgba(255,255,255,0.95),
    0 0 0 1px rgba(0,0,0,0.18);
}
```

### Linen / Paper (page background)
Subtle woven texture for the page/canvas surface.

```css
.linen {
  background-color: #f5f0e8;
  background-image:
    repeating-linear-gradient(0deg,  transparent 0px, transparent 1px, rgba(160,140,100,0.1) 1px, rgba(160,140,100,0.1) 2px),
    repeating-linear-gradient(90deg, transparent 0px, transparent 1px, rgba(160,140,100,0.07) 1px, rgba(160,140,100,0.07) 2px);
  background-size: 4px 4px;
}
```

### Notepad / Ruled Paper
The Notes.app yellow ruled paper. Horizontal lines via repeating gradient + red margin line via pseudo-element.

```css
.notepad {
  background-color: #fdfbe6;
  background-image: repeating-linear-gradient(
    180deg,
    transparent 0px,
    transparent 23px,
    rgba(0,80,200,0.12) 23px,
    rgba(0,80,200,0.12) 24px
  );
  line-height: 24px; /* must match rule spacing */
}

/* Red margin line */
.notepad::before {
  content: '';
  position: absolute;
  left: 40px; top: 0; bottom: 0;
  width: 1px;
  background: rgba(200,50,50,0.25);
}
```

### Wood (bookshelf)
Used for iBooks shelf, podcast app, iTunes LP.

```css
.wood {
  background: linear-gradient(180deg,
    #a06832 0%,
    #8b5a2b 40%,
    #7a4820 70%,
    #8b5a2b 100%
  );
}
```

---

## Shadow System

Skeuomorphism uses shadows to communicate physical depth. Three patterns:

### Raised (convex surface — button, card)
```css
box-shadow:
  0 3px 8px rgba(0,0,0,0.35),    /* main drop shadow */
  0 1px 3px rgba(0,0,0,0.25),    /* close detail shadow */
  inset 0 1px 0 rgba(255,255,255,0.4);  /* top edge specular */
```

### Pressed (button active state)
```css
box-shadow:
  0 1px 2px rgba(0,0,0,0.3),
  inset 0 2px 4px rgba(0,0,0,0.35);  /* recessed into surface */
```

### Inset (recessed input)
```css
box-shadow:
  inset 0 2px 6px rgba(0,0,0,0.35),
  inset 0 1px 2px rgba(0,0,0,0.2);
```

### Book/page stack (offset shadow)
```css
/* Simulates stacked pages visible at right/bottom edge */
box-shadow:
  3px 3px 0 0 #b0aca4,   /* page 1 edge */
  6px 6px 0 0 #c4c0b8,   /* page 2 edge */
  0 8px 20px rgba(0,0,0,0.4),
  0 3px 8px rgba(0,0,0,0.3);
```

---

## iOS 6 Button Gradient Recipe

The definitive iOS button. Every interactive element used this blue across the entire platform.

```css
/* Default state */
.ios-btn-primary {
  background: linear-gradient(180deg,
    #62bbff 0%,
    #3a9af0 25%,
    #2a7ad4 60%,
    #1a5ab0 100%
  );
  color: #fff;
  text-shadow: 0 -1px 0 rgba(0,0,60,0.3);
  box-shadow:
    0 2px 6px rgba(0,0,0,0.4),
    0 1px 2px rgba(0,0,0,0.3),
    inset 0 1px 0 rgba(255,255,255,0.42),
    0 0 0 1px rgba(0,0,100,0.18);
  border-radius: 9999px;
  border: none;
  padding: 0.6875rem 1.75rem;
  font-family: 'Helvetica Neue', Helvetica, sans-serif;
  font-weight: 600;
}

/* Hover state */
.ios-btn-primary:hover {
  background: linear-gradient(180deg,
    #78c8ff 0%, #4aaaf8 25%, #3a8ae4 60%, #2a6ac0 100%
  );
  box-shadow:
    0 3px 9px rgba(0,0,0,0.45),
    inset 0 1px 0 rgba(255,255,255,0.42);
}

/* Active / pressed state — gradient REVERSES */
.ios-btn-primary:active {
  background: linear-gradient(180deg,
    #1a5ab0 0%, #2a7ad4 50%, #3a9af0 100%
  );
  box-shadow:
    0 1px 2px rgba(0,0,0,0.3),
    inset 0 2px 4px rgba(0,0,0,0.35);
  transform: scale(0.98);
}
```

**Button variants** follow the same structure, only the color changes:
- Red delete: `#e86060 → #c03030 → #a82020`
- Green confirm: `#5acc5a → #2a8a2a → #1a6a1a`
- Chrome secondary: `#ffffff → #d4d4d4 → #c4c4c4` (text: `#333`)

---

## iOS 6 Toggle Switch

The most iconic skeuomorphic component. Looks and behaves like a real physical switch.

```css
.tgl-track {
  display: block;
  width: 51px; height: 31px;
  background: linear-gradient(180deg, #bcb8b0 0%, #d0ccc4 100%);
  box-shadow:
    inset 0 2px 5px rgba(0,0,0,0.42),
    inset 0 1px 2px rgba(0,0,0,0.25),
    0 1px 0 rgba(255,255,255,0.28);
  border-radius: 15.5px;
  border: 1px solid rgba(0,0,0,0.18);
  position: relative;
  overflow: hidden;
  transition: background 0.3s, box-shadow 0.3s;
}

/* "ON" label fades in when checked */
.tgl-track::before {
  content: 'ON';
  position: absolute;
  left: 6px; top: 50%;
  transform: translateY(-50%);
  font: 700 9px/1 'Helvetica Neue';
  color: rgba(255,255,255,0.9);
  opacity: 0;
  transition: opacity 0.2s;
}

.tgl-thumb {
  position: absolute;
  top: 2px; left: 2px;
  width: 27px; height: 27px;
  border-radius: 13.5px;
  background: linear-gradient(180deg, #fff 0%, #ececec 50%, #dcdcdc 100%);
  box-shadow:
    0 2px 5px rgba(0,0,0,0.48),
    0 1px 2px rgba(0,0,0,0.3),
    inset 0 1px 0 rgba(255,255,255,0.95);
  transition: transform 0.3s cubic-bezier(0.34,1.56,0.64,1);  /* spring */
}

/* Checked = green, thumb slides right */
input:checked ~ .tgl-track {
  background: linear-gradient(180deg, #1a6a1a 0%, #2a8a2a 50%, #1e7a1e 100%);
  box-shadow: inset 0 1px 3px rgba(0,0,0,0.32);
  border-color: rgba(0,80,0,0.28);
}
input:checked ~ .tgl-track::before { opacity: 1; }
input:checked ~ .tgl-track .tgl-thumb { transform: translateX(20px); }
```

---

## iOS 6 Tab Bar

```css
.ios6-tabbar {
  background: linear-gradient(180deg,
    #3c3c3c 0%,
    #2c2c2c 50%,
    #1e1e1e 100%
  );
  box-shadow:
    0 -1px 0 rgba(255,255,255,0.09),
    0 -3px 8px rgba(0,0,0,0.42);
}

/* Selected tab — blue gloss pill */
.ios6-tab.active .ios6-tab-inner {
  background: linear-gradient(180deg,
    rgba(130,180,255,0.28) 0%,
    rgba(40,120,220,0.82) 45%,
    rgba(20,80,180,0.92) 100%
  );
  box-shadow:
    0 1px 3px rgba(0,0,0,0.52),
    inset 0 1px 0 rgba(255,255,255,0.24),
    0 0 0 1px rgba(0,50,150,0.38);
  border-radius: 8px;
}
```

---

## Typography Rules

| Role | Font | Weight | Style | Size |
|------|------|--------|-------|------|
| Display / H1 | Georgia | 700 | Italic | 48px / 36px |
| H2 / H3 | Georgia | 700 | Italic / Roman | 28px / 22px |
| H4 / Body heading | Georgia | 700 | Roman | 18px |
| UI body | Helvetica Neue | 400 | — | 16px |
| UI labels | Helvetica Neue | 600 | — | 13px |
| Captions | Helvetica Neue | 600 | Uppercase | 12px |

**Text shadow for embossed headings:**
```css
/* Embossed (appears raised) */
text-shadow: 0 1px 0 rgba(255,255,255,0.5), 0 -1px 0 rgba(0,0,0,0.08);

/* Debossed (appears pressed in) */
text-shadow: 0 1px 0 rgba(255,255,255,0.3), 0 -1px 0 rgba(0,0,0,0.25);

/* On dark (leather) background */
text-shadow: 0 1px 3px rgba(0,0,0,0.6);
```

---

## AI Prompting Guidance

Use these prompts to generate skeuomorphic UI with any AI tool:

### For components
```
Create a [component] in iOS 6 skeuomorphic style. Use:
- Leather texture: crosshatch via repeating 45deg + -45deg linear gradients, base color #3a2414, background-size 8px 8px
- Chrome buttons: linear-gradient 180deg from #fff to #c4c4c4, box-shadow with inset highlight + outer drop shadow
- iOS blue: linear-gradient 180deg from #62bbff to #1a5ab0, inverted on active state
- Inset inputs: linear-gradient from darker to lighter gray, heavy inset box-shadow
- Fonts: Georgia (italic for headings), Helvetica Neue (UI elements)
- All shadows are multi-value: drop shadow + secondary shadow + inset specular highlight
Do NOT use flat colors. Every element needs a gradient and shadow to create physical depth.
```

### For layout
```
Design a [screen/layout] like iOS 6 or OS X Mountain Lion (2012). Include:
- Page background: linen texture (#f5f0e8 with 4px repeating grid noise)
- Navigation bar: dark multi-stop gradient (#686868 → #3a3a3a) with 50% gloss overlay
- Table view cells: white background with subtle gradient, gray disclosure chevron
- Use Georgia for the page/screen title
- Tab bar: very dark gradient with blue gloss pill for selected state
Reference: iOS 6 Mail app, Notes app, Contacts app visual language.
```

### For mood/style
```
The aesthetic is "2012 Apple before Jony Ive flattened everything." Think:
- Game Center leather tables
- Find My Friends green felt
- iBooks wooden shelf  
- Notes yellow ruled paper
- The Notes app stitched leather binding
- iPod click wheel chrome
- OS X Mountain Lion brushed aluminum panels
Every surface should look like you could reach through the screen and touch the material.
```

---

## Anti-Patterns

| Wrong | Right |
|-------|-------|
| Flat color fills | Multi-stop gradients on every surface |
| No shadows | Every raised element has drop + specular shadows |
| Generic sans-serif for everything | Georgia for headings/editorial, Helvetica for UI |
| Abstract color meaning | Colors = materials (blue=chrome, green=felt, brown=leather) |
| Single-value border | Border + box-shadow for 3D edge effect |
| CSS variables for button fill | The actual gradient values — they vary by hover/active state |
| Icons without drop shadows | `filter: drop-shadow()` for realistic icon depth |

---

## Historical Context

- **2007** iOS 1: First major skeuomorphic OS on mobile
- **2010** iOS 4 / iPhone 4 Retina: HD skeuomorphism, textures at full resolution  
- **2012** iOS 6 / OS X Mountain Lion: Peak skeuomorphism — Game Center leather, Notes ruled paper, Calendar leather, Find My Friends green felt, iBooks wooden shelf
- **2013** iOS 7: Jony Ive flattens everything. The leather burns.
- **2019** Neumorphism emerges as a nostalgic echo
- **2024** Skeuomorphism resurfaces in AI-era "tactile digital" aesthetic

The era was controversial. The leather was "embarrassing" to many designers. It was also loved — warmth, familiarity, zero learning curve. You already knew what a book looked like.
