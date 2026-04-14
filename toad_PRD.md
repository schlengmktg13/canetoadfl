# South Florida Invasive Species Lead Generation — Project Reference Document

**Last Updated:** March 2026
**Status:** In build — site running locally, deploying to Cloudflare Pages
**Owner:** Andrew

---

## CURSOR INSTRUCTIONS

This file is the single source of truth for the entire project. When building or editing any page, refer to this document for:
- Target keyword and search volume for each page
- Internal linking rules — which pages link to which
- Content priorities and what each page needs to accomplish
- Lead form placement and CTA language
- Revenue model context (helps write conversion-focused copy)

**Tech stack decisions (final):**
- Framework: Astro 6.0.8
- Hosting: Cloudflare Pages (free, auto-deploys from GitHub)
- Forms: Tally (free tier, embed via iframe)
- Lead routing: Zapier (zip-code based routing to providers)
- SEO tracking: Ahrefs
- Local dev: `npm run dev` → http://localhost:4321

**Content workflow:**
- Page drafts are written in Claude.ai (claude.ai) using this PRD as context
- Pages are implemented in Cursor as `.astro` files
- All pages use `src/layouts/BaseLayout.astro` — edit that file for global style/nav/footer changes
- New pages go in `src/pages/[slug]/index.astro` — Astro auto-generates the URL
- Use `src/components/ContentToc.astro` for table-of-contents blocks (no inline styling)
- **Images:** put optimizable rasters in `src/assets/images/`, import them in each page (or use `src/components/ContentImage.astro`), and render with `Image` from `astro:assets` (build-time WebP, width/height for CLS). Use `getImage()` from `astro:assets` for CSS backgrounds. For favicons or anything that must stay at a fixed URL with no processing, keep files in `public/` and use a normal `<img>` with explicit dimensions where layout matters. Global content-image styles live in `BaseLayout.astro`.

---

## 1. Project Overview

### What This Is
An online lead generation business that captures search demand from South Florida homeowners looking for cane toad (bufo toad) removal services, then sells those leads to local removal providers. The business does NOT provide removal services directly — it is a digital middleman that monetizes the gap between searchers and service providers.

### Why This Works
- South Florida has a massive, permanent, and growing invasive species problem
- Cane toads can kill dogs in 15 minutes — emotional urgency drives high-intent search behavior
- The provider landscape is fragmented (10-15 small operators), with weak SEO and no dominant marketplace
- 80% of toad-related searches (~13,000/mo) are landing on non-specialized destinations (Reddit, generic pest control, news articles)
- ToadBusters.com, the market leader, captures only ~16% of total search volume despite being the most established player (DA 27, 2,578 traffic/mo)

### Core Insight: Gap Capture, Not Competitive Displacement
The opportunity is NOT stealing traffic from ToadBusters. It's capturing the ~13,000 monthly searches that nobody is serving well — particularly 45+ geo-modified city/county keywords with zero dedicated pages from any competitor, and 12,400/mo in informational searches with no comprehensive resource site.

---

## 2. Market Data (Validated)

### Search Volume (from Google Keyword Planner, Florida filter)

**Cane Toad Keywords:**
- Total keywords researched: 74
- Commercial intent: 56 keywords, 3,250/mo reported + est. 360-810/mo long-tail below threshold = ~3,600-4,060/mo
- Informational: 18 keywords, 12,400/mo reported
- Combined toad search universe: ~16,000-16,500/mo

**Iguana Keywords (Phase 2):**
- Total keywords researched: 38
- Commercial intent: 29 keywords, 14,650/mo reported
- Informational: 9 keywords, 55,500/mo
- Iguana opportunity is ~4-5x larger than toads

**Growth Signals:**
- "cane toad removal" — 900% YoY growth
- "cane toad removal florida" — 900% YoY growth
- "iguana removal florida" — 900% YoY growth

### Top Commercial Keywords (Toad)
| Keyword | Volume/mo | CPC Range | Competition |
|---------|-----------|-----------|-------------|
| cane toad removal florida | 500 | n/a | Low |
| cane toad control | 500 | n/a | Low |
| cane toad repellent | 500 | $0.31-$2.08 | High |
| cane toad trap | 500 | $0.25-$3.02 | Low |
| how to get rid of cane toads | 500 | $0.20-$2.55 | Low |
| how to get rid of bufo toads | 500 | $0.38-$1.00 | Low |
| cane toad removal | 50 | $0.30-$4.56 | Low |
| cane toad removal near me | 50 | n/a | High |
| bufo toad removal | 50 | n/a | Medium |
| toad proof fencing | 50 | n/a | Low |
| 45+ geo-modified keywords | <10 each | n/a | n/a |

### Top Informational Keywords (Toad)
| Keyword | Volume/mo |
|---------|-----------|
| cane toad florida | 5,000 |
| bufo toad florida | 5,000 |
| are cane toads poisonous | 500 |
| cane toad dog symptoms | 500 |
| cane toad eggs | 500 |
| cane toad vs southern toad | 500 |

### Top Iguana Keywords (Phase 2)
| Keyword | Volume/mo | CPC Range |
|---------|-----------|-----------|
| iguanas in florida | 50,000 | $0.05-$1.83 |
| iguana repellent | 5,000 | $0.24-$3.99 |
| iguana trapping | 5,000 | $0.34-$6.07 |
| iguana removal near me | 500 | $3.87-$14.00 |
| iguana removal service | 500 | $4.70-$14.00 |
| iguana removal miami | 500 | $2.59-$10.77 |
| iguana control | 500 | $3.04-$12.00 |

---

## 3. Competitor Analysis (Validated)

### Competitor Traffic Data
| Site | Category | Organic Traffic | Keywords | DA | Backlinks |
|------|----------|----------------|----------|----|-----------| 
| iguanacontrol.com | Iguana | 28,658 | 2,977 | 25 | 2,585 |
| toadbusters.com | Toad | 2,578 | 434 | 27 | 319 |
| xceptionalwildlife.com | All | 1,984 | 2,821 | 18 | 5,959 |
| redlineiguana.com | Toad-Iguana | 1,691 | 689 | 21 | 112 |
| nuisancewildliferangers.com | All | 1,320 | 3,927 | 25 | 27,092 |
| animalrangers.com | All | 425 | 1,227 | 20 | 1,789 |
| iggytrap.com | Toad-Iguana | 341 | 318 | 16 | 253 |
| wildliferemovalservicesofflorida.com | Iguana | 242 | 1,360 | 19 | 1,750 |
| iguanaexterminators.com | Iguana | 117 | 132 | 5 | 983 |
| humaneanimalremoval.com | All | 114 | 272 | 12 | 96 |
| canecatcher.com | Toad | 65 | 34 | 10 | 43 |
| abugslifepest.com | All | 55 | 332 | 6 | 732 |
| trekscanetoadremoval.com | Toad | 32 | 61 | 6 | 42 |
| iguanagoneremoval.com | Iguana | 24 | 36 | 1 | 0 |
| wildthingsflorida.com | Toad-Iguana | 20 | 49 | 13 | 268 |
| allnixservices.com | All | 7 | 56 | 6 | 84 |

**Key finding:** All toad competitors combined capture only ~3,200 visits/mo of the ~16,250/mo total toad search volume. 80% of searches are unserved.

### ToadBusters Deep Dive
- Founded 2015 by Jeannine Tilford (herpetologist/vet tech)
- FWC-registered nuisance wildlife trapper
- Serves SW + SE Florida
- Also runs Pet Protect Fencing (barrier installation)
- Hiring technicians (night-only work), indicating demand > capacity

**ToadBusters Pricing (actual, as of 2026):**
- Initial consultation: $190 (includes first collection + property assessment)
- Recurring maintenance (≤1 acre): $170/mo (2 visits, 3-month min) — BEST VALUE
- Single monthly visit (≤1 acre): $100/mo (3-month min)
- On-demand visit (≤1 acre): $120/visit
- 1-2 acres: $120/visit
- 2-4 acres: $150/visit
- Emergency visit: $315
- Barrier fencing: custom quoted

**Estimated ToadBusters revenue:** $250K-$400K/year

**Critical implication for lead pricing:** At $190 initial + $170/mo recurring, customer LTV is $1,200-$2,000+/year. Providers should pay $40-75/lead.

---

## 4. Revenue Model

### Lead Gen Revenue Projections (Toad Only)

| | Year 1 (Building) | Year 2 (Established) | Year 3 (Dominant) |
|---|---|---|---|
| Commercial traffic capture | 10-15% | 20-30% | 30-45% |
| Info traffic capture | 5-10% | 12-18% | 18-25% |
| Total leads/mo | 36-86 | 115-223 | 173-393 |
| Lead price | $40-$75 | $40-$75 | $40-$75 |
| **Lead gen revenue** | **$11K-$36K** | **$42K-$107K** | **$73K-$236K** |

### Additional Revenue Streams
| Stream | Year 1 | Year 2 | Year 3 |
|--------|--------|--------|--------|
| Affiliate/e-commerce (traps, repellents, fencing) | $1K-$3K | $3K-$8K | $5K-$15K |
| Emergency pet kit (own product, $25-40) | $0-$2K | $2K-$8K | $5K-$15K |
| Ad revenue on informational content | $0-$500 | $500-$2K | $1K-$5K |

### With Iguana Expansion (Phase 2+)
Iguana market is ~4-5x larger. Adding iguanas in Year 2 pushes total mature revenue to $150K-$300K with $100K-$240K net profit.

---

## 5. Lead Gen Model

### Lead Delivery Flow
1. Homeowner finds site via Google (organic or paid)
2. Submits Tally quote form or calls tracked phone number
3. Lead auto-routed to matched provider(s) by zip code via Zapier
4. Provider receives email + SMS with lead details
5. Lead logged to Google Sheet for billing
6. Provider billed weekly/biweekly

### Lead Pricing
- Shared leads (sent to 2-3 providers): $40-$50/lead
- Exclusive leads (sent to 1 provider): $60-$75/lead

### Provider Protection Mechanisms
- Control the initial connection (call tracking, booking forms)
- Bill on short cycles (weekly/biweekly)
- Maintain 2-3 competing providers per zip code
- If a provider stops paying, redirect their leads to competitor
- Call recording provides proof of lead delivery

---

## 6. Site Architecture & Page Status

### Page Build Status

| Status | URL | Target Keyword | Volume/mo | Priority |
|--------|-----|---------------|-----------|----------|
| ✅ Built | / | cane toad removal florida | 500 | P1 |
| ✅ Built | /cane-toad-removal/ | cane toad removal | 50 | P1 |
| ✅ Built | /cane-toad-florida/ | cane toad florida | 5,000 | P1 |
| ✅ Built | /providers/ | (B2B, not SEO target) | — | P1 |
| ✅ Built | /cane-toad-dog-poisoning/ | cane toad dog symptoms | 500 | P1 |
| ✅ Built | /bufo-toad-florida/ | bufo toad florida | 5,000 | P1 |
| ✅ Built | /cane-toad-removal-cost/ | cane toad removal cost | <10 | P1 |
| ✅ Built | /cane-toad-removal-miami-dade/ | cane toad removal miami | <10 | P2 |
| ✅ Built | /cane-toad-removal-broward-county/ | cane toad removal broward | <10 | P2 |
| ✅ Built | /cane-toad-removal-palm-beach-county/ | cane toad removal palm beach | <10 | P2 |
| ✅ Built | /cane-toad-removal-collier-county/ | cane toad removal naples | <10 | P2 |
| ✅ Built | /cane-toad-removal-lee-county/ | cane toad removal cape coral | <10 | P2 |
| ✅ Built | /how-to-get-rid-of-cane-toads/ | how to get rid of cane toads | 500 | P2 |
| ✅ Built | /cane-toad-trap/ | cane toad trap | 500 | P2 |
| ✅ Built | /cane-toad-repellent/ | cane toad repellent | 500 | P2 |
| ✅ Built | /cane-toad-removal-martin-st-lucie/ | cane toad removal stuart | <10 | P3 |
| ✅ Built | /cane-toad-removal-parkland/ | cane toad removal parkland | <10 | P3 |
| ✅ Built | /cane-toad-removal-west-palm-beach/ | cane toad removal west palm | <10 | P3 |
| ✅ Built | /cane-toad-vs-southern-toad/ | cane toad vs southern toad | 500 | P3 |
| ✅ Built | /are-cane-toads-poisonous/ | are cane toads poisonous | 500 | P3 |
| ✅ Built | /cane-toad-eggs/ | cane toad eggs | 500 | P3 |
| ✅ Built | /toad-proof-fencing/ | toad proof fencing | 50 | P3 |
| ✅ Built | /about/ | — | — | P3 |
| ✅ Built | /contact/ | — | — | P3 |
| ✅ Built | /privacy-policy/ | — | — | P3 |

### Internal Linking Rules (follow these on every page)
- Every page links to `/` (homepage) and `/cane-toad-removal/` via nav — already handled by BaseLayout
- All informational pages link to `/cane-toad-florida/` (pillar page) — always include a contextual link
- All pages include a CTA linking to `/cane-toad-removal/` or the relevant geo page
- All informational pages include: "Already seeing toads? [Connect with a removal pro →](/cane-toad-removal/)"
- Geo pages link to adjacent county pages
- Product pages (`/cane-toad-trap/`, `/cane-toad-repellent/`) link to `/how-to-get-rid-of-cane-toads/` and `/cane-toad-removal/`
- `/cane-toad-dog-poisoning/` links to `/cane-toad-removal/` prominently — highest-urgency conversion path

### Page Template (copy for every new page)
```astro
---
import BaseLayout from '../../layouts/BaseLayout.astro';
---

<BaseLayout
  title="[Target Keyword, Title Case] | CaneToadFL"
  description="[150-160 chars, includes target keyword, includes location 'South Florida' or specific county]"
>

  <div class="urgency">
    <strong>⚠️ Have a dog?</strong> Cane toad toxin can kill a dog in 15 minutes.
    <a href="/cane-toad-dog-poisoning/">Emergency response guide →</a>
  </div>

  <div class="hero">
    <h1>[H1 — matches or closely mirrors target keyword]</h1>
    <p>[2-3 sentence intro — lead with the problem/urgency, not the solution]</p>
    <a href="#get-quote" class="btn btn-lg">Get a Free Quote →</a>
  </div>

  <div class="lead-form-wrap" id="get-quote">
    <h2>Get Connected with a Local Provider</h2>
    <p>Enter your zip code and we'll match you with a licensed removal professional in your area.</p>
    <!-- Replace with Tally embed -->
    <div class="tally-placeholder">
      📋 <strong>Tally form goes here</strong><br/>
      <code>&lt;iframe src="https://tally.so/embed/YOUR_FORM_ID" width="100%" height="400" frameborder="0"&gt;&lt;/iframe&gt;</code>
    </div>
  </div>

  <div class="content">
    <!-- Page body content here -->
    <!-- Always end with FAQ section and internal links to related pages -->
  </div>

</BaseLayout>
```

---

## 7. CSS Classes Reference (BaseLayout.astro)

Use these classes in all pages — do not add inline styles unless absolutely necessary:

| Class | Use |
|-------|-----|
| `.hero` | Green-tinted hero box with H1 and intro paragraph |
| `.urgency` | Yellow warning banner — use on every page above the hero |
| `.btn` | Orange CTA button |
| `.btn-lg` | Larger version of CTA button — use in hero |
| `.lead-form-wrap` | Dark green form container — place after hero |
| `.tally-placeholder` | Placeholder box until Tally form is embedded |
| `.content` | Main body content wrapper — provides heading styles, spacing |
| `.geo-grid` | Responsive grid of county/city cards |
| `.geo-card` | Individual card in geo grid |
| `.faq` | FAQ section wrapper |

---

## 8. Tech Stack

| Component | Decision | Cost |
|-----------|----------|------|
| Framework | Astro 6.0.8 | Free |
| Hosting | Cloudflare Pages | Free |
| Forms | Tally | Free |
| Lead routing | Zapier | Free–$20/mo |
| Call tracking | CallRail (when needed) | $45-95/mo |
| SEO research & tracking | Ahrefs | Existing subscription |
| Analytics | Google Analytics 4 + Search Console | Free |
| Local dev | Cursor + npm run dev | Free / $20/mo |
| Google Ads (test) | Direct | $300-500/mo when ready |

**Monthly cost at launch: ~$0-20/mo** (before CallRail and Google Ads)

---

## 9. Geo-Modified Keywords (Full List)

These are the <10/mo keywords that collectively represent 360-810+ monthly searches. Each geo page should target a cluster of these:

bufo toad exterminator, bufo toad removal boca raton, bufo toad removal cost, bufo toad removal florida, bufo toad removal fort lauderdale, bufo toad removal miami, bufo toad removal naples, bufo toad removal near me, bufo toad removal palm beach, cane toad exterminator, cane toad removal boca raton, cane toad removal bonita springs, cane toad removal boynton beach, cane toad removal broward county, cane toad removal cape coral, cane toad removal collier county, cane toad removal coral springs, cane toad removal cost, cane toad removal davie, cane toad removal delray beach, cane toad removal doral, cane toad removal estero, cane toad removal fort lauderdale, cane toad removal homestead, cane toad removal jupiter, cane toad removal kendall, cane toad removal lee county, cane toad removal miami, cane toad removal miami dade, cane toad removal naples, cane toad removal palm beach, cane toad removal parkland, cane toad removal pembroke pines, cane toad removal plantation, cane toad removal st lucie, cane toad removal stuart, cane toad removal vero beach, cane toad removal wellington, cane toad removal west palm beach, cane toad removal weston, cane toad trapping, poison toad removal, toad removal near me, toad removal service, toad removal service florida

---

## 10. Provider Outreach Plan

### Target Providers (priority order)
1. **Treks Cane Toad Removal** — Small, Naples/Collier focus, likely hungry for leads
2. **Wild Things Florida** — SW Florida, HOA/CDD work
3. **Redline Iguana** — Toads + iguanas, Boca/FTL/Miami (good Phase 2 partner)
4. **Humane Animal Removal** — Miami-Dade, 35+ years
5. **Allnix Services** — Deerfield Beach to Hollywood corridor
6. **Animal Rangers** — Statewide, larger operation
7. **Iggy Trap** — Toads + iguanas
8. **ToadBusters** — Market leader, try last

### Outreach Script
"Hi [Name], I'm building a website focused on helping South Florida homeowners find cane toad removal services. I'm going to be generating leads from people actively searching for removal in [their area].

I'd like to send those leads your way. You only pay when you receive a qualified lead — someone with a name, phone number, and address who's looking for removal service. I'm thinking $[40-60] per lead.

Given that a typical customer is worth $1,200+ in recurring service over a year, the economics should work well for you. Would you be open to a quick conversation?"

### Key Questions for Provider Calls
- What do you currently pay for customer acquisition?
- What's your close rate on inbound leads?
- Which geographic areas are you looking to grow?
- Shared leads or exclusive?
- What's your average customer lifetime?

---

## 11. Validation Checklist

| Step | Status | Notes |
|------|--------|-------|
| Keyword volume validation | ✅ Done | 114 keywords researched |
| Competitor SEO audit | ✅ Done | 17 competitors analyzed |
| ToadBusters pricing research | ✅ Done | $190 initial, $170/mo recurring |
| Tech stack decision | ✅ Done | Astro + Cloudflare Pages + Tally + Zapier |
| Domain registered | ⬜ Pending | Top picks: CaneToadFL.com, BufoAlert.com, CaneToadFL.com |
| Site running locally | ✅ Done | Astro 6.0.8, localhost:4321 |
| GitHub repo created | ⬜ Pending | Required for Cloudflare Pages deploy |
| Cloudflare Pages connected | ⬜ Pending | Free hosting, auto-deploy on push |
| Tally forms created | ⬜ Pending | Homeowner form + provider application form |
| Google Search Console set up | ⬜ Pending | After domain + deploy |
| Call 3-5 providers | ⬜ Pending | Validate $40-75/lead willingness |
| Sign first 2-3 providers | ⬜ Pending | Start with smaller operators |
| Google Ads test ($300-500) | ⬜ Pending | After 10+ pages live |

---

## 12. Risk Register

| Risk | Severity | Mitigation |
|------|----------|------------|
| Market ceiling (toad-only ~$60-180K max) | Medium | Layer iguanas in Year 2 for 4-5x multiplier |
| Provider payment risk | Medium | 2-3 providers per zip, weekly billing, call tracking proof |
| Seasonality (Nov-Feb dropoff) | Medium | Plan cash flow; use off-season for content building |
| Competitive entry (Angi, Thumbtack) | Low | First-mover + niche authority moat |
| Google algorithm changes | Low | Diversify with paid ads + direct provider relationships |
| Regulatory changes (FWC licensing) | Low | Monitor; could reduce provider supply |

---

## 13. Phase Roadmap

### Phase 1: Cane Toad Beachhead (Months 1-6)
- Launch 25+ page authority site ← IN PROGRESS
- Sign 5-10 providers
- Run Google Ads test
- Target: 36-86 leads/mo by month 6
- Revenue target: $10K-$29K Year 1

### Phase 2: Add Iguanas (Months 6-12)
- Expand site with 20-30 iguana pages
- Sign 5-10 iguana providers (many overlap with toad providers)
- Scale Google Ads to iguana keywords ($3-19 CPCs)
- Revenue target: $34K-$102K Year 2

### Phase 3: Full Invasive Species Platform (Months 12-24)
- Add pythons, general wildlife, barrier fencing
- E-commerce layer (emergency kits, deterrents)
- HOA/commercial lead premium tier ($100-250/lead)
- Provider subscription model ($200-500/mo)
- Revenue target: $80K-$150K

### Phase 4: Scale & Optimize (Year 2+)
- Geographic expansion (Central FL, Gulf Coast)
- Multiple revenue streams: leads + subscriptions + ads arbitrage + affiliate
- Revenue target: $150K-$300K with $100K-$240K net profit

---

## 14. Domain Options

**Toad-specific (better for Phase 1 SEO):**
- CaneToadFL.com ← current working name used in codebase
- BufoAlert.com
- CaneToadFL.com
- ToadGuardFL.com
- SouthFloridaToadRemoval.com

**Broader (better for multi-species expansion):**
- InvasiveFreeFlorida.com
- FloridaWildlifeRemoval.com

**Note:** Once domain is registered, update `astro.config.mjs` → `site:` field and BaseLayout.astro og:url meta tag.

---

## 15. Open Decisions

| Decision | Status | Notes |
|----------|--------|-------|
| Domain name | ⬜ Pending | Toad-specific vs. broader — decide before launch |
| Shared vs. exclusive leads | ⬜ Pending | Start shared (easier to sell), move to exclusive later |
| Google Ads timing | ⬜ Pending | Wait until 10+ pages indexed |
| Content pace | ✅ Decided | ~3 pages/week, AI-drafted in Claude, implemented in Cursor |

---

## 16. Research Notes

### Australian Toad Technology
Australia has developed pheromone-based tadpole traps not yet available in the US market. Potential future product opportunity — importing/licensing or developing a US version. Not a launch priority but worth monitoring.

### Seasonal Revenue Planning
Peak season May–October. Plan for 40-50% revenue drop in Nov–Feb. Use slow months for content building (iguana pages, utility pages) and provider relationship development.
