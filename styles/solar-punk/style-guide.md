# Solar Punk · Style Guide

**Personality:** Optimistic-ecological. Plant-tech-hybrid. Golden-hour. Conservatory-luxury. Anti-cyberpunk.

> "Where technology integrates with nature. Where solar panels share gardens with vines. Where the future is grown, not built."

Solar Punk is the direct counter-narrative to Cyberpunk's dystopia — a movement that imagines an optimistic ecological future where technology and nature are not in tension but interwoven. Design should feel like sitting in a glass conservatory at golden hour: warm cream walls, brass joinery, terracotta pots, and mossy green spilling everywhere.

---

## Identity

| Attribute        | Value                                                                  |
|------------------|------------------------------------------------------------------------|
| Era              | Circa 2050 · post-fossil, post-scarcity, post-cynicism                  |
| Mood             | Warm, hopeful, lushly grown, quietly luxurious                         |
| Shape language   | Organic-but-precise · pill radii · leaf silhouettes · brass hairlines  |
| Light source     | Golden hour — sun low through glass, warm cast on every surface        |
| Texture          | Aged paper · hemp weave · fired clay · brushed brass · living moss     |
| Reference points | William Morris · Studio Ghibli's Laputa · Hayao Miyazaki's Nausicaä · Olafur Eliasson's solar pavilions · Hundertwasser · the Eden Project |

---

## Counter-narrative comparison

Solar Punk is best understood by what it is *not*.

| Aspect              | Cyberpunk                         | Organic                            | **Solar Punk**                                          |
|---------------------|-----------------------------------|------------------------------------|---------------------------------------------------------|
| Future outlook      | Dystopia, corporations rule       | Ambiguous · abstract               | **Optimistic ecological future**                        |
| Light               | Neon from below, rain-slick       | Diffuse daylight                   | **Golden hour, warm sun through glass**                 |
| Palette             | Neon red/yellow on near-black     | Earthy muted (sage, ochre)         | **Mossy green + terracotta + brass on warm cream**     |
| Metals              | Chrome, silver, gunmetal          | None (anti-metal)                  | **Brass, copper — warm metals only**                    |
| Imagery             | Skyscrapers, dense urban decay    | Blobs, biomorphic abstraction      | **Plant + circuit hybrids · specific objects**          |
| Type                | Condensed sans, glitch, mono      | Editorial italic serif             | **Humanist serif + clean geometric sans**               |
| Shadows             | Cool blue / neon glow             | Earth-tinted gray                  | **Golden-hour warm shadows (rgba(168,90,48,…))**       |
| Narrative           | Threat, control, density          | Abstract feeling                   | **Specific solarpunk objects: conservatory, vine turbine, stained-glass panel** |

**Rule of thumb:** if it could appear in *Blade Runner 2049*, it isn't Solar Punk. If it could appear in *Studio Ghibli's Laputa*, it probably is.

---

## Design Tokens

```css
:root {
  /* Surfaces — warm cream like aged paper at golden hour */
  --bg:        #f0e9d6;
  --bg-2:      #e8dfc4;
  --surface-1: #ddd1b3;   /* hemp weave */
  --surface-2: #c8b896;   /* dried tussock */

  /* Botanical accents */
  --moss:      #5a8a4e;   /* lichen sample · primary */
  --moss-dk:   #3d6438;   /* conifer shadow · hover */
  --moss-lo:   rgba(90,138,78,0.15);
  --terra:     #c87544;   /* fired clay · secondary */
  --terra-dk:  #a85a30;
  --terra-lo:  rgba(200,117,68,0.15);

  /* Warm metals — brass replaces silver */
  --brass:     #b8923a;   /* harvested honey */
  --brass-hi:  #d4b04a;   /* beeswax glow */
  --brass-lo:  rgba(184,146,58,0.18);

  /* Forest depths for text — never pure black */
  --forest:    #2d3a2d;
  --t1:        #2d3a2d;
  --t2:        rgba(45,58,45,0.7);
  --t3:        rgba(45,58,45,0.45);
  --t4:        rgba(45,58,45,0.22);
  --t-inv:     #f0e9d6;

  /* Hairlines */
  --border:       1px solid rgba(45,58,45,0.12);
  --border-hi:    1px solid rgba(45,58,45,0.25);
  --border-brass: 1px solid rgba(184,146,58,0.45);

  /* Radii — moderate; organic but never blob */
  --r-sm:   8px;
  --r:      14px;
  --r-md:   20px;
  --r-lg:   28px;
  --r-full: 9999px;

  /* Type */
  --f-disp: 'DM Serif Display', Georgia, serif;
  --f:      'Manrope', 'Inter', system-ui, sans-serif;
  --f-mono: 'JetBrains Mono', 'Courier New', monospace;

  /* Motion */
  --ease:     cubic-bezier(0.4,0,0.2,1);
  --spring:   cubic-bezier(0.34,1.56,0.64,1);

  /* Golden-hour shadows — warm-tinted, NEVER cool gray */
  --sh-sm:  0 2px 8px  rgba(168,90,48,0.08);
  --sh-md:  0 4px 16px rgba(168,90,48,0.12);
  --sh-lg:  0 12px 36px rgba(168,90,48,0.15);

  /* Brass glow — like a candle, sunset reflection */
  --glow-warm: 0 0 24px rgba(212,176,74,0.30);
  --glow-moss: 0 0 0 3px rgba(90,138,78,0.15);
}
```

---

## Palette Rationale

Every Solar Punk colour is named after a real natural source. If you can't picture where it comes from in the world, it doesn't belong here.

| Token        | Hex         | Natural source                           | Use                                          |
|--------------|-------------|------------------------------------------|----------------------------------------------|
| `--bg`       | `#f0e9d6`   | Aged paper in afternoon sun              | Page background — the warm base              |
| `--bg-2`     | `#e8dfc4`   | Linen warp                               | Subtle surfaces, kicker chips                |
| `--surface-1`| `#ddd1b3`   | Hemp weave                               | Card surfaces, form panels                   |
| `--surface-2`| `#c8b896`   | Dried tussock grass                      | Tertiary surface, contrast block             |
| `--moss`     | `#5a8a4e`   | Lichen on north-facing stone             | Primary buttons, active states, focus rings  |
| `--moss-dk`  | `#3d6438`   | Conifer canopy shadow                    | Hover depth, deep accents                    |
| `--terra`    | `#c87544`   | Kiln-fired terracotta pot                | Secondary actions, decorative highlights     |
| `--terra-dk` | `#a85a30`   | Burnished pottery                        | Terracotta hover/press                       |
| `--brass`    | `#b8923a`   | Harvested honey · brushed brass          | Accents, borders, label colour               |
| `--brass-hi` | `#d4b04a`   | Beeswax glow · candle highlight          | Brass-gradient buttons, warm glow            |
| `--forest`   | `#2d3a2d`   | Forest floor                             | Primary text — never pure black              |

### The mossy-green + terracotta + brass + cream rule

These four colours are the **non-negotiable signature**. A page that uses them will read as Solar Punk even if you change everything else. Conversely, a page that omits any of them — especially the brass — will not. Brass is what separates Solar Punk from generic eco-design.

**Anti-palette:** any neon, any chrome silver, any cold blue. If you reach for those, you've slipped into Cyberpunk.

---

## Typography

### Type stack

```css
--f-disp: 'DM Serif Display', Georgia, serif;    /* warm humanist serif */
--f:      'Manrope', 'Inter', system-ui, sans-serif;  /* clean geometric */
--f-mono: 'JetBrains Mono', monospace;
```

### Google Fonts import

```html
<link href="https://fonts.googleapis.com/css2?family=DM+Serif+Display:ital@0;1&family=Manrope:wght@300;400;500;600;700;800&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
```

### Pairing rationale

| Role           | Font                | Weight | Style   | Why                                                          |
|----------------|---------------------|--------|---------|--------------------------------------------------------------|
| Display H1     | DM Serif Display    | 400    | Italic  | Hand-set wood-type warmth; humanist, never austere           |
| H1 upright     | DM Serif Display    | 400    | Normal  | Editorial gravitas without aggression                        |
| H2             | DM Serif Display    | 400    | Italic  | Optimistic register — italic = warmth, not emphasis          |
| H3–H4          | Manrope             | 600    | Normal  | Clean geometric — friendly without being clinical            |
| Body           | Manrope             | 400    | Normal  | High legibility on warm cream background                     |
| Captions       | Manrope             | 600–700| Normal  | Wide letter-spacing (0.16–0.20em) reads as botanical label   |
| Field labels   | DM Serif Display    | 400    | Italic  | Sets brass-italic label as a signature                       |
| Tabular / hex  | JetBrains Mono      | 400–500| Normal  | Modern but warm; for design tokens, times, percentages       |

### Anti-rules

- Do NOT use condensed display sans (Bebas Neue, Oswald) — that's Cyberpunk territory.
- Do NOT use Playfair Display — too high-contrast, drifts toward fashion-editorial. Solar Punk is a touch warmer and rounder.
- Do NOT use more than two voices (DM Serif + Manrope). Mono is for tabular data only.

---

## Plant Motif SVG Library

Solar Punk's signature is the **SVG botanical motif**. Every section gets at least one. Embed them as `<symbol>` elements at the top of the document and reference with `<use>`.

### Leaf

```html
<svg viewBox="0 0 32 40">
  <path d="M16 38 Q8 28 8 18 Q8 8 16 4 Q24 8 24 18 Q24 28 16 38 Z"
        fill="currentColor" stroke="rgba(45,58,45,0.45)" stroke-width="0.8"/>
  <path d="M16 4 L16 38" stroke="rgba(45,58,45,0.55)" stroke-width="0.7" fill="none"/>
  <!-- side veins -->
  <path d="M16 12 L11 14 M16 12 L21 14 M16 20 L10 22 M16 20 L22 22 M16 28 L11 30 M16 28 L21 30"
        stroke="rgba(45,58,45,0.4)" stroke-width="0.6" fill="none"/>
</svg>
```

### Horizontal vine (section divider)

```html
<svg viewBox="0 0 240 22">
  <path d="M0 11 Q30 2 60 11 T120 11 T180 11 T240 11"
        stroke="currentColor" stroke-width="1.4" fill="none" stroke-linecap="round"/>
  <!-- alternating leaves above/below -->
  <path d="M45 11 Q42 5 48 3 Q54 5 51 11 Z" fill="currentColor" fill-opacity="0.65"/>
  <path d="M90 11 Q88 17 94 19 Q100 17 96 11 Z" fill="currentColor" fill-opacity="0.65"/>
  <!-- repeat at 135, 180… -->
</svg>
```

Place a vine SVG **below every section heading** as a divider — this is the most recognisable signature in the system.

### Sun / seed motif

```html
<svg viewBox="0 0 24 24">
  <circle cx="12" cy="12" r="4.5" fill="currentColor"/>
  <g stroke="currentColor" stroke-width="1.5" stroke-linecap="round">
    <line x1="12" y1="2" x2="12" y2="5"/>
    <line x1="12" y1="19" x2="12" y2="22"/>
    <!-- 8 rays in total at 45° increments -->
  </g>
</svg>
```

Use sparingly — sun motifs are reserved for the hero kicker, the navigation date strip, and section icons where a botanical metaphor doesn't fit.

### Plant + circuit hybrid

Where a tech motif would otherwise appear (icons, illustrations, badges), draw it with **plant integration**:

- Wind turbine → blades drawn as elongated leaves
- Solar panel → stained-glass leaf shapes in each pane
- WiFi symbol → arched vine petals
- Database → terracotta clay pot with rings
- Server rack → vertical garden tower

This is the rule that separates Solar Punk from "just an eco design system." Tech is not absent — it is **botanised**.

---

## Shape & Radius

Solar Punk is **organic-but-precise**. Use moderate radii — never blob, never sharp.

```css
--r-sm:   8px;     /* hints, small chips */
--r:      14px;    /* inputs, search bars */
--r-md:   20px;    /* secondary surfaces */
--r-lg:   28px;    /* cards, panels */
--r-full: 9999px;  /* buttons, pills, progress */
```

The **leaf shape** is a non-radius signature, created with asymmetric border-radius:

```css
.leaf-shape {
  border-radius: 0 100% 0 100%;
  transform: rotate(45deg);    /* point up-right */
}
```

Use it for: progress dots, checkboxes (toggle the rotation when checked), nav active indicators, decorative bullets.

---

## Warm Shadow System

**The single most important non-palette rule.** All shadows are golden-hour warm — never cool gray.

```css
--sh-sm:  0 2px 8px  rgba(168,90,48,0.08);
--sh-md:  0 4px 16px rgba(168,90,48,0.12);
--sh-lg:  0 12px 36px rgba(168,90,48,0.15);
```

The colour `rgba(168,90,48,…)` is **dark terracotta** — it casts a sunset-coloured shadow, the colour of warm light through warm matter. Compare to cyberpunk's cool-blue glow shadows or organic's gray-green shadows: Solar Punk specifically casts terracotta.

### Brass glow accent

```css
--glow-warm: 0 0 24px rgba(212,176,74,0.30);
```

Apply on hover to important elements — primary buttons, active cards, the play button. It's a warm halo, the visual equivalent of a candle behind glass. **Never neon, always warm.**

```css
.btn-primary:hover {
  box-shadow: var(--sh-lg), 0 0 24px rgba(212,176,74,0.32);
  transform: translateY(-2px);
}
```

---

## Component Patterns

### Buttons

```css
/* Primary — moss pill with brass hairline */
.btn-primary {
  background: var(--moss);
  color: var(--t-inv);
  border: 1px solid var(--moss-dk);
  border-radius: var(--r-full);
  padding: 0.75rem 1.75rem;
  font-family: var(--f);
  font-weight: 600;
  box-shadow: var(--sh-md), inset 0 1px 0 rgba(212,176,74,0.18);
}
.btn-primary:hover {
  background: var(--moss-dk);
  transform: translateY(-2px);
  box-shadow: var(--sh-lg), 0 0 24px rgba(212,176,74,0.32);
}
.btn-primary:active { transform: translateY(0); box-shadow: var(--sh-sm); }
```

A primary button on hover **also sprouts a tiny leaf SVG** in the top-right corner — a small but signature delight:

```html
<button class="btn btn-primary">
  Tend the garden
  <svg class="btn-sprout" viewBox="0 0 32 40"><use href="#leaf"/></svg>
</button>
```

```css
.btn-sprout {
  position: absolute; right: -6px; top: -6px;
  width: 14px; height: 18px;
  color: var(--brass-hi);
  opacity: 0;
  transform: rotate(20deg) scale(0.4);
  transition: opacity 0.25s, transform 0.35s var(--spring);
}
.btn:hover .btn-sprout { opacity: 1; transform: rotate(28deg) scale(1); }
```

**Brass-gradient button** — reserved for luxury / hero / subscription moments:

```css
.btn-brass {
  background: linear-gradient(160deg, #d4b04a 0%, #b8923a 60%, #9a7a2e 100%);
  color: var(--forest);
  font-weight: 700;
  border: 1px solid rgba(58,42,16,0.4);
  text-shadow: 0 1px 0 rgba(255,240,200,0.35);
}
```

### Form inputs

```css
.inp {
  background: var(--bg);
  border: 1px solid rgba(45,58,45,0.25);
  border-radius: var(--r);
  padding: 0.875rem 1.125rem;
  font-family: var(--f);
}
.inp:focus {
  border-color: var(--moss);
  box-shadow: 0 0 0 3px rgba(90,138,78,0.15);
  outline: none;
}
```

On focus, a small leaf SVG fades in at the right edge — this is a signature delight:

```css
.inp-leaf {
  position: absolute; right: 0.95rem; top: 50%;
  transform: translateY(-50%) rotate(15deg) scale(0.5);
  opacity: 0;
  transition: opacity 0.25s, transform 0.3s var(--spring);
}
.inp-wrap:focus-within .inp-leaf {
  opacity: 1;
  transform: translateY(-50%) rotate(20deg) scale(1);
}
```

### Leaf-shaped checkboxes

```css
.chk-leaf {
  width: 22px; height: 22px;
  border-radius: 0 100% 0 100%;       /* leaf silhouette */
  background: var(--bg);
  border: 1px solid rgba(45,58,45,0.25);
  transition: transform 0.25s var(--spring);
}
.chk-in:checked + .chk-leaf {
  background: var(--moss);
  border-color: var(--moss-dk);
  transform: rotate(8deg);              /* gentle twist when checked */
}
.chk-mark { color: var(--brass-hi); }   /* brass check, not white */
```

### Toggles with brass thumb

```css
.tgl-track {
  width: 56px; height: 30px;
  background: var(--bg-2);
  border: 1px solid rgba(45,58,45,0.25);
  border-radius: var(--r-full);
}
.tgl-thumb {
  width: 24px; height: 24px;
  background: linear-gradient(160deg, var(--brass-hi), var(--brass));
  border-radius: 50%;
  box-shadow: 0 2px 6px rgba(168,90,48,0.30);
}
.tgl-thumb::before {
  /* tiny seed mark inside the brass thumb */
  content: '';
  width: 6px; height: 6px;
  background: rgba(58,42,16,0.45);
  border-radius: 50%;
}
.tgl-in:checked ~ .tgl-track { background: var(--moss); }
```

### Cards

```css
.card {
  background: var(--surface-1);
  border: 1px solid rgba(45,58,45,0.12);
  border-radius: var(--r-lg);     /* 28px */
  box-shadow: var(--sh-md);
}
.card:hover {
  box-shadow: var(--sh-lg), 0 0 28px rgba(212,176,74,0.25);
  transform: translateY(-4px);
  border-color: rgba(184,146,58,0.4);    /* brass border glow */
}
```

**Card thumbnails** must be hand-drawn-feeling SVG botanical illustrations — never stock photography, never abstract gradients. The library includes:

- Glass conservatory dome with plants inside
- Wind turbine with leaf-shaped blades
- Stained-glass solar panel (leaf shapes in each pane)
- Vertical garden tower with vines spilling out
- Bioluminescent lamp with vines inside the globe

### Spec callout · botanical bookmark

```css
.spec-callout {
  background: var(--bg-2);
  border-left: 3px solid var(--moss);
  border-radius: 0 var(--r) var(--r) 0;
  padding: 1rem 1.25rem 1rem 1.5rem;
  box-shadow: var(--sh-sm);
}
.spec-callout::before {
  /* tiny leaf nesting on the moss border */
  content: '';
  position: absolute;
  left: -8px; top: 50%;
  transform: translateY(-50%) rotate(45deg);
  width: 12px; height: 12px;
  background: var(--moss);
  border-radius: 0 100% 0 100%;
  box-shadow: var(--glow-warm);
}
.spec-callout-text {
  font-family: var(--f-disp);
  font-style: italic;
  color: var(--t2);
}
.spec-callout-ico { color: var(--brass); }   /* ❦ floral ornament */
```

### Side progress dots — leaves, not circles

```css
.prog-dot {
  width: 12px; height: 12px;
  border-radius: 0 100% 0 100%;        /* leaf shape */
  transform: rotate(45deg);
  border: 1px solid var(--t4);
  background: transparent;
}
.prog-dot.active {
  background: var(--moss);
  border-color: var(--moss-dk);
  box-shadow: 0 0 18px rgba(90,138,78,0.45);
}
.prog-dot:hover {
  border-color: var(--brass);
  box-shadow: var(--glow-warm);
}
```

### Bottom nav with brass leaf indicator

```css
.sp-navbar::before {
  /* vine line above the nav */
  content: '';
  position: absolute;
  top: -1px; left: 0; right: 0; height: 1px;
  background: linear-gradient(90deg,
    transparent, rgba(90,138,78,0.45) 25%, rgba(184,146,58,0.6) 50%,
    rgba(90,138,78,0.45) 75%, transparent);
}
.ni::before {
  /* brass leaf indicator above active tab */
  content: '';
  position: absolute; top: -1px; left: 50%;
  transform: translateX(-50%) rotate(45deg) scale(0);
  width: 8px; height: 8px;
  background: var(--brass-hi);
  border-radius: 0 100% 0 100%;
  box-shadow: var(--glow-warm);
  transition: transform 0.3s var(--spring);
}
.ni-on::before { transform: translateX(-50%) rotate(45deg) scale(1); }
```

---

## Motion

| Property        | Value                                | Use                                       |
|-----------------|--------------------------------------|-------------------------------------------|
| `--ease`        | `cubic-bezier(0.4,0,0.2,1)`          | Standard transitions, hover               |
| `--spring`      | `cubic-bezier(0.34,1.56,0.64,1)`     | Toggle thumb, leaf sprout, checkbox twist |
| Section reveal  | `0.7s ease-out` + `translateY(24px)` | First view of each section                |
| Hero leaf drift | `14–19s ease-in-out infinite`        | Decorative floating leaves                |
| Button lift     | `0.15s` → `translateY(-2px)`         | Primary, terracotta, brass hover          |
| Card lift       | `0.3s` → `translateY(-4px)` + glow   | Card hover                                |

**Motion philosophy:** subtle, slow, life-like. Leaves drift on 14–19 second cycles. Cards rise like a gentle breath. Avoid anything that snaps or pops — Solar Punk is patient.

---

## Layout & Section Anatomy

Every section follows this scaffold:

```html
<section class="sec" id="sec-{name}">
  <header class="sec-hd">
    <div class="sec-kicker">
      <span class="sec-kicker-dot"></span>
      Part III // Buttons
    </div>
    <h2 class="sec-title">Pills with brass borders &amp; vine sprouts</h2>
    <span class="sec-ghost" aria-hidden="true">03</span>
    <svg class="sec-vine" viewBox="0 0 240 22"><use href="#vine"/></svg>
  </header>
  <div class="spec-callout">…</div>
  <!-- content -->
</section>
```

Components in order:
1. **Kicker** — Manrope uppercase, moss colour, with a glowing brass dot
2. **Section title** — DM Serif Display italic, clamp(2rem, 4vw, 2.625rem)
3. **Ghost number** — DM Serif Display italic, massive, `rgba(90,138,78,0.09)`
4. **Vine divider** — full-width SVG vine below the heading
5. **Spec callout** — botanical bookmark with `❦` ornament and italic text
6. Section content

---

## Accessibility

- All interactive elements have `:focus-visible` outline: `2px solid var(--moss)` with `outline-offset: 3px`.
- `prefers-reduced-motion` collapses all transition durations to `0.01ms`.
- Text contrast on cream:
  - Forest (`#2d3a2d`) on cream (`#f0e9d6`): **9.4:1** — passes WCAG AAA
  - Moss-dk (`#3d6438`) on cream: **6.8:1** — passes AA for normal text
  - Moss (`#5a8a4e`) on cream: **3.9:1** — large UI text only (14px+ semibold)
  - Brass (`#b8923a`) on cream: **3.0:1** — large display text & label decoration only; never body
- All SVG decorations are `aria-hidden="true"`; semantic content stays in `<h*>` / `<p>` / `<button>` elements.

---

## AI Prompting Guidance

When generating Solar Punk UI with AI tools (Figma AI, Midjourney, image generators, or coding agents), use these phrases:

### Positive descriptors

- "solarpunk, optimistic-ecological future, plant-tech hybrid"
- "golden hour palette, warm cream background"
- "mossy green and terracotta with brass accents"
- "DM Serif Display italic headlines, Manrope body"
- "botanical SVG decorations — leaves, vines, sun motifs"
- "hand-drawn-feeling illustrations: glass conservatory, vine turbine, stained-glass solar panel"
- "warm-tinted shadows (terracotta-shadow, not cool gray)"
- "brass hairline borders on buttons and cards"
- "asymmetric border-radius for leaf-shaped checkboxes and progress dots"
- "humanist serif paired with clean geometric sans"
- "Ghibli's Laputa meets William Morris meets the Eden Project"

### Anti-descriptors (what to avoid)

- "no neon colors, no fluorescent palette"
- "no chrome, no silver, no cold metals — only brass and copper"
- "no cool gray or blue shadows — only warm golden-hour shadows"
- "no dystopian or doom-and-gloom tone"
- "no Bebas Neue or condensed display sans"
- "no pure white or pure black — cream and forest instead"
- "no glassmorphism · no flat material design · no Y2K chrome"

### Figma prompt template

> "Create a mobile app UI in Solar Punk style. Background `#f0e9d6` (warm cream). Primary accent `#5a8a4e` (mossy green). Secondary `#c87544` (terracotta). Metal accents `#b8923a` (brass) — never silver. Buttons are moss-green pills with a 1px brass border. Cards have 28px border-radius and a warm-tinted shadow `rgba(168,90,48,0.12)`. Headings in DM Serif Display italic; body in Manrope. Add hand-drawn SVG botanical decorations — leaves, vines, suns — in every section. Hand-drawn-feeling illustrations of: glass conservatory dome, wind turbine with leaf-blades, stained-glass solar panel, vertical garden tower. Optimistic ecological future. Golden hour everywhere."

---

## Do / Don't

| ✓ Do                                                            | ✗ Don't                                                       |
|-----------------------------------------------------------------|----------------------------------------------------------------|
| Use brass as the metal — always warm                            | Use chrome or silver — instant cyberpunk drift                 |
| Cast warm-terracotta shadows (`rgba(168,90,48,…)`)              | Cast cool gray or blue-tinted shadows                          |
| Pair DM Serif Display italic with Manrope                       | Use condensed display sans (that's cyberpunk territory)        |
| Embed SVG botanicals in every section                           | Skip plant motifs — the page reads as generic eco              |
| Draw tech as plant: turbines = leaves, panels = stained glass   | Show raw circuitry without botanical integration               |
| Animate slowly (14–19s leaf drift, 0.7s section reveal)         | Animate fast — Solar Punk is patient                           |
| Use `❦` botanical ornaments and italic serif in callouts        | Use solid blocks of UI text in spec callouts                   |
| Keep the cream + moss + terracotta + brass signature visible    | Drift toward all-green eco — brass is the differentiator       |
| Let warm light bathe the page (golden-hour radial washes)       | Use stark white surfaces or pure-black text                    |
| Write copy in the optimistic register ("a greener tomorrow")    | Use doom-and-gloom or earnest-hippie tone                      |
| Use brass-gradient buttons for hero/luxury moments only         | Make every button brass — it loses meaning                     |

---

## The Quality Bar

> The page should feel like sitting in a glass conservatory at golden hour: warm cream walls, brass joinery, terracotta pots, mossy green spilling everywhere, sun low through the glass. Not earnest-hippie — *luxurious eco-design studio*. The future is grown, not built.

If any single element on the page could survive a swap into a Cyberpunk page (chrome metal, neon glow, cool shadows, condensed type) — that element doesn't yet belong to Solar Punk. Fix it.

---

*Style guide generated for the UI Styles Gallery · Solar Punk edition · circa 2050.*
