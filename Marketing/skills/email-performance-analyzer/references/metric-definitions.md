# Email Metric Definitions & Formulas

Reference for analysts and for validating incoming data.

---

## Core Delivery Metrics

**Sends**
Total number of emails attempted, including those that bounced.

**Delivered**
Sends minus hard and soft bounces.
`Delivered = Sends - Bounced`

**Delivered Rate**
`Delivered Rate = Delivered / Sends × 100`
Healthy range: 97–99%+. Below 95% is a deliverability problem.

**Bounce Rate (Bounced/Failed Rate)**
`Bounce Rate = Bounced / Sends × 100`
Includes hard bounces (invalid address) and soft bounces (temporary failure).
Flag if >1.5%. Investigate if >2%.

---

## Engagement Metrics

**Open Rate**
`Open Rate = Opens / Delivered × 100`
⚠️ Inflated by Apple Mail Privacy Protection (MPP) since iOS 15 (Sept 2021).
Use Non-MPP open rate as primary metric wherever available.

**Open Rate (Non-MPP)**
Excludes opens triggered by Apple's privacy relay.
`Non-MPP Open Rate = Non-MPP Opens / Delivered × 100`
This is the preferred metric for true engagement measurement.

**Click Rate (CTR)**
`Click Rate = Total Clicks / Delivered × 100`
Measures all clicks including multiple clicks by the same person.

**Unique Click Rate**
`Unique Click Rate = Unique Clickers / Delivered × 100`
Preferred over total click rate for audience reach measurement.

**CTOR (Click-to-Open Rate)**
`CTOR = Clicks / Opens × 100`
Measures content quality independent of subject line performance.
High CTOR + low open rate = great content, weak subject line.
Low CTOR + high open rate = strong subject line, weak content/CTA.

**Reads Rate**
Time-based engagement metric. Typically: Glanced (<2s), Skimmed (2–8s), Read (8s+).
Use to assess content depth engagement where available.

---

## Conversion & Revenue Metrics

**Conversion Rate**
`Conversion Rate = Conversions / Delivered × 100`
Definition of "conversion" varies — confirm with client (purchase, sign-up, booking, etc.)

**Revenue**
Total attributed revenue from the email send.
Attribution window varies by ESP (typically 5–7 day last-click or 1-day view).
Always confirm attribution model when comparing across brands or platforms.

**AOV (Average Order Value)**
`AOV = Revenue / Orders (Conversions)`

**RPM (Revenue per 1,000 Messages)**
`RPM = (Revenue / Delivered) × 1,000`
Also written as $/1000msg. Best single metric for comparing email revenue efficiency
across sends of different sizes.

**Revenue per Email (RPE)**
`RPE = Revenue / Delivered`
Same as RPM/1000. Use RPM for comparability.

---

## List Health Metrics

**Unsubscribe Rate**
`Unsub Rate = Unsubscribes / Delivered × 100`
Healthy: <0.1%. Concerning: >0.2%. Critical: >0.5%.
Spikes often indicate: wrong segment, irrelevant content, send frequency fatigue, or
a list quality issue.

**Spam Complaint Rate**
`Complaint Rate = Spam Complaints / Delivered × 100`
Gmail threshold: <0.10% (above triggers filtering). Critical: >0.30%.
Not always available in ESP exports — check platform spam reporting separately.

**Visits**
Sessions driven to site from email. Not available in all ESPs.
Use as a secondary engagement signal where available.

---

## Derived / Diagnostic Ratios

**Subject Line Effectiveness**
Proxy metric: `Open Rate (Non-MPP) vs. Brand Baseline`
High = strong subject line. Low = subject line not resonating with segment.

**Content Quality Score**
Proxy metric: `CTOR vs. Brand Baseline`
Measures whether people who opened actually engaged with content.

**Offer Effectiveness**
Proxy metric: `Conversion Rate vs. Brand Baseline for same email type`
Controls for open/click variance, isolates purchase intent.

**List Quality Index**
Composite signal: `Bounce Rate + Unsub Rate + (inverse of Deliverability Rate)`
Not a standard metric — use directionally when list health is a concern.

---

## Attribution Notes

Email attribution windows vary significantly:

| Platform | Default Window |
|----------|---------------|
| Klaviyo | 5-day click, 1-day open |
| SFMC | Configurable (often 30-day) |
| Bloomreach | Configurable |
| Listrak | Configurable |
| Mailchimp | 5-day |

Always confirm attribution window before comparing revenue figures across platforms
or when a client questions revenue numbers.

---

## MPP Impact Guide

Apple Mail Privacy Protection (MPP) pre-loads email content including tracking pixels,
making it appear emails were opened even when they weren't read.

**Affected ESPs:** All major platforms
**Affected Users:** Apple Mail users on iOS 15+ and macOS Monterey+ (est. 40–55% of email opens as of 2025)

**How to handle:**
1. Use Non-MPP open rate as primary metric
2. If only MPP-inclusive opens available, caveat all open rate analysis
3. Use CTOR and conversion rate as primary engagement proxies
4. Do not compare current open rates to pre-2021 historical benchmarks without MPP caveat

---

## Glossary of ESP-Specific Terms

| Term | Platform | Standard Equivalent |
|------|----------|-------------------|
| Message Sends | Listrak | Sends |
| $/1000msg | Listrak | RPM |
| Bounced/Failed | Listrak | Bounces |
| Hard Bounce | Most | Invalid/permanent bounce |
| Soft Bounce | Most | Temporary delivery failure |
| Total Opens | Most | Opens (MPP-inclusive) |
| Machine Opens | Klaviyo | MPP-triggered opens |
| Human Opens | Klaviyo | Non-MPP opens |
| Placed Order | Klaviyo | Conversions |
| Revenue | Klaviyo/Listrak | Attributed revenue |
