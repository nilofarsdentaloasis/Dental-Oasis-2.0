# Pre-Launch Migration Safety Gate

Before switching `nilofarsdentaloasis.com` DNS from Odoo to Vercel, confirm every item below:

- [x] Canonical hostname aligned to `https://www.nilofarsdentaloasis.com` (`non-www -> www` `301` configured).
- [x] Core Odoo URLs mapped and `301` redirects configured in `vercel.json` (`/our-services`, `/about-us`, `/contactus`, `/community-services`, `/appointment`, `/appointment/:id`).
- [x] `sitemap.xml` and `robots.txt` updated to `https://www.nilofarsdentaloasis.com` and returning `200 OK` locally.
- [x] Canonical URLs, OG/Twitter tags, and JSON-LD updated to `https://www.nilofarsdentaloasis.com` across all 5 pages.
- [x] No accidental `noindex` tags or broken internal links exist.
- [ ] **Owner Approval Required:** Decide handling for the 6 Hindi `/hi/*` Odoo URLs (flagged in `ODOO_TO_VERCEL_URL_MAPPING.md`).
- [ ] **Owner Approval Required:** Confirm `/community-services` -> `/about#community` (`301`) is acceptable.
- [ ] **Owner Action Required:** Export Google Search Console baseline (Queries + Indexed Pages) and Hostinger DNS (`MX`/`TXT`/`A`/`CNAME`) before cutover.

**Current Gate Status:** **AWAITING OWNER APPROVAL ON `/hi/*` & `/community-services` + PRE-CUTOVER GSC/DNS EXPORTS — DO NOT SWITCH LIVE DNS.**
