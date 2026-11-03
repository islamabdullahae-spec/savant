# vat.ad — SAVANT for Accounting website

Public website of SAVANT for Accounting (سفينت للمحاسبة), Abu Dhabi. Served by GitHub Pages from `main` at https://vat.ad (see `CNAME`). Every push to `main` goes live within a minute or two.

> This file is itself public (`.nojekyll` makes Pages serve every file). Never put prices, client names, credentials or internal notes here or anywhere in this repo.

## Structure

- `index.html` — the whole site: markup, CSS in one `<style>`, JS in inline `<script>` blocks. No build step, no framework, no package.json.
- `media/` — public hosting for social-media assets (served at `https://vat.ad/media/...` for Instagram publishing). `index.html` does not reference these files, but do not delete or rename them: scheduled posts load them by URL.
  - `T##-YYYY-MM-DD.jpg` — post cards for the insights feed.
  - `N##-YYYY-MM-DD.jpg` — next batch of post cards.
  - `HL-*.jpg` — Instagram highlight covers.
  - `R##-ar.mp4` — Arabic reels.
- `sitemap.xml`, `robots.txt`, `.well-known/security.txt` — SEO and security metadata. Update `<lastmod>` in the sitemap when content changes.

## Page sections (anchor ids, in order)

`#top` hero → `#services` → `#packages` → `#who` → `#start` → `#insights` (posts feed `#posts`) → `#faq` → `#contact` (WhatsApp enquiry form `#enq`).

## Conventions

- Bilingual. Every visible string is a pair: `<span data-l="ar">…</span><span data-l="en">…</span>`. The `#lang` toggle switches `data-lang` on `<html>`. Arabic is the default (`lang="ar" dir="rtl"`). Never add a string in only one language.
- Brand tokens: ink `#0B0C0A`, paper `#F2F2EE`, sage `#A9B98A`. Fonts: IBM Plex Sans Arabic, IBM Plex Sans, IBM Plex Mono (Google Fonts).
- Content Security Policy is strict (`default-src 'self'`, `connect-src 'none'`, `form-action 'none'`). Do not add third-party scripts, trackers, iframes or forms that post anywhere. If a new external origin is truly needed, update the CSP meta tag deliberately.
- Contact goes only through WhatsApp `+971 56 266 7020` (`wa.me` links) and `contact@vat.ad`. The enquiry form builds a WhatsApp message client-side; it sends nothing to a server.
- Packages show **no public prices** ("Tailored quotation"). Keep it that way.

## Adding a post to the insights feed

Copy an existing `<article class="post" data-date="YYYY-MM-DD" data-tag="TAG">` inside `#posts`.
- Posts with `data-date` later than today are hidden automatically by the script, so posts can be scheduled ahead.
- `data-tag` must match one of the filter groups in the script near the `apply()` function, or the post will not show under its filter.
- Tax and legal posts end with `<p class="disc">General information only, not advice for your specific business.</p>`.

## Accuracy rules for tax content (UAE)

- Verify every rate, threshold and deadline against the Federal Tax Authority (tax.gov.ae) or the Ministry of Finance (mof.gov.ae) before publishing. Cite the decision number when it is new.
- Current reference points, rechecked November 2026:
  - Corporate tax: 0% up to AED 375,000 of taxable income, 9% above.
  - VAT registration: mandatory above AED 375,000, voluntary from AED 187,500.
  - Small Business Relief: AED 3M revenue threshold, extended to tax periods ending on or before 31 Dec 2029 (Ministerial Decision No. 131 of 2026).
  - E-invoicing: phased rollout starting 2027.
- SAVANT itself is not VAT-registered. Never show a TRN or "VAT included" wording.

## Before pushing

1. Open `index.html` locally and check both languages, mobile width (375px) and the posts filter.
2. Keep `media/` lean: compress JPGs (about 150 KB each at most) and reels (about 11 MB each at most) before committing. The repo is already about 230 MB.
3. Use small commits with clear messages. Push to `main` only when the change is ready to go live.
