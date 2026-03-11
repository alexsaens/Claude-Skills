# Email Performance Analyzer — Claude Code Skill

A Claude Code skill for analyzing email marketing performance data. Drop in your ESP export and marketing calendar, and get a structured analysis with scored rankings, winners, underperformers, and strategic recommendations.

Built to work with any email platform and any brand — from a single boutique to a multi-brand agency portfolio.

---

## What It Does

- **Scores every email** sent in a period using a weighted composite metric model that adjusts by email type (promotional, editorial, newsletter, automated flows)
- **Identifies winners and underperformers** with specific, causal explanations — not just "open rate was low"
- **Benchmarks performance** against a brand baseline, period-over-period data, or industry benchmarks (with source citations)
- **Generates two report formats:**
  - `MONTHLY` — strategic, narrative-driven, executive-ready
  - `WEEKLY` — tactical, operational, scannable by the email team
- **Handles messy real-world data** — unstructured marketing calendars, MPP-inflated open rates, mixed campaign and flow data

---

## File Structure

```
email-performance-analyzer/
├── SKILL.md                        # Main skill — analysis framework, scoring, report templates
└── references/
    ├── benchmarks.md               # Industry benchmarks by vertical with sources
    └── metric-definitions.md       # Metric formulas, MPP guide, ESP terminology glossary
```

---

## Supported Platforms

Platform-agnostic. Tested against:

- **Listrak**
- **Klaviyo**
- **Salesforce Marketing Cloud (SFMC)**
- **Bloomreach**
- **Mailchimp**
- Any ESP that exports a CSV or tabular performance report

The skill maps platform-specific column names to a normalized field set automatically.

---

## Inputs Required

### 1. ESP Performance Report

A CSV or pasted export from your email platform. The skill handles any column naming convention.

Key fields it looks for (by any name):

- Campaign name, send date, message type
- Sends, delivered, opens (MPP and Non-MPP), clicks, CTOR
- Revenue, conversions, AOV, RPM ($/1000)
- Unsubscribes, bounces, visits

### 2. Marketing Calendar *(optional but recommended)*

Does not need to be structured — the skill is designed to parse planning documents with mixed content. It extracts:

- Campaign concept and theme
- Audience segment
- Subject lines and preheader text
- Offer / promo code
- Email type (inferred from concept)
- Send time

If your calendar already has performance rows at the bottom, the skill cross-references them against the ESP report and flags discrepancies.

### 3. Brand Baseline *(optional)*

Historical average performance for the brand. If not available, the skill falls back to period-over-period comparison, then industry benchmarks.

---

## How It Works

At the start of each session, the skill asks 5 setup questions:

1. Brand name and industry/vertical
2. Report mode (MONTHLY or WEEKLY)
3. Whether a historical baseline is available
4. Time period for the report
5. Data upload (ESP report + calendar)

Then it:

1. Parses and normalizes all input data
2. Classifies each email by type (promotional, trend/editorial, brand, newsletter, welcome flow, abandonment flow, winback flow, post-purchase flow, transactional)
3. Scores each email 0–100 using weighted metrics — weights shift by email type
4. Ranks all emails from winner to underperformer
5. Benchmarks against baseline → period-over-period → industry benchmarks (in that order)
6. Generates the report in the requested format

---

## Scoring Framework

Scores are weighted differently depending on email type:

| Email Type         | Primary Weight        | Secondary Weights                               |
| ------------------ | --------------------- | ----------------------------------------------- |
| Promotional / Sale | Revenue / RPM (35%)   | Conversion rate, CTOR, open rate, unsub rate    |
| Trend / Editorial  | CTOR (30%)            | Open rate, revenue, conversion rate, unsub rate |
| Newsletter         | Open Rate (35%)       | CTOR, unsub rate, revenue                       |
| Automated Flows    | Conversion Rate (35%) | Revenue / RPM, CTOR, unsub rate                 |

Score thresholds: 🏆 Winner (80–100) · ✅ Solid (60–79) · ⚠️ Watch (40–59) · 🔴 Under (0–39)

Flows are always analyzed separately from campaigns — they have different audience warmth, frequency, and benchmark expectations.

---

## Benchmarking

The skill uses a three-tier fallback:

```
1. Brand baseline (provided by user)
   ↓ not available?
2. Period-over-period (prior month or prior year same period)
   ↓ not available?
3. Industry benchmarks (references/benchmarks.md)
```

Industry benchmarks are sourced from Klaviyo (2024–2025), Litmus (2025), Mailchimp (2024), and Campaign Monitor (2024), organized by vertical:

- Apparel & Fashion Retail
- Luxury / Premium Apparel
- General Retail / eCommerce
- Travel & Hospitality
- Financial Services
- Automated flows (all verticals)

The benchmark tier used is always stated in the report with caveats.

---

## Report Formats

### Monthly Report (Strategic)

For CMO, VP, or Director-level stakeholders.

- Executive summary (3–5 sentence narrative)
- Program health scorecard (8 KPIs vs. baseline)
- Full ranked email table with scores
- Winners section — what worked and why, what to replicate
- Underperformers section — root cause hypothesis and fix
- Strategic recommendations (prioritized: quick wins → medium-term → structural)
- Deliverability and list health summary
- Flows performance (separate section)
- Benchmark notes and caveats

### Weekly Report (Tactical)

For email managers and coordinators.

- Week at a glance (2–3 sentences)
- Campaign scorecard table
- This week's winner with replication note
- Watch list with immediate action items
- Quick actions for next week (max 5 bullets)
- Strategic nudge — one forward-looking observation

---

## MPP Handling

Apple Mail Privacy Protection inflates open rates for all senders. The skill:

- Prioritizes Non-MPP open rate as the primary engagement metric wherever available
- Flags when only MPP-inclusive opens are present and caveats all open rate analysis
- Uses CTOR and conversion rate as primary engagement proxies when open data is unreliable

---

## Installation

1. Download `email-performance-analyzer.skill`
2. Place in your Claude Code skills directory:
   
   ```
   ~/.claude/skills/
   ```
3. Restart Claude Code — the skill will appear in your available skills list

---

## Contributing

Suggestions for additional verticals, ESP platform mappings, or scoring model improvements are welcome. Open an issue or submit a PR.

---

## License

MIT — free to use, modify, and distribute. Attribution appreciated but not required.

---

*Built with Claude Code · Developed by [XDO](https://xdo.it.com)*
