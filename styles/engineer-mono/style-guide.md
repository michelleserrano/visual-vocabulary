# Engineer Mono
**Personality: Mono-as-voice. Atmospheric. Engineer-philosophical. Near-monochrome. Generous-whitespace.**

> "Designed by an engineer who also reads philosophy. The monospace isn't decoration — it's the voice of the document. The gradient orbs aren't trends — they're atmosphere. Restraint is the entire feature."

The visual language of **Linear** (linear.app), **Vercel**, **Cursor**, **Raycast**, **Resend**, **Supabase**. A near-monochrome canvas where mono is the body voice, Inter is the rare display moment, violet is the only chromatic affordance, and gently-drifting blurred orbs do all the atmospheric work.

---

## Identity

| Property | Value |
|---|---|
| Origin | The 2020s indie-startup aesthetic — Linear (2019), Vercel rebrand (2021), Cursor / Resend / Supabase (2022–24) |
| Theme | Dark only. There is no light mode in the spirit of this style. |
| Base surface | `#0a0a0c` (warm near-black, never `#000`) |
| Body typeface | **JetBrains Mono** — every paragraph, label, hint, badge, button shortcut |
| Display typeface | **Inter** — only at ≥ 24px, weights 600–700, tight tracking |
| Accent | `#7c5cff` violet — the **only** chromatic moment |
| Status hues | `#2dd4bf` mint · `#fbbf24` amber · `#f87171` coral — status only, never decoration |
| Border-radius | `4–12px` (small, never pill-shaped surfaces — only badges and toggles get full pill) |
| Atmosphere | Large blurred radial gradient orbs (~500–700px, `blur(80px)`), drifting on 20–30s loops |
| Motion curve | `cubic-bezier(0.4, 0, 0.2, 1)` (ease) for transitions; `cubic-bezier(0.32, 0.72, 0, 1)` (spring) for affordances |

---

## Design Tokens

```css
:root {
  /* Surfaces — true dark, warm */
  --bg:        #0a0a0c;
  --bg-2:      #0e0e12;
  --surface-1: #131319;
  --surface-2: #1c1c24;
  --surface-3: #25252f;

  /* Text — opacity scale, never solid white */
  --t1: #ffffff;                   /* primary headings, hero numbers */
  --t2: rgba(255,255,255,0.70);    /* default body */
  --t3: rgba(255,255,255,0.45);    /* labels, captions, muted */
  --t4: rgba(255,255,255,0.22);    /* placeholders, dividers */
  --t5: rgba(255,255,255,0.08);    /* hairlines, faint borders */

  /* The accent — violet, the Linear/Vercel signal */
  --ac:       #7c5cff;
  --ac-hi:    #9b85ff;             /* hover */
  --ac-lo:    rgba(124,92,255,0.15); /* halos, focus rings */
  --ac-faint: rgba(124,92,255,0.04); /* code highlight bg */
  --ac-glow:  rgba(124,92,255,0.35); /* outer shadow glow */

  /* Status (use ONLY for status communication — never as decoration) */
  --ac3:  #2dd4bf;   /* mint — success */
  --warn: #fbbf24;   /* amber — warning */
  --err:  #f87171;   /* coral — error */

  /* Borders — extremely light */
  --border:    1px solid rgba(255,255,255,0.06);
  --border-hi: 1px solid rgba(255,255,255,0.12);

  /* Geometry */
  --r-sm: 4px;
  --r:    6px;
  --r-md: 8px;
  --r-lg: 12px;
  --r-full: 9999px;     /* badges, toggle thumbs, dots */

  /* Typography — mono is the default */
  --f-mono:    'JetBrains Mono', 'Geist Mono', 'SF Mono', Menlo, monospace;
  --f-sans:    'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
  --f-display: 'Inter', sans-serif;
  --f:         var(--f-mono);   /* default body IS mono */

  /* Motion */
  --ease:   cubic-bezier(0.4, 0, 0.2, 1);
  --spring: cubic-bezier(0.32, 0.72, 0, 1);
}

body {
  background: var(--bg);
  color: var(--t1);
  font-family: var(--f);     /* mono — yes, on the body */
  font-size: 14px;
  letter-spacing: -0.005em;
  line-height: 1.55;
  -webkit-font-smoothing: antialiased;
}
```

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&family=JetBrains+Mono:wght@300;400;500;600&display=swap" rel="stylesheet">
```

---

## The Big Rule — Mono as Body Font

**Body text is monospace. Always.** Paragraphs, labels, hints, button shortcuts, badges, table cells, captions — all `JetBrains Mono`. This is the single most important rule of the style. Get this wrong and the page collapses into either generic dark-mode SaaS or generic dark-mode marketing.

| Where | Font | Weight | Size |
|---|---|---|---|
| Hero H1, section titles, stats | **Inter** | 600–700 | ≥ 24px |
| Body paragraphs | **JetBrains Mono** | 400 | 14–16px |
| Labels (form, sec-kicker, status badge) | **JetBrains Mono** | 400 | 11–12px, uppercase, `letter-spacing: 0.10em` |
| Hints, helper, metadata | **JetBrains Mono** | 400 | 11–12px, color `--t3` or `--t4` |
| Buttons (primary, secondary) | **Inter** | 500 | 14px |
| Code-style buttons / kbd shortcuts | **JetBrains Mono** | 400 | 12px |
| Captions, kickers | **JetBrains Mono** | 400 | 11px, uppercase, color `--ac` |

**The split, in one sentence:** Inter for poetry (large, warm), Mono for prose (small, precise).

---

## The Inter Rule — Display Only

Inter only appears at **24px or larger**. At smaller sizes, sans loses its restraint and the design starts to read like marketing.

```css
.h-display { font-family: 'Inter'; font-weight: 700; font-size: 5rem;   letter-spacing: -0.04em;  line-height: 0.97; }
.h1        { font-family: 'Inter'; font-weight: 700; font-size: 2.25rem; letter-spacing: -0.03em; line-height: 1.1; }
.h2        { font-family: 'Inter'; font-weight: 600; font-size: 1.75rem; letter-spacing: -0.025em; line-height: 1.15; }
.h3        { font-family: 'Inter'; font-weight: 600; font-size: 1.375rem; letter-spacing: -0.02em; line-height: 1.25; }
```

**Tracking guide.** Display Inter at large sizes always wants negative tracking — the bigger it gets, the tighter it goes:

| Size | letter-spacing |
|---|---|
| 5rem (display) | `-0.04em` |
| 36px (h1) | `-0.03em` |
| 28px (h2) | `-0.025em` |
| 22px (h3) | `-0.02em` |
| 18px and below (Mono) | `-0.005em` (or `0`) |

---

## Signature — Atmospheric Gradient Orbs

The blurred gradient orbs are **not decoration**. They establish the entire aesthetic. Without them, the page is a generic dark theme. With them, it becomes Vercel/Linear.

### Page-level ambient orbs (always on, always subtle)

```css
.ambient {
  position: fixed;
  inset: 0;
  pointer-events: none;
  z-index: -10;
  overflow: hidden;
}
.ambient::before, .ambient::after {
  content: '';
  position: absolute;
  border-radius: 50%;
  filter: blur(120px);
}
.ambient::before {
  width: 700px; height: 700px;
  background: radial-gradient(circle, rgba(124,92,255,0.18), transparent 65%);
  top: -250px; right: -150px;
  animation: drift-1 26s ease-in-out infinite;
}
.ambient::after {
  width: 600px; height: 600px;
  background: radial-gradient(circle, rgba(45,212,191,0.10), transparent 60%);
  top: 40%; left: -200px;
  animation: drift-2 32s ease-in-out infinite;
}
@keyframes drift-1 { 0%,100% { transform: translate(0,0) scale(1); } 50% { transform: translate(-60px, 50px) scale(1.08); } }
@keyframes drift-2 { 0%,100% { transform: translate(0,0) scale(1); } 50% { transform: translate(80px, -60px) scale(1.10); } }
```

### Per-section orb composition (varies by section)

Each section gets its own orb composition, with different positions and a slightly different secondary hue. Apply `.orb-bg` and a section modifier:

```css
.orb-bg { position: relative; isolation: isolate; }
.orb-bg::before, .orb-bg::after {
  content: '';
  position: absolute;
  border-radius: 50%;
  pointer-events: none;
  filter: blur(80px);
  z-index: -1;
}

/* Hero — big violet, mint accent */
.orb-hero::before {
  width: 720px; height: 720px;
  background: radial-gradient(circle, rgba(124,92,255,0.32), transparent 65%);
  top: -180px; right: -120px;
  animation: drift-1 22s ease-in-out infinite;
}
.orb-hero::after {
  width: 520px; height: 520px;
  background: radial-gradient(circle, rgba(45,212,191,0.14), transparent 60%);
  bottom: -160px; left: -80px;
  animation: drift-2 28s ease-in-out infinite;
}

/* Other sections — single orb, lower intensity */
.orb-colors::before {
  width: 480px; height: 480px;
  background: radial-gradient(circle, rgba(124,92,255,0.18), transparent 60%);
  top: 20%; left: -150px;
}
```

**Recipe.** Per-section orbs follow a formula:
- 1 or 2 orbs per section (max)
- 480–720px diameter
- `filter: blur(80px)` (page-ambient: `blur(120px)`)
- Opacity 0.10–0.32 — never higher
- Position partially **off-canvas** (negative `top`/`right`/`left`)
- Animate 22–32s, ease-in-out, infinite — drifts must feel slower than breathing

---

## Signature — Geometric Line Dividers

Thin 1px horizontal rules with a gradient that fades from transparent at the edges through `--ac-lo` at the center. Optional centered mono label that overlaps the line.

```css
.divider {
  height: 1px;
  background: linear-gradient(90deg,
    transparent,
    var(--t5) 18%,
    var(--ac-lo) 50%,
    var(--t5) 82%,
    transparent
  );
  margin: 5rem 0;
  position: relative;
}
.divider-label {
  position: absolute;
  top: -8px;
  left: 50%;
  transform: translateX(-50%);
  background: var(--bg);
  padding: 0 0.875rem;
  font-family: var(--f-mono);
  font-size: 0.6875rem;
  color: var(--t3);
  letter-spacing: 0.14em;
  text-transform: uppercase;
}
```

```html
<div class="divider"><span class="divider-label">§ specifications</span></div>
```

---

## The Violet-Only Accent Rule

There is one chromatic accent. It is `#7c5cff`. **It only appears where interaction lives** — buttons, focus rings, active states, glows. Mint/amber/coral exist for status badges only and never for decoration.

| ✅ Acceptable use of violet | ❌ Forbidden use |
|---|---|
| Primary button background | Body text |
| Focus halo on inputs | Headings |
| Active sidebar rule | Card backgrounds |
| Status badge `.violet` | Section ghost numbers |
| Caret color | Decorative shapes |
| Active progress dot | Big illustrations |
| Section number `.sec-kicker-num` | Borders that aren't focus |
| Slider fill + thumb | Random hover effects |

If you find yourself reaching for a second hue (cyan, pink, orange) and it's not status — back off. The restraint is the feature.

---

## Status Badges — The Signal Vocabulary

Mono pills with subtle backgrounds. Used liberally throughout: card meta rows, deployment status, system health.

```css
.badge {
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  font-family: var(--f-mono);
  font-size: 0.6875rem;
  font-weight: 400;
  padding: 2px 8px;
  border-radius: var(--r-full);
  border: 1px solid;
  letter-spacing: 0.02em;
  line-height: 1.5;
}
.badge-dot { width: 5px; height: 5px; border-radius: 50%; background: currentColor; }

.badge.success { color: #2dd4bf; border-color: rgba(45,212,191,0.30);  background: rgba(45,212,191,0.06); }
.badge.warn    { color: #fbbf24; border-color: rgba(251,191,36,0.30);  background: rgba(251,191,36,0.06); }
.badge.err     { color: #f87171; border-color: rgba(248,113,113,0.30); background: rgba(248,113,113,0.06); }
.badge.muted   { color: var(--t3); border-color: var(--t5); background: var(--surface-1); }
.badge.violet  { color: #9b85ff; border-color: rgba(124,92,255,0.35); background: rgba(124,92,255,0.06); }
```

```html
<span class="badge success"><span class="badge-dot"></span>passing</span>
<span class="badge warn"><span class="badge-dot"></span>building 32%</span>
<span class="badge muted">v1.4.0</span>
<span class="badge violet"><span class="badge-dot"></span>preview</span>
```

---

## Spec Callout — The `// note` Pattern

Dark surface with a left-rule violet bar. Mono throughout. The label reads like a code comment.

```css
.spec-callout {
  background: var(--surface-1);
  border: var(--border);
  border-left: 2px solid var(--ac);
  border-radius: var(--r-md);
  padding: 1rem 1.25rem;
  font-family: var(--f-mono);
}
.spec-callout-label { font-size: 0.6875rem; color: var(--t3); letter-spacing: 0.04em; }
.spec-callout-text  { font-size: 0.8125rem; color: var(--t2); line-height: 1.65; }
.spec-callout-text code {
  color: var(--ac-hi);
  background: var(--ac-faint);
  padding: 0.0625rem 0.375rem;
  border-radius: 3px;
}
```

---

## Buttons — Four Voices

```css
.btn {
  display: inline-flex; align-items: center; justify-content: center;
  gap: 0.4375rem;
  padding: 0.5rem 1rem;
  border-radius: var(--r-md);
  font-family: var(--f-sans);
  font-size: 0.875rem;
  font-weight: 500;
  cursor: pointer;
  border: none;
  transition: all 0.18s var(--ease);
}
.btn-p { background: var(--ac); color: #fff; }
.btn-p:hover { background: var(--ac-hi);
  box-shadow: 0 0 0 1px rgba(155,133,255,0.40), 0 6px 20px rgba(124,92,255,0.30); }
.btn-p:active { transform: scale(0.98); }

.btn-s { background: transparent; color: var(--t1); border: 1px solid var(--t5); }
.btn-s:hover { border-color: var(--t3); background: var(--surface-1); }

.btn-g { background: transparent; color: var(--t2); font-family: var(--f-mono); font-size: 0.8125rem; padding: 0.5rem 0.75rem; }
.btn-g:hover { color: var(--t1); text-decoration: underline; text-underline-offset: 4px; }

.btn-c {
  background: var(--surface-2);
  color: var(--t1);
  border: var(--border-hi);
  font-family: var(--f-mono);
  font-size: 0.75rem;
  padding: 0.375rem 0.625rem;
}
.btn-c kbd { color: var(--t3); margin-left: 0.4rem; padding-left: 0.4rem; border-left: 1px solid var(--t5); }
```

| Variant | When to use |
|---|---|
| **Primary** (`btn-p`) | The single most important action. One per view. Inter. |
| **Secondary** (`btn-s`) | Alternate actions. Outlined. Inter. |
| **Ghost** (`btn-g`) | Tertiary links, "view docs", "skip". Mono, underlines on hover. |
| **Code-style** (`btn-c`) | Keyboard shortcuts, command palette triggers. Mono with optional `<kbd>`. |

---

## Form Inputs — Editor-grade

```css
.inp {
  width: 100%;
  background: var(--bg-2);
  border: var(--border-hi);
  border-radius: var(--r-md);
  padding: 0.625rem 0.875rem;
  font-family: var(--f-mono);
  font-size: 0.8125rem;
  color: var(--t1);
  outline: none;
  caret-color: var(--ac);
  transition: border-color 0.15s var(--ease), box-shadow 0.18s var(--ease);
}
.inp:focus {
  border-color: var(--ac);
  box-shadow: 0 0 0 3px var(--ac-lo);
}
.label {
  font-family: var(--f-mono);
  font-size: 0.6875rem;
  color: var(--t3);
  letter-spacing: 0.08em;
  text-transform: uppercase;
}
```

**Focus rule.** Always `1px violet border + 3px violet halo` (`box-shadow: 0 0 0 3px var(--ac-lo)`). Caret matches the accent. The halo is the affordance — no labels move, no rings inflate, no underlines animate in.

**Toggle.** Track is 32×18px (small). When checked, track fills violet and gets an outer glow. Thumb is white, 12px circle.

**Checkbox.** 16×16px square with 3px radius. When checked, fills violet with a glow; the check is white.

---

## Cards — Documentation Aesthetic

```css
.card {
  background: var(--surface-1);
  border: var(--border);
  border-radius: var(--r-lg);
  overflow: hidden;
  transition: all 0.28s var(--ease);
}
.card:hover {
  border-color: rgba(124,92,255,0.30);
  transform: translateY(-3px);
  box-shadow:
    0 24px 48px -12px rgba(0,0,0,0.4),
    0 0 0 1px rgba(124,92,255,0.06),
    0 0 32px -8px var(--ac-glow);
}
```

Each card thumbnail shows one of three things, never a photograph:
1. **Code snippet** — mono, syntax-highlighted, dark surface
2. **Atmospheric orb gradient** — single radial gradient, optionally with a faint grid overlay
3. **Terminal session** — `$` prompt, output line, blinking caret

---

## Sliders — Hairline Tracks

A 1px horizontal track. Solid violet fill. A 12px violet circle thumb with a 4px halo and 14px outer glow. Tabular-figure readout to the right.

```css
.rng {
  -webkit-appearance: none;
  width: 100%;
  height: 16px;
  background: transparent;
  outline: none;
  --val: 50%;
}
.rng::-webkit-slider-runnable-track {
  height: 1px;
  background: linear-gradient(to right, var(--ac) 0%, var(--ac) var(--val), var(--t5) var(--val), var(--t5) 100%);
}
.rng::-webkit-slider-thumb {
  -webkit-appearance: none;
  width: 12px; height: 12px;
  border-radius: 50%;
  background: var(--ac);
  margin-top: -5.5px;
  box-shadow: 0 0 0 4px rgba(124,92,255,0.18), 0 0 14px rgba(124,92,255,0.35);
}
```

Tip: in JS, set `el.style.setProperty('--val', pct + '%')` on input to draw the violet fill correctly across browsers.

---

## Section Headings — `§` Number Format

Section heads carry three layers:
1. **Mono kicker** above with the section number: `§ 03 / 08 — Buttons`
2. **Inter display heading** — large, tight, max 18ch wide
3. **Mono lede** — the explanatory paragraph beneath, max 60ch
4. (Optional) **Ghost mega-number** behind the heading at `rgba(255,255,255,0.025)`, JetBrains Mono 600, ~9rem

```html
<div class="sec-hd">
  <span class="sec-ghost">03</span>
  <span class="sec-kicker">§ <span class="sec-kicker-num">03</span> / 08 — Buttons</span>
  <h2 class="sec-title">Four voices. One accent.</h2>
  <p class="sec-lede">Primary in violet for the single most important action…</p>
</div>
```

---

## Generous Whitespace

Sections have **5–8rem of top margin**. Cards have ample internal padding. Form fields breathe. Never crowd.

| Element | Spacing |
|---|---|
| Between `<section>` blocks | 8rem (`5rem` mobile) |
| Section heading → first content | 3rem |
| Inside `.spec-callout` | 1rem 1.25rem |
| Inside `.card` | 1.125rem 1.25rem |
| Form field gap | 1.5rem (vertical), 1.25rem (horizontal) |
| Page max-width | 880px |

If a section feels packed, increase the surrounding margin before adjusting anything inside.

---

## Comparison — How Engineer Mono Differs From IBM Carbon

The two styles look superficially similar (both dark, both use mono, both have a single accent). They are completely different in spirit.

| | **IBM Carbon** | **Engineer Mono** |
|---|---|---|
| **Mono usage** | Labels and code only | **Body voice** — paragraphs, buttons, badges, everything < 18px |
| **Sans usage** | Body and headings | Headings only (≥ 24px) |
| **Background** | Flat `#161616` gray | Warm near-black `#0a0a0c` with **drifting orbs** |
| **Atmosphere** | None — strict, flat surfaces | Atmospheric — gradient orbs, soft glows, slow drift |
| **Border-radius** | `0px` (zero everywhere) | `4–12px` (warm, not extreme) |
| **Whitespace** | Dense — 8px grid, packed dashboards | Generous — 5–8rem section gaps, 880px column |
| **Accent** | IBM Blue `#0f62fe` (corporate, industrial) | Violet `#7c5cff` (creative, indie-startup) |
| **Status colors** | `#fa4d56` red, `#42be65` green, `#f1c21b` yellow | `#f87171` coral, `#2dd4bf` mint, `#fbbf24` amber (softer, more contemporary) |
| **Personality** | Enterprise specification | Indie-startup philosophy |
| **Reference apps** | IBM Cloud, Watson, internal enterprise dashboards | Linear, Vercel, Cursor, Raycast, Resend, Supabase |
| **Typical user** | Enterprise engineer/admin | Solo dev / startup team |
| **Emotional register** | "Every pixel is intentional" | "Designed by an engineer who also reads philosophy" |

Both styles are **right** — for different products. Carbon for enterprise dashboards with hundreds of data points per screen. Engineer Mono for marketing sites, dev tools, deploy pipelines, and command palettes where restraint is the brand promise.

---

## Anti-Patterns

Things that break the aesthetic instantly:

| ❌ Don't | Why |
|---|---|
| **Body text in sans** | Page collapses into generic dark-mode SaaS |
| **More than one bright accent** | Restraint is the entire feature |
| **Photos or illustrations as card thumbs** | Use code snippets, orbs, or terminals |
| **Flat backgrounds with no orbs** | Page reads as a wireframe, not a product |
| **Pure `#000` background** | Eye fatigue; warmth (`#0a0a0c`) is structural |
| **High-contrast white text everywhere** | Use opacity scale (`t1`→`t5`); never solid white-on-white |
| **Dense layouts** | This style requires whitespace — if you're packing, you're wrong |
| **Drop shadows on the page** | Only cards on hover get a violet glow; no shadows on inputs, buttons-at-rest |
| **Rounded everything** | Radii are `4–12px`, not `16–24px` — never feel claymorphic |
| **Bouncy spring motion** | Press is `scale(0.98)`, not a translateY bounce |
| **Translucent cards / glassmorphism** | Surfaces are opaque; only the orbs do atmosphere |
| **Loud color in code snippets** | Code uses muted violet/cyan/mint — never the full Monokai palette |
| **Display text in mono** | Mono is the body voice; display is Inter, always |

---

## AI Prompting Guidance

When you want an LLM (Claude, GPT, Cursor) to generate this aesthetic, anchor with these phrases:

**Yes** ✅
- "Linear / Vercel mono aesthetic"
- "engineer-philosophical, near-monochrome"
- "JetBrains Mono as body voice, Inter as display only"
- "true near-black background with drifting violet gradient orbs"
- "single violet accent, generous whitespace, 1px hairline dividers"
- "Cursor / Raycast minimalism — feels like reading documentation"
- "monospace pills for status, code-style keyboard-shortcut buttons"

**No** ❌
- "dark theme dashboard" (too generic — could be Bloomberg or Carbon)
- "neon glow" (this style is *soft* glow, not arcade glow)
- "futuristic" (this style is calm, not sci-fi)
- "vibrant" (the only vibrant element is one violet)
- "playful" (this style is serious — it's earnest, not whimsical)

**Skeleton prompt:**
> Build a [thing] in the Engineer Mono aesthetic — like Linear / Vercel / Cursor. Body text in JetBrains Mono. Headings in Inter at large display sizes only. Background `#0a0a0c` with drifting blurred violet gradient orbs. Single violet accent `#7c5cff` for buttons, focus rings, active states. Status uses mono pill badges (mint = success, amber = warn, coral = error). Generous whitespace. Hairline 1px dividers with optional centered `§` labels. Cards rest on `#131319` and gain a violet halo on hover.

---

## Personality, in One Paragraph

Engineer Mono is what happens when an engineer who also reads philosophy designs a product. The page reads like well-written documentation — every word in JetBrains Mono, every spacing decision deliberate, every color held back. The single violet accent is a vow: this is the *only* place we will touch saturation. The drifting gradient orbs are not decoration — they're atmosphere, the way a bookshop has a smell. And the generous whitespace says: *we trust you to read this slowly.*

> "Restraint, not minimalism. Atmosphere, not decoration. Mono, not for code — for everything."
