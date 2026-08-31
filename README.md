# hall-bookkeeping-site

Marketing site for Hall Bookkeeping, a solo bookkeeping practice run by Taylor Hall in Charleston, SC.

Production: https://hallbookkeepingsc.com

## What this is

A static site: a home page, four service and city pages, and three legal pages. No build step, no framework, no dependencies. Each page carries its own inline CSS; fonts come from Google Fonts, icons from the lucide CDN, and booking from an inline Calendly embed.

Everything sits at the repo root, which is what Vercel serves.

```
index.html                          home page (inline CSS, LocalBusiness + FAQPage JSON-LD)
cleanup-catch-up.html               service page
quickbooks-setup-charleston.html    service page
bookkeeping-mount-pleasant-sc.html  city page
bookkeeping-summerville-sc.html     city page
privacy.html                        legal, noindex
terms.html                          legal, noindex
disclaimer.html                     legal, noindex
vercel.json                         cleanUrls
logo-oak-*.svg                      brand marks, palmetto and white
favicon.*, apple-touch-icon.png     the oak icon; raster copies are for Google Search
badge-*.png                         QuickBooks and Intuit certification badges
taylor-cutout.png                   headshot used in the About section
taylor-signature.png                signature shown under the About photo
og-image.png                        1200x630 link preview
DESIGN.md                           the design spec this site was built from
```

## Local preview

```bash
python -m http.server 8000
```

Then open http://localhost:8000. Note that `http.server` serves `/page.html`
but not the extensionless `/page` that production serves; use `vercel dev` if
you need the real routing.

## Deploying

Vercel, static, no build step. Pushes to `main` deploy to production
automatically. The project's Root Directory is the repo root and the Framework
Preset is "Other" with the build step skipped, so the files are served as-is.

`vercel.json` sets `cleanUrls: true`, so `cleanup-catch-up.html` is served at
`/cleanup-catch-up` and `/cleanup-catch-up.html` returns a 308 to it. The
`<link rel="canonical">` on every page is already the extensionless form.
Internal navigation still links to the `.html` filenames and picks up that 308.

Because `vercel.json` is read from the Root Directory, it must stay at the repo
root. If the Root Directory setting ever moves to a subfolder, `vercel.json`
has to move with it.

The repo is public on purpose. Vercel's Hobby plan refuses Git deployments on a
private repo when the commit author is not the project owner, so keep it public
unless the account moves to Pro.

Production domain is `hallbookkeepingsc.com`. DNS lives at Namecheap, not Vercel,
because the Google Workspace MX records are managed there. Do not move the
nameservers to Vercel or mail will break.

## Editing

The design is client-approved and high fidelity. Before changing colors, type, spacing, or copy, read DESIGN.md. Prices, phone number, and email appear in more than one place per page, including the JSON-LD block in the head of `index.html`, so change them everywhere at once.
