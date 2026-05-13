# arconsis Forge — Design System

The full design reference for **arconsis Forge**. Colours, typography, logo usage, layout patterns by format (web, carousels, slides, ads), motion, accessibility, voice and known rendering pitfalls.

For repo orientation and asset paths, see [`README.md`](./README.md).

> **Contact:** `forge@arconsis.com` (lowercase `f`, always. Never `Forge@arconsis.com`. Do not work around this with CSS `text-transform`.)

---

## 1. Brand idea

Forge is a forge. Pure black, warm fire and earth tones. **No blue.** No grey copy. Type is heavy and confident. Motion is slow and ember-like.

Hierarchy comes from **font weight and size**, not from colour. All copy renders in pure white on black. If something looks weak, increase weight, do not desaturate.

---

## 2. Colour tokens

Define these as CSS custom properties on `:root` (or as constants in any other tooling).

| Token | Value | Use |
|-------|-------|-----|
| `--bg` | `#000000` | Page / canvas background |
| `--surface` | `#0a0602` | Cards, panels |
| `--surface-hi` | `#120b04` | Modals, elevated surfaces |
| `--border` | `rgba(255,255,255,0.055)` | Subtle separators |
| `--border-hi` | `rgba(255,255,255,0.10)` | Hovered separators |
| `--border-fire` | `rgba(190,70,0,0.30)` | Card borders (warm) |
| `--border-fire-hi` | `rgba(230,100,0,0.55)` | Card borders on hover |
| `--fire-deep` | `#7a2000` | Gradient start, deep CTA |
| `--fire-mid` | `#d04500` | Mid-gradient, eyebrows on dark |
| `--fire-hi` | `#d04800` | Hover, mid-gradient end |
| `--fire-glow` | `#e86010` | Links, accents, page numbers |
| `--fire-bright` | `#ff7820` | Headline gradient peak, focus ring |
| `--text` | `#ffffff` | All primary text |
| `--text-sec` | `#ffffff` | Subheadlines (hierarchy via weight) |
| `--muted` | `#ffffff` | Labels |
| `--muted-hi` | `#ffffff` | Body text |
| `--ease` | `cubic-bezier(0.16,1,0.3,1)` | Standard easing |

### Signature gradients

```css
/* CTA buttons */
background: linear-gradient(135deg, #7a2000, #d04800);

/* Headline / wordmark accent */
background: linear-gradient(118deg, #d04500 0%, #ff7820 100%);

/* Furnace glow behind hero / CTA */
background: radial-gradient(ellipse 90% 40% at 50% 100%,
            rgba(150,45,0,.22), transparent 65%);

/* Card surface (warm forge wash) */
background: linear-gradient(160deg,
            rgba(78,32,8,.95)  0%,
            rgba(42,18,6,.92) 38%,
            rgba(16,8,3,.88) 100%);
```

---

## 3. Typography

**Two faces only.** Nothing else.

| Role | Family | Weights |
|------|--------|---------|
| Display, headlines, wordmark | **Outfit** | 300, 400, 500, 600, 700, 800, 900 |
| Body, subheadlines, page numbers, captions, UI | **Inter** | 300, 400, 500, 600, 700 |

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;500;600;700;800;900&family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
```

Banned: DM Sans, DM Mono, Big Shoulders, Bricolage, Syne, Space Grotesk, Barlow Condensed, JetBrains Mono. Do not introduce a third family for "small accents".

### No eyebrow labels

Slides and sections **start directly with the headline**. No small uppercase labels above headlines like `STATUS QUO`, `KLEINGEDRUCKTES`, `UNPOPULAR OPINION`. The headline carries alone.

---

## 4. Logos

Files live under `logos/`, `favicons/`, `demos/`.

| File | Use |
|------|-----|
| `logos/forge-flame.png` | Pure flame inside diamond (image mark). Hero, favicons, small marks, hero cinemagraph. |
| `logos/forge-wordmark.png` | Flame + "arconsis Forge" wordmark, no glow. Footer, dense layouts, top-left header in slides. |
| `logos/forge-badge.png` | Compact badge for thumbnails, social profiles. |
| `logos/products/amp.png`, `p4e.png`, `kap.png` | Master product logos (1.5 MB each). |
| `logos/products/amp-web.png`, `p4e-web.png`, `kap-web.png` | Optimised web-size variants (~60–100 KB). |
| `favicons/favicon.ico`, `favicon-16.png`, `favicon-32.png`, `apple-touch-icon.png` | Browser / app icons. |
| `demos/amp-demo.webm`, `p4e-demo.webm` | Product demo videos (B-roll). |

### Sizing reference

| Surface | Wordmark size |
|---------|---------------|
| Web nav | 60 px |
| Web hero | 96 px |
| Web footer (landing) | 54 px |
| Web footer (product pages) | 42 px |
| Web CTA box | 180 px with `drop-shadow(0 0 70px rgba(232,96,16,.55))` |
| Carousel slide top-left header | 340 × 181 container, `background-size: contain` |
| 16:9 slide top-left | target height 72 px, x=60, y=58 |

### Critical: composite before previewing

The wordmark text is white on a transparent background. Default image previewers (Finder, web upload widgets, Slack hover) render the asset on white and show only the diamond, making it look like a pure image mark. Always composite over `#000` or `--surface` before judging it.

### Customer logo handling

Customer/client logos are **not** stored in this repo. When a Forge artefact needs a "trusted by" row, source the original logos per use case. Render them as **white silhouettes** via `filter: brightness(0) invert(1)`, opacity `.78` (hover `1`). The source PNG must have a transparent background.

---

## 5. Patterns by format

### 5.1 Web — cards, hero, CTA

**Cards** (`.gc`, `.apart-item`, `.svc-row`, `.aud-card`):

```css
background: linear-gradient(160deg,
            rgba(78,32,8,.95) 0%,
            rgba(42,18,6,.92) 38%,
            rgba(16,8,3,.88) 100%);
border: 1px solid rgba(232,96,16,.22);
box-shadow: inset 0 1px 0 rgba(255,255,255,.08),
            0 8px 28px rgba(0,0,0,.6);
```

`::before` adds a top wash: `linear-gradient(180deg, rgba(255,140,50,.10), transparent)`. On hover: border `rgba(255,120,32,.55)`, shadow `0 22px 70px rgba(0,0,0,.75)`.

**Hero layout:**

```
[Wordmark, h: 96px]
[Lead "Part of the {arconsis Group}" link]
[H1 in 3 lines, last line in fire gradient]
[Lead paragraph]
[CTA pair: primary fire-gradient + secondary outline]
[Right column: forge-flame.png with slow flameBreathe animation]
```

**CTA box:**

```css
max-width: 900px;
padding: 60px 50px;
border: 1px solid rgba(232,96,16,.34);
box-shadow: 0 24px 80px rgba(232,96,16,.18);
```

Inner radial: 920×520 `rgba(232,96,16,.26)`. Top hairline: `linear-gradient(90deg, transparent, rgba(255,120,32,.7), transparent)`.

**Bento "what we do" grid:** 3D inner-layer parallax. `.bento { perspective: 1600px }`, cards rotate up to 8°. Inner elements lifted via `translateZ`: icon 60px, h3 40px, p 22px. Disable under `prefers-reduced-motion`.

**Services list:** No numbers. Vertical "ember bar" left of each row, gradient top-to-bottom `--fire-deep` → `--fire-glow` → `--fire-bright`, box-shadow `0 0 10px rgba(232,96,16,.4)`. Hover: bar grows 3 → 5 px, glow 10 → 18 px.

### 5.2 4:5 carousels (1080 × 1350) — Instagram, LinkedIn

**Canvas:** 1080 × 1350 px.
**Padding:** `44px 60px 110px 60px`. Bottom padding ≥ 100 px is non-negotiable. Below 80 px the footer drops into the furnace glow and copy gets eaten.

**Body reset (mandatory for Chrome headless renders):**

```css
html, body {
  margin: 0 !important;
  padding: 0 !important;
  width: 1080px;
  overflow: hidden !important;
  background: #000;
}
```

Without this, Chrome headless leaves a 15–25 px sub-pixel artefact "frame" on the left and top edges (~`#0E0E0E` instead of pure black). The `* { margin: 0 }` reset is not enough.

**Bottom glow stack** (radials first, linear last):

```css
background:
  radial-gradient(140% 70% at 50% 118%, rgba(255,120,32,.42) 0, transparent 72%),
  radial-gradient(180% 60% at 50% 122%, rgba(208,69,0,.26)   0, transparent 80%),
  linear-gradient(to top, rgba(180,58,0,.18) 0%, rgba(180,58,0,.08) 18%, transparent 48%),
  #000;
```

Anchor radial centres **outside the slide** (`118%`, `122%`) so the hot spot is never in frame. Never set a linear stop below 14 % with alpha > 0.30 — that produces a visible horizontal "wall".

**Type sizes (Founder Story scale, scale down for denser slides):**

```
hero-xl:    168 px / 900 / -.04em
hero-lg:    122 px / 800 / -.035em
hero-md:     86 px / 700 / -.025em
hero-sm:     68 px / 700 / -.02em
sub:         46 px / 500 / -.01em
meta:        32 px / 400
footer-note: 38 px / 500
page-num:    60 px / 700  (Inter, no letter-spacing, no uppercase, current digit in --fire-glow)
```

Never go below 24 px on labels or 30 px on the footer note.

**Header:** Wordmark top-left in a 340 × 181 container, `background-size: contain`. Page number top-right (`current/total`, current in `--fire-glow`, slash + total in white).

**Footer arrow:** Bottom-right on every content slide. **Not** on the final / CTA slide — there the email box is the terminal element.

**Chrome headless 8K cutoff:** When stack-rendering ≥ 6 slides at 1350 px height, Chrome cuts the last ~80–90 px of the stitched output to black. Fix: render with `--window-size={W},{total_h + 200}`, plus `--run-all-compositor-stages-before-draw` and `--virtual-time-budget=20000`. Crop the result, do not resize. Smoke-test the bottom 100 px of the last slide for `(0,0,0)`.

### 5.3 16:9 slides (1920 × 1080) — pitch decks, web hero banners

**Canvas:** 1920 × 1080 px.

**No tech aesthetic.** No terminal headers, no JetBrains Mono headlines, no grid backgrounds, no progress bars. That is a different (and rejected) direction.

**No lead text, no eyebrows, no card headers.** A 16:9 product showcase shows hero + logo + abbreviation + caption + short paragraph per column.

**Geometry (3-product showcase):**

| Token | Value |
|-------|-------|
| Wordmark top-left | `target_h=72`, `x=60`, `y=58` |
| Margin-X | 60 |
| Column count | 3, equal width |
| Gap between columns | 28 |
| Column width | `(1920 − 120 − 56) / 3 ≈ 581` |
| Panel top / bottom | 150 / 1010 (panel height 860) |

**Hero panel composition:**

```
darken         = 0.24
grad_start_pct = 0.20    # bottom fade starts early
grad_end_pct   = 0.58    # full black from ~58% panel height
top_fade_pct   = 0.16
top_fade_alpha = 200
crop_bias      = 0.22 (people-heavy crops) or 0.30 (product-heavy)
```

`grad_end = 0.58` is intentional and **overrides** the carousel default (`0.92`). The text in 16:9 sits **under** the hero, not on it, so the lower 42 % must be solid black for legibility.

**Text stack per column (centered, top → bottom):**

```
product logo    →  cy = panel_top + 0.45·panel_h, height 160
abbreviation    →  Outfit Bold 124, fire gradient (118°)
full name       →  Inter SemiBold 20, letter-spacing +3, white, uppercase
hairline        →  1 px, ±90 px from centre, color (90,54,30)
description     →  Inter Regular 20, line-height 1.32, white
```

**Furnace floor:** `floor_start = 0.92`, intensity 0.85, radial hot-spot anchored at `(W/2, H + 40)` outside the frame.

### 5.4 Single-image social posts

For square (1080×1080) or 4:5 single posts, follow the 4:5 carousel rules with these deltas:

- One slide, no page number, no footer arrow.
- Headline scale: `hero-md` (86 px) for square, `hero-lg` (122 px) for 4:5.
- Forge wordmark bottom-left or top-left, never both.
- CTA / email line at the bottom in `footer-note` size.

### 5.5 Display ads, banners

- Always carry the wordmark + flame visible.
- Headline in fire gradient or solid `--fire-bright` (PDF-safe — see §8).
- Background: pure `#000` with optional furnace radial bottom-anchored outside the frame.
- CTA button in `linear-gradient(135deg, #7a2000, #d04800)`, Outfit 600, 14 px, padding 13×28.
- No animated rasters that flash. Slow ember pulses only. Respect `prefers-reduced-motion` if delivered as HTML5.

---

## 6. Motion

- Standard easing: `cubic-bezier(0.16,1,0.3,1)`.
- Card hovers: 220 ms.
- Hero flame breathe: 6.5 s, infinite, `scale(1) ↔ scale(1.025)`, drop-shadow pulses with it.
- Sparks loops: low opacity, hidden under `prefers-reduced-motion`.
- 3D parallax: capped at 8°, disabled under `prefers-reduced-motion`.

If a user opts out of motion, **everything** must stop: animations, parallax, autoplay video, breathing. Wrap every new animation in `@media (prefers-reduced-motion: reduce)`.

---

## 7. Accessibility

- `<html lang="en">` (or `lang="de"` for German pages).
- Skip link: `position: fixed; top: -200px`, visible only on `:focus-visible` (avoids flash on page load).
- Hamburger / menu buttons: toggle both `aria-expanded` and `aria-controls`.
- Focus outline: `2px solid #ff7820`.
- Alt text on every image, ARIA labels on nav and buttons.
- `history.scrollRestoration = 'manual'` and strip stale `#main-content` hashes on load.

---

## 8. Voice and copy

- Email: **`forge@arconsis.com`** with lowercase `f`. Always.
- Headlines short and concrete. Sentence fragments are fine.
- Active voice. "We build X." not "X is built."
- One claim per paragraph. No filler.
- Banned filler: *seamless, robust, cutting-edge, innovative, leverage, unlock, elevate, navigate the landscape, in the realm of*.
- Banned punctuation for separating thoughts: em-dash `—`, spaced en-dash ` – `. Use period, comma, colon, parentheses, or a new sentence.
- No emojis unless explicitly asked.
- No meta-comments about the text itself ("This article explores…").

---

## 9. Common rendering pitfalls

**Chrome PDF: gradient text on block elements.** `background-clip: text` on an `<h1>`/`<h2>`/`<h3>` produces a 1 px orange outline around the block in headless Chrome PDF export. Fix: either use solid `color: #ff7820` (PDF-safe), or wrap the gradient text in an inline `<span>` and apply the gradient only there. The bug is invisible in the live browser, only the final PDF shows it.

**macOS `file://` blocks Desktop assets.** Chrome will not load images from `~/Desktop` over `file://` (`ERR_ACCESS_DENIED`). When previewing locally, embed images as base64 data URIs or serve via a local web server (`python -m http.server`).

**Logo composite check.** The wordmark is white-on-transparent. On any white preview surface, you only see the diamond and assume it is a pure image mark. Composite over black before judging it.

**Carousel last-slide cutoff.** When stitching ≥ 6 slides à 1350 px in headless Chrome, the last 80–90 px render black. See §5.2 for the fix.

---

## 10. Asset inventory

```
logos/
├── forge-flame.png            ← image mark (flame in diamond)
├── forge-wordmark.png         ← wordmark, no glow
├── forge-badge.png            ← compact social/thumbnail badge
└── products/
    ├── amp.png                ← AMP product logo (master, 1.4 MB)
    ├── p4e.png                ← P4E product logo (master, 1.5 MB)
    ├── kap.png                ← KAP product logo (master, 1.5 MB)
    ├── amp-web.png            ← AMP, web-optimised variant
    ├── p4e-web.png            ← P4E, web-optimised variant
    └── kap-web.png            ← KAP, web-optimised variant

favicons/
├── favicon.ico
├── favicon-16.png
├── favicon-32.png
└── apple-touch-icon.png

demos/
├── amp-demo.webm              ← AMP product demo video (B-roll)
└── p4e-demo.webm              ← P4E product demo video (B-roll)
```

Customer logos are intentionally **not** part of this repo.

---

## 11. Maintenance

Treat this file as load-bearing. Every Forge artefact built by an agent or human references it. Keep it accurate, trim what no longer holds, and add a rule the moment you find yourself explaining the same thing twice.
