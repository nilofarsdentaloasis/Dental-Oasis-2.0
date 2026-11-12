# Dental Oasis — Initial SEO & Migration Audit Report (Phase 1 & Phase 2)

**Business:** Dr. Nilofar's Dental Oasis  
**Preferred Canonical Domain:** `https://nilofarsdentaloasis.com`  
**Current Live Odoo Domain:** `https://www.nilofarsdentaloasis.com/` (`https://nilofarsdentaloasis.com/` currently 301-redirects to `www`)  
**Audit Date:** 2026-11-12  
**Migration Status:** **NOT READY FOR DOMAIN MIGRATION** (Pending SEO, Routing, Redirects & GSC Baseline)

---

## 1. Local Project Architecture (New Vercel Website)

- **Architecture:** 5 standalone static HTML files with inline `<style>` and `<script>` blocks, plus local image assets in `images/`.
  - `index.html` (333 KB) — Fully static rendered HTML.
  - `about.html` (295 KB) — Hybrid static + client-side JS router (`#app`) with `route()`.
  - `treatments.html` (121 KB) — Hybrid static + client-side JS router (`#app`).
  - `smile-gallery.html` (137 KB) — Hybrid static + client-side JS router (`#app`).
  - `contact.html` (125 KB) — Client-side JS (`route()`) overwrites `#app` on load with `contact()`.
- **Deployment Config:** No `vercel.json` exists yet.
- **Indexing Files:** No `sitemap.xml` or `robots.txt` exists yet.

---

## 2. Existing SEO Features (Local Project)

- Valid `<html lang="en">` and mobile `<meta name="viewport">` on all 5 pages.
- Favicon (`images/favicon.jpg`) and `apple-touch-icon` linked on all 5 pages.
- All `<img>` tags across all 5 pages have non-empty `alt` attributes (`0` missing alt texts).
- External `target="_blank"` links include `rel="noopener noreferrer"` (`0` unsafe external links).
- `index.html` includes basic `Dentist` JSON-LD (`name`, `telephone`, `address`, `sameAs`).
- Basic `og:type`, `og:title`, `og:description` exist on all 5 pages.

---

## 3. Missing SEO Features & Critical Issues

### Critical Issues
1. **No `vercel.json` (Routing & 301 Redirects Missing):**
   - Old Odoo URLs (`/our-services`, `/about-us`, `/contactus`, `/community-services`, `/appointment`, `/appointment/5`, `/hi/*`) have no 301 redirects configured.
   - `cleanUrls: true` and `www` -> non-`www` canonical host normalization are not configured.
2. **Missing `sitemap.xml` and `robots.txt`:**
   - Search engines have no production XML sitemap at `https://nilofarsdentaloasis.com/sitemap.xml` or crawl directives at `https://nilofarsdentaloasis.com/robots.txt`.
3. **Missing Canonical Tags (`<link rel="canonical">`):**
   - None of the 5 pages declare a canonical URL.
4. **Duplicate / Weak Meta Descriptions:**
   - `about.html`, `treatments.html`, and `contact.html` share an identical generic meta description.
   - `index.html` meta description is only 63 characters.
5. **Client-Side JS Overwrite & Title/Route Bugs:**
   - `smile-gallery.html` has `window.__pageRoute='/treatments'` instead of `'/smile-gallery'`.
   - `route()` in `about.html`, `treatments.html`, `smile-gallery.html`, and `contact.html` overwrites `document.title` dynamically with lowercase/slug-derived titles (`about | Dr. Nilofar's Dental Oasis`), degrading custom SEO titles.
   - `contact.html` overwrites `<main id="app">` via JS on load; `about.html`, `treatments.html`, and `smile-gallery.html` also contain unused SPA route strings in inline JS.
6. **Incomplete Open Graph & Missing Twitter/X Metadata:**
   - Missing `og:url`, `og:image`, `og:site_name`, and all `twitter:*` tags across all 5 pages.
7. **Incomplete Structured Data (JSON-LD):**
   - `index.html` `Dentist` schema lacks `url`, `image`, `logo`, `openingHoursSpecification`, `hasMap`, and `areaServed`.
   - `about.html`, `treatments.html`, `smile-gallery.html`, and `contact.html` have no JSON-LD (`Dentist`, `BreadcrumbList`, `FAQPage`).

---

## 4. Live Odoo Website Audit (`https://nilofarsdentaloasis.com`)

Observed directly via HTTP requests on 2026-11-12:
- **Canonical Host:** `https://nilofarsdentaloasis.com/` returns `301` -> `https://www.nilofarsdentaloasis.com/`.
- **Discovered Live Odoo URLs (`200 OK`):**
  - `/` — Title: `Dental Clinic`, Canonical: `https://www.nilofarsdentaloasis.com/`
  - `/our-services` — Title: `Services | Nilofar's Dental Oasis`
  - `/community-services` — Title: `Community Services | Nilofar's Dental Oasis`
  - `/about-us` — Title: `About Us | Nilofar's Dental Oasis`
  - `/contactus` — Title: `Contact Us | Nilofar's Dental Oasis`
  - `/appointment` (`303` -> `/appointment/5`) — Title: `Dr. Appointments | Nilofar's Dental Oasis`
  - `/hi`, `/hi/our-services`, `/hi/community-services`, `/hi/about-us`, `/hi/contactus`, `/hi/appointment/5` — Hindi alternate pages (`hreflang="hi"`).
- **Odoo `robots.txt`:** `200 OK` (Cloudflare managed + `Allow: /`).
- **Odoo `sitemap.xml`:** Returned HTML fallback rather than XML; Google Search Console export is recommended to confirm any additional indexed URLs.

---

## 5. Migration Risks

1. **Ranking Loss from Unmapped Odoo URLs:** `/our-services`, `/about-us`, `/contactus`, `/community-services`, `/appointment`, `/appointment/5`, and `/hi/*` will 404 on Vercel without explicit `301` redirects in `vercel.json`.
2. **`www` vs non-`www` Host Flip:** Odoo currently canonicalizes to `www.nilofarsdentaloasis.com`, while the new target canonical is `https://nilofarsdentaloasis.com`. Must enforce `301` from `www` -> non-`www` and update Google Business Profile URL after migration.
3. **Google Search Console Baseline Missing:** No GSC export has been provided yet to verify every indexed URL and top-performing query.
4. **JavaScript Title Overwrite:** Dynamic `route()` script overwriting `<title>` on secondary pages can cause Google to index degraded titles.

