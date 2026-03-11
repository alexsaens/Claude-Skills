# Management Consultant 2.0 — Claude Code Skill Suite

A complete library of world-class management consulting methodologies, implemented as Claude Code skills. Drop in a business problem and get structured, senior-level consulting frameworks applied immediately — from problem definition through to implementation roadmap.

Built for consultants, strategists, operators, and executives who want rigorous analytical firepower without the billable hours.

---

## What It Does

This suite gives Claude access to **9 consulting methodology skills** orchestrated by a master routing skill that assesses your problem and recommends the right framework — or combination of frameworks — to solve it.

Rather than asking Claude to "think like a consultant," each skill embeds the actual methodology, deliverables, engagement protocol, and analytical frameworks used by the world's top consulting firms.

---

## Skill Index

| Skill File | Methodology | Firm | Best For |
|------------|-------------|------|----------|
| `mc-consultant` | **Management Consultant 2.0 — Orchestrator** | All firms | Start here — assesses your problem and routes to the right methodology |
| `mc-mckinsey-problem-solving` | McKinsey 7-Step Problem Solving | McKinsey & Co. | Ill-defined problems, hypothesis testing, MECE decomposition |
| `mc-mckinsey-7s` | McKinsey 7-S Framework | McKinsey & Co. | Organizational alignment, restructuring, M&A integration |
| `mc-bain-results-delivery` | Bain Results Delivery | Bain & Co. | Strategy-to-execution gaps, change management, adoption |
| `mc-bcg-portfolio` | BCG Portfolio Strategy & Competitive Analysis | BCG | Portfolio decisions, resource allocation, competitive positioning |
| `mc-bcg-tipping-point` | BCG Tipping Point Leadership | BCG | Rapid transformation with limited resources, overcoming inertia |
| `mc-deloitte-greenhouse` | Deloitte Business Chemistry & Breakthrough Labs | Deloitte | Team dynamics, innovation facilitation, breaking groupthink |
| `mc-accenture-adm` | Accenture Delivery Method (ADM) | Accenture | Large-scale tech implementations, ERP rollouts, multi-workstream delivery |
| `mc-pwc-bxt` | PwC BXT Innovation | PwC | Digital product innovation, customer experience, human-centric design |
| `mc-kpmg-powered` | KPMG Powered Enterprise | KPMG | Back-office modernization, Finance/HR/IT/Procurement transformation |

---

## How to Use It

### Option 1: Use the Orchestrator (Recommended)
Invoke `mc-consultant` with any business problem. The orchestrator will:
1. Ask clarifying questions to understand scope, constraints, and urgency
2. Classify the problem across four dimensions (nature, definition, scale, time horizon)
3. Recommend the primary methodology with rationale
4. Optionally recommend a complementary second methodology
5. Hand off directly into the engagement — no re-invocation needed

**Example:**
```
/mc-consultant We're six months into a digital transformation and nothing is sticking. 
We have the strategy but the business isn't changing its behavior.
```
→ Orchestrator classifies as: Behavioral / Structured but Unexecuted / Enterprise / Near-term  
→ Routes to: **Bain Results Delivery** (primary) + **BCG Tipping Point** (secondary)

### Option 2: Invoke a Methodology Directly
If you already know which framework you need, invoke it directly:

```
/mc-mckinsey-problem-solving How can we reduce customer churn in our enterprise segment?
/mc-bcg-portfolio Which of our 6 business units should we invest in vs. divest?
/mc-deloitte-greenhouse Our leadership team is stuck in groupthink — we need a breakthrough session
```

---

## Skill Descriptions

### `mc-consultant` — The Orchestrator
The master router. Analyzes any business challenge across four dimensions and recommends the optimal methodology. Knows when to combine frameworks and in what sequence. Use this as your default entry point.

**Problem Classification Dimensions:**
- **Nature:** Strategic / Operational / Organizational / Behavioral / Innovation
- **Definition:** Ill-defined → Defined → Structured → Executing → Scaling
- **Scale:** Team → Function → Business Unit → Enterprise
- **Time Horizon:** Crisis (<3 months) → Near-term → Medium-term → Long-term (3+ years)

**Multi-Methodology Patterns:**
| Pattern | Sequence | Use When |
|---------|----------|----------|
| Diagnose & Execute | McKinsey Problem Solving → Bain Results Delivery | Problem unclear AND execution is critical |
| Align & Transform | McKinsey 7-S → Accenture ADM | Restructuring before major implementation |
| Strategize & Modernize | BCG Portfolio → KPMG Powered | Portfolio decisions driving functional transformation |
| Innovate & Deliver | PwC BXT → Accenture ADM | Innovation concept needs industrialized delivery |
| Unblock & Scale | BCG Tipping Point → Bain Results Delivery | Inertia must be broken before sustained execution |

---

### `mc-mckinsey-problem-solving` — 7-Step Problem Solving
McKinsey's hypothesis-led problem solving process using MECE logic.

**Engagement Flow:** Problem Definition → Issue Trees → Prioritization Matrix → Workplan → Analysis → Pyramid Principle Synthesis → Implementation Roadmap

**Key Deliverables:** Problem Statement Worksheet, MECE Issue/Hypothesis Tree, 2x2 Prioritization Matrix, Engagement Workplan, Synthesis Deck, Implementation Roadmap with Business Case

**Invoke when:** The problem is ill-defined, the team is solving the wrong problem, or structured decomposition is needed before any action is taken.

---

### `mc-mckinsey-7s` — Organizational Alignment
The seven-element organizational effectiveness model: Strategy, Structure, Systems (Hard) + Shared Values, Style, Staff, Skills (Soft).

**Engagement Flow:** 7-S Diagnostic Dashboard → Alignment Matrix (misalignment heat map) → Intervention Plan → Organizational Design → Culture Transformation → Transition Roadmap (3 waves)

**Key Deliverables:** 7-S Diagnostic Dashboard, Alignment Matrix, Organizational Design Blueprint, Culture Transformation Roadmap, Transition Plan

**Invoke when:** Strategy and execution are misaligned, M&A integration is needed, or restructuring requires a systemic view of the organization.

---

### `mc-bain-results-delivery` — Execution & Adoption
Bain's methodology for closing the "execution gap" — the space between a strategy's promise and its P&L impact. Research-backed: only 12% of companies achieve 100% of their change ambitions.

**Engagement Flow:** Value Bridge → Adoption Risk Heat Map → Initiative Charters → Results Delivery Office (RDO) Design → Change Story → Emotional Cycle Management → Financial Verification

**Key Deliverables:** Value Bridge Table, Adoption Risk Heat Map (2x2), Initiative Charters, RDO Operating Model, Change Story Package, Reinforcement System Design, Financial Verification Framework

**Invoke when:** You have a strategy but it's not becoming behavior. The "reporting theater" is running but the P&L isn't moving.

---

### `mc-bcg-portfolio` — Portfolio Strategy & Competitive Analysis
Three BCG frameworks: Growth-Share Matrix (Stars/Cash Cows/Question Marks/Dogs), Experience Curve Analysis, and Advantage Matrix.

**Engagement Flow:** Business unit mapping → Relative market share calculation → Quadrant classification → Cash Flow Architecture design → Experience curve projection (if applicable) → Advantage Matrix environment classification → Portfolio Action Plan

**Key Deliverables:** Growth-Share Matrix with classifications, Cash Flow Architecture, Experience Curve analysis, Advantage Matrix classification, Resource Reallocation Recommendation

**Invoke when:** Deciding which businesses to invest in, hold, harvest, or divest. Resource allocation decisions. Competitive positioning assessment.

---

### `mc-bcg-tipping-point` — Rapid Transformation
The Tipping Point Leadership methodology: transform organizations by engaging disproportionate influence factors rather than seeking consensus or new budget.

**The Four Hurdles:**
1. **Cognitive** — People don't see the need for change → Force confrontation with reality
2. **Resource** — No new budget → Redirect from cold spots to hot spots
3. **Motivational** — No will to change → Identify and flip the kingpins
4. **Political** — Powerful opponents → Build a coalition of angels; neutralize devils

**Key Deliverables:** Four Hurdles Diagnostic, Cognitive Confrontation Plan, Resource Reallocation Map, Kingpin Influence Map, Political Landscape Map, Leadership Canvas, 90-Day Action Plan

**Invoke when:** Organizational inertia is the primary blocker. Resources are constrained. Speed matters more than consensus.

---

### `mc-deloitte-greenhouse` — Team Dynamics & Breakthrough Labs
Two integrated Deloitte methodologies: Business Chemistry behavioral profiling (Pioneer, Guardian, Driver, Integrator) and the Breakthrough Lab 10-principle facilitation system.

**Business Chemistry Flow:** Type identification → Team composition analysis → Clash zone mapping → Mitigation strategies

**Breakthrough Lab Flow:** Discovery → Session design → 10-principle facilitation (Silence Your Cynic, Strip Away Everything, Check Your Edge, Don't Play Nice, etc.) → Rapid prototyping → Convergence → Action Plan

**Key Deliverables:** Business Chemistry Team Profile Map, Clash Zone Analysis, Breakthrough Lab Agenda, Orthodoxy List, Prioritized Solution Set, Strategic Roadmap, 30/60/90 Day Action Plan

**Invoke when:** Team dynamics are creating friction. Groupthink is preventing breakthrough thinking. Innovation sessions need structure.

---

### `mc-accenture-adm` — Industrialized Transformation Delivery
Accenture's end-to-end delivery framework for large-scale technology implementations and multi-workstream programs. Reduces "Value Leakage" through standardized, predictable delivery.

**Six Lifecycle Stages:** Envision/Define → Design → Build → Test → Deploy → Run/Optimize

**Delivery Pathway Selection:** Agile (digital products) / Waterfall Stage-Gated (ERP, compliance-bound) / Hybrid (regulated industries with digital components)

**Key Deliverables:** Business Case & Value Tree, Target Operating Model, Delivery Pathway Selection Rationale, Solution Build Blueprint, Test Strategy, Cutover Plan, Runbooks, Value Realization Dashboard

**Invoke when:** Major technology implementation, ERP rollout, digital transformation program, or multi-workstream delivery requiring industrialized governance.

---

### `mc-pwc-bxt` — Human-Centric Digital Innovation
PwC's Business + Experience + Technology convergence model. Every solution is tested against the BXT Triangle: viable (Business), desirable (Experience), feasible (Technology).

**Co-Creation Flow:** Discovery (ethnographic research, journey mapping, Jobs-to-be-Done) → Session design → Co-creation workshop (Reframe → Ideate → Converge → Prototype → Test) → Debrief → Deliverable realization

**Key Deliverables:** Current-state Journey Map, Persona Profiles, BXT Triangle Assessment, Future-state Journey Map, Rapid Prototypes, Business Model Canvas, Technology Roadmap, Implementation Plan

**Invoke when:** Building new digital products or services. Customer experience redesign. Innovation that must balance business viability with human desirability.

---

### `mc-kpmg-powered` — Functional Transformation
KPMG's 80/20 cloud-based transformation methodology for back-office functions. 80% pre-configured leading practice Target Operating Model, 20% tailored to client needs.

**Three Pillars:** Target Operating Model (6 layers: Process, People, Service Model, Technology, Data, Governance) → Powered Technology (pre-built assets, templates, test scripts) → Powered Evolution (continuous improvement, evergreen updates)

**Four Execution Phases:** Vision → Validate → Construct → Deploy

**Key Deliverables:** Current-State Assessment, Target Operating Model, Fit-Gap Analysis, Customization Register, Implementation Plan, Pre-configured Process Models, Analytics Dashboard Design, Powered Evolution Roadmap

**Invoke when:** Modernizing Finance, HR, IT, Procurement, or Supply Chain. Implementing or optimizing ERP/SaaS platforms. Designing a Target Operating Model.

---

## Research Foundation

This skill suite is backed by `Consulting_Methodologies_Report_Generation.md` — a research report analyzing the theoretical foundations, technical deliverables, and documented impact of each methodology across McKinsey, Bain, BCG, Deloitte, Accenture, PwC, and KPMG.

---

## Installation

1. Download or clone this repository
2. Copy all skill folders to your Claude Code skills directory:
   ```
   ~/.claude/skills/
   ```
3. Restart Claude Code — all 10 skills will appear in your available skills list
4. Start with `/mc-consultant [your problem]` or invoke any methodology directly

---

## File Structure

```
management-consultant-skills/
├── README.md                                         ← this file
├── mc-consultant/
│   └── SKILL.md                                      ← Orchestrator (start here)
├── mc-mckinsey-problem-solving/
│   └── SKILL.md
├── mc-mckinsey-7s/
│   └── SKILL.md
├── mc-bain-results-delivery/
│   └── SKILL.md
├── mc-bcg-portfolio/
│   └── SKILL.md
├── mc-bcg-tipping-point/
│   └── SKILL.md
├── mc-deloitte-greenhouse/
│   └── SKILL.md
├── mc-accenture-adm/
│   └── SKILL.md
├── mc-pwc-bxt/
│   └── SKILL.md
├── mc-kpmg-powered/
│   └── SKILL.md
└── references/
    └── Consulting_Methodologies_Report_Generation.md ← Research foundation
```

---

## Contributing

Suggestions for additional methodologies, improved engagement protocols, or new deliverable templates are welcome. Open an issue or submit a PR.

Methodologies under consideration for future versions:
- Oliver Wyman — Actuarial & Risk
- Roland Berger — European market strategy
- A.T. Kearney — Operations & procurement
- Monitor Deloitte — Demand-led strategy

---

## License

MIT — free to use, modify, and distribute. Attribution appreciated but not required.

---

*Built with Claude Code · Developed by [XDO](https://xdo.it.com)*
