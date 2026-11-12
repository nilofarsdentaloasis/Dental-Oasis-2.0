# Vercel + Hostinger DNS Migration Runbook (Corrected for `www` Canonical)

**Rule:** Do NOT change live DNS or disconnect Odoo until all Pre-Launch SEO Checklist gates pass and the owner explicitly approves cutover.

## 1. Pre-Cutover Documentation (Hostinger)
1. Log in to **Hostinger -> Domains -> nilofarsdentaloasis.com -> DNS / Nameservers**.
2. Screenshot or export **all existing DNS records** (`MX`, `TXT` / `SPF` / `DKIM` / `DMARC`, `A`, `CNAME`) for rollback and email preservation.

## 2. Vercel Domain Setup (Critical Loop Prevention)
1. In **Vercel Project -> Settings -> Domains**:
   - Add `www.nilofarsdentaloasis.com` and set it as **Primary Domain**.
   - Add `nilofarsdentaloasis.com` (apex) and set it to **Redirect (`301`) to `www.nilofarsdentaloasis.com`**.
   - *(This matches the `nilofarsdentaloasis.com -> https://www.nilofarsdentaloasis.com/:path*` rule in `vercel.json` so there is zero redirect loop.)*

## 3. DNS Cutover (Hostinger)
1. Update the root `@` `A` record to Vercel's assigned IP.
2. Update the `www` `CNAME` record to Vercel's assigned `CNAME`.
3. Do **not** modify `MX` or `TXT` email/verification records.
4. Wait for SSL certificate provisioning in Vercel (`Valid Configuration`).

## 4. Rollback Procedure
1. In Hostinger DNS, restore the saved Odoo `A` and `CNAME` records.
