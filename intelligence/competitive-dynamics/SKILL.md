---
name: competitive-dynamics
version: 1.0.0
description: >
  Identifies and structures competitive dynamics from source documents. Extracts key players,
  market positioning, differentiation signals, competitive displacement, pricing patterns,
  win/loss indicators, and consolidation activity. Maps how vendors and solutions relate to and
  compete with each other within a defined market. Use when a user says "map the competitive
  dynamics," "who are the key players in these docs," "extract competitive positioning,"
  "identify displacement signals," "what's the pricing pattern," "who's winning and losing,"
  "is there consolidation happening," or asks for any competitive landscape analysis from
  document content. All analysis is grounded in source material only — no hallucinated signals.
---

# Competitive Dynamics Analysis

Identifies and structures **competitive dynamics** from source documents. Produces a discrete, structured JSON output record covering key players, market positioning, differentiation signals, competitive displacement, pricing patterns, win/loss indicators, and consolidation activity.

The defining quality standard: **differentiation claims must be classified as evidence-backed or assertion-only**. Vendor-stated differentiation and independently verified differentiation are not the same thing.

All analysis is **document-driven**. Every finding must be traceable to content in the source document.

---

## Workflow Overview

1. **Stage the source document** and assess content quality
2. **Identify all players** named or clearly implied in the document
3. **Extract positioning, differentiation, and displacement signals** for each player
4. **Map competitive relationships** between players
5. **Extract pricing, win/loss, and consolidation signals**
6. **Identify white space** — gaps no player is filling
7. **Synthesize market structure** across all extracted signals
8. **Output structured JSON** and flag gaps for human review

---

## Pre-Analysis Setup

### Source Staging
- Identify the source document: file name, document type, ingestion date
- Note document characteristics: length, format density, technical vs. general content, recency signals
- Capture any metadata already extracted (title, author, date, source organization)

### Content Quality Assessment
Rate the source document on two axes:
- **Signal Density**: High / Medium / Low — how many substantive, extractable competitive signals does the document contain?
- **Recency**: Current (within 12 months) / Recent (1–3 years) / Dated (3+ years) / Unknown

### Source Bias Assessment
Classify the document source and apply the appropriate bias flag:
- `VENDOR_AUTHORED` — produced by one of the players in the competitive landscape. All self-promotional claims are assertion-only unless independently corroborated.
- `ANALYST_AUTHORED` — produced by an independent research firm. Competitive assessments carry higher weight but note known coverage biases.
- `CUSTOMER_AUTHORED` — produced by a buyer organization (case study, RFP, procurement analysis). Win/loss signals are most credible here.
- `PRESS_OR_MEDIA` — news coverage or trade publication. Verify sourcing within the document.
- `UNKNOWN`

---

## Part A: Player Extraction

For each vendor, product, platform, or solution named or clearly implied in the document:

### Field 1: Player Profile
- `name` — the vendor or product name as it appears in the document
- `category` — classify as: VENDOR / PLATFORM / OPEN_SOURCE_PROJECT / SYSTEMS_INTEGRATOR / HYPERSCALER / STARTUP / INCUMBENT
- `market_segment` — the specific segment this player occupies as described in the document
- `target_buyer` — the buyer profile this player appears to serve (if discernible)

### Field 2: Positioning Archetype
Classify how this player positions itself in the market:
- `PRICE_LEADER` — competing primarily on cost
- `PERFORMANCE_LEADER` — competing on technical capability, speed, or measurable outcomes
- `EASE_OF_USE` — competing on simplicity, deployment speed, or user experience
- `ECOSYSTEM_PLAY` — competing through integrations, partnerships, and platform lock-in
- `VERTICAL_SPECIALIST` — competing through deep industry-specific functionality
- `FULL_STACK` — competing by offering end-to-end coverage of a workflow or problem
- `CHALLENGER` — explicitly positioned against a dominant incumbent
- `UNKNOWN` — insufficient evidence to classify

### Field 3: Positioning Language
Extract the specific language used in the document to describe how this player positions itself. Use direct quotes or close paraphrases from the source. Do not substitute your own positioning summary.

### Field 4: Differentiation Claims
List the specific claims this player (or the document author) makes about what sets this player apart. For each claim:
- State the claim
- Classify as `EVIDENCE_BACKED` or `ASSERTION_ONLY`
  - `EVIDENCE_BACKED` — the document provides a customer reference, benchmark, case study, or independent validation
  - `ASSERTION_ONLY` — the claim is made but no supporting evidence is provided

**Hard rule:** Never mark a differentiation claim as EVIDENCE_BACKED based on vendor-supplied data alone.

### Field 5: Displacement Signals
Evidence that this player is displacing a competitor — or being displaced:
- Who is displacing whom
- The mechanism (price / capability / integration / brand / ecosystem / regulatory)
- The evidence basis from the document

---

## Part B: Competitive Relationship Mapping

### Field 6: Head-to-Head Relationships
For each explicitly stated or clearly implied competitive pair:
- `player_a` and `player_b`
- `competitive_axis` — PRICE / CAPABILITY / ECOSYSTEM / VERTICAL / FULL_STACK_VS_POINT_SOLUTION / OTHER
- `advantage_holder` — which player appears to hold competitive advantage, or `CONTESTED`
- `advantage_basis` — the specific reason one player holds advantage as described in the document
- `evidence` — what in the document supports this assessment

Only extract relationships explicitly stated or strongly implied. Do not invent competitive relationships.

---

## Part C: Pricing, Win/Loss, and Consolidation

### Field 7: Pricing Patterns
Extract any pricing signals present in the document:
- Specific pricing tiers, models, or ranges mentioned
- Pricing pressure or commoditization signals
- Premium pricing justification signals
- Freemium or land-and-expand patterns
- Consumption-based or usage-based pricing signals

If no pricing signals are present, return an empty array.

### Field 8: Win/Loss Indicators
Signals of competitive outcome:
- Named customer wins (player chosen over a competitor)
- Named displacement stories
- Reference accounts or logo lists
- Churn or loss signals
- Competitive RFP win/loss mentions

Classify each indicator as `WIN` or `LOSS` from the perspective of the named player.

### Field 9: Consolidation Signals
Signs that the competitive landscape is concentrating:
- M&A activity
- Strategic partnerships that reduce independent competition
- Platform absorption
- Investment activity concentrating around fewer players

### Field 10: White Space
Areas where the document suggests unmet need, underserved buyer segments, or capability gaps no current player is filling well. For each white space:
- Describe the gap or unmet need
- Identify the underserved buyer segment
- Note supporting evidence from the document
- Classify as `EXPLICIT` (document states the gap directly) or `INFERRED`

---

## Market Structure Synthesis

Write a `market_structure_summary`:
- A 3–5 sentence executive read on how this market is structured competitively
- Who is leading, who is challenging, who is being displaced
- Whether the market appears to be consolidating, fragmenting, or stable
- The dominant competitive axis (price, capability, ecosystem, or other)

---

## Confidence Scoring Framework

| Score | Label | Meaning |
|-------|-------|---------|
| 0.9–1.0 | **HIGH** | Multiple explicit statements; quantitative data present; corroborated across sections |
| 0.7–0.89 | **MODERATE-HIGH** | Clear statement; some supporting context; limited quantitative data |
| 0.5–0.69 | **MODERATE** | Present in document but limited context; single mention |
| 0.3–0.49 | **LOW-MODERATE** | Implied or inferred; not directly stated |
| 0.0–0.29 | **LOW** | Highly inferred; minimal textual basis |

**Rules:**
- VENDOR_AUTHORED documents cap player self-assessments at MODERATE confidence
- ASSERTION_ONLY differentiation claims cap at MODERATE-HIGH
- Competitive relationships without explicit document evidence cap at LOW-MODERATE
- Never assign HIGH confidence to advantage claims sourced only from the player making them

---

## Human Review Flag Conditions

Set `human_review_flag: true` when:
- Signal Density = Low (fewer than 2 named players with extractable competitive signals)
- Document is VENDOR_AUTHORED and all competitive claims favor only the authoring vendor
- More than 50% of differentiation claims are ASSERTION_ONLY
- No competitive relationships can be mapped
- More than 50% of findings score below 0.4 confidence
- Document recency is Dated (3+ years old)

---

## JSON Output Schema

```json
{
  "analysis_type": "COMPETITIVE_DYNAMICS",
  "document_id": "",
  "document_title": "",
  "analysis_date": "",
  "signal_density": "",
  "document_recency": "",
  "source_bias": "",
  "players": [
    {
      "player_id": "",
      "name": "",
      "category": "",
      "market_segment": "",
      "target_buyer": "",
      "positioning_archetype": "",
      "positioning_language": "",
      "differentiation_claims": [
        {
          "claim": "",
          "evidence_classification": ""
        }
      ],
      "displacement_signals": [
        {
          "direction": "",
          "mechanism": "",
          "evidence": ""
        }
      ],
      "confidence": 0.0
    }
  ],
  "competitive_relationships": [
    {
      "player_a": "",
      "player_b": "",
      "competitive_axis": "",
      "advantage_holder": "",
      "advantage_basis": "",
      "evidence": ""
    }
  ],
  "pricing_patterns": [],
  "win_loss_indicators": [
    {
      "player": "",
      "outcome": "",
      "indicator_type": "",
      "evidence": ""
    }
  ],
  "consolidation_signals": [],
  "white_space_opportunities": [
    {
      "gap_description": "",
      "underserved_segment": "",
      "supporting_evidence": "",
      "gap_type": ""
    }
  ],
  "market_structure_summary": "",
  "knowledge_gaps": [],
  "human_review_flag": false,
  "human_review_reason": ""
}
```

---

## Quality Checklist

Before finalizing output, verify:
- [ ] Every player has a `positioning_archetype` classification
- [ ] Every differentiation claim has an `evidence_classification`
- [ ] No differentiation claim is marked EVIDENCE_BACKED based solely on vendor-provided data
- [ ] `competitive_relationships` only contains explicitly stated or strongly implied pairs
- [ ] `white_space_opportunities` are classified as EXPLICIT or INFERRED
- [ ] `market_structure_summary` is a synthesis, not a player list
- [ ] `source_bias` is populated and influences confidence scoring
- [ ] `human_review_flag` is evaluated — never left as a default false

---

## Edge Cases

**Document is vendor-authored:**
Set `source_bias: "VENDOR_AUTHORED"`. All self-promotional claims are ASSERTION_ONLY. Still extract fully — vendor framing is itself competitive intelligence.

**Document is an analyst report (Gartner, Forrester, IDC):**
Highest-yield document type. Player positioning and relationships can carry MODERATE-HIGH to HIGH confidence. Note analyst methodology limitations.

**Document is a customer case study:**
Win/loss indicators are most credible. Be cautious: case studies are typically vendor-curated.

**Document is press or news:**
M&A signals and financial signals are credible. Competitive positioning claims from quoted executives are ASSERTION_ONLY.

**Document names only one player:**
Competitive relationship mapping will be sparse. Note in `knowledge_gaps`: "Document focuses on a single vendor — competitive landscape view is one-sided."

**Document is dated (3+ years old):**
Set `document_recency: "DATED"` and `human_review_flag: true`. Note: "Competitive positions may be materially outdated."
