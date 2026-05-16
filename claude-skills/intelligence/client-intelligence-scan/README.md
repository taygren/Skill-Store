# client-intelligence-scan

**Category:** Intelligence  
**Trigger:** Any request involving a named client, company, or industry + intelligence, trends, risks, or landscape

---

## What It Does

Produces a real-time, five-dimension intelligence briefing tailored to a specific company or client. Pulls live signals across market dynamics, technology landscape, competitive intelligence, risk signals, and innovation opportunities — then synthesizes them into a client-relevant analyst briefing rendered as an HTML artifact.

Designed for consultants, account managers, and advisors who need to walk into a meeting fully briefed on what's happening in a client's world.

---

## When to Use

- Preparing for a client meeting, QBR, or discovery call
- Building a proactive insight briefing for an account
- Onboarding a new client and mapping their landscape
- Answering: *"What should we be paying attention to?"*

---

## Trigger Phrases

- "What's going on in [client's] space?"
- "Catch me up on [industry]"
- "What should I know before my call with [company]?"
- "Run an intelligence scan on [company]"
- "Build me a briefing for [client]"

---

## Key Inputs

| Input | Required? | Notes |
|---|---|---|
| Company / client name | ✅ | |
| Industry / vertical | ✅ | |
| Known tech priorities or pain points | Optional | Sharpens relevance layer |
| Recency window | Optional | Default: 90 days |

---

## Output

An HTML artifact structured as a premium analyst briefing:
- Five intelligence dimension cards with sourced signal bullets
- Cross-dimension synthesis (2–3 compounding patterns)
- Key Watch Items summary panel
- All claims linked to live retrieved sources

---

## Source Integrity

This skill enforces strict source integrity. Every signal traces to a live web search result from the current session. No fabricated statistics, no hallucinated report citations, no training-data-as-research. Dimensions with thin search results are flagged with ⚠️ rather than gap-filled.

---

## Example Output Snapshot

```
📊 INTELLIGENCE BRIEFING: Acme Corp | Manufacturing | Scanned: May 2026

DIMENSION 1: Market & Industry Dynamics
What's happening: Tariff volatility is compressing margins across mid-market manufacturers...
Why it matters for Acme: Their heavy reliance on Southeast Asian suppliers puts them in the highest-exposure tier...

🆕 [Reuters, Apr 2026] New tariff schedule...  🎯 [Industry Week, Mar 2026] Automation ROI...
```
