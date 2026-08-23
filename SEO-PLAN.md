# PayJamm SEO Plan

**Site:** https://payjamm.com · **Audited:** August 2026 · **Scope:** index.html, signin.html, verify.html, dashboard.html

---

## 1. Where the site stands today

PayJamm is a one-page landing site (plus sign-in/verify/dashboard app pages). The audit found:

- **PayJamm does not appear in Google results**, even for branded searches combined with "music royalties." The site is either not indexed or barely indexed. This is the single biggest traffic blocker — everything else in this plan matters only after Google can find and index the site.
- **No meta description** on any page. Google writes its own snippet, which hurts click-through rate.
- **No Open Graph / Twitter Card tags.** Links shared on Instagram, TikTok bios, Facebook, or LinkedIn (all linked in the footer) render with no preview image or description.
- **No structured data** (JSON-LD). The homepage already has 7 FAQs — a ready-made FAQPage schema opportunity — plus a video and an organization identity, all unmarked.
- **No robots.txt and no sitemap.xml.**
- **No canonical tag**, and the footer mixes hosts: in-page links are relative, but Terms/Privacy/Contact/Platforms point to `https://www.payjamm.com/...`. Pick one host (recommend non-www `payjamm.com`) and 301-redirect the other.
- **Footer links likely 404:** `/terms`, `/privacy`, `/contact`, `/platforms` don't exist in the repo. Missing Terms and Privacy pages also hurt trust/E-E-A-T and will block most ad platforms.
- **Placeholder phone number** `tel:+1234567890` on both "Click to Call" buttons — a conversion bug, and a trust signal problem if crawled.
- **Tailwind loaded from the CDN `<script>`** — render-blocking JS that Tailwind itself says is not for production. Hurts Core Web Vitals (LCP/TBT).
- **App pages are indexable.** signin.html, verify.html, and dashboard.html have no `noindex`, so thin utility pages can compete with the homepage.
- **Thin content overall:** ~600 words on one page. Competitors ranking for your keywords (TuneRegistry, Songtrust, Ari's Take, Melody Rights) rank on deep educational content.
- **Copy bug with SEO impact:** the Pricing section is headed "It's a wrap! The big day is almost here" — leftover copy that carries zero keyword value and confuses both users and crawlers about what the section is.

## 2. Who you're competing with, and for what

PayJamm's category is **music publishing administration / royalty registration for independent artists**. The winners in search are TuneRegistry, Songtrust, CD Baby Pro, and educational sites (Ari's Take, Soundcharts, Indie Music Academy) that capture artists researching royalties and then funnel them to a service.

**Target keyword map:**

| Intent | Keywords | Target page |
|---|---|---|
| Buy (high intent) | music royalty registration service, publishing administration for independent artists, register my music with ASCAP BMI SoundExchange MLC | Homepage |
| Compare | PayJamm vs TuneRegistry, Songtrust alternatives, DistroKid vs publishing admin, is DistroKid enough to collect royalties | Comparison pages |
| Learn (top of funnel) | how to collect music royalties, SoundExchange registration guide, what is The MLC, ASCAP vs BMI, types of music royalties, unclaimed royalties (MLC black box) | Blog / guides |
| Brand | PayJamm, PayJamm reviews, PayJamm pricing | Homepage + future reviews/pricing pages |

The learn-intent cluster is where the traffic volume is. Every competitor ranking today does it with guides; PayJamm's "TurboTax for music royalties" angle (simple, automated, keep 100%) is a strong differentiator to write from.

## 3. Phase 1 — Get indexed and fix the foundation (Week 1)

1. **Verify the domain in Google Search Console** (and Bing Webmaster Tools). Check the Pages report: if the site isn't indexed, find out why (crawl blocked, hosting issue, never discovered). Request indexing for the homepage.
2. **Add robots.txt** at the site root:
   ```
   User-agent: *
   Allow: /
   Disallow: /dashboard.html
   Disallow: /verify.html
   Sitemap: https://payjamm.com/sitemap.xml
   ```
3. **Add sitemap.xml** listing the homepage (and each new page as it ships), then submit it in Search Console.
4. **Choose one canonical host** — recommend `https://payjamm.com` — 301-redirect www to it, and update the four footer links to relative URLs.
5. **Fix the placeholder phone number** or remove the Click-to-Call buttons until a real number exists.
6. **Create the missing pages** (`/terms`, `/privacy`, `/contact`) or remove the dead footer links. Terms and Privacy are also prerequisites for running Google/Meta ads later.
7. **Noindex the app pages** — add to signin.html, verify.html, dashboard.html:
   ```html
   <meta name="robots" content="noindex, nofollow">
   ```

## 4. Phase 2 — On-page optimization of the homepage (Week 1–2)

**Head section rewrite** for index.html:

```html
<title>PayJamm | Music Royalty Registration for Independent Artists — ASCAP, BMI, SoundExchange & The MLC</title>
<meta name="description" content="PayJamm's AI registers your songs with ASCAP, BMI, SoundExchange, The MLC and more from one upload — so independent artists and producers collect every royalty they're owed. Keep 100% of your rights.">
<link rel="canonical" href="https://payjamm.com/">

<!-- Social sharing -->
<meta property="og:type" content="website">
<meta property="og:url" content="https://payjamm.com/">
<meta property="og:title" content="PayJamm — We Register Your Music, Get You Paid">
<meta property="og:description" content="One upload. Every royalty agency. Keep 100% of your rights and royalties.">
<meta property="og:image" content="https://payjamm.com/og-image.png">
<meta name="twitter:card" content="summary_large_image">
```

Create a 1200×630 `og-image.png` (logo + tagline on the brand gradient).

**Copy changes:**

- H1 is decent; consider working "royalties" in: *"We Register Your Music — Plug In, Get Paid Every Royalty."*
- Replace the Pricing heading "It's a wrap!" with something like **"Simple Membership Pricing"**, and show actual prices. Pages that hide pricing rank worse for "payjamm pricing"-type queries and convert worse.
- Add a short **"How It Works"** section (Upload → We register everywhere → You get paid) with the agency names in text — those entity mentions (ASCAP, BMI, SoundExchange, The MLC) help Google understand the category.
- Add real alt text where images carry meaning, and explicit `width`/`height` on the logo to prevent layout shift.

**Structured data** (JSON-LD in index.html):

- `FAQPage` for the 7 existing FAQs — eligible for rich results, effectively free SERP real estate.
- `Organization` (name, logo, url, sameAs → the four social profiles).
- `VideoObject` for the YouTube embed.
- `Service` or `Product` with offers once pricing is public.

**Performance:**

- Replace the Tailwind CDN script with a compiled Tailwind CSS file (or ~10 KB of hand-written CSS — the page is small enough).
- Load the YouTube embed as a click-to-play facade (thumbnail + play button that injects the iframe on click). The iframe is currently the heaviest thing on the page and drags Core Web Vitals.
- Serve `logo.png` (and future images) as compressed WebP with explicit dimensions.

## 5. Phase 3 — Content engine (Weeks 2–12, ongoing)

Add a `/blog/` (static HTML is fine) and publish 2 posts per month minimum. First eight, in priority order:

1. **How to Collect Every Music Royalty You're Owed (2026 Guide)** — the pillar page; internally link every later post to it.
2. **ASCAP vs BMI: Which PRO Should Independent Artists Join?** — high-volume evergreen comparison.
3. **What Is The MLC and Do You Need to Register?** — includes the "unclaimed/black box royalties" hook: artists searching this are your exact customer.
4. **SoundExchange Registration: Step-by-Step Guide for Independent Artists.**
5. **Is DistroKid/TuneCore Enough? Distribution vs Royalty Collection Explained** — this is already FAQ #2; expand it into the page that intercepts artists who think distribution covers royalties.
6. **The 6 Types of Music Royalties Explained (and Who Pays Them).**
7. **PayJamm vs TuneRegistry vs Songtrust: Publishing Admin Compared** — honest comparison page targeting "alternatives" searches.
8. **Producer Royalties: How Beatmakers and Producers Get Paid.**

Each post: 1,500+ words, one target keyword in title/H1/URL, FAQ block with FAQPage schema, and a CTA back to the homepage. The YouTube channel is a multiplier — publish each guide as a video too, and embed it (video results + a second SERP presence).

## 6. Phase 4 — Authority and off-page (ongoing)

- **Directories/profiles:** complete Google Business Profile (if there's a business address), Crunchbase, Product Hunt launch, Trustpilot. These also create branded SERP coverage so searches for "PayJamm" look trustworthy.
- **Music-industry backlinks:** pitch guest posts / tool mentions to indie-artist blogs and newsletters (Ari's Take, Hypebot, DIY Musician, Water & Music), and "best publishing admin tools" listicles that currently feature TuneRegistry.
- **Social consistency:** the four footer profiles should link back to payjamm.com and share each new guide (social links don't rank pages directly, but they drive discovery and branded search volume).
- **Reviews:** ask early members for Trustpilot/Google reviews — review stars dominate "payjamm reviews" queries you'll want to own before someone else does.

## 7. Measurement

- **Search Console:** weekly check of Pages (indexing), Queries (impressions/CTR), and Enhancements (FAQ rich results).
- **GA4** (or a privacy-friendly alternative like Plausible): track organic sessions and the two conversion events — checkout link clicks and sign-in starts.
- **Targets:** homepage indexed and ranking #1 for "PayJamm" within 2–4 weeks of Phase 1; first non-branded impressions in 4–8 weeks; measurable non-branded clicks from the content cluster by month 3–4.

## 8. Priority checklist

| # | Action | Effort | Impact |
|---|---|---|---|
| 1 | Google Search Console + fix indexing | Low | Critical |
| 2 | robots.txt + sitemap.xml | Low | Critical |
| 3 | Meta description, canonical, OG tags | Low | High |
| 4 | Fix placeholder phone + dead footer links | Low | High |
| 5 | FAQPage + Organization JSON-LD | Low | High |
| 6 | Noindex app pages, fix "It's a wrap!" heading | Low | Medium |
| 7 | Compiled CSS + YouTube facade (Core Web Vitals) | Medium | Medium |
| 8 | Terms/Privacy/Contact pages | Medium | Medium |
| 9 | Blog: pillar + first 4 posts | High | High (compounding) |
| 10 | Comparison pages + backlink outreach | High | High (compounding) |
