# Handoff: Hall Bookkeeping website

## Overview
One-page marketing site for Hall Bookkeeping, a solo bookkeeping business run by Taylor Hall in Charleston, SC. Sections: nav, hero, services (2 cards), about, FAQ, Calendly booking, footer. Goal: get visitors to book a 15-minute call.

## About the design files
`site/` contains a **design reference created in HTML** — a complete, working prototype of the intended look and behavior. It is deploy-ready as-is (static hosting: Netlify/Vercel/Cloudflare Pages, upload `site/` contents to the domain root). If instead you are recreating it in a framework (Next.js, Astro, etc.), treat the HTML as the source of truth for markup, values, and copy — recreate it with the codebase's patterns; do not redesign.

## Fidelity
**High-fidelity.** Colors, type, spacing, and copy are final and client-approved. Recreate pixel-perfectly. Copy is verbatim-approved: do not rewrite any text.

## Design tokens
Colors:
- `--ink: #12263F` (headings, primary text, hero/footer-mark ink, hero background)
- `--slate: #4A5C73` (secondary text)
- `--paper: #FFFFFF` (page background)
- `--rule: #D9DEE6` (borders, dividers)
- `--palmetto: #1D4E89` (accent: buttons, links, ticks, icons)
- `--palmetto-tint: #EAF1F8` (photo backdrop wash)
- Section wash: `#F5F8FB` (soft boxes), hover blue `#163C6B`

Type (Google Fonts):
- Source Serif 4, 700, letter-spacing -0.015em — logo + all headings
- Public Sans 400/500/600 — body and UI
- IBM Plex Mono 400/500, tabular figures — EVERY number (prices, phone, dates, year)
- Scale: h1 clamp(38px→58px) hero / 34px mobile; h2 26px; h3 19px; body 17/1.6; small 15; label 12 mono uppercase tracked 0.12em
- Rules: never a 4th typeface; never weights other than 400/500/700; sentence case everywhere; no em dashes in copy

Radii: buttons 3px, cards 10px, soft section boxes 14px. No shadows except focus ring `0 0 0 3px rgba(29,78,137,.35)`. No gradients.

## Screens / views
One page, 960px content column (`max-width:960px`), nav+hero at 1200px.

1. **Nav** — grid `1fr auto 1fr`, wrap max-width 868px: stacked lockup flush left (book SVG 34px above "Hall" 28px above "Bookkeeping" 14px); links true-centered (Services, About, FAQ, 16px/500); "Book a call with Taylor" primary button flush right → `#contact`.
2. **Hero** — indigo `#12263F`, padding 96/120px, centered column max 820px. H1 white, three lines: "Bookkeeping for / small businesses / in Charleston"; sub-copy `#D9DEE6` 19px; white button "Book a call with Taylor" → `#contact`.
3. **Services** — soft box `#F5F8FB` r14, h2 "Bookkeeping services", 2 equal-height white cards (r10, 1px `#D9DEE6`): lucide icon 28px palmetto (history / calendar-check), h3, intro 16px slate, 3 check bullets (lucide `check` 18px palmetto), price row: mono 25px price + mono uppercase label beside ("one time" / "per month"). Prices: $1,000 to $5,000 one time; $400 to $1,000 per month.
4. **About me** — soft box, 2-col: copy left (4 paragraphs, verbatim in file: intro, brokerage background, why founded, personal line), photo right: `taylor-cutout.png` bottom-aligned on `#EAF1F8` r14 block, 420px tall, max 340px wide, vertically centered, `taylor-signature.png` (68px) centered beneath.
5. **FAQ** — soft box, 4 `<details>` accordions, +/– indicator in palmetto, 1px rules between.
6. **Contact** — soft box, h2 "Book a call", Calendly inline embed (url `https://calendly.com/taylor-hallbookkeepingsc/15min?hide_gdpr_banner=1`), height 1060px, no internal scroll.
7. **Footer** — lockup + "Charleston, SC", phone/email in mono, anchor links, service-area line, © 2026.

## Interactions & behavior
- Anchor scrolling with `scroll-behavior:smooth`, disabled under `prefers-reduced-motion`.
- Hover: links + buttons darken to `#163C6B`. No motion/scale effects anywhere.
- Focus: visible ring `0 0 0 3px rgba(29,78,137,.35)` on all interactive elements.
- Mobile ≤760px: single column, centered nav with ≥44px tap targets, hero padding 56/64, full-width CTA, display 34px, footer stacked/centered.
- Icons: lucide via CDN (`lucide@0.462.0`), `lucide.createIcons()` after load.

## State management
None. Static page; Calendly iframe handles booking state.

## SEO (already in the file — keep it)
Title/meta description; canonical `https://hallbookkeepingsc.com/`; Open Graph tags + `og-image.png` (1200×630); JSON-LD: ProfessionalService (phone +18432147610, email, 7 service areas, priceRange) and FAQPage (4 questions verbatim).

## Assets (in `site/`)
- `logo-book-duo.svg` — open-book mark, ink covers + palmetto spine; also used as favicon
- `taylor-cutout.png` — headshot with background removed, bottom-aligned in About
- `og-image.png` — 1200×630 link preview
- `taylor-signature.png` — handwritten signature, shown under the About photo
- `privacy.html`, `terms.html`, `disclaimer.html` — legal pages, linked from the footer, noindex
- Fonts load from Google Fonts CDN

## Files
- `site/index.html` — the complete page (inline CSS), asset paths flattened to same-folder
- `site/*.svg|png` — assets, deploy alongside index.html at the domain root

## Launch checklist (owner tasks)
- Point `hallbookkeepingsc.com` at the host; deploy `site/` contents at root
- Verify Calendly event is live at the embedded URL
- Create Google Business Profile (biggest local-search lever)
- Test on a real phone
