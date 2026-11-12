# Google Search Console Setup & Baseline Guide

## 1. Before Domain Cutover (Record Baseline on Odoo)
1. Sign in to **Google Search Console** for the existing property (`nilofarsdentaloasis.com` or `www.nilofarsdentaloasis.com`).
2. Export **Performance -> Search Results** (Last 3 months & Last 28 days):
   - Total Clicks, Total Impressions, Average CTR, Average Position.
   - Top 20 Queries and Top Pages.
3. Export **Indexing -> Pages**:
   - Record all currently indexed URLs to verify none are missing from `docs/seo/ODOO_TO_VERCEL_URL_MAPPING.md`.

## 2. Property Verification (Recommended: Domain Property)
1. In Google Search Console, add a **Domain property**: `nilofarsdentaloasis.com`.
2. Copy the provided `TXT` DNS record (`google-site-verification=...`).
3. Add the `TXT` record in **Hostinger DNS Zone Editor** (keep it permanently; do not delete after verification).
4. Click **Verify** in Google Search Console.

## 3. Immediately After Vercel Cutover
1. Go to **Sitemaps** -> Submit `https://nilofarsdentaloasis.com/sitemap.xml`.
2. Use **URL Inspection** on:
   - `https://nilofarsdentaloasis.com/`
   - `https://nilofarsdentaloasis.com/treatments`
   - `https://nilofarsdentaloasis.com/about`
   - `https://nilofarsdentaloasis.com/smile-gallery`
   - `https://nilofarsdentaloasis.com/contact`
3. Click **Request Indexing** for the homepage and key service pages if needed, and monitor **Pages** & **Redirects** weekly for 30 days.

