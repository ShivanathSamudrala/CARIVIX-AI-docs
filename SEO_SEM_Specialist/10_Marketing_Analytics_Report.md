---
title: "CARIVIX AI — Marketing Analytics Report"
document_id: "SEO-10"
version: "1.0"
status: "Final"
last_updated: "2026-09-19"
author: "Shivanath Samudrala"
role: "Technical Writer"
---

# CARIVIX AI — Marketing Analytics Report

## 1. Overview

This document closes out the SEO/SEM workstream with a **consolidated marketing analytics report**, a **review of the complete digital-growth framework**, and a set of **prioritized recommendations**.

It draws on the full set of CARIVIX deliverables produced to date:

| # | Deliverable |
|---|---|
| 1 | Measurement architecture |
| 2 | SEM strategy |
| 3 | Backlink strategy |
| 4 | Content / editorial calendar |
| 5 | Digital growth measurement framework |

> These are evaluated **together as one system** rather than as separate documents.

---

## 2. Project Context

CARIVIX (`carivixai.in`) is a **voice-first data analytics and crisis intelligence platform**. Its strategy work is organized around **five intelligence domains** and **three revenue streams**, both of which are used throughout this report to keep SEO, SEM, and analytics tied back to how the business actually earns.

### 2.1 Five Intelligence Domains

| # | Domain |
|---|---|
| 1 | Business Intelligence |
| 2 | Government Intelligence |
| 3 | Economic Intelligence |
| 4 | Smart City Intelligence |
| 5 | Research Intelligence |

### 2.2 Three Revenue Streams

| # | Revenue Stream |
|---|---|
| 1 | Basic / Professional self-serve SaaS |
| 2 | Enterprise SaaS |
| 3 | Government Licensing & Consulting |

---

## 3. Review of the Complete Digital-Growth Framework

The full framework was reviewed end-to-end — analytics foundation, content and editorial strategy, SEM strategy, backlink strategy, and the digital growth measurement framework — against **three questions**:

1. Is it internally consistent?
2. Is it sequenced correctly?
3. Is it actually buildable with the resources implied?

Findings are grouped below by workstream.

### 3.1 Analytics Foundation (GA4 / GSC / GTM)

| Status | Finding |
|---|---|
| On track | The phased setup — GSC verification, GA4 property and GTM install, GSC-GA4 linking, then QA — is correctly sequenced and matches how these tools actually need to be stood up |
| On track | DPDPA 2023 consent gating is built into the tracking plan from the start rather than bolted on later, which is the right call for an India-facing platform |
| On track | Custom dimensions and key events are mapped to CARIVIX's five intelligence domains and three revenue streams, so reporting will be able to break down by both from day one |
| Gap | The framework doesn't flag GA4/GSC setup as a **hard dependency** for the dashboards and SEM tracking that come later — it should, since nothing downstream works without it |

### 3.2 Content & Editorial Strategy

| Status | Finding |
|---|---|
| On track | The 3-month, 24-post blog calendar is mapped cleanly to the five domains by month (Business & Economic, Government & Smart City, Research Intelligence & Conversion) |
| On track | Five domain landing pages and five gated resources (two guides, one whitepaper, one ROI calculator, one webinar series) give the SEM and backlink workstreams something concrete to point traffic at — this wasn't true in earlier drafts of the framework |
| Gap | No owner is assigned per content piece in the current version; this is the **single biggest risk** to the 3-month calendar slipping |

### 3.3 SEM Strategy

| Status | Finding |
|---|---|
| On track | Google Ads and LinkedIn Ads roles are split correctly by revenue stream — LinkedIn for Enterprise/Government (longer B2B cycles), Google Search for self-serve SaaS (higher intent, shorter cycle) |
| On track | The account/campaign group/ad group hierarchy and audience segmentation (in-market, custom, remarketing, Customer Match, lookalike) are Google Ads-buildable as written, not just theoretical |
| On track | The ₹3,50,000/month indicative budget split is clearly flagged as an **assumption** pending real budget confirmation — this framing should stay in the final version rather than being presented as fixed |

### 3.4 Backlink Strategy

| Status | Finding |
|---|---|
| On track | The tiered structure (journalist platforms, self-serve directories, editorial/media, institutional collaboration) is sound and every link in the current version has been verified as live and working |
| On track | Two previously-flagged sources — Analytics India Magazine's write-for-us page and Geospatial World's guest-blog archive — remain excluded from the active target list rather than silently dropped, which keeps the report honest |
| On track | The 90-day outreach plan is realistically ordered by probability of success rather than by prestige of target, which is the right prioritization for a new platform with no existing coverage |

### 3.5 Digital Growth Measurement Framework

| Status | Finding |
|---|---|
| On track | The four-pillar structure (Acquisition, Engagement, Conversion, Retention) ties cleanly to the three revenue streams and gives each buyer journey (government long-cycle vs SME self-serve) its own success definition |
| Gap | KPI ownership by workstream is defined, but a few KPIs are marked as needing future CRM integration without a target date — worth pinning down so they don't get permanently deferred |

### 3.6 Why This Review Approach Fits CARIVIX

> CARIVIX runs five intelligence domains against three distinct revenue streams with different buyer cycles (government long-cycle vs SME self-serve vs enterprise).
>
> Reviewing the workstreams **together**, rather than sign-off document by document, is what catches sequencing gaps like the GA4/GSC dependency above — the kind of issue that only shows up when analytics, content, SEM, and backlink plans are **read as one system** feeding the same five domains and three revenue lines.

---

## 4. Consolidated SEO/SEM Strategy

This section pulls together the **SEO foundation, SEM campaign architecture, paid channel strategy, and the content and backlink work** that feed organic visibility, into the current working strategy.

### 4.1 SEO Foundation & Content Programme

Keyword and search-opportunity research was completed across **GEO, AEO, and SEO** angles for all five intelligence domains, feeding into a three-month content calendar and the domain landing page set.

| Content Asset | Details |
|---|---|
| **Blog Topics** | 24 posts (8 per month) — Month 1: Business & Economic; Month 2: Government & Smart City; Month 3: Research Intelligence & Conversion |
| **Domain Landing Pages** | 5 pages — Business, Government, Smart City, Research Intelligence, and Pricing |
| **Gated Resources** | 5 — 2 guides, 1 whitepaper, 1 ROI calculator, 1 webinar series |

> Each content item carries a persona/domain mapping and a stated reason it supports the domain and revenue stream it targets, so content ties back to **acquisition rather than being produced on a generic calendar**.

### 4.2 Backlink & Off-Page Strategy

Backlink work is organized into **four partner tiers**, each with defined criteria and expected turnaround, and is now supported by a **live tracking system** rather than a static list.

| Tier | Partner Type | Examples |
|---|---|---|
| **Tier 1** | Self-serve directories | Product Hunt, G2, Crunchbase, AlternativeTo, SaaSHub, Startup India Hub |
| **Tier 2** | Editorial / media | eGov Magazine, CGII, NASSCOM Community, INDIAai directory |
| **Tier 3** | Journalist platforms | Qwoted, Featured, Source of Sources, Help a B2B Writer, #JournoRequest |
| **Tier 4** | Institutional collaboration | NDMA, IUDX, CSIR-NIScPR/AcSIR, NASSCOM, DSCI, Smart Cities India Expo |

> A companion Excel tracker holds **28 verified partners** across the four tiers, with dropdown-driven Status, Tier, Domain, and Outcome fields, an 8-stage outreach status workflow, and a formula-driven KPI summary tab.
>
> Outreach and status updates run on a **weekly cadence**, monthly for lower-priority tiers, under a **single accountable owner**.
>
> Only verified, currently-working submission routes are included — unverified or stale links (for example, dormant guest-blog programmes) are flagged rather than listed as live options.

### 4.3 SEM Campaign Architecture

The Google Ads account is structured **by revenue stream rather than by domain**, so budget and bidding decisions map directly to how each stream converts.

| Element | Structure |
|---|---|
| **Hierarchy** | Account → campaign group → ad group, split across the three revenue streams |
| **Campaign Types** | Search for high-intent domain keywords, Performance Max for reach, Remarketing for return visitors |
| **Ad Group Themes** | Set per intelligence domain |
| **Segment Rollout** | Three-phase — in-market and custom segments first, Customer Match and lookalike audiences once there is a baseline list |

### 4.4 Paid Channel Strategy — Google Ads & LinkedIn Ads

Google Ads and LinkedIn Ads are assigned **different jobs** by revenue stream and funnel stage rather than run as duplicate campaigns on both platforms.

| Revenue Stream | Primary Channel Role | Google Ads Objective | LinkedIn Ads Objective |
|---|---|---|---|
| **Self-serve SaaS** | Capture existing search intent | Capture High Intent | Content Engagement |
| **Enterprise SaaS** | Build consideration with named accounts | Build Consideration | Professional Targeting |
| **Government / Consulting** | Long-cycle authority building | Maximise Reach | Brand Authority |

> The indicative combined monthly budget is **₹3,50,000**, split across the two platforms by revenue-stream priority. This figure is an **assumption pending an approved marketing budget**, not a committed spend.
>
> LinkedIn targeting is built around job titles, seniority, and industry lists per persona; Google targeting is built around domain keyword themes and in-market segments. Worked CPC/CTR/CPL examples for both platforms sit behind the campaign structure so spend can be sanity-checked once campaigns go live.

---

## 5. Marketing Analytics Framework

This section consolidates the **tracking foundation, KPI framework, search performance monitoring, and reporting cadence** into the current analytics picture.

> This is a **framework and reporting plan** rather than a live results report — GA4/GSC data will populate it once the site is fully instrumented.

### 5.1 Tracking Foundation

The measurement stack is **GA4, Google Search Console, and Google Tag Manager**, set up in phases: GSC verification, GA4 property and GTM install, GSC–GA4 linking, then QA.

> **DPDPA 2023 consent gating** is built into the event plan so tracking does not fire before consent is captured.

| Layer | Details |
|---|---|
| **Automatic Events** | Automatically collected and enhanced-measurement events (page views, scrolls, outbound clicks, site search) form the base layer |
| **Custom Events** | 10 CARIVIX-specific custom events mapped to the five intelligence domains and three revenue streams |
| **Key Events (Conversions)** | Defined separately per revenue stream — self-serve sign-up, Enterprise MQL/SQL stages, and Government/Consulting milestone progression |

### 5.2 KPI Framework

KPIs sit on a **four-pillar model** — Acquisition, Engagement, Conversion, Retention — each tied back to the three revenue streams so a single dashboard number can be traced to a business outcome rather than read as a vanity metric.

| Pillar | What It Tracks | Example Metric |
|---|---|---|
| **Acquisition** | Organic and paid traffic quality by domain and channel | Organic sessions by domain, paid CPL |
| **Engagement** | Content and page-level interaction quality | Avg. engagement time, scroll depth, gated-resource downloads |
| **Conversion** | Movement into and through the funnel, per revenue stream | Self-serve sign-up rate, Enterprise MQL/SQL rate |
| **Retention** | Post-acquisition activity and renewal signals | Product login frequency, Government contract milestone progression |

> **Tracking approach by revenue stream:**
> - **Self-serve conversion** is tracked as a straightforward **rate**
> - **Enterprise** is tracked through **MQL/SQL stages** because the cycle is longer and multi-touch
> - **Government/Consulting** is tracked as **milestone progression** rather than a single conversion rate, since that pipeline runs on procurement timelines rather than a marketing funnel

### 5.3 Search Performance Monitoring

Google Search Console is reviewed across **five data areas** — coverage, performance, enhancements, links, and security/manual actions — on a **daily/weekly/monthly/quarterly cadence** with defined alert thresholds for sudden drops.

| Metric Category | Details |
|---|---|
| **Visibility Metrics** | Impressions, average position, and click-through rate by domain landing page |
| **Ranking-Opportunity Tracking** | Striking-distance keywords (positions 5–15) prioritized for on-page work |
| **Technical Health** | Index coverage, Core Web Vitals, and crawl errors |

### 5.4 Dashboards & Reporting Cadence

Reporting is built on **three Looker Studio dashboards** sitting on top of the GA4/GSC implementation.

| Dashboard | Purpose |
|---|---|
| **Executive Overview** | Single-page snapshot for leadership |
| **SEO & Content Performance** | Organic visibility, rankings, and content engagement |
| **Conversion & Domain Performance** | Funnel performance by revenue stream and by intelligence domain |

**Cadence:**

| Frequency | Format |
|---|---|
| Weekly | Informal pulse check |
| Monthly | Formal dashboard plus written narrative |
| Quarterly | Trend review against targets |

> This mirrors the cadence already set for GSC monitoring so the two run on the same rhythm rather than as separate schedules.

---

## 6. SEO/SEM Analytics Report — Current-State Summary

This section consolidates the SEO/SEM analytics work delivered across prior reports into a single current-state summary: **what's being tracked, how campaigns are structured, and what the benchmark numbers look like**.

> This is a **synthesis report, not a new build** — figures and structures below are carried forward from the GSC/GA4 implementation plan, the SEM campaign structure report, and the two Paid Advertising Strategy reports.

### 6.1 Tracking & Measurement Setup

| # | Item |
|---|---|
| 1 | GA4 property and GTM container installed with server-side tagging for the acquisition, waitlist, engagement, and revenue event groups |
| 2 | GSC linked to GA4 for combined organic-search and on-site behaviour reporting |
| 3 | UTM convention standardized across campaign type, source, and revenue-stream so cross-campaign comparison doesn't need manual cleanup |
| 4 | Consent gating (DPDPA 2023) applied before any tracking fires for India-based users |

### 6.2 SEM Campaign Structure

Campaigns are structured by **revenue stream first, then by funnel stage**, using a mix of Search, Performance Max, and Remarketing depending on intent level.

| Revenue Stream | Primary Campaign Type | Funnel Stage Focus |
|---|---|---|
| Basic / Professional SaaS (self-serve) | Search + Remarketing | Capture High Intent |
| Enterprise SaaS | Search + LinkedIn | Build Consideration |
| Government Licensing / Consulting | LinkedIn (Professional Targeting) | Brand Authority + Long-Cycle Nurture |

### 6.3 Budget & Benchmark Figures

> Budget figures below are the **indicative combined Google Ads + LinkedIn Ads split** (~₹3,50,000/month across both platforms) — flagged in the original strategy report as an **assumption pending confirmed marketing spend**, and that caveat still applies here.

| Metric | Google Ads (Search) | LinkedIn Ads |
|---|---|---|
| Primary use | High-intent capture, self-serve SaaS | Enterprise & government targeting |
| Indicative monthly budget | ~₹1,50,000 – ₹2,00,000 | ~₹1,50,000 – ₹2,00,000 |
| Benchmark CPC / CTR / CPL | Worked examples in Paid Advertising Strategy report | Worked examples in Paid Advertising Strategy report |

### 6.4 KPI Framework Summary

| Element | Details |
|---|---|
| **Six KPI Categories** | Traffic & visibility, engagement, SEO/domain authority, conversion/leads, revenue-stream pipeline, technical/trust health — the six KPI categories from the dashboard framework remain the current reporting structure |
| **Dashboard Views** | Three Looker Studio views — Executive Overview, SEO & Content Performance, and Conversion & Domain Performance |
| **CRM-Dependent KPIs** | A subset of pipeline and revenue KPIs still depend on future CRM integration and are marked as **not yet live** |

---

## 7. Status Review & Open Gaps

Reviewing the SEO/SEM and analytics work together surfaces a few gaps that **carry across both workstreams** rather than being specific to one report.

| # | Gap |
|---|---|
| 1 | GA4/GSC implementation is **not yet formally marked as a blocking dependency** for SEM and content reporting, even though every downstream KPI depends on it |
| 2 | **No content item on the blog calendar has an assigned owner per post** — the calendar defines what and when, not who |
| 3 | **Enterprise and Government KPIs** (MQL/SQL stages, milestone progression) still need CRM integration before they can be tracked automatically; target dates for that integration are not yet set |
| 4 | **Paid Ads budget** (₹3,50,000/month indicative) is not yet an approved figure, and the company's bank account is not yet open — both sit upstream of any real campaign launch |

---

## 8. Recommendations

Based on the framework review and the analytics consolidation above, the following are the recommended next moves, in priority order.

### 8.1 Immediate (This Cycle)

| # | Recommendation |
|---|---|
| 1 | Formally mark **GA4/GSC/GTM setup as a blocking dependency** for SEM tracking and dashboard build-out, so it can't get scheduled in parallel with work that depends on it |
| 2 | **Assign an owner to each of the 24 blog posts and 5 landing pages** in the content calendar before Month 1 publishing begins |
| 3 | **Confirm actual marketing budget** so the ₹3,50,000/month SEM split can move from assumption to committed figure |
| 4 | **Assign a single accountable owner** to the backlink outreach tracker, consistent with the weekly update cadence already defined |

### 8.2 Near-Term (Next 30–60 Days)

| # | Recommendation |
|---|---|
| 1 | Begin **Tier 1 self-serve directory submissions** (Product Hunt, G2, Crunchbase, AlternativeTo) — these carry the highest success probability and need no outreach dependency |
| 2 | **Launch the first Search campaigns** for Basic/Professional self-serve SaaS, since this funnel has the shortest cycle and will generate the earliest performance data to validate CPC/CTR/CPL assumptions |
| 3 | **Set a target date for CRM integration** so the pipeline and revenue KPIs currently marked "future" have a concrete point at which they go live |
| 4 | **Assign per-post owners** on the content calendar before Month 1 publishing begins |

### 8.3 Ongoing

| # | Recommendation |
|---|---|
| 1 | Continue the **90-day backlink outreach plan** in its current priority order, re-verifying any editorial links (Analytics India Magazine, Geospatial World) on a **quarterly basis** rather than assuming they stay excluded permanently |
| 2 | **Review the SEM budget split and campaign performance monthly** against the CPC/CTR/CPL benchmarks and adjust the Google-to-LinkedIn allocation based on which revenue stream is converting faster |
| 3 | **Review striking-distance keywords monthly** and route them into the content calendar as on-page work |
| 4 | **Set CRM integration target dates** for Enterprise and Government KPI tracking once the CRM is selected |

### 8.4 Why These Recommendations Fit CARIVIX

> The recommendations are ordered by **what unblocks the most downstream work for the least effort** — analytics setup and content ownership come first because SEM tracking, dashboards, and the publishing calendar all depend on them.
>
> This keeps CARIVIX's **five-domain, three-revenue-stream framework** moving as one coordinated build rather than several workstreams progressing at different, uncoordinated speeds.

---

## 9. Next Actions

| Workstream | First Action | Owner | Dependency |
|---|---|---|---|
| **Analytics Foundation** | Complete GA4/GSC/GTM install and mark as blocking dependency | TBD | None — can start immediately |
| **Content Calendar** | Assign per-post owners for Month 1 (Business & Economic domain) | TBD | None |
| **Backlink Outreach** | Confirm single accountable owner for the tracker and weekly cadence | TBD | Tracker already built |
| **SEM Launch** | Get budget sign-off on the ₹3,50,000/month indicative split | TBD | Company bank account must be open |
| **KPI / CRM** | Select CRM and set integration target dates for Enterprise/Government KPIs | TBD | CRM selection |

---

## Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-09-19| Shivanath Samudrala | Initial version — marketing analytics report and consolidated SEO/SEM strategy |
