---
name: blueprint-lab-theme
description: Apply the "Blueprint Lab" design theme (warm paper grid, hairline panels with corner brackets, monospace micro-labels, black and green accents) to Bootstrap 5 pages. Use when building or restyling HTML/CSS pages, storefronts or dashboards in this look.
---

# Blueprint Lab Theme

A technical-drawing look for Bootstrap 5 pages: warm off-white paper with a faint grid, hairline-bordered panels framed by corner brackets, monospace micro-labels, near-black primary actions and a single green accent.

Apply the **look only**. Never change the user's content, copy, images, or class names unless a rule below requires it. Always deliver separate `index.html` and `styles/HomePage.css` unless asked otherwise, plus a preview.

---

## 1. Stack

- Bootstrap 5.3.8 CSS + JS bundle (jsDelivr), Bootstrap Icons 1.11.3.
- Google Fonts: `Inter` (400, 500, 600, 700) and `JetBrains Mono` (400, 500, 700).
- One custom stylesheet loaded after Bootstrap so overrides win.

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500;700&display=swap" rel="stylesheet">
```

---

## 2. Design tokens (define exactly these)

```css
:root {
    --bg: #f7f6f2;          /* page paper */
    --panel: #fbfaf7;       /* panel surface */
    --panel-alt: #f0efea;   /* hover, image wells, banner */
    --ink: #0f0f0f;         /* text, primary buttons, dark brackets */
    --ink-soft: #2a2a28;    /* primary button hover */
    --muted: #6f6e68;       /* secondary text */
    --line: #dcdad2;        /* hairline borders */
    --line-strong: #a9a79f; /* input borders, light brackets */

    --accent: #10b981;      /* green: active marker, focus, badge border */
    --accent-ink: #0a7a55;  /* green text on light */
    --accent-soft: #e6f6ef; /* green tint background */
    --danger: #c8372d;      /* discount / negative values only */

    --font-sans: "Inter", system-ui, -apple-system, "Segoe UI", Roboto, Arial, sans-serif;
    --font-mono: "JetBrains Mono", ui-monospace, SFMono-Regular, Menlo, Consolas, monospace;

    --gap: 24px;   /* vertical space between panels */
    --pad: 20px;   /* panel inner padding */
}
```

Rules:
- Green is the only accent. Red is only for discounts or errors.
- No gradients, no drop shadows on panels, no pure white page background. Pure `#fff` is allowed only for inputs, product cards and image frames.
- Single light theme. Do not add dark mode unless asked.

---

## 3. Base

```css
* { box-sizing: border-box; }

body {
    margin: 0;
    font-family: var(--font-sans);
    font-size: 15px;
    color: var(--ink);
    background-color: var(--bg);
    background-image:
        linear-gradient(to right, rgba(15,15,15,.045) 1px, transparent 1px),
        linear-gradient(to bottom, rgba(15,15,15,.045) 1px, transparent 1px);
    background-size: 48px 48px;
    -webkit-font-smoothing: antialiased;
}

img { max-width: 100%; }

.container { max-width: 1240px; padding-left: 24px; padding-right: 24px; }
.page-main { padding-top: var(--gap); padding-bottom: 56px; }
```

Alignment rule: **every block on the page (navbar, search, carousel, panels, banner) sits inside the same `.container`** so left and right edges line up exactly. Do not use percentage widths such as `width: 85%` on page blocks.

---

## 4. Typography

| Role | Font | Size | Weight | Tracking | Case |
|---|---|---|---|---|---|
| Panel title | Sans | `clamp(20px, 2.4vw, 28px)` | 500 | `-0.03em` | Normal |
| Banner h2 | Sans | `clamp(24px, 3.2vw, 38px)` | 600 | `-0.035em` | Normal |
| Banner h3 | Sans | `clamp(16px, 2vw, 22px)` | 500 | `-0.02em` | Normal, green-ink |
| Product title | Sans | 15px | 600 | `-0.01em` | Normal |
| Price | Sans | 21px | 700 | `-0.02em` | Normal |
| Body / nav links | Sans | 14–15px | 400–500 | 0 | Normal |
| Buttons | Mono | 12px | 500 | `0.08em` | UPPERCASE |
| Category labels | Mono | 12px | 500 | `0.06em` | UPPERCASE |
| Banner tag | Mono | 11px | 700 | `0.12em` | UPPERCASE |
| Offer badge | Mono | 10px | 700 | `0.04em` | UPPERCASE |
| Capacity, MRP, discount | Mono | 11px | 400 / 700 | `0.04em` | Normal |
| Search input | Mono | 13px | 400 | 0 | Normal |

Headings use tight negative tracking. Anything that reads as a label, tag, unit or control text uses mono.

---

## 5. Signature device: corner brackets

Dark brackets on panels and the navbar (class `.bracket`), 14px arms, 1px, sitting on the outer border:

```css
.bracket { position: relative; }

.bracket::after {
    content: "";
    position: absolute;
    inset: -1px;
    pointer-events: none;
    --b: var(--ink);
    --l: 14px;
    background:
        linear-gradient(var(--b), var(--b)) top left / var(--l) 1px no-repeat,
        linear-gradient(var(--b), var(--b)) top left / 1px var(--l) no-repeat,
        linear-gradient(var(--b), var(--b)) top right / var(--l) 1px no-repeat,
        linear-gradient(var(--b), var(--b)) top right / 1px var(--l) no-repeat,
        linear-gradient(var(--b), var(--b)) bottom left / var(--l) 1px no-repeat,
        linear-gradient(var(--b), var(--b)) bottom left / 1px var(--l) no-repeat,
        linear-gradient(var(--b), var(--b)) bottom right / var(--l) 1px no-repeat,
        linear-gradient(var(--b), var(--b)) bottom right / 1px var(--l) no-repeat;
}
```

Light brackets around panel titles (`.panel-title::before`): same technique, `inset: 0`, `--b: var(--line-strong)`, `--l: 8px`.

Rules:
- Dark brackets: panels, navbar, search panel. Light brackets: titles only.
- The `.bracket` element must not use `overflow: hidden` on itself unless it is the pharmacy banner (the banner's `::after` stays inside because it uses `inset: -1px` on an element with `overflow: hidden`; keep the banner brackets visible by accepting a 1px clip).
- Do not put brackets on cards, buttons, inputs or images.

---

## 6. Components

### 6.1 Panel

```css
.panel { background: var(--panel); border: 1px solid var(--line); margin-bottom: var(--gap); }
.panel-head {
    display: flex; align-items: center; justify-content: space-between;
    flex-wrap: wrap; gap: 12px;
    padding: 16px var(--pad); border-bottom: 1px solid var(--line);
}
.panel-body { padding: var(--pad); }
.panel-body-tight { padding: 12px; }  /* carousel */
.panel-body-flush { padding: 0; }     /* category grid */
.panel-actions { display: flex; gap: 8px; }
```

Structure: `section.panel.bracket > .panel-head (h2.panel-title + optional .panel-actions) + .panel-body`.
Section headings are `h2.panel-title`, never `h4` with inline styles.

### 6.2 Navbar

- Custom `.site-nav.bracket`, not Bootstrap's `.navbar`: flex, `gap: 12px 20px`, `padding: 12px 18px`, panel background, 1px `--line` border.
- Brand: 36×36 image inside a 3px padded white frame with a 1px `--line` border. Square, not circular.
- Links `.site-links a`: 14px, weight 500, `--muted`, padding `8px 14px`. Hover: `--ink`. Active: `--ink` plus a 6×6 green square (`::before`) with 8px gap.
- Right side `.site-actions`: two 40×40 square `.icon-btn` (1px `--line` border, `--panel` fill, hover `--panel-alt`) and one `btn btn-primary` Login.
- `.site-links` uses `margin: 0 auto 0 8px` so the actions are pushed right.

### 6.3 Buttons (Bootstrap variable overrides)

```css
.btn { font-family: var(--font-mono); font-size: 12px; font-weight: 500;
       letter-spacing: .08em; text-transform: uppercase; line-height: 1.2;
       display: inline-flex; align-items: center; justify-content: center; gap: 8px; }

.btn-primary {
    --bs-btn-color: #fff;  --bs-btn-bg: var(--ink);  --bs-btn-border-color: var(--ink);
    --bs-btn-border-radius: 2px;
    --bs-btn-hover-color: #fff;  --bs-btn-hover-bg: var(--ink-soft);  --bs-btn-hover-border-color: var(--ink-soft);
    --bs-btn-active-color: #fff; --bs-btn-active-bg: #000; --bs-btn-active-border-color: #000;
    --bs-btn-focus-shadow-rgb: 16,185,129;
    padding: 10px 22px;
}

.btn-outline-primary {
    --bs-btn-color: var(--ink); --bs-btn-border-color: var(--line-strong);
    --bs-btn-border-radius: 2px;
    --bs-btn-hover-color: #fff; --bs-btn-hover-bg: var(--ink); --bs-btn-hover-border-color: var(--ink);
    --bs-btn-active-color: #fff; --bs-btn-active-bg: var(--ink); --bs-btn-active-border-color: var(--ink);
    --bs-btn-focus-shadow-rgb: 16,185,129;
    background: var(--panel);
}
.btn-outline-primary.btn-sm { width: 36px; height: 36px; padding: 0; font-size: 14px; } /* carousel arrows */
```

Radius is 2px at most. No pill buttons.

### 6.4 Search

- Panel with `padding: 14px var(--pad)`; form is flex, `gap: 8px`, `max-width: 640px`, centered.
- Input: height 44px, padding `0 14px`, mono 13px, white fill, 1px `--line-strong` border, 2px radius. Focus: border `--accent` and `box-shadow: 0 0 0 3px var(--accent-soft)`.
- Submit button: 44px tall, `padding: 0 22px`, icon at 15px.

### 6.5 Carousel

- Wrapped in a panel with `.panel-body-tight` (12px).
- Image: `width: 100%`, `height: clamp(200px, 30vw, 380px)`, `object-fit: cover`. No rounded corners.
- Keep Bootstrap carousel markup and `data-bs-interval` values.

### 6.6 Doctor / image cards

- `.doctor-card`: 8px padding, white fill, 1px `--line` border. Image inside: 100% wide, 220px tall (180px under 768px), `object-fit: cover`.
- Grid: Bootstrap `row g-3`, `col-12 col-md-4`.

### 6.7 Banner

- `section.panel.bracket.pharmacy-banner`: flex, `align-items: stretch`, `min-height: 260px`, `background: var(--panel-alt)`, `overflow: hidden`.
- Image column: `flex: 0 0 42%`, `max-width: 42%`, `border-right: 1px solid var(--line)`, image absolutely positioned with `inset: 0` and `object-fit: cover`.
- Content: `padding: 28px 40px`, vertically centered.
- Tag: inline-block, mono 11px bold, `--accent-ink` text, `--accent-soft` fill, 1px `--accent` border, padding `5px 10px`, `margin-bottom: 14px`.

### 6.8 Category grid

- `.category-list`: grid, 5 equal columns, inside a flush panel body.
- Cells share hairlines (`border-right: 1px solid var(--line)`, none on the last).
- Cell: column flex, centered, `gap: 14px`, `padding: 26px 12px 22px`, mono uppercase label. Hover: `--panel-alt` background and image `scale(1.08)`.
- Circle: 100×100, `border-radius: 50%`, 1px `--line-strong` border, `--panel-alt` fill, `overflow: hidden`. Circles stay round (the only rounded element in the theme besides nothing else).

### 6.9 Product card

- Grid: `row g-3`, columns `col-6 col-lg-3` (2 per row until 992px, then 4). Do not use `col-md-4` for four items.
- Card: `.card.pharmacy-product.h-100`, radius 0, 1px `--line` border, white fill. Hover: border `--ink` and `box-shadow: 4px 4px 0 rgba(15,15,15,.07)` (hard offset, no blur).
- Image well: height 190px, padding 14px, `--panel-alt` fill with a dot grid (`radial-gradient(rgba(15,15,15,.09) 1px, transparent 1px)` at `14px 14px`), 1px bottom border, `object-fit: contain`.
- Offer badge: absolute `top: 10px; right: 10px`, mono 10px bold, `--accent-ink` on `--accent-soft`, 1px `--accent` border, `padding: 4px 7px`, `white-space: nowrap`.
- Body: column flex, padding 16px. Title is one line with ellipsis. Capacity in mono muted. MRP is mono 11px muted with line-through. Discount is mono 11px bold `--danger`.
- Price: `margin: auto 0 0; padding-top: 10px` so all prices share one baseline across cards.
- Product titles use `h3.card-title`, not `h6`.

---

## 7. Responsive behaviour

| Breakpoint | Changes |
|---|---|
| `max-width: 991.98px` | Navbar: brand `order:1`, actions `order:2; margin-left:auto`, links `order:3; width:100%; margin:0; padding-top:8px; border-top:1px solid var(--line); overflow-x:auto` with hidden scrollbar. |
| `max-width: 767.98px` | `--gap: 16px; --pad: 14px`. Container side padding 16px. Header top padding 16px. Panel title padding `8px 14px`. Doctor image 180px. Banner min-height 190px, image column 38%, content padding 16px, tag 9px. Category grid becomes 3 columns, cell padding `18px 8px 16px`, label 10px, circle 72px, add bottom borders and remove the right border on every third cell and the bottom border on cells 4+. Product image 150px/padding 10px, card body padding 12px, title 14px, price 18px. |
| `max-width: 400px` | Nav padding `10px 12px`. Banner image column 34%, content padding 12px, h2 20px, h3 13px, text 12px. Category circle 58px. Product image 128px. Badge 9px, padding `3px 5px`. |

The page body must never scroll horizontally at 320px and up. Always give flex children that hold text `min-width: 0`.

---

## 8. Do and don't

**Do**
- Keep hairlines at exactly 1px using `--line` (or `--line-strong` for inputs and light brackets).
- Use mono for every label, unit, tag and button.
- Keep radii at 0 to 2px; only category circles are round.
- Use a hard offset shadow (`4px 4px 0`) for hover emphasis, never blurred shadows.
- Use the green square marker for the active nav item.

**Don't**
- Don't use Bootstrap's default blue anywhere; override every `btn-primary` and `btn-outline-primary` through the variables above.
- Don't use `rounded-*` utility classes on images, cards or banners.
- Don't add gradients, glassmorphism, glows or emoji.
- Don't mix widths (for example a carousel at 85% beside full-width panels).
- Don't use inline styles; every value belongs in the stylesheet.
- Don't alter the user's text or image paths.

---

## 9. Workflow when applying this theme

1. Read the user's HTML and CSS; list the sections (navbar, search, carousels, banner, lists, grids, cards).
2. Wrap every section in the matching component: `.panel.bracket` with `.panel-head`/`.panel-body`, or the navbar/banner variants.
3. Replace Bootstrap utility styling that conflicts (`bg-white`, `shadow-sm`, `rounded-4`, `fs-5`, `btn-primary` colours) with the classes above. Keep all other markup and content.
4. Write the tokens, base, bracket helper, components, then responsive blocks in that order in `styles/HomePage.css`.
5. Produce placeholder images only for the preview; the real HTML must keep the user's `./media/...` paths.
6. Check at 1366px, 820px and 390px: no horizontal scroll, brackets visible on all four corners, equal card heights, prices aligned, nav links reachable.
7. Deliver `index.html`, `styles/HomePage.css`, and a preview.

---

## 10. Final checklist

- [ ] Tokens match section 2 exactly
- [ ] Body has the 48px grid background
- [ ] Every section is inside the same `.container`
- [ ] Panels have 1px borders and dark corner brackets; titles have light brackets
- [ ] All labels and buttons use JetBrains Mono, uppercase where listed
- [ ] Primary buttons are near-black with 2px radius, no blue anywhere
- [ ] Active nav item has the green square
- [ ] Category grid is 5 columns on desktop and 3 on mobile
- [ ] Products are 4 per row on desktop and 2 per row below 992px
- [ ] Prices align across cards; titles ellipsize on one line
- [ ] Carousel and doctor images fill their frames with no distortion
- [ ] No horizontal scroll at any width
