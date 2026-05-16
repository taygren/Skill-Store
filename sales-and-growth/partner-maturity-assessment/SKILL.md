---
name: partner-maturity-assessment
description: >
  Partner Maturity Assessment — evaluate the depth, breadth, presence, and sophistication
  of a technology company's partner ecosystem and go-to-market (GTM) programs. Use this skill
  whenever a user wants to assess, audit, benchmark, or score a company's partner program,
  channel strategy, or ecosystem maturity. Triggers include: "partner maturity", "channel
  assessment", "partner program audit", "ecosystem analysis", "ISV partnerships",
  "hyperscaler alignment", "VAR program", "SI strategy", "OEM maturity", "MSP program",
  "distributor strategy", "partner GTM", "channel readiness", "partner ecosystem review",
  "marketplace strategy", or any request to evaluate, score, or benchmark how well a company
  works with partners. Also trigger when the user provides a company name and asks about their
  partnerships, channel, alliances, or go-to-market. Always use this skill for partner-related
  assessments — even if phrased as "how good is X's partner program" or "does X have a strong
  channel".
---

# Partner Maturity Assessment Skill

> **Philosophy:** Partner ecosystems are a force multiplier. This skill assesses not just
> whether a company *has* partners — but how *well-engineered* that partner motion is, and
> where the highest-leverage GTM opportunities remain untapped.

---

## Commands

| Command | What It Does | Reference |
|---------|-------------|-----------|
| `/partner assess <company>` | Full partner maturity assessment across all 7 partner types | `references/full-assessment.md` |
| `/partner quick <company>` | Rapid ecosystem snapshot (5-min view) | inline below |
| `/partner type <company> <type>` | Deep-dive on a single partner type | `references/partner-types.md` |
| `/partner gtm <company>` | Strategic GTM opportunity analysis across partner types | `references/gtm-analysis.md` |
| `/partner benchmark <company> <peer>` | Side-by-side partner maturity comparison | `references/benchmarking.md` |
| `/partner report <company>` | Executive-ready partner maturity deliverable (.docx) | `references/report-output.md` |

**When executing any command:** read the corresponding reference file before proceeding.

---

## The 7 Partner Types Assessed

| # | Partner Type | Abbreviation | GTM Role |
|---|-------------|-------------|---------|
| 1 | Original Equipment Manufacturer | OEM | Embed product into another vendor's offering |
| 2 | Independent Software Vendor / Tech Alliances | ISV | Integration ecosystem and technical co-sell |
| 3 | Hyperscalers / Cloud Marketplaces | Hyperscaler | AWS, Azure, GCP marketplace listing and co-sell |
| 4 | Value Added Resellers | VAR | Indirect sales through solution-oriented resellers |
| 5 | Distributors | Distributor | Two-tier channel for scale and geographic reach |
| 6 | System Integrators / Consultants | SI | Implementation, transformation, and advisory layer |
| 7 | Managed Service Providers | MSP | Recurring managed delivery of company's product |

---

## Maturity Scoring System

### Composite Partner Maturity Score (0–100)

Each of the 7 partner types is scored independently across 5 dimensions, then weighted into a composite.

#### The 5 Assessment Dimensions

| Dimension | Weight | What It Measures |
|-----------|--------|-----------------|
| **Presence** | 20% | Does this partner motion exist at all? Are partners named, listed, or visible? |
| **Depth** | 25% | How sophisticated is the program structure (tiers, enablement, certification, MDF)? |
| **Breadth** | 20% | How wide is the partner network (geographic coverage, volume, diversity)? |
| **Enablement** | 20% | Training, sales tools, co-sell support, sandbox access, partner portals |
| **GTM Activation** | 15% | Joint marketing, pipeline generation, co-sell motions, marketplace activation |

#### Partner Type Weights (Composite Score)

Weights reflect typical GTM leverage for a B2B technology company. Adjust based on company's business model.

| Partner Type | Default Weight |
|-------------|---------------|
| ISV / Tech Alliances | 20% |
| Hyperscalers | 20% |
| System Integrators | 18% |
| VARs | 15% |
| MSPs | 12% |
| OEM | 10% |
| Distributors | 5% |

> **Note:** Weights should be recalibrated for specific company profiles (e.g., infrastructure
> hardware companies weight Distributors and VARs higher; pure SaaS companies weight Hyperscalers
> and ISVs higher).

#### Maturity Score Scale

| Score | Maturity Level | Meaning |
|-------|---------------|---------|
| 85–100 | **Elite** | Industry-leading partner program; others benchmark against it |
| 70–84 | **Advanced** | Strong program with few significant gaps |
| 55–69 | **Developing** | Functional program with meaningful optimization opportunities |
| 40–54 | **Emerging** | Foundational elements exist but program lacks consistency |
| 25–39 | **Nascent** | Minimal structure; ad hoc partnerships only |
| 0–24 | **Absent** | No discernible partner motion in this category |

---

## Issue Triage System (P0 / P1 / P2)

Apply this to flag gaps across every assessment:

| Level | Action Timeline | Examples |
|-------|----------------|---------|
| **P0 Critical** | Immediate | No hyperscaler listing, zero SI engagement for enterprise product, no partner portal |
| **P1 Important** | 30–60 days | Untrained VAR base, no MDF program, no co-sell motion with cloud providers |
| **P2 Recommended** | 90 days | Thin ISV integration catalog, no MSP-specific pricing, missing distributor program guide |

---

## Research Protocol

When assessing a company, gather signals from these sources (in order of reliability):

1. **Company partner page** — `/partners`, `/alliances`, `/ecosystem`, `/channels`
2. **Cloud marketplace listings** — AWS Marketplace, Azure Marketplace, GCP Marketplace
3. **Press releases & case studies** — Co-sell wins, SI deployments, OEM embeds
4. **Partner portals (public-facing)** — Tier structures, certification requirements, MDF availability
5. **LinkedIn** — Partner managers, alliance roles, channel directors (headcount signal)
6. **Industry analyst coverage** — Gartner, Forrester, IDC ecosystem assessments
7. **Job postings** — Partner/channel/alliances roles signal investment and program gaps
8. **G2, Capterra, TrustRadius** — Integration listings and partner-sourced reviews
9. **Conference presence** — AWS re:Invent, Microsoft Inspire, Google Next, Salesforce Dreamforce
10. **Competitor comparison** — What is the peer set doing that this company is not?

---

## Quick Assessment (`/partner quick <company>`)

Run inline without reading a reference file. Delivers a 5-point ecosystem snapshot:

1. Fetch company partner/ecosystem pages
2. Check marketplace listings (AWS, Azure, GCP)
3. Scan for SI/GSI named partnerships (Accenture, Deloitte, PwC, Capgemini, Wipro, Infosys)
4. Review ISV integration catalog size and depth
5. Look for partner portal, certification program, and MDF mentions

**Output format:**
```
🤝 OEM:          [Absent / Nascent / Developing / Advanced / Elite] — [1-line signal]
🔗 ISV/Alliances: [score] — [1-line signal]
☁️ Hyperscalers:  [score] — [1-line signal]
🏪 VARs:          [score] — [1-line signal]
📦 Distributors:  [score] — [1-line signal]
🔧 SIs:           [score] — [1-line signal]
🛠️ MSPs:          [score] — [1-line signal]

Composite Maturity: [XX/100] — [one-sentence verdict]
Top P0 Gap: [single most critical finding]
Top GTM Opportunity: [single highest-leverage unlock]
```

---

## GTM Opportunity Framework

For each partner type, analyze strategic GTM opportunities across 4 lenses:

| Lens | Question to Answer |
|------|-------------------|
| **Revenue Acceleration** | How can this partner type compress the sales cycle or expand deal size? |
| **Market Coverage** | What geographies, segments, or verticals can partners unlock that direct sales cannot? |
| **Product Extension** | How can partners embed, integrate, or co-develop to extend the product's value? |
| **Competitive Defense** | Which partner motions, if underdeveloped, create vulnerability to competitors? |

See `references/gtm-analysis.md` for full GTM playbook by partner type.

---

## Reference Library

Read the relevant reference file before executing detailed commands.

| File | Contents |
|------|---------|
| `references/full-assessment.md` | End-to-end assessment workflow, scoring rubrics, output template |
| `references/partner-types.md` | Deep-dive rubrics for each of the 7 partner types |
| `references/gtm-analysis.md` | GTM opportunity analysis framework by partner type |
| `references/benchmarking.md` | Peer comparison methodology and output format |
| `references/report-output.md` | Executive deliverable format (.docx export instructions) |

---

## Output Standards

All Partner Maturity Assessments must include:
- **Scored dimension table** per partner type (Presence / Depth / Breadth / Enablement / GTM Activation)
- **Composite maturity score** with confidence level (High / Medium / Low based on data availability)
- **P0/P1/P2 gap triage** across all partner types
- **GTM opportunity analysis** for each partner type
- **Strategic narrative** — executive-level synthesis connecting partner maturity to business outcomes
- **Recommended 90-day action plan** — prioritized by impact and feasibility

For full report output (`.docx`), see `references/report-output.md`.
