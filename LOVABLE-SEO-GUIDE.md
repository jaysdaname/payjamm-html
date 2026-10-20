# PayJamm SEO in Lovable: prompts and code

This guide carries out the SEO plan (`SEO-PLAN.md`) in a Lovable project. Paste the three prompts into Lovable's chat **one at a time, in order**, and check the result after each before sending the next. Prompt 1 includes the exact code, which was tested in a React + Vite + react-helmet-async build like Lovable's. Prompts 2 and 3 are written for Lovable's AI to build from.

**Before you start**

1. Upload `og-image.png` (in this repo) into the project's `public/` folder. In Lovable's chat, attach the file and say *"Put this file at public/og-image.png"*.
2. Make sure your logo is at `public/logo.png` (the structured data points there).
3. In Prompt 2, replace the `[BRACKETED]` placeholders with your real prices, phone number, and email before sending.

**Why the code looks the way it does.** Lovable sites are single-page React apps: every URL serves the same `index.html`, and JavaScript fills in the page. That causes three classic SEO bugs, and this code avoids all of them:

- A canonical tag hard-coded in `index.html` would tell Google *every* page is the homepage. So canonicals are set per page instead.
- FAQ structured data in `index.html` would appear on every page, which breaks Google's rules. So it is added only on the homepage.
- Defaults in `index.html` plus per-page tags would produce duplicate descriptions. Marking the defaults `data-rh="true"` lets the per-page tags replace them cleanly.

---

## Prompt 1: Technical SEO foundation

Copy everything inside the box below into Lovable.

````
Add technical SEO to this project. Use exactly the code below; don't paraphrase it.

1. Install the package react-helmet-async.

2. In src/main.tsx, wrap <App /> in <HelmetProvider> imported from react-helmet-async. Keep everything else in that file as it is.

3. Replace the <head> of index.html with the following. Keep any existing favicon <link> tags. Do NOT add a <link rel="canonical"> to index.html; canonicals are set per page by the Seo component.

```html
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>PayJamm | Music Royalty Registration for Independent Artists</title>

<!-- Defaults for crawlers that don't run JavaScript (Facebook, LinkedIn, iMessage, Slack).
     data-rh="true" lets react-helmet-async replace them per page instead of duplicating them. -->
<meta data-rh="true" name="description" content="PayJamm's AI registers your songs with ASCAP, BMI, SoundExchange, The MLC and more from one upload — so independent artists and producers collect every royalty they're owed. Keep 100% of your rights." />
<meta data-rh="true" property="og:type" content="website" />
<meta data-rh="true" property="og:site_name" content="PayJamm" />
<meta data-rh="true" property="og:url" content="https://payjamm.com/" />
<meta data-rh="true" property="og:title" content="PayJamm — We Register Your Music, Get You Paid" />
<meta data-rh="true" property="og:description" content="One upload. Every royalty agency. Keep 100% of your rights and royalties." />
<meta data-rh="true" property="og:image" content="https://payjamm.com/og-image.png" />
<meta data-rh="true" property="og:image:width" content="1200" />
<meta data-rh="true" property="og:image:height" content="630" />
<meta data-rh="true" name="twitter:card" content="summary_large_image" />
<meta data-rh="true" name="twitter:title" content="PayJamm — We Register Your Music, Get You Paid" />
<meta data-rh="true" name="twitter:description" content="One upload. Every royalty agency. Keep 100% of your rights and royalties." />
<meta data-rh="true" name="twitter:image" content="https://payjamm.com/og-image.png" />

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Organization",
  "name": "PayJamm",
  "url": "https://payjamm.com/",
  "logo": "https://payjamm.com/logo.png",
  "description": "PayJamm's AI platform registers independent artists' and producers' music with ASCAP, BMI, SoundExchange, The MLC, and other royalty collection agencies so they collect every royalty they're owed.",
  "address": {
    "@type": "PostalAddress",
    "addressLocality": "Miami",
    "addressRegion": "FL",
    "addressCountry": "US"
  },
  "sameAs": [
    "https://facebook.com/profile.php?id=61581331973254",
    "https://instagram.com/payjamm",
    "https://linkedin.com/company/payjamm",
    "https://tiktok.com/@payjamm"
  ]
}
</script>
```

4. Create src/components/Seo.tsx:

```tsx
import { Helmet } from "react-helmet-async";

const SITE_URL = "https://payjamm.com";
const DEFAULT_IMAGE = `${SITE_URL}/og-image.png`;

type JsonLd = Record<string, unknown>;

interface SeoProps {
  title: string;
  description: string;
  /** Route path, e.g. "/" or "/blog/unclaimed-mlc-royalties". */
  path: string;
  image?: string;
  type?: "website" | "article";
  /** Sign-in, dashboard and other app screens: keep them out of Google. */
  noindex?: boolean;
  jsonLd?: JsonLd | JsonLd[];
}

export function Seo({
  title,
  description,
  path,
  image = DEFAULT_IMAGE,
  type = "website",
  noindex = false,
  jsonLd,
}: SeoProps) {
  const url = `${SITE_URL}${path}`;
  const schemas = jsonLd ? (Array.isArray(jsonLd) ? jsonLd : [jsonLd]) : [];

  return (
    <Helmet>
      <title>{title}</title>
      <meta name="description" content={description} />
      <meta name="robots" content={noindex ? "noindex, nofollow" : "index, follow"} />
      {!noindex && <link rel="canonical" href={url} />}

      <meta property="og:type" content={type} />
      <meta property="og:site_name" content="PayJamm" />
      <meta property="og:url" content={url} />
      <meta property="og:title" content={title} />
      <meta property="og:description" content={description} />
      <meta property="og:image" content={image} />
      <meta property="og:image:width" content="1200" />
      <meta property="og:image:height" content="630" />

      <meta name="twitter:card" content="summary_large_image" />
      <meta name="twitter:title" content={title} />
      <meta name="twitter:description" content={description} />
      <meta name="twitter:image" content={image} />

      {schemas.map((schema, i) => (
        <script key={i} type="application/ld+json">
          {JSON.stringify(schema)}
        </script>
      ))}
    </Helmet>
  );
}
```

5. Create src/lib/seo.ts. The homepage FAQ section must render from this FAQS array (replace any hard-coded FAQ items with a map over FAQS), so the visible FAQs and the structured data always match:

```ts
export const FAQS = [
  {
    question: "What services does PayJamm offer?",
    answer:
      "PayJamm registers your music with all major royalty collection agencies including ASCAP, BMI, SoundExchange, The MLC, and more using our custom AI tools.",
  },
  {
    question: "Is this the same as music distribution like DistroKid or TuneCore?",
    answer:
      "No, PayJamm handles royalty registrations and collections, which is different from music distribution. We complement distribution services by ensuring you collect all the royalties you're owed.",
  },
  {
    question: "Do I keep 100% of my rights and royalties?",
    answer:
      "Yes! You retain 100% ownership of your rights and royalties. We simply help you collect what's already yours.",
  },
  {
    question: "What if I already have a PRO like BMI or ASCAP?",
    answer:
      "That's great! We work with your existing PRO affiliations and help ensure all your works are properly registered.",
  },
  {
    question: "How do you do it all — is this automated or manual?",
    answer:
      "We use custom AI tools to automate the registration process, making it fast and accurate while eliminating tedious paperwork.",
  },
  {
    question: "How much does it cost?",
    answer:
      "We offer flexible monthly and annual membership plans. Check our pricing section for current rates.",
  },
  {
    question: "Is my music safe with you?",
    answer:
      "Absolutely. We use industry-standard security measures to protect your music and personal information.",
  },
];

export const faqSchema = {
  "@context": "https://schema.org",
  "@type": "FAQPage",
  mainEntity: FAQS.map(({ question, answer }) => ({
    "@type": "Question",
    name: question,
    acceptedAnswer: { "@type": "Answer", text: answer },
  })),
};

export const videoSchema = {
  "@context": "https://schema.org",
  "@type": "VideoObject",
  name: "PayJamm Introduction",
  description:
    "See how PayJamm registers your music with every major royalty collection agency from one upload.",
  thumbnailUrl: "https://i.ytimg.com/vi/oRMZ-OZF_Uc/hqdefault.jpg",
  embedUrl: "https://www.youtube.com/embed/oRMZ-OZF_Uc",
};
```

6. Add <Seo /> as the first element of every page component:

Homepage (route "/"):
```tsx
<Seo
  title="PayJamm | Music Royalty Registration for Independent Artists"
  description="PayJamm's AI registers your songs with ASCAP, BMI, SoundExchange, The MLC and more from one upload — so independent artists and producers collect every royalty they're owed. Keep 100% of your rights."
  path="/"
  jsonLd={[faqSchema, videoSchema]}
/>
```

Sign-in, sign-up, email verification, dashboard, account/settings, and any other logged-in or utility screen:
```tsx
<Seo title="Sign In | PayJamm" description="Sign in to your PayJamm account." path="/signin" noindex />
```
(Adjust the title and path for each screen; always keep noindex on these.)

The 404 / NotFound page:
```tsx
<Seo title="Page Not Found | PayJamm" description="This page doesn't exist." path="/404" noindex />
```

7. Create public/robots.txt. If the dashboard or verify routes use different paths in this project, use the real paths:

```
User-agent: *
Allow: /
Disallow: /dashboard
Disallow: /verify

Sitemap: https://payjamm.com/sitemap.xml
```

8. Create public/sitemap.xml listing only public, indexable routes that actually exist (never sign-in, dashboard, or verify). For now:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://payjamm.com/</loc>
    <lastmod>2026-10-20</lastmod>
  </url>
</urlset>
```

When done, tell me which page components you added <Seo /> to and which ones are noindex.
````

**Check before moving on:** open the preview, right-click → *View page source*, and confirm the `og:` tags and the Organization script are there. Then visit `/robots.txt` and `/sitemap.xml` in the preview URL.

---

## Prompt 2: Copy, trust, and legal pages

Replace every `[BRACKETED]` value first. If you don't have a phone number, delete that line and keep the "remove the buttons" instruction.

````
Make these content and trust fixes. Keep the existing design, colors, and fonts.

1. Homepage H1: change it to "We Register Your Music — Plug In, Get Paid Every Royalty", keeping the gradient styling on the second half.

2. Pricing section: change the heading to "Simple Membership Pricing" and the subheading to "Lock in pre-launch pricing before we go live". Show the prices on the cards: Monthly [MONTHLY PRICE]/month, Annual [ANNUAL PRICE]/year. Keep the existing checkout links.

3. Add a "How It Works" section directly after the hero with three numbered steps:
   1. "Upload your music": add your songs once; no forms or spreadsheets.
   2. "We register everywhere": our AI registers your works with ASCAP, BMI, SoundExchange, The MLC and more.
   3. "You get paid": collect every royalty you're owed and keep 100% of your rights.
   Use an <h2> for the section title and <h3> for each step.

4. Phone: replace every tel:+1234567890 link with tel:[YOUR PHONE NUMBER]. If no number is given, remove the "Click to Call" buttons entirely.

5. Logo: give every logo <img> the alt text "PayJamm" and explicit width and height attributes matching its displayed size.

6. YouTube video: replace the iframe with a click-to-play facade. Show the thumbnail https://i.ytimg.com/vi/oRMZ-OZF_Uc/hqdefault.jpg with a play button, and only load the YouTube iframe (with autoplay=1) when it's clicked. Use loading="lazy" on the thumbnail.

7. Create three pages, each using the existing site header and footer and starting with the Seo component (not noindex):
   - /terms: "Terms of Service | PayJamm". Draft standard SaaS terms for a music royalty registration membership service operated by PAYJAMM LLC, a Florida company. Add a visible note at the top: "Last updated: [DATE]".
   - /privacy: "Privacy Policy | PayJamm". Draft a standard privacy policy covering account data, uploaded music metadata, payment processing by a third party, and contact for privacy requests.
   - /contact: "Contact PayJamm". Show the email [YOUR CONTACT EMAIL] as a mailto link, plus "Based in Miami, Florida".
   Give each a unique description of 140–160 characters.

8. Footer: point Terms of Service, Privacy Policy, and Contact to the new routes using router links (relative paths, not https://www.payjamm.com/...). Remove the "Platforms" link unless a /platforms page exists.

9. Add /terms, /privacy, and /contact to public/sitemap.xml.
````

**Before publishing:** the legal pages are AI-drafted. Have a lawyer review the Terms and Privacy Policy before you rely on them.

---

## Prompt 3: Blog and the first post

````
Add a blog to the site.

1. Store posts in src/content/posts.ts as an array with: slug, title, description (140–160 characters), datePublished (YYYY-MM-DD), sections (array of { heading, paragraphs }), and faqs (array of { question, answer }).

2. Create /blog (list of posts, newest first) and /blog/:slug (single post). Use the existing header and footer. On a post page, render the title as the only <h1>, each section heading as an <h2>, and the FAQs under a "Frequently Asked Questions" <h2>. End every post with a call-to-action box: "Stop leaving royalties on the table. Let PayJamm register your music everywhere." linking to the pricing section of the homepage.

3. SEO for blog pages:
   - /blog: <Seo title="Music Royalty Guides for Independent Artists | PayJamm" description="Plain-English guides to collecting every music royalty you're owed — PROs, The MLC, SoundExchange, and more — from the PayJamm team." path="/blog" />
   - Post pages: <Seo title={`${post.title} | PayJamm`} description={post.description} path={`/blog/${post.slug}`} type="article" jsonLd={[articleSchema, faqSchemaForThisPost]} /> where articleSchema is a schema.org "BlogPosting" with headline, description, datePublished, dateModified, image "https://payjamm.com/og-image.png", url, author { "@type": "Organization", "name": "PayJamm" }, and publisher { "@type": "Organization", "name": "PayJamm", "logo": { "@type": "ImageObject", "url": "https://payjamm.com/logo.png" } }; and faqSchemaForThisPost is a FAQPage built from post.faqs.
   - Unknown slugs show the NotFound page.

4. Add "Blog" to the header navigation and the footer.

5. Write the first post:
   - slug: unclaimed-mlc-royalties
   - title: "You May Have Unclaimed Royalties Waiting at The MLC — Here's How to Check"
   - Sections: What The MLC is and which royalties it pays (US streaming mechanicals); Why royalties go unmatched (unregistered songs, missing or wrong songwriter splits, ISRCs not linked to the composition); What happens to unmatched money (The MLC holds it for a limited period, then distributes it to publishers by market share — so artists who never register lose it); How to check your songs (search The MLC's public work search and compare against your catalog); How to claim what's yours (register as a member or through a publishing administrator, add your works and splits); How PayJamm handles this for you.
   - 3 FAQs: "Do I need to register with The MLC if I use DistroKid?", "Is joining The MLC free?", "How far back can I collect unmatched royalties?"
   - Target 1,500+ words, plain English, written for independent artists and producers.
   - Do NOT invent statistics, dollar amounts, or exact deadlines. Where a specific number would help, write [VERIFY: ...] so I can fact-check it.

6. Add /blog and /blog/unclaimed-mlc-royalties to public/sitemap.xml, and add a "Latest guide" link to this post on the homepage above the FAQ section.
````

**Before publishing:** search the post for `[VERIFY` and fill in each item from themlc.com.

---

## After Lovable is done

1. **Publish** the project in Lovable.
2. **Domain:** in the project's domain settings, connect both `payjamm.com` and `www.payjamm.com`, and make `payjamm.com` the primary domain so www redirects to it.
3. **Check it's live:** open `https://payjamm.com/robots.txt`, `https://payjamm.com/sitemap.xml`, and `https://payjamm.com/og-image.png` in a browser.
4. **Test the structured data:** paste `https://payjamm.com/` into Google's Rich Results Test (search "Rich Results Test"). It should detect FAQ, Organization, and Video.
5. **Test the link preview:** paste the URL into LinkedIn's Post Inspector or opengraph.xyz. You should see the purple PayJamm card.
6. **Google Search Console:** add a *Domain* property for `payjamm.com`, verify it with the DNS TXT record at your domain registrar, submit `https://payjamm.com/sitemap.xml`, then use URL Inspection → *Request indexing* on the homepage and on the blog post. Do the same in Bing Webmaster Tools, which can import from Search Console.

**One known limitation.** Google runs JavaScript, so it sees each page's own title, description, and canonical. Facebook, LinkedIn, iMessage, and Slack don't, so a shared link to *any* page (including blog posts) shows the homepage preview from `index.html`. That's fine for now. If blog posts later get shared a lot on social media, the fix is a prerendering service in front of the site.
