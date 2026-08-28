# Hall Bookkeeping website

One-page marketing site for Hall Bookkeeping LLC, a solo bookkeeping practice run by
Taylor Hall in Charleston, SC, plus three legal pages. Goal: get visitors to book a
15-minute call.

This document describes **what is deployed**, not an incoming design package. It is
maintained in this repo. Do not overwrite it with the README from a design handoff zip;
those are generated from an older baseline and have been wrong about the typeface, the
logo, and the section list since the redesign.

Copy, colors, type, and spacing are client-approved. Do not rewrite copy or redesign.

## Design tokens

Colors:
- `--ink: #12263F` headings, primary text, hero and footer background
- `--slate: #4A5C73` secondary text
- `--paper: #FFFFFF` page background
- `--rule: #D9DEE6` borders and dividers
- `--palmetto: #1D4E89` accent: buttons, links, ticks, icons, the oak mark
- `--palmetto-tint: #EAF1F8` photo backdrop wash
- `--flag: #8A6410` reserved, currently unused
- Section wash `#F5F8FB`, hover blue `#163C6B`, hero underline accent `#7FA3CF`

Type, all from Google Fonts:
- **Playfair Display** 700 — logo wordmark and all headings, letter-spacing -0.015em
- **Public Sans** 400/500/600 — body and UI
- **IBM Plex Mono** 400/500, tabular figures — every number: prices, phone, dates, year
- Scale: body 18/1.65; h1 40px; h2 29px; h3 21px; hero display `clamp(38px, 4.6vw, 58px)`,
  34px on mobile; label 12px mono uppercase tracked 0.12em
- Never a fourth typeface. Never weights outside 400/500/700. Sentence case throughout.
  No em dashes in copy.

Radii: buttons 3px, cards 10px, soft section boxes 14px. No shadows except the focus ring
`0 0 0 3px rgba(29,78,137,.35)`. No gradients.

## Page structure

Single page, 960px content column (`.wrap`), hero at 1200px. There is **no separate
`<header>`** on the homepage; the nav lives inside the hero.

1. **Hero** — indigo, padding 18px top / 120px bottom. Nav row across the top, max-width
   880px centered: oak mark (`logo-oak-white.svg`, 58px) beside a stacked "Hall" 34px /
   "Bookkeeping" 17px, then white links Services, About me, FAQ at 15px/500. The mark
   carries `margin-left:-24px` as an optical pull, overridden to 0 under 760px. Below:
   H1 "Your books, handled." with "handled" underlined 3px in `#7FA3CF`, sub-copy at 19px
   in `#D9DEE6`, and a white CTA "Book a call with Taylor" to `#contact`.
2. **Pain points** (`#why`) — soft box with a 2px palmetto border. H2 "If you are a
   business owner who...", four palmetto check items at 18px, closing line
   "...that is exactly what I fix."
3. **Services** — soft box, H2 "Bookkeeping services", two equal-height white cards.
   Monthly bookkeeping first, then Cleanup or catch-up. Each: lucide icon 28px palmetto
   (calendar-check / history), h3, intro with `min-height:112px`, four check bullets, then
   a price row and a note. Prices: "$400 to $1,000 per month" and "Flat quote one time".
   A primary CTA sits centered below the cards.
   **The price row uses `margin-top:auto`.** The two bullet lists differ in height by 7px
   because Monthly wraps three bullets to two lines and Cleanup only two. `auto` pushes
   the price row to the card bottom and absorbs that. A fixed margin here visibly
   misaligns the two price rows; this has regressed once already.
4. **About me** — soft box, two columns. Four paragraphs left. Right: `taylor-cutout.png`
   bottom-aligned on a `#EAF1F8` block, 420px tall, max 340px wide, with
   `taylor-signature.png` at 68px beneath. Three Intuit badges at 120px span both columns.
5. **FAQ** — soft box, six `<details>` accordions, +/– indicator in palmetto.
6. **Contact** — soft box, H2 "Start with a 15 minute call", reassurance line, Calendly
   inline embed at 1060px with no internal scroll.
7. **Footer** — oak lockup and "Charleston, SC", phone and email in mono, anchor links,
   service-area line, "© 2026 Hall Bookkeeping LLC. All rights reserved." and legal links.

## Behavior

- Smooth anchor scrolling, disabled under `prefers-reduced-motion`.
- Hover darkens links and buttons to `#163C6B`. No motion or scale effects.
- Visible focus ring on every interactive element.
- Mobile ≤760px: single column, hero padding 56/64, full-width hero CTA, display 34px,
  photo 360px, footer stacked and centered, price 22px.
- `.icon-list li` carries `min-height:44px` for tap targets. Keep it.
- Icons: lucide via CDN (`lucide@0.462.0`), `lucide.createIcons()` after load.
- No state management. The Calendly iframe owns booking state.

## SEO

Title and meta description, canonical `https://hallbookkeepingsc.com/`, Open Graph tags
with `og-image.png` at 1200×630. Two JSON-LD blocks: `ProfessionalService` (name, url,
email, founder, address, 7 service areas, knowsAbout) and `FAQPage` with all six questions
matching the visible accordions verbatim and in order.

Note: `ProfessionalService` currently declares **no `telephone` and no `priceRange`**, both
of which earlier versions had. The phone number is still in the footer. This looks
incidental rather than deliberate and is worth restoring.

## Assets

In use:
- `logo-oak-palmetto.svg` — oak mark in palmetto. Favicon on all four pages, footer
  lockup, and the legal page headers.
- `logo-oak-white.svg` — white oak mark, hero nav only.
- `taylor-cutout.png`, `taylor-signature.png` — About section.
- `og-image.png` — 1200×630 link preview: indigo ground, white oak, wordmark, tagline.
- `badge-intuit-bookkeeping.png`, `badge-qb-level1.png`, `badge-qb-level2.png` — About.

Shipped but referenced by nothing: `favicon.svg`, `logo-book-duo.svg`,
`logo-book-white.svg`, `logo-tick-palmetto.svg`, `logo-tick-white.svg`,
`badge-qb-payroll.png`. The book marks are previous branding and should not come back.
The payroll badge is kept in case it is added to the About row later.

## Legal pages

`privacy.html`, `terms.html`, `disclaimer.html`. Noindex, linked from the footer, each
with its own inline CSS and a simple oak lockup header. They are on the same Playfair
Display / Public Sans / IBM Plex Mono stack as the homepage. They name **Hall Bookkeeping
LLC** in body copy; the privacy policy deliberately does not describe the business as a
sole proprietorship.

These pages are maintained separately from `index.html`, so branding changes have to be
applied to them by hand. That has been missed before.
