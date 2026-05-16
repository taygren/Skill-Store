---
name: client-intelligence-scan
version: 1.0.0
description: >
  Client Intelligence Scan — activate whenever an engagement requires real-time, client-tailored
  intelligence across market, technology, vertical, or competitive dimensions. Use when: preparing
  for a client meeting or QBR, building a proactive insight briefing for a specific account,
  onboarding a new client and needing to understand their landscape, identifying what's changed in
  a client's world since last engagement, or when a client asks "what should we be paying attention
  to?". Trigger for any request involving a named client, company, or industry combined with
  intelligence, trends, risks, or landscape — even if phrased casually ("what's going on in
  [client's space]", "catch me up on [client's industry]", "what should I know before my call with
  [client]").
---

# Client Intelligence Scan

Produces a **real-time, client-tailored intelligence briefing** that surfaces actionable trends, risks, opportunities, and competitive dynamics relevant to a specific client or company. Designed for consultants, account managers, and advisors preparing for engagements and anticipating client needs.

---

## Workflow Overview

1. **Intake** — Capture client context and scan dimensions
2. **Live Research** — Run targeted searches across five intelligence dimensions
3. **Synthesize** — Build client-specific insight layer filtered through their lens
4. **Render** — Produce a visual intelligence briefing as an HTML artifact

---

## Source Integrity Protocol

**This skill operates under a strict source integrity rule. Every data point, statistic, report finding, or named development in the output must trace directly to a live web search result retrieved during this session.**

### What this means in practice:

- **Do not invent sources.** Do not reference a Gartner report, McKinsey study, IDC forecast, or any named publication unless you have a retrieved URL or concrete snippet from it in your search results.
- **Do not fabricate statistics.** If you cannot find a real, retrieved number, do not use one. Use directional language instead ("adoption is accelerating," not "adoption grew 47% in 2024").
- **Do not hallucinate recency.** Do not add 🆕 flags to signals you cannot anchor to a retrieved result from the last 30–90 days.
- **Source log is required.** Before synthesis, maintain an internal running log of what you actually retrieved — URL, publication, and the specific claim it supports. Only draw from this log when writing signal bullets.
- **When searches return thin results:** Acknowledge the gap explicitly rather than filling it with inferred or training-based content. Flag the entire dimension card with ⚠️.
- **Fabrication is a worse outcome than a gap.** A missing bullet is recoverable. A fabricated statistic delivered to a client is not.

### Source log format (maintain internally, do not render):
```
[Dimension] | [URL or publication] | [Specific claim retrieved]
```

---

## Step 1: Intake

Identify the following before scanning. Extract from conversation context first; only ask if genuinely missing.

### Required
- **Client / Company name** — Who is this scan for?
- **Client's primary industry / vertical** — e.g., financial services, healthcare, retail, manufacturing

### Useful (pull from memory or ask once)
- **Client's known technology priorities or active initiatives** (e.g., AI adoption, cloud migration, data modernization)
- **Known pain points or strategic pressures** the client has expressed
- **Recency window** — default: last 90 days; extend to 6 months for slower-moving verticals

If none of this is available, proceed with industry-level defaults and note assumptions.

---

## Step 2: Live Research — Five Intelligence Dimensions

**Always run live web searches.** Do not rely on training data alone. Searches should be targeted, not generic.

After each search, log what you retrieved (URL, source, claim) before moving to the next dimension. If a search returns no usable results, note the gap — do not substitute training knowledge as if it were a retrieved source.

**Research posture:** Lead with what is *actually happening externally* — in the market, the technology landscape, the competitive environment. Gather the real signal first, then apply client relevance in Step 3.

---

### Dimension 1: Market & Industry Dynamics
*What is happening in this client's market right now?*

Search targets:
- `"[industry] market trends [year]"`
- `"[industry] outlook [year]"`
- `"[industry] challenges [year]"`
- Regulatory or macroeconomic signals: `"[industry] regulation [year]"` or `"[industry] economic pressure"`

Synthesize for: Structural shifts, demand changes, regulatory headwinds/tailwinds, macroeconomic pressures.

---

### Dimension 2: Technology Landscape
*What technology developments are most relevant to this client's priorities?*

Search targets:
- If client has known tech priorities: `"[tech area] enterprise [year]"` or `"[tech area] adoption [industry]"`
- General: `"[industry] technology trends [year]"` or `"[industry] digital transformation [year]"`
- Emerging: `"[industry] AI [year]"`, `"[industry] automation [year]"`

Synthesize for: Capability releases, adoption benchmarks, emerging tools relevant to client's stack or roadmap.

---

### Dimension 3: Competitive Intelligence
*What are this client's competitors doing?*

Search targets:
- `"[client company] competitors [year]"`
- `"[client industry] competitive landscape [year]"`
- Moves by named competitors if known: `"[competitor] announcement [year]"`
- `"[industry] market share [year]"` or `"[industry] consolidation"`

Synthesize for: Competitive moves that create pressure or opportunity, shifts in market positioning, M&A activity.

---

### Dimension 4: Risk & Threat Signals
*What risks could blindside this client?*

Search targets:
- `"[industry] risks [year]"` or `"[industry] vulnerabilities [year]"`
- `"[industry] cybersecurity [year]"` if relevant
- `"[industry] supply chain [year]"` or `"[industry] talent [year]"` as context warrants
- `"[industry] AI risk"` or `"[industry] compliance [year]"`

Synthesize for: Emerging threat vectors, compliance/regulatory risk, operational vulnerabilities.

---

### Dimension 5: Innovation & Opportunity Signals
*Where is there greenfield opportunity relevant to this client?*

Search targets:
- `"[industry] innovation [year]"` or `"[industry] investment [year]"`
- `"[industry] startup activity"` or `"[industry] venture funding [year]"`
- `"[industry] growth opportunity [year]"` or `"[industry] whitespace"`

Synthesize for: Emerging business models, unaddressed needs, investment thesis signals.

---

## Step 3: Synthesize — External Signal First, Client Relevance Second

**Before writing any synthesis, review your source log.** Only include claims anchored to retrieved sources.

### Pass 1: What is actually happening? (External-first)

For each dimension, characterize the external environment on its own terms — independent of this client. Ask:

> *"What are the most significant developments, shifts, or signals in this space right now?"*

### Pass 2: What does this mean for this client? (Relevance layer)

Once the external picture is clear, apply a **client-specific relevance filter**. Ask:

> *"Given what we know about this client — their priorities, stage, pain points — which of these external dynamics matter most to them, and why?"*

### For each dimension, produce:
1. **What's happening** (1–2 sentences): A crisp, external-first characterization of the key development.
2. **Why it matters for [client]** (1–2 sentences): The specific relevance to their situation.
3. **Key signals** (3–5 bullets): Each bullet leads with the external fact, then closes with the client implication. Every bullet must have a linked source attribution.
   - Source format: `<a href="[retrieved URL]">[Publication, Date]</a>`
   - Flag: 🆕 signals from the last 30–90 days (only if the retrieved source confirms recency)
   - Flag: ⚡ high-stakes or high-urgency signals
   - Flag: 🎯 directly tied to a known client priority or pain point
   - Flag: ⚠️ dimension where live search returned limited results — treat as directional

### Cross-Dimension Synthesis
Identify 2–3 patterns that cut across dimensions — these are the highest-value outputs. They should reflect compounding external dynamics, not just a summary of each section.

---

## Step 4: Render — Visual Intelligence Briefing

Produce a **visual HTML artifact** that reads like a premium analyst briefing customized for this client — not a generic market report.

The artifact should include:
- A header with client name, industry, and scan date
- One card per intelligence dimension with signals and source links
- A cross-dimension synthesis section
- A "Key Watch Items" summary panel

---

## Output Checklist

Before delivering:
- [ ] Live web searches performed across all five dimensions
- [ ] Source log maintained — every signal bullet traces to a retrieved result
- [ ] No statistics or findings included that were not retrieved in this session
- [ ] Dimensions with thin search results flagged with ⚠️
- [ ] All signal bullet source attributions link to real retrieved URLs
- [ ] Client-specific filter applied (not just generic industry summary)
- [ ] 🆕 flags used only where retrieved source confirms recency
- [ ] Cross-dimension synthesis produced only from sourced signals
- [ ] Visual HTML artifact rendered

---

## Edge Cases

**Client is well-known (Fortune 500):**
Search for them directly: `"[company name] strategy [year]"`, `"[company name] technology"` — supplement with industry signals.

**Client is niche or private:**
Focus on their vertical and competitive tier rather than the company directly. Note the limitation explicitly.

**No known client priorities:**
Run a broader industry scan and close with: *"To sharpen this briefing, it would help to know [client]'s current technology focus areas."*

**Client spans multiple industries:**
Scope to the business unit or use-case most relevant to the engagement. Flag that a multi-vertical scan may be warranted.

**Urgency / meeting prep context:**
Prioritize the most client-relevant signals from each dimension, reduce depth, and surface 3–5 "talking points" as a fast-read layer at the top of the briefing.
