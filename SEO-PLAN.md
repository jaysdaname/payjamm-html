# PayJamm SEO Plan

**Site:** https://payjamm.com · **Audited:** August 2026 · **Re-audited:** October 20, 2026 · **Scope:** index.html, signin.html, verify.html, dashboard.html

---

## October 2026 re-audit: what changed in two months

**Short version: PayJamm is still invisible in search, and the fixes that would start changing that are already written but not live.**

- **None of the plan has shipped yet.** The Phase 1–2 fixes (meta tags, canonical, Open Graph image, FAQ/Organization/Video structured data, robots.txt, sitemap.xml, noindex on app pages, pricing-heading fix) have been ready in PR #1 since August 23, but the PR is unmerged and `main` still holds the pre-fix homepage. Unless the live site is deployed from somewhere other than this repo, it is still running the unoptimized version.
- **Still not indexed.** Fresh searches for `"payjamm"` and `payjamm.com register music royalties independent artists` return zero pages from payjamm.com. That's roughly two more months without organic traffic.
- **New: your brand name collides with "PayJam".** A search for "payjamm" surfaces **PayJam** (payj.am and payjam.webflow.io), an unrelated fintech. Until payjamm.com is indexed and has brand signals, Google may treat "payjamm" as a misspelling of "PayJam" and send your branded searches to that company.
- **New: the only things ranking for your brand are a business registry and TikTok.** The Florida registry listing for PAYJAMM LLC (Miami, filed May 2025) and your TikTok account are what Google shows for your name. So TikTok is your most discoverable asset today, and every TikTok should drive viewers to payjamm.com.
- **New: a direct competitor has taken the pillar-content slot.** **Stackt** (getstackt.co) now ranks with *"The Complete Guide to Music Royalty Registrations for Independent Artists (2026)"*, which is nearly the same pillar page this plan recommended for PayJamm. TunePact, Orphiq, Symphonic, and Ditto also publish royalty guides aimed at independent artists. The category is getting crowded, so a generic "royalties explained" guide is no longer enough to stand out.

### Revised 30-day sprint (replaces the original week numbers)

| When | Action | Who |
|---|---|---|
| This week | **Merge PR #1 and deploy.** Confirm `payjamm.com/robots.txt`, `/sitemap.xml`, and `/og-image.png` load in a browser. | You |
| This week | **Google Search Console:** verify the domain, submit the sitemap, and use URL Inspection → *Request indexing* on the homepage. Do the same in Bing Webmaster Tools. | You |
| This week | Replace the placeholder `tel:+1234567890` with the real number (or remove the Click-to-Call buttons). Set the www → non-www 301 redirect at your host. | You |
| Week 2 | **Brand-disambiguation push:** create a Google Business Profile under the exact name "PayJamm" (you have a Miami business registration), and make every social bio use "PayJamm" with the double m and link to `https://payjamm.com`. Pin a TikTok that says the URL out loud. | You |
| Week 2 | Publish real `/terms`, `/privacy`, and `/contact` pages (the footer links to them and they don't exist). | Dev |
| Weeks 3–4 | Publish the first two blog posts, taking a different angle from Stackt's generic guide (see below). Cut each into TikTok clips that link back to the post. | Content |
| Months 2–3 | Remaining posts from Phase 3, a "PayJamm vs Stackt vs TuneRegistry vs Songtrust" comparison page, and the Phase 4 outreach. | Content |

### Updated content angle: lead with unclaimed royalties

Stackt already owns "complete guide to royalty registration". Instead, lead with the angle that creates urgency and fits PayJamm's "we find and collect it for you" pitch:

1. **"You May Have Unclaimed Royalties Waiting at The MLC — Here's How to Check"**: The MLC holds unmatched royalties for a limited period before redistributing them by market share, so unregistered artists lose that money for good. This is your strongest hook, and it is the exact moment an artist needs PayJamm.
2. **"Is DistroKid Enough? What Your Distributor Doesn't Collect"**: this expands homepage FAQ #2 and catches artists who assume distribution covers everything.
3. Then continue with the original Phase 3 list (ASCAP vs BMI, SoundExchange step-by-step, types of royalties, producer royalties).

### Revised targets (counted from the day PR #1 is deployed)

- Homepage indexed and ranking #1 for "PayJamm" (ahead of PayJam) within 2–4 weeks.
- Google Business Profile and social profiles filling the rest of the branded results page within 6 weeks.
- First non-branded impressions in Search Console within 4–8 weeks, and measurable non-branded clicks by month 3–4.

---

*The original August 2026 audit follows. Its findings about the site's code still apply, because the fixes haven't been deployed.*

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
| Compare | PayJamm vs Stackt, PayJamm vs TuneRegistry, Songtrust alternatives, DistroKid vs publishing admin, is DistroKid enough to collect royalties | Comparison pages |
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
