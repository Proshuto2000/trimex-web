# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static HTML/CSS/JS website for **Trimex SRL** — a plastic manufacturing company in Lima, Peru with 30 years of history. Products span two lines: household plastics (Línea Hogar) and agro-industrial plastics (Línea Agroindustrial). Language: Spanish.

## Development

No build step. Open `index.html` directly in a browser, or serve with any static file server:

```bash
# Python (if available)
python -m http.server 3000

# Node (if available)
npx serve .
```

## Architecture

Three files, flat structure:

| File | Role |
|------|------|
| `index.html` | Full single-page site, all sections in order |
| `styles.css` | All styles — tokens at top via CSS custom properties |
| `script.js` | Nav scroll, mobile menu, reveal animations, counter animation, form mock |

## Design Tokens (styles.css `:root`)

All colors and fonts are defined as CSS variables at the top of `styles.css`. Key values:
- `--navy` / `--navy-2` / `--navy-3` — background hierarchy (dark blue)
- `--amber` / `--amber-2` — primary accent (molten gold, brand color)
- `--green` / `--green-2` — agro product line accent
- `--cream` — warm off-white for body text
- `--steel` — muted text / secondary info
- `--font-display` — Bebas Neue (Google Fonts, industrial condensed)
- `--font-body` — DM Sans (Google Fonts, clean readable)

## Page Sections (in order)

1. **Nav** — fixed, scrolled state adds glass blur + amber border
2. **Hero** — full-viewport, animated radial glows, large Bebas Neue title, `30 AÑOS` watermark stamp
3. **Band** — amber marquee ticker strip
4. **Nosotros** — two-column: copy + 4 animated stat counters
5. **Productos** — full-width split: dark navy (Hogar) vs green (Agroindustrial)
6. **Proceso** — 4-step manufacturing process on `--navy-2` background
7. **CTA Band** — centered call-to-action with amber-bordered card
8. **Contacto** — info column + contact form (mock submit with success state)
9. **Footer** — 4-column grid

## Key Patterns

**Reveal animations**: Add class `reveal` to any element. `IntersectionObserver` in `script.js` adds `visible` when it enters the viewport. Stagger siblings by setting `transition-delay` inline or via nth-child rules in CSS.

**Stat counters**: `<span class="stat-num" data-target="30">0</span>` — the counter observer triggers `animateCounter()` on intersection.

**Responsive breakpoints**: 1024px (2-col → 1-col grids), 768px (mobile nav, stacked products), 480px (single-col stats/process).

## Content to Update

Replace placeholder values before going live:
- Phone: `(01) 000-0000` (appears in contact section and footer)
- Email: `ventas@trimexsrl.com.pe`
- Address details in the contact section
- Product lists in both `product-half` sections
- Stat numbers (`data-target` attributes) in the Nosotros section
- Form action — currently mocked; wire to a backend or form service (Formspree, etc.)
