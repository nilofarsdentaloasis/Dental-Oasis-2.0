# Odoo-to-Vercel URL Migration Mapping (Corrected)

**Canonical Hostname (Preserved from Odoo):** `https://www.nilofarsdentaloasis.com`  
**Apex Host Redirect:** `https://nilofarsdentaloasis.com/*` -> `https://www.nilofarsdentaloasis.com/:path*` (`301 Permanent Redirect`)

## 1. English & Core Odoo URLs (7 Redirects Implemented in `vercel.json`)

| # | Existing Odoo URL | New Vercel Destination | HTTP Action | Verification / Notes |
|---|---|---|---|---|
| 1 | `https://nilofarsdentaloasis.com/*` | `https://www.nilofarsdentaloasis.com/:path*` | **301 Redirect** | Preserves existing `www` canonical host; configure `www` as Primary in Vercel Domains to prevent loops. |
| 2 | `/` | `/` (`index.html`) | **Preserve (200 OK)** | Primary homepage. |
| 3 | `/our-services` | `/treatments` | **301 Redirect** | Exact treatment catalog equivalent (`treatments.html`). |
| 4 | `/about-us` | `/about` | **301 Redirect** | Exact clinic, doctors, awards & community equivalent (`about.html`). |
| 5 | `/contactus` | `/contact` | **301 Redirect** | Exact clinic address, Google Map, FAQs & contact equivalent (`contact.html`). |
| 6 | `/community-services` | `/about#community` | **301 Redirect (Review)** | `about.html` contains the equivalent `#community` section (3+ camps, 125+ consultations). Note: Googlebot drops `#community` when indexing `/about`; flag if you prefer a dedicated `/community-services` page. |
| 7 | `/appointment` | `/contact#appointment` | **301 Redirect** | Leads directly to the 45-min WhatsApp slot booking form (`id="appointment"`). |
| 8 | `/appointment/5` (via `/appointment/:id`) | `/contact#appointment` | **301 Redirect** | Preserves Odoo's `/appointment/5` booking URL. |
| 9 | *(New)* `/smile-gallery` | `/smile-gallery` | **New Canonical (200 OK)** | Before/after patient transformations (`smile-gallery.html`). |

## 2. Hindi Odoo URLs — FLAGGED FOR OWNER APPROVAL (Not Redirected Indiscriminately)

No Hindi (`/hi/*`) pages exist in the new Vercel website. Per SEO best practice, indiscriminate redirects from Hindi URLs to English pages have been **removed** from `vercel.json` pending your decision:

| # | Existing Odoo Hindi URL | Equivalent New Page | Current `vercel.json` Status | Options Requiring Owner Approval |
|---|---|---|---|---|
| 1 | `/hi` | None | **Not redirected (Flagged)** | **A)** Create Hindi `/hi` page; **B)** Approve `301` to `/` if GSC shows negligible Hindi traffic |
| 2 | `/hi/our-services` | None | **Not redirected (Flagged)** | **A)** Create `/hi/our-services`; **B)** Approve `301` to `/treatments` |
| 3 | `/hi/about-us` | None | **Not redirected (Flagged)** | **A)** Create `/hi/about-us`; **B)** Approve `301` to `/about` |
| 4 | `/hi/contactus` | None | **Not redirected (Flagged)** | **A)** Create `/hi/contactus`; **B)** Approve `301` to `/contact` |
| 5 | `/hi/community-services` | None | **Not redirected (Flagged)** | **A)** Create `/hi/community-services`; **B)** Approve `301` to `/about#community` |
| 6 | `/hi/appointment/5` | None | **Not redirected (Flagged)** | **A)** Create `/hi/appointment`; **B)** Approve `301` to `/contact#appointment` |
