# competitive-dynamics

**Category:** Intelligence  
**Trigger:** Requests to map competitive landscape, extract player positioning, or analyze who's winning/losing from a document

---

## What It Does

Extracts and structures competitive dynamics from source documents. Produces a structured JSON record covering every named player's positioning, differentiation claims (evidence-backed vs. assertion-only), competitive relationships, pricing patterns, win/loss indicators, consolidation signals, and white space opportunities. Closes with a market structure synthesis.

---

## When to Use

- Analyzing an analyst report, white paper, RFP, or case study for competitive signals
- Mapping who the key players are in a defined market
- Identifying displacement patterns (who's replacing whom and why)
- Finding white space — unmet needs no current player is addressing well
- Building a competitive landscape briefing from document content

---

## Trigger Phrases

- "Map the competitive dynamics in this document"
- "Who are the key players here?"
- "Extract competitive positioning"
- "Who's winning and losing?"
- "Is there consolidation happening?"
- "What's the pricing pattern in this market?"

---

## Key Inputs

| Input | Required? | Notes |
|---|---|---|
| Source document | ✅ | Any format — analyst report, white paper, case study, press coverage |

---

## Output

Structured JSON record with:
- Per-player profiles (positioning archetype, differentiation claims, displacement signals)
- Competitive relationship map (head-to-head pairs with advantage assessment)
- Pricing patterns, win/loss indicators, consolidation signals
- White space opportunities (classified as EXPLICIT or INFERRED)
- Market structure synthesis (3–5 sentence executive read)
- Confidence scores and human review flags

---

## Quality Guarantee

Every differentiation claim is classified as `EVIDENCE_BACKED` or `ASSERTION_ONLY`. No claim is marked evidence-backed based solely on vendor-supplied data. Findings without document support are flagged for human review rather than included as facts.

---

## Example JSON Snippet

```json
{
  "players": [{
    "name": "Acme Platform",
    "positioning_archetype": "PERFORMANCE_LEADER",
    "differentiation_claims": [{
      "claim": "3x faster inference than nearest competitor",
      "evidence_classification": "EVIDENCE_BACKED"
    }],
    "confidence": 0.85
  }],
  "white_space_opportunities": [{
    "gap_description": "No player addresses mid-market buyers with sub-$50K budgets",
    "gap_type": "EXPLICIT"
  }]
}
```
