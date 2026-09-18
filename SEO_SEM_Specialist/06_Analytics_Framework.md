---
title: "CARIVIX AI — Analytics Framework"
document_id: "SEO-06"
version: "1.0"
status: "Final"
last_updated: "2026-09-19"
author: "Shivanath Samudrala"
role: "Technical Writer"
---

# CARIVIX AI — Analytics Framework

## Document Structure

This document defines the complete analytics framework for CARIVIX AI across eight parts:

| Part | Topic |
|---|---|
| 1 | GSC & GA4 Implementation Plan and Tracking Requirements |
| 2 | Analytics Architecture & KPI Framework |
| 3 | Website Analytics Strategy & Campaign Tracking Metrics |
| 4 | GA4 Event Tracking Plan & Conversion Goals |
| 5 | GA Event Structure, User Acquisition Metrics & Engagement Metrics |
| 6 | GSC Monitoring Plan, Search Performance Metrics & Reporting Structure |
| 7 | Website Analytics Events, Page Engagement Metrics & Conversion Events |
| 8 | GSC Monitoring Framework, Search-Performance KPIs & Reporting Format |

---

# Part 1 — GSC & GA4 Implementation Plan and Tracking Requirements

## 1.1 Executive Summary

This part addresses two specific deliverables: a **structured implementation plan** for Google Search Console and GA4, and a **comprehensive definition of CARIVIX's tracking requirements**.

> Every procedure outlined below has been cross-verified against Google's official Search Console and Analytics Help resources, alongside current 2026 industry implementation standards. To account for Google's frequent interface updates, these steps focus on **stable architectural elements** such as menu hierarchies, permission levels, and verification protocols — ensuring the logic remains sound even if the UI shifts.

## 1.2 Four-Phase Build Overview

The implementation follows a four-phase build:

1. Verify the site in Search Console
2. Create and install the GA4 property
3. Link the two together
4. Verify everything is actually collecting data correctly before relying on it

## 1.3 Phase 1 — Google Search Console Setup

### Step 1: Choose the property type

Search Console offers two property types — the choice affects which verification methods are available:

| Property Type | Coverage | Verification Method |
|---|---|---|
| **Domain property** (recommended for CARIVIX) | All protocols and subdomains: http, https, www, non-www, and any subdomain under one property | DNS (TXT record) only |
| **URL-prefix property** | Only the exact URL prefix entered (e.g., `https://www.carivixai.in`) | HTML tag, HTML file upload, Google Analytics, Google Tag Manager, or DNS |

> **Recommendation:** Set up a **Domain property** for `carivixai.in`. It gives complete coverage in one place instead of separate properties for http/https/www variants, and DNS verification — while it needs registrar access — is the most stable method over time, since it isn't affected by later template or plugin changes on the site.

### Step 2: Verify ownership

1. Go to Google Search Console and add the property using the `carivixai.in` domain
2. Google will provide a **DNS TXT record** (a name/value pair). Log in to the domain registrar's DNS settings, add a new TXT record at the root domain with the exact value provided, and save
3. Click **Verify** in Search Console. DNS changes typically propagate within 10–30 minutes, though it can take longer depending on the registrar — allow up to 48 hours before troubleshooting
4. If a **URL-prefix property** is used instead (for example, if DNS access isn't available yet), the fastest method is the **HTML tag**: paste the provided meta tag into the `<head>` section of the homepage — ideally through a global, version-controlled template component rather than a page that could be overwritten. A theme update removing the tag is the most common cause of properties losing verified status later

### Step 3: Submit the sitemap

1. In Search Console, go to **Sitemaps** in the left-hand menu
2. Enter the sitemap URL (typically `/sitemap.xml`) and submit
3. If no sitemap exists yet, generate one via the CMS/SEO plugin in use, or a static `sitemap.xml` file

### Step 4: Request initial indexing

Use **URL Inspection** in Search Console, paste the homepage URL, and click **Request Indexing** to prompt an initial crawl rather than waiting for organic discovery.

> If Search Console still shows no data after a week, the most common cause is an **incomplete or broken verification** (tag removed, DNS record wrong scope) — re-check verification status before assuming it's a crawling issue.

## 1.4 Phase 2 — Google Analytics 4 (GA4) Property Setup

### Step 1: Create the account and property

1. Go to `analytics.google.com` and sign in with the Google account that will administer CARIVIX's analytics long-term (not a personal account)
2. Create an **Account** (organisation-level container) named **CARIVIX AI**, then create a **Property** within it named **CARIVIX — Website**
3. Set the reporting **time zone to India Standard Time** and **currency to INR** — this affects how session boundaries and revenue figures are calculated and displayed
4. Select business details and objectives; for CARIVIX, the closest fit is **"Generate leads"** combined with **"Examine user behaviour"** — this shapes the default report templates Google suggests. This can be adjusted later without losing data

### Step 2: Create the data stream

1. Under the new property, go to **Data Streams → Add stream → Web**, and enter the site URL (`https://carivixai.in`) and a stream name
2. This generates the **Measurement ID** (format: `G-XXXXXXXXXX`) — this ID is required for every installation method

### Step 3: Install the tracking code

| Method | Best For | How |
|---|---|---|
| **Google Tag Manager** (recommended) | Ongoing flexibility — marketing can add/adjust tracking without a developer for every change | Install the GTM container snippet once (in `<head>` and after opening `<body>`), then configure the GA4 Configuration tag and all future event tags inside GTM's interface |
| **CMS plugin** (e.g., WordPress + a GA4/SEO plugin) | Fastest setup if the site runs on a supported CMS | Enter the Measurement ID directly into the plugin's settings field |
| **Manual gtag.js snippet** | Fully custom-coded sites, developer-controlled | Paste the Google tag snippet directly into the `<head>` of every page template |

> **Recommendation for CARIVIX:** Google Tag Manager. Because tracking requirements will include multiple custom events tied to five different product domains and three buyer types, GTM avoids repeated developer requests every time a new event needs tracking — events and triggers are managed by the marketing/SEO team directly inside GTM once it's installed.

### Step 4: Confirm data is flowing

1. Browse the live site, then check the **Realtime report** in GA4 — activity should appear within a few minutes
2. If using GTM, use GTM's built-in **Preview mode** before publishing any container change, to confirm each tag fires correctly against a live or staging page prior to going live
3. Allow up to 30 minutes for data to begin appearing in standard reports after initial setup

## 1.5 Phase 3 — Link Google Search Console to GA4

This step surfaces organic search queries, impressions, and average position directly inside GA4 reports, alongside on-site behaviour.

> **Prerequisites (verified against Google's own documentation):** The same Google account must have at least **Editor access** on the GA4 property and be a **verified owner** in Search Console, and ideally both should sit under the same Google account/organisation to avoid permission mismatches.

1. In GA4, go to **Admin → Property column → Product Links → Search Console Links**
2. Click **Link**, then **Choose account**, and select the verified `carivixai.in` Search Console property
3. Click **Confirm**, then **Next**
4. Select the web data stream created in Phase 2 to associate with this link
5. Review and click **Submit** — a "Link Created" confirmation should appear
6. Search Console data typically appears in GA4's Search Console reports (under **Reports → Acquisition**) within **24–48 hours** of linking, not instantly

> A single Search Console property can only be linked to **one GA4 property**, and a link **cannot be edited once created** — it must be deleted and recreated if a change is needed. Keep this in mind if CARIVIX later restructures its GA4 property setup.

## 1.6 Phase 4 — Verification and Quality Assurance

- Use GA4's **DebugView** (Admin → DebugView) alongside a browser debug extension to confirm custom events fire with the correct parameters before relying on any tracking requirement
- **Exclude internal traffic** (team members' own visits) via GA4's internal traffic rules, so team browsing doesn't distort real visitor data — do this in the first week, not after data has already been polluted
- **Increase data retention** from the 2-month default to the maximum **14 months** (Admin → Data Settings → Data Retention), since the default is too short for meaningful year-over-year SEO/SEM analysis
- Re-check the Search Console link and GA4 Realtime report **weekly for the first month**, since this is the period most implementation errors surface (a removed verification tag, a GTM container not published, an incorrect Measurement ID)

## 1.7 Phase 5 — Implementation Timeline

| S.no | Action |
|---|---|
| 1 | Create GA4 account/property/data stream; note the Measurement ID. Add Search Console property and begin DNS verification |
| 2 | Install Google Tag Manager container on the site; configure the base GA4 Configuration tag in GTM |
| 3 | Confirm DNS propagation and complete Search Console verification; submit the XML sitemap; request indexing on the homepage |
| 4 | Confirm GA4 Realtime data is flowing; set up internal traffic exclusion and extend data retention to 14 months |
| 5 | Link Search Console to GA4 following Phase 3; confirm "Link Created" status |
| 6 | Configure tracking requirements (events, key events, custom dimensions) inside GTM/GA4 |
| 7 | Verify Search Console data has appeared in GA4 Acquisition reports (allow up to 48 hours from linking); QA all custom events via DebugView |
| 8 | Weekly check for the first month, then monthly: confirm tracking integrity, review Search Console coverage/index errors, review key event volumes |

## 1.8 Tracking Requirements

We don't want to just track empty pageviews. We want to measure the actions that actually matter to CARIVIX's business goals.

### 1.8.1 How GA4 Events Work

In GA4, every single thing a user does is called an **event**. Some are tracked automatically, some you can toggle on with a switch, and some we have to custom-build.

### 1.8.2 Turn on Enhanced Measurement

Go to **Data Stream settings** and flip the switch for **Enhanced Measurement**. This tracks great materials out-of-the-box with no extra code:

- Scroll tracking (when users read 90% of a page)
- Outbound clicks (when they click links to external sites)
- Site search (if we have a search bar)
- File downloads (super important for our whitepapers and PDF reports)
- Video engagement (if we host demo videos on the site)

### 1.8.3 Custom Events

We've mapped these out to follow our buyers — from just looking around, to evaluating our tools, to finally converting across our three revenue streams (SaaS, Gov Licensing, Consulting):

| Event Name | Type | When does it happen? |
|---|---|---|
| `domain_page_view` | Custom | A visitor checks out one of our five core domain landing pages |
| `pricing_view` | Custom | A visitor views the SaaS pricing/plans page |
| `case_study_view` | Custom | A visitor opens a case study or our Tier 1 data report |
| `file_download` | Automatic (Enhanced) | A PDF (whitepaper, case study) is downloaded |
| `sign_up` | Recommended | A visitor creates a self-serve SaaS trial or basic account |
| `generate_lead` | Recommended | A visitor requests a demo or contacts sales for Business Intelligence |
| `government_enquiry` | Custom | Someone submits the specific Government Licensing form |
| `consulting_enquiry` | Custom | Someone asks about Consulting Services |
| `voice_assistant_demo_play` | Custom | A visitor interacts with the Voice Intelligence Assistant demo |

> **Note:** It's important to use the **exact names** for the 'Recommended' events above so GA4 builds the right default reports for us.

### 1.8.4 Choosing our Key Events (Conversions)

We shouldn't mark everything as a conversion, otherwise the data gets messy. Here are the events we should officially toggle on as **Key Events**:

- `generate_lead` (SaaS business-tier demo requests)
- `sign_up` (Self-serve account creations)
- `government_enquiry` (Gov licensing pipeline — super important to watch separately)
- `consulting_enquiry` (Consulting pipeline)

> We'll leave things like downloads and page views as regular events to track engagement.

### 1.8.5 Adding Custom Details (Dimensions)

To make our reports really powerful, we need to attach extra info to our events inside the GA4 **Custom Definitions** menu:

| Dimension | Purpose |
|---|---|
| `intelligence_domain` | Helps us see which of our 5 domains (Business, Gov, Economic, etc.) is driving traffic and form fills |
| `buyer_segment` | Attaches the buyer type (SaaS, Government, Consulting) to our lead events |
| `content_asset_name` | Tells us exactly which whitepaper or case study someone downloaded |

### 1.8.6 Tagging our Links (UTMs)

Whenever we share links around the web (ads, guest posts, directory listings), we need to use a consistent UTM tag structure so we know exactly where the traffic came from.

- **Source** (e.g., `producthunt`, `google`, `inc42`)
- **Medium** (e.g., `cpc`, `guestpost`, `social`)
- **Campaign** (e.g., `tier1_data_report_launch`)

> **Pro Tip:** Keep a shared spreadsheet of every link created. If someone types 'Inc42' and someone else types 'inc42', GA4 will treat them as two totally different sources.

### 1.8.7 Privacy and Data Protection (India DPDPA Context)

Because CARIVIX deals with business and government data under India's Digital Personal Data Protection Act (DPDPA), we need to be smart about privacy from day one:

- Set up a proper **cookie consent banner** and use **Google's Consent Mode** in GTM so we respect what users opt into
- **Never collect plain-text personal info** (like names, emails, or phone numbers) in GA4 events. It breaks Google's rules and creates compliance headaches. If we need to track users, we should use anonymous, hashed IDs

## 1.9 Quick Checklist

| Task | How to check it's done |
|---|---|
| GSC Domain verified | "Verified" badge shows in Search Console |
| Sitemap submitted | Shows "Success" status (not "Couldn't fetch") |
| GA4 stream created | Measurement ID is generated |
| GTM installed | Preview mode works on your live pages |
| GA4 tag live | Realtime report shows active visitors |
| GSC linked to GA4 | "Link Created" message; data appears within 48h |
| Internal traffic hidden | Our own team's visits no longer show in Realtime |
| Data retention updated | Setting shows 14 months |
| Custom events tested | Firing nicely inside the GA4 DebugView |
| Consent mode active | GA4 respects the banner choices in DebugView |

---

# Part 2 — Analytics Architecture & KPI Framework

## 2.1 Executive Summary

This part outlines the strategic architecture for deploying a **centralized web analytics dashboard** for `carivixai.in`. The objective is to transition from fragmented data siloes (GA4 and Google Search Console) into a unified, single-pane-of-glass intelligence hub.

> By mapping precise Key Performance Indicators (KPIs) to business objectives, this framework ensures that marketing spend and organic search efforts directly correlate with **lead generation and product adoption**.

## 2.2 Dashboard Strategy & Information Architecture

### 2.2.1 Strategic Definition

A website analytics dashboard is **not a data dump** — it is a **diagnostic narrative**. It consolidates raw telemetry — such as visitor velocity, click-through rates, organic ranking flux, and lead pipeline volume — into actionable visualizations.

> Instead of manually querying GA4 or Search Console, stakeholders receive immediate answers regarding traffic health and conversion efficiency in **under 30 seconds**.

### 2.2.2 Information Architecture

To prevent cognitive overload, the dashboard must be restricted to **four specialized operational blocks**, tailored to answer core business questions:

| Block | Question Answered | Purpose |
|---|---|---|
| **Overview (Volume & Velocity)** | How many users are visiting, and what is the growth trajectory? | Tracks baseline health |
| **Acquisition (Channel Efficacy)** | Where is the traffic originating? | Segments traffic into organic search, direct access, social media, referral, and paid advertising to determine which channels drive the most qualified users |
| **Behavioral Analysis (Engagement Depth)** | What is the on-page experience? | Measures which pages retain attention, average session depth, and immediate exit points |
| **Pipeline & Conversion (Business Value)** | Are users taking high-value actions? | Tracks core milestones, such as "Request Demo," "Get Started" clicks, or direct email inquiries |

### 2.2.3 UI/UX Layout & Visual Hierarchy

The layout relies on a **strict top-down structure**, ensuring the most critical data is processed first:

| Tier | Content | Purpose |
|---|---|---|
| **Top Tier (Executive Summary)** | 4–5 "Big Number" scorecards (Total Sessions, Conversion Rate, Total Leads) | Immediate health check |
| **Middle Tier (Diagnostic Trends)** | Line charts plotting the last 30–90 days | Visualizing trends is critical for spotting seasonal anomalies or the impact of recent marketing campaigns |
| **Bottom Tier (Granular Detail)** | Sortable data tables isolating the Top 10 performing pages, high-yielding search queries, and specific channel breakdowns | Detailed analysis |

> **Design Rules:** The dashboard should be contained within a **single viewport** (no endless scrolling). Color must be used as a **semantic indicator** (e.g., green for pacing above target, red for pacing below), **never for mere decoration**.

### 2.2.4 Data Typology

| Type | Description |
|---|---|
| **Absolute Aggregates** | Top-line metrics (Total Users, Total Sessions) |
| **Trend Vectors** | Historical mapping of aggregates to indicate growth or decay |
| **Efficiency Ratios (Percentages)** | Metrics like Conversion Rate and Bounce Rate, which measure the quality of traffic, not just the volume |
| **Dimensional Breakdowns** | Data segmented by Device (Mobile vs. Desktop), Geography, and Traffic Source |

## 2.3 KPI Framework & Performance Metric Definitions

Before assigning data points to the dashboard, it is critical to distinguish between a **Key Performance Indicator (KPI)** and a **Performance Metric**.

| Concept | Definition |
|---|---|
| **Performance Metrics (The "Play-by-Play")** | Quantifiable measurements used to track the tactical, day-to-day activities and processes within a business. They are diagnostic data points that provide granular insight into specific friction points or channel behaviors |
| **Key Performance Indicators (The "Scoreboard")** | A specific, high-level metric that is directly tied to a core strategic business objective. KPIs measure the ultimate outcome, telling stakeholders whether the overarching business strategy is actually succeeding |

> **The Strategic Relationship:** Every KPI is technically a metric, but **not every metric qualifies as a KPI**. **KPIs set the destination, while metrics monitor the engine.**

### Data Point Classification Table

| Data Point | Classification | Strategic Definition | Dashboard Location | Operational Application | Data Format |
|---|---|---|---|---|---|
| Total Users / Sessions | Metric | The aggregate volume of unique visitors and total browsing sessions | Overview Tier | Acts as the foundational denominator | Count (MoM/YoY) |
| Traffic by Source | Metric | The segmentation of inbound traffic by channel | Acquisition Tier | Dictates budget and resource allocation | Percentage Split |
| Bounce Rate / Engagement Rate | Metric | The percentage of sessions resulting in zero interaction | Behavioral Tier | High bounce rates on core landing pages signal a mismatch | Percentage |
| Average Engagement Time | Metric | The active time a user spends consuming content on the site | Behavioral Tier | Low engagement times on high-value pages indicate friction | Time (MM:SS) |
| Organic Impressions & Rank | Metric | The frequency of URL visibility in Google search results | SEO Detail Tier | A leading indicator of SEO health | Count + Position |
| Conversion Rate (CVR) | KPI | The percentage of total sessions that culminate in a defined business goal | Pipeline Tier | The ultimate efficiency indicator | Percentage |
| Goal Completions (Leads) | KPI | Raw counts of high-value actions | Pipeline Tier | Quantifies the exact pipeline volume generated | Absolute Count |

---

# Part 3 — Website Analytics Strategy & Campaign Tracking Metrics

## 3.1 Executive Summary

This part defines the complete **Website Analytics Strategy & Campaign Tracking Protocol** for CARIVIX AI.

> Website analytics is the process of collecting, measuring, and analyzing data about how people interact with a website. It tracks user behavior, traffic sources, and performance metrics to help businesses optimize their online presence.

This protocol bridges raw web telemetry with strategic business outcomes across our **5 Intelligence Domains** (Business, Government, Economic, Smart City, Research) and **3 Revenue Streams** (SaaS Subscriptions, Government Licensing, Strategic Consulting).

> By standardizing our attribution models, event tracking, UTM taxonomy, and data governance, this framework ensures every rupee spent and every hour invested in growth directly correlates with **verified pipeline generation**.

## 3.2 Introduction — What is Website Analytics for CARIVIX AI?

Website analytics is the systematic collection, measurement, and analysis of data regarding how visitors interact with `carivixai.in/com`.

> Instead of viewing web traffic as a single number, analytics tracks user behavior, traffic channels, and conversion milestones to help CARIVIX optimize its online presence and accelerate buyer journeys.

### What the Platform Tracks

| Category | Details |
|---|---|
| **User Demographics** | Geographic location (e.g., specific Indian states/metros), age, gender, and preferred language |
| **Technology Profile** | Device types (Desktop vs. Mobile), operating systems, and browsers used by enterprise and government decision-makers |
| **Traffic Sources** | Inbound acquisition channels including Organic Search (SEO/AEO), Paid Ads (SEM), Social Media (LinkedIn), or Direct links |
| **Visitor Behavior** | Specific pages viewed, time spent reading whitepapers, scroll depth on solution pages, and immediate exit (bounce) rates |
| **User Actions (Key Events)** | Form submissions, button clicks, demo requests, PDF whitepaper downloads, and voice assistant interactions |

## 3.3 Website Analytics Strategy

### 3.3.1 The 4 Core Questions Analytics Must Answer

Every report, dashboard, and tracking configuration in CARIVIX serves to answer four fundamental business questions:

| # | Question | Purpose |
|---|---|---|
| 1 | **Domain Interest** | Which of the 5 intelligence domains — Business, Government, Economic, Smart City, or Research — is generating genuine user interest versus casual clicks? |
| 2 | **Channel Attribution** | Which specific marketing channel actually produced a verified lead, account sign-up, or government enquiry? |
| 3 | **Revenue Stream Performance** | Are our SEO, backlink, and content campaigns converting separately for SaaS Subscriptions, Government Licensing, and Consulting Services? |
| 4 | **Data Integrity** | Is the underlying telemetry clean, accurate, and trustworthy enough for executive decision-making? |

### 3.3.2 GA4 Attribution Strategy

Attribution determines how credit for a conversion is distributed across a user's multi-touch journey.

**Key GA4 Attribution Rules:**

| Rule | Description |
|---|---|
| **Data-Driven Attribution (DDA)** | GA4's default model uses machine learning to split conversion credit across up to 50 touchpoints, rather than giving 100% credit to the final click |
| **Volume Thresholds** | DDA requires approximately 400 key event conversions and 20,000 total conversions within a lookback window to operate active machine learning. If volume drops below this, GA4 silently falls back to a **Last-Click** model without displaying a warning |
| **Per-Event Configuration** | Each key event possesses its own independent attribution model and lookback window under **Advertising → Conversion Management** |
| **Lookback Windows** | The default 30-day first-visit lookback window is insufficient for long-cycle enterprise and government prospects |

**Recommended Attribution Setup:**

| Key Event (Conversion) | Target Revenue Stream | Attribution Model | Lookback Window | Strategic Justification |
|---|---|---|---|---|
| `generate_lead` / `sign_up` | SaaS Plans (Basic/Pro) | Data-Driven (Fallback: Last-Click) | 30–60 Days | Faster, transactional decisions with shorter evaluation cycles |
| `government_enquiry` | Government Licensing | Data-Driven (Fallback: Last-Click) | 90 Days (Max) | Extended evaluation and multi-department approval before submission |
| `consulting_enquiry` | Strategic Advisory | Data-Driven (Fallback: Last-Click) | 90 Days (Max) | High-ticket consideration phase requiring deep internal alignment |

> **Channel Credit Setting:** Set to **"Paid and organic"** across the property so organic content, PR, and SEO receive fair credit alongside paid search ads.

### 3.3.3 Required Report Segmentation

Never evaluate top-line site metrics in isolation. Every report must be sliced across four specific dimensions:

| # | Dimension | Description |
|---|---|---|
| 1 | **By Intelligence Domain** | Segment by Business, Government, Economic, Smart City, and Research Intelligence pages |
| 2 | **By Buyer Segment / Revenue Stream** | Separate traffic intended for SaaS, Government Licensing, and Consulting offerings due to vastly different deal sizes |
| 3 | **By Acquisition Channel** | Segment into Organic Search, Direct, Referrals (directories/backlinks), Paid Search (SEM), and Organic Social |
| 4 | **By Visitor Type** | Compare New vs. Returning Visitors (Government and Enterprise buyers frequently visit multiple times before converting) |

### 3.3.4 Data Governance & Quality Control

To maintain clean, unpolluted analytics over time:

| # | Control |
|---|---|
| 1 | **Single Ownership** — One designated GA4 Administrator must approve all tracking modifications (new custom events, renamed dimensions, attribution tweaks) |
| 2 | **Central Change Log** — Maintain a documented log detailing the date, description, and author of every tracking modification |
| 3 | **Internal Traffic Exclusion** — Filter out team and internal IP addresses, reviewed on a quarterly basis |
| 4 | **Standardized Source Naming** — Enforce strict lowercase naming conventions (e.g., `inc42` instead of `Inc42`) to prevent data splitting across separate rows |
| 5 | **Quarterly QA Audits** — Perform quarterly checks in GA4 DebugView to verify event firing, Search Console linking, and attribution stability |

### 3.3.5 India Privacy Context & Data Protection (DPDPA)

| # | Control |
|---|---|
| 1 | **Google Consent Mode:** Enabled by default. No analytics scripts or event tags trigger prior to explicit user consent on the banner |
| 2 | **Prohibition:** No plain-text Personally Identifiable Information (names, phone numbers, raw email addresses) is ever transmitted to GA4 |
| 3 | **Data Retention:** Configured to GA4's maximum retention limit of **14 months** to support year-over-year growth reporting |

### 3.3.6 Anomaly Response Protocols

| Trigger Event | Immediate Action Required |
|---|---|
| Domain key events drop >20% in a week | Audit GA4 DebugView immediately for a broken tracking tag before assuming market demand dropped |
| Search Console rankings drop sharply | Perform live search checks to distinguish between technical indexing issues and Google core algorithm updates |
| Cost per key event runs >1.5x target budget | Pause or adjust the specific SEM campaign immediately; do not wait for the monthly performance review |
| DDA status reverts to Last-Click | Log the shift in the Change Log to explain resulting attribution variance across marketing channels |

### 3.3.7 Strategic Maintenance & CRM Integration

| Frequency | Action |
|---|---|
| **Monthly** | Verify that active reporting dashboards still resolve the 4 core business questions |
| **Quarterly** | Re-evaluate attribution lookback windows as conversion volume scales; archive unassigned custom dimensions |
| **CRM Connection** | Once the CRM is integrated, link web enquiries directly to closed-won revenue outcomes to unlock full ROI measurement |

## 3.4 Campaign Tracking Framework & UTM Governance

A **campaign** is defined as any bounded marketing push with a distinct start and end date, measured independently from baseline web traffic.

### 3.4.1 Strict UTM Parameter Rules

UTM parameters must follow a standardized, locked taxonomy to prevent fragmented reporting.

**Example URL:**

```
https://carivixai.in/solutions/smart-city-intelligence?utm_source=linkedin&utm_medium=cpc&utm_campaign=smartcity_licensing_trafficreport_aug26&utm_content=v1_map_visual
```

| UTM Parameter | Allowed Values for CARIVIX | Enforced Governance Rule |
|---|---|---|
| `utm_source` | `producthunt`, `g2`, `inc42`, `linkedin`, `google` | Exact platform name in all lowercase. One single spelling per source |
| `utm_medium` | `directory`, `guestpost`, `cpc`, `social`, `referral`, `email`, `pr` | Selected strictly from this pre-approved list |
| `utm_campaign` | Format: `domain_segment_initiative_month` | Embeds the target domain and revenue stream directly into the campaign tag |
| `utm_content` | `v1_banner`, `v2_textlink`, `pdf_download` | Used exclusively when testing multiple creative variants within the same campaign |

### 3.4.2 Primary Metrics Mapped by Campaign Type

| Campaign Type | Primary Success Metric | Secondary Metrics | Measurement Note |
|---|---|---|---|
| **SEO / Content Push** | Organic Sessions to target URLs | Search Console Clicks, Impressions, Keyword Rank | Evaluate over a 4–6 week window; organic indexing takes time |
| **Paid Search (SEM)** | Cost per Key Event (by Segment) | Click-Through Rate (CTR), Cost Per Click (CPC), Key Events | Use a 30–60 day lookback window for SaaS event evaluation |
| **Backlink / Directory** | New Referring Domains | Referral Sessions, Key Events generated | Measure at Day-1, Week-1, and Month-1 (referral traffic spikes then plateaus) |
| **Digital PR / Media** | Referring Domains + Branded Search Lift | Referral Sessions, Secondary Enquiries | PR builds brand equity; measure overall search volume lift alongside direct links |
| **Content Asset Launch** | Asset Downloads + Case Study Views | Assisted Conversions, Referring Citation Links | Monitor over 90+ days as research assets accumulate citations over time |
| **Product Hunt Launch** | Launch-Day Sessions & Sign-ups | Product Hunt Ranking, Day-7 Referral Retention | Compare acquisition spikes directly against pre-launch marketing effort |

### 3.4.3 The 3-Point Measurement Protocol

Every campaign must be evaluated across three chronological checkpoints:

| # | Phase | Action |
|---|---|---|
| 1 | **Baseline Phase** | Calculate the 2–4 week pre-launch traffic average to isolate incremental impact |
| 2 | **Launch Window** | Monitor daily for high-intensity launches (e.g., Product Hunt, PR drop) and weekly for long-term campaigns (e.g., SEO content pushes) |
| 3 | **Post-Launch Phase (30–90 Days)** | Measure long-term retention to verify if campaign traffic held, faded, or continued growing passively |

### 3.4.4 Cross-Campaign Evaluation Standard

To evaluate different marketing initiatives against one another objectively, use the following standardized comparison criteria:

| # | Criterion | Purpose |
|---|---|---|
| 1 | **Cost per Key Event** | Primary benchmark for all paid acquisition channels |
| 2 | **Key Events per Hour of Effort** | Benchmark for non-paid channels (Organic SEO, PR, Directories) to account for team labor costs |
| 3 | **Referring Domains Acquired** | The universal currency for evaluating all link-building activities |
| 4 | **Time-to-Impact** | Total days elapsed from campaign launch until the first key event is registered |

### 3.4.5 Standardized One-Page Campaign Log Template

Every marketing initiative must record an entry using this structure:

```
Campaign Name: government_licensing_databacklink_aug26
Target Domain: Government Intelligence | Revenue Stream: Government Licensing
Campaign Type: Digital PR / Data Report Launch
Pre-Launch Baseline: 120 weekly organic sessions / 2 government enquiries

Launch Results:
Day 1: 450 sessions, 12 downloads
Day 30: 1,200 sessions, 6 government enquiries, 8 new DR40+ referring links
Day 90: 2,100 cumulative sessions, 14 government enquiries

Financial Cost: ₹0 direct spend
Time Investment: 18 hours total (Data generation + Outreach)
Efficiency Metric: 0.77 Key Events per Hour of Effort
Final Verdict: REPEAT — High-performing data PR template. Replicate for Smart Cities.
```

## 3.5 Operational Implementation Checklist

| Item / Deliverable | Strategic Action | Responsible Owner |
|---|---|---|
| Attribution Configuration | Configure per-event attribution models and 90-day lookback windows in GA4 | GA4 Administrator |
| Segmentation Standards | Distribute domain and buyer segment reporting dimensions to growth team | GA4 Administrator |
| Analytics Change Log | Establish the central tracking change log repository | GA4 Administrator |
| UTM Taxonomy Guide | Publish locked UTM parameters as the team's single source of truth | SEO/SEM Specialist |
| Campaign Log System | Mandate the One-Page Campaign Log for all upcoming growth pushes | SEO/SEM Specialist |
| Quarterly Audit Schedule | Calendar recurring 90-day audits for data quality and consent compliance | GA4 Administrator |

---

# Part 4 — GA4 Event Tracking Plan & Conversion Goals

## 4.1 Executive Summary

>  **Note:** The source document is truncated here — Part 4 (and Parts 5–8 listed in the document structure above) were not included in the material provided. This section, and everything after it, is pending content from the source file.

*This part establishes the official...*

---

## Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-09-19 | Shivanath Samudrala | Initial version — analytics framework, Parts 1–3 complete; Parts 4–8 pending source content |
