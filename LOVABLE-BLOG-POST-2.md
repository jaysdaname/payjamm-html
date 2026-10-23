# Blog post #2 for Lovable: "Is DistroKid Enough?"

Copy everything inside the box below into Lovable's chat. It adds the post exactly as written, links it into the sitemap, and lists you as the author on every blog post so Google connects your About page to your writing.

Before publishing, read it once to make sure it matches how PayJamm works today. The facts about DistroKid, PROs, The MLC and SoundExchange are general industry facts, but check DistroKid's current add-ons if you mention them anywhere else.

````
Add a second blog post and two small structured-data updates. Make only these changes.

1. In src/content/posts.ts, add this post to the posts array. Use the text exactly as written. Set datePublished to today's date (YYYY-MM-DD).

slug: "is-distrokid-enough"
title: "Is DistroKid Enough? The Royalties Your Distributor Doesn't Collect"
description: "DistroKid gets your music on Spotify and pays your master royalties, but performance, mechanical and SoundExchange royalties are collected elsewhere. Here's what to register."

Section: "What DistroKid actually does"
- "DistroKid, TuneCore, CD Baby, UnitedMasters and other distributors do one job very well: they deliver your recordings to streaming services and stores, then collect the money those services pay for your recordings and pass it to you. If you upload a single to DistroKid and it gets streamed on Spotify, the payout you see in your DistroKid dashboard is the recording's share of that revenue."
- "That money is real, and for many independent artists it is the only royalty income they ever see. But it is only one of several income streams a song creates. A distributor is not a royalty collection service for everything your music earns, and assuming it is can leave a large part of your income uncollected."

Section: "The two copyrights inside every song"
- "Every track you release contains two separate copyrights. The sound recording, often called the master, is the actual audio file: your performance, captured and mixed. The composition is the song itself: the melody and lyrics you or your co-writers wrote."
- "Your distributor collects for the master. The composition earns its own royalties, and those are collected by different organizations. If you write your own songs, you own both copyrights, which means you are owed money from both sides. Most independent artists only ever collect the first."

Section: "Royalties your distributor doesn't collect"
- "Performance royalties. When your song is streamed, played on radio or TV, or performed in a venue, the composition earns a performance royalty. In the US these are collected by performing rights organizations (PROs) such as ASCAP, BMI and SESAC. You have to join a PRO and register each song with its writers and splits. PROs pay a writer's share and a publisher's share, and self-published writers often miss the publisher's share entirely unless they set up a publishing entity or use a publishing administrator."
- "Mechanical royalties. Every stream or download of your song in the US also creates a mechanical royalty for the composition. Streaming mechanicals are collected by The Mechanical Licensing Collective (The MLC), and you only get paid if you are a member and your works are registered and matched to your recordings. Your distributor does not do this for you."
- "Digital performance royalties for your recording. When your recording plays on non-interactive digital radio, such as SiriusXM, internet radio and similar services, a separate royalty is paid by SoundExchange to the featured artist and to the owner of the master. These are not paid through your distributor. If you never registered with SoundExchange, this money can sit waiting for you."
- "International royalties. When your music is played outside the US, local collection societies collect performance, mechanical and neighboring rights royalties. Some of that reaches you through your PRO and other organizations, but only if your songs and recordings are registered correctly with matching metadata."

Section: "How to tell if you're missing money"
- "Answer these five questions for your catalog. Are you a member of a PRO, and is every song you wrote registered with all of its writers and splits? Are you a member of The MLC, and are your works matched to your releases? Are you registered with SoundExchange as a featured artist, and as the rights owner if you own your masters? Do your ISRCs (recording codes) match the songs registered with your PRO and The MLC? Have you and your co-writers agreed on splits in writing?"
- "If the answer to any of these is no or not sure, there is a good chance some of your royalties are not reaching you. The fix is registration, not a new distributor. Keep releasing through the distributor that works for you, and make sure the composition and recording are registered everywhere they earn."

Section: "What it takes to set this up"
- "Most of these organizations are free or low cost for songwriters and artists to join, and you can register with each of them yourself. The hard part is not the fees. It is the time: separate accounts, separate forms, and the same song details entered again and again, correctly, for every release and every collaborator."
- "That is manageable for one single. For a growing catalog with co-writers, features and producers, it quickly becomes a part-time job, and one small metadata mismatch can stop a song from paying."

Section: "How PayJamm handles this for you"
- "PayJamm was built to close the gap between distribution and getting paid. You add your release details once. PayJamm organizes your songs, writers, splits and ISRCs, helps you create and sign split sheets with collaborators, checks your metadata for gaps, and prepares registrations for the royalty organizations that apply to your music."
- "Keep using DistroKid or whichever distributor you prefer. PayJamm works alongside it, so the royalties your distributor does not collect have somewhere to go. Not sure where your songs stand today? Start with the free royalty check."

FAQs:
- Q: "Does DistroKid collect publishing royalties?" A: "Distribution on its own covers your master recording. Publishing royalties, meaning the performance and mechanical royalties your composition earns, are collected through PROs, The MLC and international societies, either directly by you or through a publishing administrator. If you have signed up for any optional add-ons in your distributor account, check exactly what they cover."
- Q: "If I'm already with ASCAP or BMI, am I covered?" A: "Only for performance royalties, and only for the songs you have registered with them. Your PRO does not collect US streaming mechanicals, which are paid by The MLC, or digital radio royalties for your recordings, which are paid by SoundExchange."
- Q: "Do I need SoundExchange if DistroKid already pays me for Spotify streams?" A: "Yes. Your distributor pays you for on-demand streams on services like Spotify and Apple Music. SoundExchange pays for a different kind of play: non-interactive digital radio such as SiriusXM and internet radio. The two never overlap, so you need both."

2. In the post page, link the words "free royalty check" in the last section to /royalty-finder, the same way the first post does.

3. In src/pages/blog/BlogPost.tsx, change the BlogPosting "author" from the PayJamm organization to {"@type": "Person", "name": "Justin Henry", "url": "https://payjamm.com/about"}. Keep "publisher" as the PayJamm organization.

4. In index.html, add "founder": {"@type": "Person", "name": "Justin Henry", "url": "https://payjamm.com/about"} to the Organization object in the JSON-LD.

5. In public/sitemap.xml, add https://payjamm.com/blog/is-distrokid-enough next to the existing blog post entry.

6. In the first post (unclaimed-mlc-royalties), make the FAQ answer to "Do I need to register with The MLC if I use DistroKid?" end with a link to the new post: "Read more: Is DistroKid Enough?" linking to /blog/is-distrokid-enough.
````

**After it's published:** in Google Search Console, use URL Inspection on `https://payjamm.com/blog/is-distrokid-enough` and click *Request indexing*. Then cut the "five questions" section into a TikTok that ends with "link in bio."
