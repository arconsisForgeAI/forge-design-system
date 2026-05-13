# arconsis Forge — Design System

This folder is the source of truth for the arconsis Forge brand. Use these tokens, fonts and logos whenever you produce anything that ships under the Forge name (slides, posts, docs, ads, internal tools).

---

## Brand vibe

Pure black canvas. Warm fire and earth tones. Engineering tone, not marketing tone. No blue. No corporate gloss.

The look should read **"forged in production"** — closer to a workshop than a startup pitch deck.

---

## Color tokens

Use these tokens directly in CSS, design tools or slides. Names are stable; hex values are the source of truth.

| Token            | Hex        | Use                                              |
|------------------|-----------|--------------------------------------------------|
| `--bg`           | `#000000` | Main background. Always pure black.              |
| `--surface`      | `#0a0602` | Cards, panels, raised surfaces.                  |
| `--surface-hi`   | `#120b04` | Modals, elevated overlays.                       |
| `--fire-deep`    | `#7a2000` | Gradient start, deep accent.                     |
| `--fire-mid`     | `#d04500` | Borders, eyebrow labels.                         |
| `--fire-hi`      | `#d04800` | Gradient end, hover state.                       |
| `--fire-glow`    | `#e86010` | Links, badges, primary accent on dark.           |
| `--fire-bright`  | `#ff7820` | Headline gradient peak, focus rings.             |
| `--text`         | `#ffffff` | Primary text. Always pure white on dark.         |
| `--border`       | `rgba(255,255,255,0.055)` | Hairline dividers.                  |
| `--border-fire`  | `rgba(190,70,0,0.30)`     | Card borders.                       |

**Hierarchy on dark backgrounds is built through font weight (300/400/600/700/900) and font size, never through grey gradations.** Pure white reads cleaner than any warm-white we tried.

---

## Signature gradients

Three gradients carry the brand. Use them exactly as written.

```css
/* CTA buttons — flat angled gradient */
background: linear-gradient(135deg, #7a2000, #d04800);

/* Headlines, wordmark — wider gradient with bright peak */
background: linear-gradient(118deg, #d04500 0%, #ff7820 100%);

/* Furnace glow — subtle warm pool from below */
background: radial-gradient(ellipse 90% 40% at 50% 100%, rgba(150,45,0,.22), transparent 65%);
```

For headline gradient text, apply on an inline `<span>` only, not on a block element. Block-level `background-clip: text` produces a 1px artifact in Chrome PDF export.

---

## Typography

Two fonts carry everything. Don't add a third.

| Role     | Font                | Weights                |
|----------|---------------------|------------------------|
| Display  | **Outfit** (variable) | 300 / 400 / 600 / 700 / 800 / 900 |
| Body     | **Inter**             | 300 / 400 / 500 / 600 |
| Mono     | DM Mono             | 400 (only when truly needed) |

Both load free from Google Fonts:

```html
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Outfit:wght@300..900&display=swap" rel="stylesheet">
```

**Display rules**
- Headlines: Outfit 700–800, line-height 1.05–1.15, letter-spacing -0.01 to -0.02em
- Use the headline gradient on the punchline word only, not the whole sentence
- All-caps eyebrow labels: Inter 11–12px, letter-spacing 0.18–0.2em, color `--fire-glow`

---

## Logos

Files in `logos/`:

| File                        | Variant            | Use                                                     |
|-----------------------------|--------------------|---------------------------------------------------------|
| `forge-flame.png`           | Bildmarke (icon)   | Favicons, small placements, anywhere width < 80px       |
| `forge-wordmark.png`        | Schriftlogo (text + icon) | Hero, slide covers, signature placements         |
| `logos/products/amp.png`    | AMP product mark   | AMP product page, Forge product pitch                   |
| `logos/products/p4e.png`    | Paperclip4Enterprise mark | P4E product page, Forge product pitch            |
| `logos/products/kap.png`    | KAP product mark   | KAP placements (roadmap)                                |

### Logo rules

- **Background must be dark.** All Forge logos are designed for pure black or near-black surfaces. The wordmark is white text + diamond on transparent — on a white renderer (Figma preview, Quicklook, Slack thumbnail) you only see the diamond and think it's a pure icon mark. Always preview against `#000000` before using.
- **Minimum clearspace:** half the height of the logo on every side. Don't crowd it.
- **Don't recolor.** No outlines, no fills, no drop shadows beyond the standard glow variant.
- **Don't stretch.** Lock aspect ratio always.
- **Pair the wordmark with a glow** when it sits in a hero or cover. Standard hero glow: `drop-shadow(0 0 70px rgba(232,96,16,.55))`.

### Favicons

Available in `favicons/`:
- `favicon.ico` (multi-icon, 16/32/48 px)
- `favicon-16.png`, `favicon-32.png`
- `apple-touch-icon.png` (180×180)

All generated from `logos/forge-flame.png`.

### Product demo videos

Available in `demos/`:
- `amp-demo.webm`
- `p4e-demo.webm`

---

## Components (CSS reference)

These are the patterns used across the website. Reuse them when you build new pages.

### Card surface (`.gc`, used by all glass cards)

```css
background: linear-gradient(160deg, rgba(78,32,8,.95) 0%, rgba(42,18,6,.92) 38%, rgba(16,8,3,.88) 100%);
border: 1px solid rgba(232,96,16,.22);
box-shadow: inset 0 1px 0 rgba(255,255,255,.08), 0 8px 28px rgba(0,0,0,.6);
border-radius: 18px;
```

Top wash on `::before`:
```css
background: linear-gradient(180deg, rgba(255,140,50,.10), transparent);
```

Hover:
```css
border-color: rgba(255,120,32,.55);
box-shadow: 0 22px 70px rgba(0,0,0,.75), inset 0 1px 0 rgba(255,200,150,.18);
```

### Primary button (CTA)

```css
background: linear-gradient(135deg, #7a2000, #d04800);
color: #ffffff;
border: 1px solid rgba(255,120,32,.6);
border-radius: 999px;
padding: 12px 22px;
font-family: 'Outfit', sans-serif;
font-size: 14px;
font-weight: 600;
letter-spacing: 0.4px;
```

### Secondary button (ghost)

```css
background: transparent;
color: #ffffff;
border: 1px solid rgba(255,255,255,.18);
border-radius: 999px;
padding: 12px 22px;
font-family: 'Outfit', sans-serif;
font-size: 14px;
font-weight: 600;
```

Hover both buttons → inherit the primary CTA gradient.

### Eyebrow label

```css
font-family: 'Inter', sans-serif;
font-size: 12px;
font-weight: 600;
letter-spacing: 0.18em;
text-transform: uppercase;
color: var(--fire-glow);
```

---

## Writing style

These are the lines we don't cross when we write under the Forge name.

**Don't**
- Em-dashes (`—` / `–` with spaces). Use periods, colons, commas or rewrite as two sentences.
- "It's not X, it's Y" antithesis. Make the positive statement directly.
- Filler adjectives: *seamless, robust, cutting-edge, leverage, unlock, navigate, in the realm of*.
- Empty openers: "In today's fast-paced world", "Im Zeitalter von KI", "Let's dive in".
- Tricolons of three when two work: "fast, reliable, and scalable" → cut to two.
- Meta-commentary: "This article explores…", "Dieser Beitrag zeigt…".

**Do**
- Short sentences. Fragments are allowed. Vary rhythm.
- Concrete nouns and numbers over abstractions.
- Active voice. "We ship X." not "X is shipped."
- One thesis per paragraph. No filler.
- When in doubt, write less.

---

## Email and contact

The Forge contact email is **`forge@arconsis.com`** — always lowercase `f`. Don't capitalize, even at the start of a list item or after a period. Don't apply CSS `text-transform: capitalize` to it.

Operator: arconsis IT-Solutions GmbH, Am Storrenacker 8, 76139 Karlsruhe, Germany.

---

## Quick reference card

| Need              | Answer                                  |
|-------------------|-----------------------------------------|
| Background color  | `#000000` (always)                      |
| Accent color      | `#e86010` (fire-glow)                   |
| Headline font     | Outfit 700–800, gradient on punchline   |
| Body font         | Inter 400                               |
| Logo for cover    | `logos/forge-wordmark.png` + glow       |
| Logo for icon use | `logos/forge-flame.png`                 |
| Email             | `forge@arconsis.com` (lowercase f)      |
| No                | Em-dashes, blue, AI buzzwords           |

---

If you're unsure whether something is on-brand, check the live site `arconsisforgeai.github.io/forge-website` and the original brand kit in the Knowledge Vault. Anything that contradicts this README on either of those is outdated.
