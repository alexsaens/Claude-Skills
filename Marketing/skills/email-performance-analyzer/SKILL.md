```yaml
name: email-performance-analyzer
description: >
  Analyze email marketing performance data for any brand using ESP export reports and marketing calendars.  Use this skill whenever a user wants to analyze email campaign results, identify winners and losers,  benchmark performance, generate monthly or weekly email reports, or get strategic or tactical insights  from email data. Trigger for any request involving email metrics, email reporting, campaign performance  review, open rates, click rates, revenue per email, deliverability, or email program health assessments.  Also trigger when the user mentions "email report", "ESP data", "Klaviyo report", "SFMC report",  "Bloomreach report", "email calendar", "campaign analysis", or "email benchmarks" — even if they  don't use the word "skill."
```

# Email Performance Analyzer

A skill for analyzing email marketing performance data, producing strategic monthly reports and tactical
weekly reports for any brand and ESP platform.

---

## Overview

This skill supports two report modes:

| Mode | Audience | Cadence | Focus |
| --- | --- | --- | --- |
| `MONTHLY` | Senior / CMO / Director level | Monthly | Holistic brand health, trends, strategic recommendations |
| `WEEKLY` | Email manager / coordinator | Weekly | Campaign-by-campaign breakdown, operational wins/flags, quick actions |

Both modes use the same data inputs and analysis framework — they differ in depth, tone, and emphasis.

---

## Step 1: Session Setup (Always Run First)

Before analyzing any data, ask the user these setup questions. Ask them all at once, not one at a time.

```
1. What is the brand name and what industry/vertical are they in?
   (e.g. "Miraclesuit — women's swimwear, apparel retail")

2. What report mode do you need?
   - MONTHLY — strategic overview for senior stakeholders
   - WEEKLY — tactical operational report for the email team

3. Do you have a historical baseline for this brand?
   - YES → ask them to paste or upload it (see Baseline Format below)
   - NO → Claude will use period-over-period comparison and industry benchmarks

4. Do you have Year-over-Year (YoY) data for the same period last year?
   - YES → ask them to provide the prior year ESP export for the same month/week
   - NO → Claude will note this and flag where YoY context would strengthen the analysis
   Note: For seasonal brands (swimwear, apparel, retail, travel), YoY is strongly preferred
   over month-over-month — flag this if the user skips it.

5. What time period does this report cover?
   (e.g. "February 2026" or "Week of March 3–7, 2026")

6. Please provide your data:
   - ESP performance report — current period (CSV export or pasted data)
   - ESP performance report — prior year same period (if available, see Q4 above)
   - Marketing calendar for the period (Excel, pasted rows, or key fields)
   If you only have some of these, that's OK — note what's missing and Claude will
   adjust the analysis accordingly.
```

---

## Step 2: Data Ingestion & Parsing

### ESP Report Columns (Standard Mapping)

The skill maps incoming ESP data to these normalized field names regardless of platform:

| Normalized Field | ESP Column Examples |
| --- | --- |
| `campaign_name` | Campaign Name, Name, Message Name |
| `list_segment` | List, Segment, Audience |
| `message_type` | Message Type, Campaign Type, Email Type |
| `channel` | Channel |
| `send_date` | Send Date, Sent Date, Date |
| `sends` | Sends, Total Sends, Messages Sent |
| `delivered` | Delivered |
| `delivered_rate` | Delivered Rate, Deliverability Rate |
| `opens` | Open, Opens, Total Opens |
| `open_rate` | Open Rate |
| `open_non_mpp` | Open (Non-MPP) — use this as primary open metric when available |
| `open_rate_non_mpp` | Open (Non-MPP) Rate — preferred over MPP-inflated open rate |
| `clicks` | Clicks, Total Clicks |
| `click_rate` | Click Rate, CTR |
| `unique_clicks` | Unique Clicks |
| `unique_click_rate` | Unique Clicks Rate |
| `ctor` | CTOR, Click to Open Rate |
| `bounced` | Bounced/Failed, Bounces |
| `bounce_rate` | Bounced/Failed Rate, Bounce Rate |
| `unsubscribed` | Unsubscribed, Unsubs |
| `unsub_rate` | Unsubscribed Rate |
| `revenue` | Revenue, Total Revenue |
| `conversions` | Conversion, Conversions |
| `conversion_rate` | Conversion Rate |
| `aov` | AOV, Average Order Value |
| `rpm` | $/1000msg, Revenue per 1000, RPM |
| `visits` | Visits, Sessions |

**MPP Note:** Apple Mail Privacy Protection inflates open rates. Always prefer `open_non_mpp` and `open_rate_non_mpp` when available. Flag to the user if only MPP-inclusive opens are present.

### Marketing Calendar Parsing

The marketing calendar is a planning document, not a structured data file. It will vary by brand. Extract only these fields — ignore workflow/approval rows, image URLs, and asset links:

| Field to Extract | Where to Find It in Calendar |
| --- | --- |
| Send date | Column headers (dates) or SEND TIME row |
| Campaign concept/theme | CONCEPT row or equivalent |
| Segment | SEGMENT row |
| Subject line (final) | AGENCY SUBJECT LINE rows or equivalent |
| Preheader text | PRE-HEADER TEXT rows |
| Offer/promo code | COUPON CODE, PROMO CODE rows |
| Email type | Infer from concept: Promotional, Trend, Sale, Brand, Newsletter |
| SMS companion | SMS row (TRUE/FALSE) |
| Performance rows | OPEN RATE, CLICK RATE, CTOR, CONVERSION RATE, REVENUE, AOV rows at bottom |

**Calendar cross-reference:** If the calendar contains performance data rows at the bottom (common in planning docs), cross-reference against ESP report data. Flag any discrepancies > 5% variance.

---

## Step 3: Email Type Classification

Classify each email before scoring. Different types have different benchmarks and weights.

| Type | Classification Signals |
| --- | --- |
| `promotional` | Sale, discount, promo code, % off, EXTRA |
| `trend_editorial` | Trend, award, editorial concept, seasonal story |
| `brand` | Brand story, product launch, brand values |
| `newsletter` | Digest, roundup, multi-topic |
| `flow_welcome` | Welcome series, new subscriber |
| `flow_abandonment` | Cart, browse, checkout abandonment |
| `flow_winback` | Win-back, re-engagement, lapsed |
| `flow_post_purchase` | Post-purchase, review request, loyalty |
| `transactional` | Order confirm, shipping, receipt |

**Flows vs. Campaigns:** Always analyze separately. Flows have different frequency, audience warmth, and benchmark expectations. Never blend flow performance into campaign averages.

---

## Step 4: Scoring Framework

### Metric Weights by Email Type

Score each email 0–100 using weighted metrics. Weights shift by type:

#### Promotional / Sale Emails

| Metric | Weight | Notes |
| --- | --- | --- |
| Revenue / RPM | 35% | Primary success metric |
| Conversion Rate | 25% | Intent to purchase |
| CTOR | 20% | Engagement quality |
| Open Rate (Non-MPP) | 10% | Reach / subject line |
| Unsub Rate (inverted) | 10% | List health signal |

#### Trend / Editorial / Brand Emails

| Metric | Weight | Notes |
| --- | --- | --- |
| CTOR | 30% | Engagement depth |
| Open Rate (Non-MPP) | 25% | Subject line resonance |
| Revenue / RPM | 20% | Secondary but tracked |
| Conversion Rate | 15% | Soft conversion |
| Unsub Rate (inverted) | 10% | Audience fit |

#### Newsletter / Editorial

| Metric | Weight | Notes |
| --- | --- | --- |
| Open Rate (Non-MPP) | 35% | Core newsletter metric |
| CTOR | 30% | Content relevance |
| Unsub Rate (inverted) | 20% | Audience alignment |
| Revenue / RPM | 15% | Secondary |

#### Automated Flows

| Metric | Weight | Notes |
| --- | --- | --- |
| Conversion Rate | 35% | Flows are conversion-optimized |
| Revenue / RPM | 30% |     |
| CTOR | 20% |     |
| Unsub Rate (inverted) | 15% | Critical for flows |

### Scoring Scale

- **80–100** → 🏆 Winner
- **60–79** → ✅ Solid Performer
- **40–59** → ⚠️ Average / Watch
- **0–39** → 🔴 Underperformer

---

## Step 5: Benchmarking

Use this priority order:

```
1. Brand baseline (if provided by user)
   ↓ not available?
2. YoY — same period prior year (PREFERRED for seasonal brands)
   ↓ not available?
3. Period-over-period — prior month (use with seasonality caveat)
   ↓ not available?
4. Industry benchmarks (see references/benchmarks.md)
```

Always state which benchmark tier is being used in the report and why.

**YoY vs. MoM Priority:**
For any brand with seasonal demand patterns (apparel, swimwear, retail, travel, holidays),
always prefer YoY over month-over-month. A February 2026 vs. January 2026 comparison
for a swimwear brand is structurally misleading — February is peak season, January is not.
February 2026 vs. February 2025 is the meaningful comparison. Flag this explicitly if the
user only provides MoM data and suggest they retrieve prior year data.

**YoY Variance Thresholds — When to Flag:**
| Metric | Notable Variance | Significant Variance | Flag Language |
|--------|-----------------|---------------------|---------------|
| Open Rate | ±3pp | ±6pp | "Meaningfully above/below prior year" |
| CTOR | ±2pp | ±5pp | "Engagement quality has shifted" |
| Conversion Rate | ±0.5pp | ±1.5pp | "Purchase intent change vs. prior year" |
| Revenue / RPM | ±10% | ±25% | "Revenue per send up/down vs. prior year" |
| Unsub Rate | ±0.05pp | ±0.15pp | "List health signal — investigate" |
| Total Revenue | ±10% | ±20% | "Email program revenue trend" |

(pp = percentage points)

For benchmark reference data, see `references/benchmarks.md`.

---

## Step 6: Report Generation

### MONTHLY Report Structure

Tone: Strategic, narrative-driven, executive-ready. Lead with so-what insights, not raw numbers.

```
# [Brand] Email Performance Report — [Month Year]

## Executive Summary
3–5 sentence narrative. Month in one paragraph: what worked, what didn't, one key opportunity.
Include total revenue from email, total sends, and overall program health score.
If YoY data is available, open with the YoY revenue delta as the headline number.

## Program Health Scorecard
| Metric | This Period | Prior Year (YoY) | YoY Δ | Baseline / Benchmark | vs. Benchmark | Status |
|--------|------------|-----------------|-------|---------------------|---------------|--------|
| Avg Open Rate (Non-MPP) | | | | | | |
| Avg CTOR | | | | | | |
| Avg Conversion Rate | | | | | | |
| Total Revenue | | | | | | |
| Avg RPM | | | | | | |
| Avg Unsub Rate | | | | | | |
| Avg Bounce Rate | | | | | | |
| Deliverability Rate | | | | | | |
| Total Sends | | | | | | |

Note: If no YoY data is available, collapse "Prior Year" and "YoY Δ" columns and note the absence.

## Year-over-Year Analysis (include only if YoY data is provided)

### YoY Program Summary
2–3 sentence narrative on overall program trajectory vs. prior year.
Is the email program growing, holding, or declining? What is driving the change?

### YoY Metric Variance Table
| Metric | [Month] 2025 | [Month] 2026 | Δ (pp or %) | Signal |
|--------|-------------|-------------|------------|--------|
| Total Revenue | | | | 📈 / 📉 / ➡️ |
| Total Sends | | | | |
| Avg Open Rate (Non-MPP) | | | | |
| Avg CTOR | | | | |
| Avg Conversion Rate | | | | |
| Avg RPM | | | | |
| Avg Unsub Rate | | | | |
| Avg Bounce Rate | | | | |

Signals: 📈 Improving · 📉 Declining · ➡️ Stable (within threshold)

### Campaign-Level YoY Matching (if applicable)
Where the same campaign type or theme ran in both years, compare directly:
| Campaign Theme | 2025 Revenue | 2026 Revenue | YoY Δ | 2025 Conv% | 2026 Conv% | YoY Δ |
|---------------|-------------|-------------|-------|-----------|-----------|-------|

Note: Match by campaign type/concept, not exact name. Flag if a campaign type ran in one
year but not the other — that absence is itself a strategic signal.

### YoY Interpretation & Recommendations
3–5 observations connecting YoY variances to actionable decisions.
Structure each as: [What changed] → [Hypothesis for why] → [Recommended action]

Example: "Conversion rate on promotional emails declined 0.8pp YoY despite higher open rates,
suggesting the offer structure may have weakened. Consider auditing discount depth and
urgency messaging vs. prior year campaigns."

## Email Performance Ranked Table
Sorted by composite score descending. Include all campaigns sent in the period.

| Rank | Campaign | Type | Date | Segment | Score | Revenue | Open% | CTOR | Conv% | RPM | YoY Rev Δ | Flag |
|------|----------|------|------|---------|-------|---------|-------|------|-------|-----|-----------|------|

Flags: 🏆 Winner | ✅ Solid | ⚠️ Watch | 🔴 Under
Include YoY Rev Δ column only if prior year campaign-level data is available.

## Winners — What Worked
Top 3 emails. For each:
- Why it scored well (be specific: was it the offer? subject line? segment? timing?)
- YoY comparison if available: did it outperform the equivalent send last year?
- What to replicate

## Underperformers — What to Address
Bottom 2–3 emails. For each:
- Root cause hypothesis (subject line fatigue? wrong segment? weak offer? send time?)
- YoY context if available: is this a new problem or a worsening trend?
- Recommended fix

## Opportunities & Recommendations
3–5 strategic recommendations. Connect to brand goals, not just metrics.
Prioritize: Quick wins first, then medium-term, then structural.
Where YoY data supports a recommendation, cite the trend explicitly.

## Deliverability & List Health
- Bounce rate trend (and YoY if available)
- Unsub rate trend (and YoY if available)
- Any spam complaint signals
- List growth / shrinkage if data available

## Flows Performance (if applicable)
Separate section. Do not blend with campaign metrics.
Note: flows are evergreen — flag any that need optimization vs. campaigns which are one-time.
Include YoY flow performance comparison if prior year flow data is provided.

## Benchmark Notes
State which benchmark tier was used (brand baseline / YoY / MoM / industry) and any
caveats (seasonality, MPP inflation, list size changes, send frequency changes YoY).

If send volume changed significantly YoY (>15%), note this — it affects all rate metrics
and revenue comparisons must be normalized per-send to be meaningful.
```

---

### WEEKLY Report Structure

Tone: Direct, operational, scannable. Email team should be able to act on this in 10 minutes.

```
# [Brand] Weekly Email Report — Week of [Date Range]

## Week at a Glance
2–3 sentence summary. Revenue total, best performer, one flag to address.

## Campaign Scorecard
| # | Campaign | Date | Score | Revenue | Open% | CTOR | Conv% | RPM | Status |
|---|----------|------|-------|---------|-------|------|-------|-----|--------|

## This Week's Winner 🏆
One email. What worked and why. One sentence on what to replicate next week.

## Watch List ⚠️
1–2 emails. Brief diagnosis. Immediate action item.

## Quick Actions for Next Week
Bulleted list, max 5 items. Tactical and specific.
Examples: "Test send time — [Campaign X] sent at 9am underperformed vs [Campaign Y] at 11am"

## Strategic Nudge
One forward-looking observation that connects this week to the bigger picture.
If YoY data is available, include one YoY data point that adds context to the week's performance.
(This is the "weekly tactical with strategic nuance" element.)
```

---

## Step 7: Baseline Format

If the user has a brand baseline, ask them to provide it in this format (or as close as they can):

```
Brand: [name]
Industry: [vertical]
Period: [date range of baseline data]
Avg Open Rate (Non-MPP): x%
Avg CTOR: x%
Avg Click Rate: x%
Avg Conversion Rate: x%
Avg RPM ($/1000): $x
Avg AOV: $x
Avg Unsub Rate: x%
Avg Bounce Rate: x%
Avg Deliverability Rate: x%
Flow Benchmarks (if separate): [same fields]
Notes: [seasonality, list size, any caveats]
```

If no baseline exists, offer to help the user **create one** from the data they've just provided — this becomes their starting point for future reports.

---

## Step 8: Insight Quality Standards

Every insight must be:

- **Specific** — name the email, the metric, the delta
- **Causal** — offer a hypothesis for why, not just what
- **Actionable** — connect to a next step

Avoid generic statements like "open rates were below average." Instead write:
"The Valentine's Day Wish List email (Feb 3) had the lowest CTOR of the month at 0.25%, despite a strong open rate of 45.25%. The subject line drove opens but content or CTA likely didn't convert browsers — consider testing a more direct offer-led CTA in similar trend sends."

---

## Common Pitfalls to Flag

Always check for and call out:

| Pitfall | How to Detect | What to Say |
| --- | --- | --- |
| MPP-inflated opens | Open rate >> Non-MPP open rate | "Open rates include Apple MPP data — Non-MPP rate of X% is the more reliable signal" |
| Promo halo effect | High revenue on sale email vs. low on surrounding sends | "Sale emails lifted revenue but may suppress engagement on adjacent sends" |
| Segment size bias | Small segment with high conv% | "High conversion rate on small VIP segment — strong signal but not scalable benchmark" |
| Flow/campaign blending | Mixed types in averages | Always separate — note if user has blended data |
| Seasonality mismatch | MoM comparison for seasonal brand | "Same-period YoY is the meaningful comparison for this brand — February vs. January is structurally misleading" |
| YoY send volume change | Sends up/down >15% YoY | "Send volume changed significantly YoY — normalize revenue metrics per-send before drawing conclusions" |
| Missing Non-MPP data | Only MPP opens available | Flag and caveat all open rate analysis |

---

## Reference Files

- `references/benchmarks.md` — Industry benchmark data by vertical, with sources
- `references/metric-definitions.md` — Full definitions for every metric including calculation formulas

Read these reference files when:

- No brand baseline is available and you need benchmark fallback data
- User asks how a specific metric is calculated
- You need to validate whether a metric result is realistic

---

## Output Checklist

Before delivering the report, verify:

- [ ] Report mode matches user request (MONTHLY vs WEEKLY)
- [ ] All emails in ESP data are included in ranked table
- [ ] Flows analyzed separately from campaigns
- [ ] Benchmark tier stated (baseline / YoY / MoM / industry)
- [ ] If YoY data provided: YoY section included with variance table and interpretations
- [ ] If YoY data provided: scorecard includes YoY Δ column
- [ ] If YoY data not provided: absence noted and MoM seasonality caveat flagged
- [ ] Send volume change YoY noted if >15% (affects all rate metric comparisons)
- [ ] MPP caveat included if relevant
- [ ] Every recommendation is specific and actionable
- [ ] Scored table sorted by composite score
- [ ] Winners section references actual email names and metrics
- [ ] Underperformers section includes root cause hypothesis
