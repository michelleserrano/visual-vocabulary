# Claymorphism · Style Guide

> **Personality:** Tactile. Inflated. Soft. 3D-illusion. Joyful.

Claymorphism makes UI look like colorful 3D clay objects. Every surface appears to have physical thickness — like Play-Doh shaped into interface components. The aesthetic emerged around 2021 as a warmer, more playful evolution of neumorphism and glassmorphism.

---

## Design Tokens

```css
:root {
  /* Background & surface */
  --bg:     #f0e8f5;   /* soft lilac-white */
  --s1:     #e8e0f0;
  --s2:     #e0d8e8;

  /* Text */
  --t1:     #2d1a4a;               /* deep purple-black */
  --t2:     #5a3a7a;
  --t3:     rgba(45,26,74,0.45);
  --t4:     rgba(45,26,74,0.22);

  /* Clay colors — matte, saturated pastels */
  --pink:   #ff7eb3;
  --blue:   #7eb8ff;
  --green:  #b8ff7e;
  --yellow: #ffe27e;
  --purple: #b87eff;
  --orange: #ffaa7e;

  /* Accent */
  --ac:     #ff7eb3;
  --ac-lo:  rgba(255,126,179,0.22);

  /* Radii — very large, max-rounded */
  --r-sm:   16px;
  --r:      24px;
  --r-md:   32px;
  --r-lg:   40px;
  --r-full: 9999px;

  /* Typography */
  --f:      'Nunito', 'Poppins', system-ui, sans-serif;

  /* Easing */
  --ease:   cubic-bezier(0.4,0,0.2,1);
  --spring: cubic-bezier(0.34,1.56,0.64,1);  /* THE clay spring */
}
```

---

## The Triple Shadow System

The entire clay aesthetic rests on this one CSS formula. Apply it to **every** clay element.

```css
/* Clay shadow — the core illusion of 3D volume */
.clay {
  box-shadow:
    0 8px 24px rgba(45,26,74,0.12),          /* 1. Drop shadow — height above surface */
    inset 0 3px 8px rgba(255,255,255,0.5),   /* 2. Inner top highlight — light hitting top */
    inset 0 -3px 8px rgba(45,26,74,0.12);    /* 3. Inner bottom shadow — clay thickness */
}
```

**Why it works:** The drop shadow lifts the element. The inner top highlight simulates a light source. The inner bottom shadow creates perceived depth/thickness. Together they make the element look inflated and touchable.

### Shadow Scale

| Size | Drop shadow | Inner top | Inner bottom | Use for |
|------|------------|-----------|--------------|---------|
| `--clay-xs` | `0 3px 10px … .09` | `inset 0 2px 4px … .45` | `inset 0 -2px 4px … .08` | Pills, small chips |
| `--clay-sm` | `0 5px 16px … .11` | `inset 0 2px 6px … .5`  | `inset 0 -2px 6px … .10` | Buttons, inputs (raised) |
| `--clay-md` | `0 8px 24px … .12` | `inset 0 3px 8px … .5`  | `inset 0 -3px 8px … .12` | Cards, medium panels |
| `--clay-lg` | `0 14px 36px … .14`| `inset 0 4px 10px … .55`| `inset 0 -4px 10px … .13`| Large cards, modals |
| `--clay-xl` | `0 20px 48px … .16`| `inset 0 5px 12px … .58`| `inset 0 -5px 12px … .14`| Hero panels, featured |

---

## Clay Button Recipe

The signature interaction element. Each color gets a **matched colored drop shadow** — a pink button casts a pink shadow.

```css
.clay-btn {
  background: var(--pink);
  border-radius: var(--r-lg);          /* 40px — very rounded */
  border: none;
  padding: 0.8rem 2rem;
  font-family: 'Nunito', sans-serif;
  font-weight: 800;
  color: #fff;

  box-shadow:
    0 8px 20px rgba(255,126,179,0.4),      /* colored drop shadow */
    inset 0 3px 6px rgba(255,255,255,0.5), /* top shine */
    inset 0 -2px 4px rgba(150,50,90,0.15); /* bottom shade */

  transform-style: preserve-3d;
  transition: transform 0.2s var(--spring), box-shadow 0.2s;
}

.clay-btn:hover {
  transform: translateY(-4px) scale(1.02);
  box-shadow:
    0 14px 28px rgba(255,126,179,0.48),
    inset 0 3px 6px rgba(255,255,255,0.5),
    inset 0 -2px 4px rgba(150,50,90,0.15);
}

.clay-btn:active {
  transform: translateY(2px) scale(0.97);
  box-shadow:
    0 3px 8px rgba(255,126,179,0.32),
    inset 0 2px 4px rgba(255,255,255,0.4),
    inset 0 -1px 3px rgba(150,50,90,0.12);
}
```

### Color-matched shadow palette

| Clay color | Drop shadow rgba |
|-----------|-----------------|
| Pink `#ff7eb3`   | `rgba(255,126,179,0.4)` |
| Blue `#7eb8ff`   | `rgba(126,184,255,0.4)` |
| Green `#b8ff7e`  | `rgba(184,255,126,0.5)` |
| Yellow `#ffe27e` | `rgba(255,226,126,0.5)` |
| Purple `#b87eff` | `rgba(184,126,255,0.4)` |
| Orange `#ffaa7e` | `rgba(255,170,126,0.4)` |

> **Note:** Yellow and green use slightly higher opacity on the drop shadow because these colors are lighter, and need more shadow to maintain the clay volume impression.

---

## Clay Ball Decoration System

Floating clay orbs add ambient depth to section backgrounds. They animate on infinite float loops with different timing per orb.

```css
.clay-orb {
  border-radius: 50%;
  position: absolute;
  pointer-events: none;
  opacity: 0.4–0.55;  /* subtle — never distracting */
}

/* Example: blue orb */
.co-blue {
  background: var(--blue);
  box-shadow:
    0 8px 24px rgba(126,184,255,0.25),
    inset 0 4px 8px rgba(255,255,255,0.5),
    inset 0 -4px 8px rgba(50,90,150,0.15);
}
```

### Orb sizing guidelines

- **Large:** 100–120px — one per section max, far corner
- **Medium:** 70–90px — main accent orb, partially off-screen
- **Small:** 48–60px — paired with medium, different corner

### Float animation

```css
@keyframes float-a {
  0%,100% { transform: translateY(0) rotate(0deg); }
  50%      { transform: translateY(-12px) rotate(6deg); }
}
@keyframes float-b {
  0%,100% { transform: translateY(0) rotate(0deg); }
  50%      { transform: translateY(-18px) rotate(-5deg); }
}
@keyframes float-c {
  0%,100% { transform: translateY(0) rotate(0deg); }
  50%      { transform: translateY(-8px) rotate(8deg); }
}
/* Use animation-delay to desync orbs */
.orb-a { animation: float-a 7s ease-in-out infinite; }
.orb-b { animation: float-b 9s ease-in-out infinite; animation-delay: -3s; }
.orb-c { animation: float-c 6s ease-in-out infinite; animation-delay: -1.5s; }
```

---

## Spring Animation

The spring timing function is **the single most important motion decision** in claymorphism. It creates the physical "clay object" sensation.

```css
--spring: cubic-bezier(0.34, 1.56, 0.64, 1);
```

- `0.34` — slow start, like overcoming clay resistance
- `1.56` — overshoots past the target (the bounce)
- `0.64` — settles back smoothly
- `1` — ends at full speed convergence

### Timing by interaction type

| Interaction | Duration | Easing |
|------------|---------|--------|
| Button hover lift | `0.2s` | `var(--spring)` |
| Button press down | `0.12s` | `var(--ease)` (fast, linear-ish) |
| Card hover float | `0.35s` | `var(--spring)` |
| Toggle thumb | `0.3s` | `var(--spring)` |
| Radio/checkbox check | `0.22s` | `var(--spring)` |
| Nav tab switch | `0.25s` | `var(--spring)` |
| Scroll reveal | `0.6s` | `cubic-bezier(0,0,0.2,1)` |

---

## Form Inputs

Clay inputs have no visible border. The triple shadow IS the field boundary.

```css
.inp {
  background: rgba(255,255,255,0.7);
  box-shadow:
    inset 0 2px 6px rgba(45,26,74,0.10),   /* pressed into surface */
    inset 0 -1px 3px rgba(255,255,255,0.6); /* bottom highlight */
  border: none;
  border-radius: var(--r);   /* 24px */
  padding: 0.875rem 1.25rem;
}

.inp:focus {
  box-shadow:
    inset 0 2px 6px rgba(45,26,74,0.10),
    inset 0 -1px 3px rgba(255,255,255,0.6),
    0 0 0 3px rgba(255,126,179,0.2);        /* pink glow ring */
}
```

---

## Typography

**Nunito** is non-negotiable. Its extreme terminal rounding mirrors the clay shape language. Every letterform curves — just like every corner curves.

| Scale | Size | Weight | Use |
|-------|------|--------|-----|
| Display | 48px | 900 | Hero headlines |
| H1 | 36px | 800 | Section titles |
| H2 | 28px | 700 | |
| H3 | 22px | 700 | |
| H4 | 18px | 600 | |
| Body | 16px | 400–600 | |
| Caption | 12px | 700 | Uppercase labels |

**Never use:** sharp geometric sans (Futura, DIN), condensed type, serif, monospace for display.

---

## Do / Don't

| Do | Don't |
|----|-------|
| Use matte, saturated pastels | Use neon or fluorescent colors |
| Match drop shadow hue to fill color | Use grey/black drop shadows on colored elements |
| Use `--r-lg` (40px) or larger | Use sharp corners (≤8px radius) |
| Apply spring easing to all physical interactions | Use linear or ease-in-out for button presses |
| Keep backgrounds light (lilac-white) | Use dark backgrounds — clay is a light aesthetic |
| Use rounded Nunito 800+ for headings | Use any geometric or display typeface |
| No borders — shadow is the edge | Add 1px borders to "define" the element |
| White/light clay containers | Glass or transparent containers |

---

## Accessibility Notes

- Ensure text contrast meets WCAG AA: deep purple (#2d1a4a) on light bg passes at all sizes
- The pink accent (#ff7eb3) on white background may fail for small body text — use for decoration and large UI only
- Yellow/green clay buttons require **dark text** (#2d5a00, #5a3a00) not white — the pastel colors lack sufficient contrast with white
- Always provide `:focus-visible` with a visible ring (3px pink glow recommended)
- Respect `prefers-reduced-motion` by disabling spring/float animations

---

## AI Prompting Guidance

Use these phrases to prompt clay-quality output:

**System context:**
> "Apply claymorphism design style. Every element should look like a 3D clay object: large border radii (40px+), triple box-shadow (drop shadow + inner top highlight + inner bottom shade), matte pastel fill colors (pink #ff7eb3, sky blue #7eb8ff, lime green #b8ff7e, banana yellow #ffe27e, lavender #b87eff), spring cubic-bezier(0.34,1.56,0.64,1) on all transitions. No borders — shadow defines the edge. Background: soft lilac #f0e8f5. Font: Nunito 800."

**For buttons:**
> "Clay button with pink fill, colored drop shadow matching the fill, inset top highlight, inset bottom shade. Hover: translateY(-4px) scale(1.02) with deeper shadow. Active: translateY(2px) scale(0.97) with minimal shadow. Spring transition."

**For cards:**
> "Clay card with solid colored header (no gradient, no image), white clay body, triple shadow. On hover, card floats up 6–8px with spring animation. No border anywhere."

**For decorative orbs:**
> "Add 2–3 floating clay balls as background decoration. Each is a circle with solid pastel fill, triple clay shadow, 0.4–0.5 opacity, animated with a gentle float keyframe at different durations (6s, 9s) and delays."

---

*Generated for the UI Styles Gallery · Claymorphism (2021–present)*
