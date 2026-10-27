# NextBorder Website Audit Report
**Date:** 2026-10-24  
**Scope:** Public repositories `next-border` and `next-border-1`, plus a static source audit of the `audit-fixes-2026-10-24` branch.

## Repository comparison
- `next-border` is the smaller public repository and the repository used by the known GitHub Pages URL.
- `next-border-1` contains the same shared HTML/CSS content files (the audited shared file blob hashes match), plus assets, an IELTS practice page, and Netlify function files.
- `next-border` was missing the `assets/` files referenced by its HTML. The audit branch restores the logo, favicon, Open Graph artwork, university logos, and university image files from the matching `next-border-1` repository.
- The two repositories create a source-of-truth risk. Keep one authoritative repository and clearly configure the intended deployment to use it.

## Confirmed source findings
1. HTML metadata and sitemap referenced `https://nextborder.netlify.app/`. The audit branch now points these references at `https://nextbordervisa-code.github.io/next-border/`.
2. Content pages did not have canonical tags. Canonical tags were added to the 18 content pages. The Google site-verification HTML file was intentionally left unchanged.
3. `robots.txt` was absent from `next-border`; it has been added with an allow-all rule and a sitemap reference.
4. The homepage already contains `id="ask-ai"`; therefore, the previous report's claim that the target element was missing was incorrect. The anchor exists in source, although a real browser click still needs to be tested.
5. The homepage and contact assistant displayed reassuring text that implied the lead had been captured, but their submit handlers did not persist a lead. The audit branch changes this to an explicit email-draft handoff. Visitors must press Send in their email app; this is a fallback, not a server-side CRM/database.
6. The regular contact form uses Netlify Forms markup. On GitHub Pages, it cannot be handled by Netlify Forms. The audit branch adds a GitHub Pages-specific email-draft fallback while leaving the native Netlify form path intact on other hosts.
7. Visible draft copy and empty testimonial placeholders were removed from the affected pages. No fake customer testimonials were added.
8. The WhatsApp link uses a number already published in the site, but the correct official NextBorder WhatsApp destination has not been independently confirmed. It was not changed to avoid redirecting leads to the wrong number.

## Static verification performed on the audit branch
- Reviewed 19 HTML files.
- Checked relative `href` and `src` references against tracked repository files: no missing local references found.
- Checked the 18 content pages for canonical tags: one found on each.
- Checked HTML and sitemap for the retired Netlify host: no remaining matches.
- Checked for known visible placeholder strings: none of the audited strings remain.
- Confirmed the `robots.txt` sitemap path matches the GitHub Pages base URL.

## Not yet verified
- No browser-based click, mobile viewport, JavaScript runtime, or accessibility interaction test was run.
- No real email was sent or delivered.
- No real lead was stored in a CRM/database.
- No live Netlify deployment was restored or configured.
- The public website was not changed by this draft PR; the branch is awaiting review and deployment validation.

## Recommended next actions
1. Select and document the single source-of-truth repository.
2. Confirm the official NextBorder WhatsApp number and the preferred lead destination.
3. Configure a server-side lead delivery path (email provider or CRM) using protected credentials, not client-side secrets.
4. Restore/configure the intended production deployment and domain.
5. Run real browser/mobile checks and submit test leads to verify delivery before merging and publishing.
