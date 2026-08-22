# hall-bookkeeping-site

Marketing site for Hall Bookkeeping, a solo bookkeeping practice run by Taylor Hall in Charleston, SC.

Production: https://hallbookkeepingsc.com

## What this is

A static, single-page site plus three legal pages. No build step, no framework, no dependencies. `index.html` carries its own inline CSS; fonts come from Google Fonts, icons from the lucide CDN, and booking from an inline Calendly embed.

```
index.html          the whole page (inline CSS)
privacy.html        legal, noindex
terms.html          legal, noindex
disclaimer.html     legal, noindex
logo-book-duo.svg   brand mark, also the favicon
taylor-cutout.png   headshot used in the About section
taylor-signature.png
og-image.png        1200x630 link preview
DESIGN.md           the design spec this site was built from
```

## Local preview

Any static server works:

```bash
python -m http.server 8000
```

Then open http://localhost:8000.

## Deploying

Vercel, static, zero config. Pushes to `main` deploy to production automatically.

## Editing

The design is client-approved and high fidelity. Before changing colors, type, spacing, or copy, read DESIGN.md. Prices, phone number, and email appear in more than one place per page, including the JSON-LD block in the head of `index.html`, so change them everywhere at once.
