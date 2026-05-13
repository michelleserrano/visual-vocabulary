# AI-Native Style Guide
**UI Styles Library — Version 2.0**
Category: Conversational Shell · Year of register: 2024+

---

## Personality

**Five words:** Warm. Conversational. Cited. Streaming. Composed.

**Voice of this style:** "The canvas is a conversation, not a form. The interface listens, thinks out loud, and replies — token by token — with citations attached. Warm gold on near-black. Generous breathing room. The Claude register, not the cold-blue register."

**Use when:** Building AI assistants, research copilots, code-pair tools, search-and-cite products, agent orchestration UIs, document analysis tools — anywhere the user is in extended dialogue with a model that streams, reasons, and cites.

**Do NOT use when:**
- Marketing landing pages (the register reads as too utilitarian)
- High-density data dashboards (line-height is too generous to scale)
- Brand-forward consumer apps that need chromatic personality (this style is intentionally one-hue)
- Anything where the model is *not* the primary interaction surface

---

## Quick Start — Copy & Paste

```css
:root {
  /* ── Surfaces — near-black, warm undertone ── */
  --bg:        #0d0d11;   /* canvas, page background */
  --surface:   #1a1a22;   /* assistant bubble, cards */
  --surface-2: #232330;   /* sources panel, raised */
  --surface-3: #2c2c3a;   /* tracks, disabled */

  /* ── Accent — warm gold, sole chromatic hue ── */
  --accent:     #c8a868;
  --accent-dim: #8b7355;
  --accent-lo:  rgba(200, 168, 104, 0.14);
  --accent-glow:rgba(200, 168, 104, 0.32);

  /* ── Text — warm off-white scale ── */
  --text:   #f4f1ec;
  --text-2: #a8a39a;
  --text-3: #6b665f;

  /* ── Edges ── */
  --border:   rgba(255, 255, 255, 0.06);
  --border-2: rgba(255, 255, 255, 0.10);
  --border-3: rgba(255, 255, 255, 0.16);

  /* ── Semantic ── */
  --ok:   #7fb88f;
  --err:  #d97a6c;
  --warn: #d9b56c;

  /* ── Shape ── */
  --r-xs:   4px;
  --r-sm:   6px;
  --r:      10px;
  --r-md:   14px;
  --r-lg:   20px;
  --r-full: 9999px;

  /* ── Motion — Apple spring ── */
  --ease:     cubic-bezier(0.32, 0.72, 0, 1);
  --ease-in:  cubic-bezier(0.4, 0, 1, 1);
  --ease-out: cubic-bezier(0, 0, 0.2, 1);

  /* ── Typography ── */
  --f:   'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
  --f-m: 'JetBrains Mono', ui-monospace, 'SF Mono', Menlo, monospace;
}

body {
  font-family: var(--f);
  background: var(--bg);
  color: var(--text);
  font-size: 15px;
  line-height: 1.65;
  -webkit-font-smoothing: antialiased;
  font-feature-settings: 'ss01', 'cv11';
}
```

---

## Token Tables

### Color

| Token | Value | Role |
|-------|-------|------|
| `--bg` | `#0d0d11` | Canvas — the page background; never tinted |
| `--surface` | `#1a1a22` | Assistant bubble, cards, form panels |
| `--surface-2` | `#232330` | Sources panel, code-block heads, raised |
| `--surface-3` | `#2c2c3a` | Slider tracks, disabled fills |
| `--accent` | `#c8a868` | Warm gold — **the only chromatic accent** |
| `--accent-dim` | `#8b7355` | Pressed, borders, low-emphasis gold |
| `--accent-lo` | `rgba(200,168,104,0.14)` | Focus rings, gold backgrounds |
| `--accent-glow` | `rgba(200,168,104,0.32)` | Halo flash, pulsing edges |
| `--text` | `#f4f1ec` | Warm off-white — primary copy |
| `--text-2` | `#a8a39a` | Secondary copy, body of cards |
| `--text-3` | `#6b665f` | Metadata, captions, placeholders |
| `--border` | `rgba(255,255,255,0.06)` | Default edge — barely visible |
| `--border-2` | `rgba(255,255,255,0.10)` | Interactive edge (buttons, inputs) |
| `--border-3` | `rgba(255,255,255,0.16)` | Hover edge |
| `--ok` | `#7fb88f` | Success — desaturated, never neon |
| `--err` | `#d97a6c` | Error / destructive — warm terracotta |
| `--warn` | `#d9b56c` | Warning — gold's sibling |

**Critical rule:** `--accent` is the **only** chromatic hue in the system. Every other UI signal uses the text scale or borders. If you need to add a color, ask twice before doing it.

### Typography

**Typefaces:** `Inter` (body, display) + `JetBrains Mono` (metadata, code, citations)
**Import:** `https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&family=JetBrains+Mono:wght@400;500;600&display=swap`

| Level | Size | Weight | Letter-spacing | Line-height | Use |
|-------|------|--------|----------------|-------------|-----|
| Display | 52px | 600 | −0.04em | 1.05 | Hero headlines |
| H1 | 36px | 600 | −0.032em | 1.1 | Page titles |
| H2 | 26px | 600 | −0.024em | 1.2 | Section headers |
| H3 | 20px | 600 | −0.018em | 1.3 | Card titles |
| Body | 16px | 400 | −0.005em | 1.7 | Standard prose |
| Body SM | 14px | 400 | −0.003em | 1.55 | Secondary copy |
| Mono | 14px | 400 | 0 | 1.55 | Code, metadata, citations |
| Caption | 11px | 500 | +0.04em | — | Status pills, section pills (mono, uppercase) |

**Why Inter + JetBrains Mono:** Inter is the warmest legitimate sans for screens with strong tracking metrics at display sizes. JetBrains Mono is a coding-monospace with rounded terminals — it reads as "system" and "machine" without feeling cold like SF Mono. The pairing carries the conversational shell aesthetic exactly.

### Spacing — 8px grid

| Step | px | rem | Use |
|------|----|-----|-----|
| 1 | 4px | 0.25rem | Icon-label gap, fine adjustments |
| 2 | 8px | 0.5rem | Stack tight elements |
| 3 | 12px | 0.75rem | Compact padding |
| 4 | 16px | 1rem | Standard padding |
| 5 | 20px | 1.25rem | Card inner |
| 6 | 24px | 1.5rem | Section padding |
| 8 | 32px | 2rem | Panel padding |
| 10 | 40px | 2.5rem | Large vertical rhythm |
| 12 | 48px | 3rem | Section gaps |

**Rule:** All spacing is a multiple of 4px (8px preferred). The eye trains on this rhythm — break it and the whole UI loses composure.

### Border Radius

| Token | Value | Use |
|-------|-------|-----|
| `--r-xs` | 4px | Citation chips, kbd, small badges |
| `--r-sm` | 6px | Sidebar items, color swatches |
| `--r` | 10px | Buttons, inputs, default cards |
| `--r-md` | 14px | Source/tool cards, message bubbles, panels |
| `--r-lg` | 20px | Conversation containers, hero widgets |
| `--r-full` | 9999px | Pills, chips, status dots, toggle tracks |

**Rule:** Citation chips and badges go small (4–6px). Cards go medium (14px). Pills go full. Avoid 8px and 12px — they don't sit in this system's rhythm.

### Motion

| Token | Value | Use |
|-------|-------|-----|
| `--ease` | `cubic-bezier(0.32, 0.72, 0, 1)` | Apple spring — default for all transitions |
| `--ease-in` | `cubic-bezier(0.4, 0, 1, 1)` | Element exiting |
| `--ease-out` | `cubic-bezier(0, 0, 0.2, 1)` | Element entering |
| Streaming shimmer | 2.4s linear infinite | Generating text |
| Caret blink | 1.05s steps(1) infinite | End-of-stream cursor |
| Generating dot | 1.4s ease-in-out infinite | Status pulse |
| Thinking edge | 3.6s linear infinite | Subtle edge gradient sweep |
| Halo flash | 0.55s var(--ease) | Active-state confirmation |
| Button hover | 180ms var(--ease) | Default state transition |

**Motion philosophy:** Everything that suggests "the model is working" pulses or sweeps. Everything that is a UI affordance uses the Apple spring (`0.32, 0.72, 0, 1`). The streaming shimmer is the signature — it must be **subtle**, low-contrast, and slow (2.4s). A jumpy shimmer reads as a loading state, not a thinking state.

---

## The 6 Signature Patterns

### 1. Streaming Shimmer

A horizontal gradient sweep across text blocks that signals the text is mid-generation. Low contrast, slow cadence.

```css
.stream-text {
  background: linear-gradient(
    90deg,
    var(--text-2) 0%,
    var(--text-2) 35%,
    var(--text)   50%,
    var(--text-2) 65%,
    var(--text-2) 100%
  );
  background-size: 200% 100%;
  -webkit-background-clip: text;
          background-clip: text;
  -webkit-text-fill-color: transparent;
  animation: shimmer 2.4s linear infinite;
}
@keyframes shimmer {
  0%   { background-position:  200% 0; }
  100% { background-position: -200% 0; }
}
```

**Rules:** Apply only while the model is actively generating. Remove the class the moment streaming completes. Never increase contrast — if you can't see the sweep, lean closer; if it's obvious, it's too loud.

### 2. Citation Chips

Small numbered superscript references that sit inline with prose and link to a source card.

```css
.cite {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  min-width: 18px;
  height: 18px;
  padding: 0 5px;
  background: var(--surface-2);
  border: 1px solid var(--border-2);
  border-radius: var(--r-xs);
  font-family: var(--f-m);
  font-size: 0.625rem;
  font-weight: 600;
  color: var(--accent);
  vertical-align: 0.18em;
  transition: all 0.18s var(--ease);
}
.cite:hover {
  background: var(--accent-lo);
  border-color: var(--accent-dim);
  transform: translateY(-1px);
}
```

**Rules:** Always numbered, never lettered. Always monospaced. Always link to a corresponding source. Hover should lift slightly and tint gold.

### 3. Expandable Thinking Block

A collapsible panel showing the model's reasoning steps, with a subtle pulsing edge while open.

```css
.thinking {
  background: var(--surface);
  border: 1px solid var(--border-2);
  border-radius: var(--r);
  position: relative;
  overflow: hidden;
}
.thinking::before {
  content: '';
  position: absolute;
  inset: 0;
  padding: 1px;
  background: linear-gradient(120deg,
    transparent 30%,
    var(--accent-lo) 50%,
    transparent 70%);
  background-size: 250% 100%;
  -webkit-mask:
    linear-gradient(#fff 0 0) content-box,
    linear-gradient(#fff 0 0);
  -webkit-mask-composite: xor;
          mask-composite: exclude;
  animation: thinking-pulse 3.6s linear infinite;
  pointer-events: none;
  opacity: 0.7;
}
@keyframes thinking-pulse {
  0%   { background-position:  250% 0; }
  100% { background-position: -250% 0; }
}
```

**Rules:** Use `<details>` for native a11y. Chevron rotates 90° when open. Reasoning steps render in JetBrains Mono with a `→` prefix in `--accent-dim`. Show step count and elapsed time in the toggle header.

### 4. Message Bubbles

User on the right (or styled bubble), assistant flush left (no bubble), each with a small avatar dot.

```css
.msg { display: flex; gap: 0.875rem; }
.msg-avatar {
  width: 26px; height: 26px;
  border-radius: 50%;
  font-family: var(--f-m);
  font-size: 0.6875rem;
  font-weight: 600;
}
.msg-avatar.user {
  background: var(--surface-2);
  border: 1px solid var(--border-2);
  color: var(--text-2);
}
.msg-avatar.ai {
  background: linear-gradient(135deg, var(--accent) 0%, var(--accent-dim) 100%);
  color: var(--bg);
  box-shadow: 0 0 0 1px rgba(200, 168, 104, 0.25);
}
.msg.user .msg-bubble {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: var(--r-md);
  padding: 0.75rem 1rem;
}
/* Assistant bubble has NO container — prose flows directly */
```

**Rules:** Assistant messages do **not** sit in a bubble — they flow as prose. Only the user message gets a contained bubble. Avatar is a small gradient dot, never a photo. Author line above the message uses JetBrains Mono in `--text-3`, lowercased.

### 5. Sources Panel

A list of cited URLs at the end of an assistant message, each with a numbered chip and a favicon dot.

```css
.sources {
  margin-top: 1.25rem;
  padding: 1rem 1.125rem;
  background: var(--surface-2);
  border: 1px solid var(--border);
  border-radius: var(--r-md);
}
.source {
  display: flex;
  gap: 0.625rem;
  padding: 0.625rem 0;
  border-bottom: 1px solid var(--border);
}
.source-num {
  width: 18px; height: 18px;
  background: var(--surface);
  border: 1px solid var(--border-2);
  border-radius: var(--r-xs);
  font-family: var(--f-m);
  font-size: 0.625rem;
  font-weight: 600;
  color: var(--accent);
}
.source-favicon {
  width: 14px; height: 14px;
  border-radius: 3px;
  background: var(--accent); /* placeholder; use real favicon */
}
```

**Rules:** Always inside a contained panel (`--surface-2`) so the cited material reads as a separate object from the prose. Each row: number → favicon → title → URL. Title in `--text` 13px, URL in `--f-m` 11px `--text-3`.

### 6. Action Chips

Pill-shaped, monospaced action row that appears below an assistant message — Copy, Regenerate, Continue, Cite.

```css
.chip {
  display: inline-flex;
  align-items: center;
  gap: 0.375rem;
  padding: 0.3rem 0.7rem;
  background: transparent;
  border: 1px solid var(--border-2);
  border-radius: var(--r-full);
  font-family: var(--f-m);
  font-size: 0.6875rem;
  font-weight: 500;
  color: var(--text-2);
  cursor: pointer;
  transition: all 0.18s var(--ease);
}
.chip:hover {
  color: var(--text);
  background: var(--surface);
  border-color: var(--border-3);
}
.chip.gold {
  color: var(--accent);
  border-color: var(--accent-dim);
}
```

**Rules:** Always pill-shaped (`--r-full`). Always monospaced. Always small (11px). Sit on a top-border-separated row beneath the message. The "Cite" chip is the only one that gets the gold variant.

---

## Component Snippets

### Chat Composer (the marquee)

```css
.composer {
  background: var(--bg);
  border: 1px solid var(--border-2);
  border-radius: var(--r-md);
  padding: 0.75rem 0.875rem 0.625rem;
  transition: border-color 220ms var(--ease),
              box-shadow   220ms var(--ease);
}
.composer:focus-within {
  border-color: var(--accent-dim);
  box-shadow: 0 0 0 3px var(--accent-lo);
}
.composer-input {
  width: 100%;
  background: transparent;
  border: none;
  outline: none;
  resize: none;
  font-family: var(--f);
  font-size: 0.9375rem;
  line-height: 1.55;
  color: var(--text);
  max-height: 200px;
}
.composer-send {
  width: 30px; height: 30px;
  border-radius: 50%;
  background: var(--accent);
  border: none;
  color: var(--bg);
}
.composer-send:disabled {
  background: var(--surface-2);
  color: var(--text-3);
}
```

### Token Caret

```css
.caret {
  display: inline-block;
  width: 0.55em; height: 1em;
  margin-left: 1px;
  background: var(--accent);
  vertical-align: text-bottom;
  animation: blink 1.05s steps(1) infinite;
  border-radius: 1px;
}
@keyframes blink {
  0%, 49%   { opacity: 1; }
  50%, 100% { opacity: 0; }
}
```

### Generating Status

```css
.generating {
  display: inline-flex;
  align-items: center;
  gap: 0.625rem;
  padding: 0.375rem 0.75rem;
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: var(--r-full);
  font-family: var(--f-m);
  font-size: 0.6875rem;
  color: var(--text-2);
}
.generating-dot {
  width: 6px; height: 6px;
  border-radius: 50%;
  background: var(--accent);
  animation: gen-pulse 1.4s ease-in-out infinite;
}
@keyframes gen-pulse {
  0%, 100% { transform: scale(0.7); opacity: 0.5; }
  50%      { transform: scale(1.1); opacity: 1; }
}
```

### Code Block (with copy + lang label)

```css
.code-wrap {
  background: var(--bg);
  border: 1px solid var(--border);
  border-radius: var(--r);
  overflow: hidden;
}
.code-head {
  display: flex;
  justify-content: space-between;
  padding: 0.4rem 0.75rem;
  background: var(--surface-2);
  border-bottom: 1px solid var(--border);
  font-family: var(--f-m);
  font-size: 0.6875rem;
  color: var(--text-3);
}
.code-lang  { color: var(--accent); }
.code-body  {
  padding: 0.75rem 1rem;
  font-family: var(--f-m);
  font-size: 0.75rem;
  line-height: 1.65;
  color: var(--text);
  overflow-x: auto;
}
```

### Sidebar Item (Active state)

```css
.sb-item.active {
  background: var(--surface);
  color: var(--text);
  position: relative;
}
.sb-item.active::before {
  content: '';
  position: absolute;
  left: -0.875rem;   /* sits in the gutter, not on the item */
  top: 0.5rem;
  bottom: 0.5rem;
  width: 2px;
  background: var(--accent);
  border-radius: 0 2px 2px 0;
}
```

---

## Comparison Tables

### AI-Native (warm gold) vs. ChatGPT-style (cold blue)

| Dimension | AI-Native (this style) | ChatGPT-style |
|-----------|------------------------|---------------|
| Accent hue | Warm gold `#c8a868` | Cold blue / teal `#10a37f` |
| Background | Near-black, warm undertone `#0d0d11` | Neutral dark `#212121` |
| Text color | Warm off-white `#f4f1ec` | Pure white `#ffffff` |
| Body font | Inter (warm modern sans) | Söhne / system stack |
| Citation pattern | Always-visible inline chips | Footer list, no inline marks |
| Thinking display | Expandable panel with pulsing edge | Hidden by default |
| Action chips | Pill-shaped, monospaced, small | Icon buttons, larger |
| Register | Editorial · meditative · sourced | Utilitarian · neutral · fast |
| Best for | Research, copilots, long-form chat | Quick tasks, broad-audience consumer |

### AI-Native (conversational) vs. Engineer-Mono (terminal)

| Dimension | AI-Native | Engineer-Mono |
|-----------|-----------|---------------|
| Primary font | Inter (proportional) | Full monospace everywhere |
| Mood | Editorial, conversational | Technical, terse, machine |
| Use of mono | Metadata + code only | Headlines + body + UI |
| Line-height | 1.6+ (generous) | 1.4 (compact) |
| Color | Warm gold + warm grays | High-contrast greens or magentas |
| Surface | Soft surfaces with rounded corners | Hard rectangles, sharp grid |
| Best for | AI dialogue products | Developer tools, terminal UIs |

---

## Guiding Principles

**1. The canvas is a conversation, not a form.**
Drop modal-and-button thinking. The user is talking to a model that streams, reasons, and cites. Build the interface to host that exchange — not to collect inputs.

**2. Warm, never cold.**
Gold (`#c8a868`), not blue. Warm off-white (`#f4f1ec`), not pure white. Near-black with warm undertone (`#0d0d11`), not neutral charcoal. If anything starts to read as cold or clinical, you've slipped into the ChatGPT register and need to come back.

**3. Show the thinking.**
The model's reasoning is content, not an implementation detail. Citation chips, sources panels, and expandable thinking blocks are non-negotiable. If you hide the work, you lose the trust.

**4. Streaming is the signature, but it must be subtle.**
The shimmer is what makes the interface feel alive. But it lives between 0.25 and 0.5 contrast — visible when you look, invisible when you don't. A loud shimmer reads as a broken loader.

**5. One accent. One typeface pair. One grid.**
Warm gold is the only chromatic hue. Inter + JetBrains Mono is the only type pair. 8px grid is the only rhythm. Coherence is the style's deepest move; the moment you add a second accent or a third font, the register collapses.

---

## Do's

- **DO** use streaming shimmer on text that is actually being generated, and remove it the instant generation completes.
- **DO** put a 1px subtle border on every surface — borders carry the depth in this style, not shadows.
- **DO** use JetBrains Mono for *all* metadata: timestamps, token counts, citations, status pills, code, file names, model names.
- **DO** anchor the screen on the chat composer — it is the marquee component and should never feel cramped.
- **DO** include citations on any factual claim the assistant makes. Inline chips first, sources panel second.

## Don'ts

- **DON'T** use cold blue, teal, neon green, or any other accent. Gold is the entire chromatic vocabulary.
- **DON'T** use pure white text (`#ffffff`) on dark surfaces — it reads as harsh in this warm-toned system. Use `#f4f1ec`.
- **DON'T** put assistant messages in bubbles. Only the user message gets a container — the assistant's prose flows free.
- **DON'T** crank up the shimmer contrast to "make it more visible." If you have to ask, it's already too loud.
- **DON'T** use serif fonts in the body. Inter is the body face. Serifs read as "blog" and break the register.

---

## Anti-Patterns to Reject Immediately

If any AI-generated output includes these, reject it and re-prompt:

| Anti-pattern | The fix |
|--------------|---------|
| Cold-blue accent (`#3b82f6`, `#10a37f`, etc.) | Replace with warm gold `#c8a868`. Don't argue, just swap. |
| Citations as a numbered footnote list at the bottom only | Add inline `.cite` chips at the point of claim. The footer list is secondary. |
| Assistant message wrapped in a surface container with rounded corners | Strip the container. Assistant prose flows free; only user messages get bubbles. |

---

## AI Prompting Block

Use this block verbatim to instruct any AI coding agent to reproduce this style:

```
Build in AI-Native conversational shell style:

ANCHOR PHRASES (always include these in the prompt):
- "Claude.ai conversational shell aesthetic"
- "Perplexity-style source citations"
- "warm gold on near-black, not cold blue"
- "streaming text shimmer, token-by-token feel"
- "expandable thinking block with pulsing edge"

COLOR (locked):
- Background: #0d0d11 (near-black with warm undertone)
- Surface: #1a1a22 (assistant/card)
- Surface-2: #232330 (sources panel)
- Accent: #c8a868 (warm gold — the ONLY chromatic accent)
- Accent-dim: #8b7355
- Text: #f4f1ec (warm off-white, never pure white)
- Text-2: #a8a39a / Text-3: #6b665f
- Borders: rgba(255,255,255,0.06) → 0.10 → 0.16 (rest → interactive → hover)

TYPOGRAPHY:
- Inter for body and display (400/500/600/700)
- JetBrains Mono for ALL metadata, citations, code, status pills
- Display: 52px / 600 / -0.04em letter-spacing / 1.05 line-height
- Body: 16px / 400 / -0.005em letter-spacing / 1.7 line-height (generous!)
- Tracking obsessive at display sizes (-0.022em to -0.04em)

SIGNATURES (must include at least 3):
1. Streaming shimmer — horizontal gradient sweep, 2.4s linear infinite, subtle low-contrast
2. Citation chips — small numbered mono superscripts that lift on hover
3. Expandable thinking blocks — pulsing edge animation while open
4. Message bubbles — user contained, assistant flows free, small gradient avatar dots
5. Sources panel — numbered chip + favicon + title + URL in surface-2 container
6. Action chips — pill-shaped, monospaced, small, under-message row
7. Token caret — blinking gold cursor at end of streaming text
8. Generating status pill — pulsing dot + monospaced elapsed time

MOTION:
- All transitions: cubic-bezier(0.32, 0.72, 0, 1) (Apple spring) at 180–220ms
- Shimmer: 2.4s linear infinite
- Caret blink: 1.05s steps(1) infinite
- Generating pulse: 1.4s ease-in-out infinite

GRID:
- 8px spacing rhythm exclusively (multiples of 4px allowed for fine work)
- Border radius: 4 → 6 → 10 → 14 → 20 → 9999px (no 8, no 12)

DO NOT use:
- Cold blue, teal, or any non-gold chromatic accent
- Pure white text
- Bubbles around assistant messages
- Serif body fonts
- Loud / fast shimmer animations
```
