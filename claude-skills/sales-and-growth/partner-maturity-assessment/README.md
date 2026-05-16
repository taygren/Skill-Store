# partner-maturity-assessment

**Category:** Sales & Growth  
**Trigger:** Any request to assess, audit, score, or benchmark a company's partner program, channel strategy, or ecosystem

---

## What It Does

Evaluates the depth, breadth, presence, and sophistication of a technology company's partner ecosystem and go-to-market programs. Scores seven partner types (OEM, ISV, Hyperscaler, VAR, Distributor, SI, MSP) across five dimensions (Presence, Depth, Breadth, Enablement, GTM Activation) into a composite 0–100 maturity score. Identifies critical gaps (P0/P1/P2) and strategic GTM opportunities across each partner motion.

---

## When to Use

- Evaluating a vendor's channel before partnering, investing, or competing with them
- Auditing your own partner program to find the highest-leverage gaps
- Benchmarking a company's ecosystem maturity against peers
- Building a partner strategy or go-to-market roadmap

---

## Trigger Phrases

- "Assess [company]'s partner program"
- "How mature is [company]'s channel?"
- "Does [company] have a strong hyperscaler motion?"
- "Partner program audit for [company]"
- "Benchmark [company] vs [peer] on ecosystem"

---

## Commands

| Command | What It Does |
|---|---|
| `/partner assess <company>` | Full 7-type assessment with scores and GTM analysis |
| `/partner quick <company>` | 5-minute ecosystem snapshot |
| `/partner type <company> <type>` | Deep-dive on a single partner type |
| `/partner gtm <company>` | Strategic GTM opportunity analysis |
| `/partner benchmark <company> <peer>` | Side-by-side maturity comparison |
| `/partner report <company>` | Executive-ready `.docx` deliverable |

---

## Scoring System

**7 Partner Types:** OEM · ISV/Tech Alliances · Hyperscalers · VARs · Distributors · SIs · MSPs

**5 Assessment Dimensions per type:**
- Presence (20%) · Depth (25%) · Breadth (20%) · Enablement (20%) · GTM Activation (15%)

**Composite Score Scale:**
`0–24 Absent` · `25–39 Nascent` · `40–54 Emerging` · `55–69 Developing` · `70–84 Advanced` · `85–100 Elite`

---

## Example Quick Output

```
🤝 OEM:           Nascent    — No embedded OEM relationships found
🔗 ISV/Alliances: Advanced   — 200+ integrations; strong Salesforce/AWS co-sell
☁️ Hyperscalers:  Developing — AWS listing active; Azure and GCP minimal
🏪 VARs:          Emerging   — ~50 VARs; no MDF program documented
📦 Distributors:  Absent     — No two-tier distribution motion
🔧 SIs:           Advanced   — Accenture and Deloitte named partners
🛠️ MSPs:          Nascent    — No MSP-specific program or pricing

Composite Maturity: 58/100 — Developing
Top P0 Gap: No distributor motion limits scale outside direct sales coverage
Top GTM Opportunity: Formalize MSP program to capture recurring revenue channel
```
