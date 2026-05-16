---
name: proposal-deck-builder
version: 1.0.0
description: >
  Proposal Deck Builder — activate whenever a proposal, pitch deck, or client-facing presentation
  needs to be created for a prospect or client. Use when: a sales conversation is progressing to a
  formal proposal, leadership wants to send a deck before a first meeting, or any deliverable is a
  PowerPoint representing your organization's value to an external audience. Trigger for phrases
  like "build a proposal for", "create a deck for", "put together a pitch for", "we're pitching
  to", "make a proposal deck", "client proposal", or any request for a presentation for a named
  company. Orchestrates live client intelligence and value framing into a polished, company-specific
  .pptx.
---

# Proposal Deck Builder

Produces a **polished, company-specific PowerPoint proposal** for a prospect or client. Orchestrates live market intelligence and your organization's value framing into a professional, narrative-driven deck tailored to the prospect's industry, competitive position, and strategic priorities.

The output is a `.pptx` file ready for delivery — not a generic template, but a bespoke pitch grounded in the prospect's world.

---

## Workflow Overview

1. **Intake** — Identify the prospect, their context, and engagement goals
2. **Intelligence Layer** — Run live research to gather market and competitive signals
3. **Value Framing** — Map opportunity and narrative to your service portfolio
4. **Deck Architecture** — Design the slide structure and narrative arc
5. **Build the Deck** — Generate the `.pptx`
6. **QA & Deliver** — Verify output and present the file

---

## Step 1: Intake

Identify the following before proceeding. Extract from conversation context first; only ask for what is genuinely missing.

### Required
- **Prospect / Company name**
- **Industry / Vertical**
- **Proposed engagement type or offering** — What are you selling?

### Useful (pull from context or memory, ask once if unclear)
- **Known pain points, stated priorities, or tech initiatives**
- **Meeting or deadline context** — Is this for a specific meeting?
- **Tone calibration** — Executive / board-level? Practitioner-focused? Exploratory?
- **Any existing relationship or prior touchpoints**

If context is thin, proceed with industry-level assumptions and note them. Do not block on missing detail.

---

## Step 2: Intelligence Layer

Run a five-dimension client intelligence scan for this prospect. Use live web searches across:
1. Market & industry dynamics
2. Technology landscape
3. Competitive intelligence
4. Risk & threat signals
5. Innovation & opportunity signals

**From the scan, capture and tag:**
- 🏢 **Company-specific facts** — what is unique about this prospect's position or ambitions?
- 📉 **Pressure signals** — competitive threats, market headwinds, risk factors
- 📈 **Opportunity signals** — whitespace, investment activity, innovation windows
- 🎯 **Priority alignment signals** — where external dynamics map to their stated priorities
- ⚡ **Urgency signals** — timelines, competitive windows, regulatory deadlines

Maintain an internal source log. Only signals with traceable retrieved sources make it into the deck.

---

## Step 3: Value Framing

Using the intelligence gathered, produce:

1. **Client archetype classification** — What type of buyer are they?
2. **Primary pain diagnosis** — What is the core problem you're solving?
3. **Service mapping** — Which 1–3 of your offerings are most relevant?
4. **Primary offering recommendation** — What is the right entry point?
5. **Expansion path** — What 1–2 adjacent services naturally follow?
6. **Tailored narrative** — 1–2 sentences framing your value in this client's specific language

---

## Step 4: Deck Architecture

Design the slide structure before building. The narrative arc should follow this pattern:

### Standard Proposal Arc (8–12 slides)

| Slide | Purpose | Key Content |
|-------|---------|-------------|
| **Cover** | First impression | Company name, your brand, proposal title |
| **Who We Are** | Positioning | Your differentiation vs. traditional alternatives |
| **The Challenge** | Mirror prospect's world | Company-specific pain + industry pressure |
| **The Strategic Opportunity** | Why now | External signals + competitive window + cost of inaction |
| **Our Approach** | The answer | Primary offering framed around their situation |
| **Use Cases / Applications** | Make it concrete | 4–6 specific use cases grounded in their operations |
| **Layered Opportunity** | Depth of value | How the engagement unfolds over time |
| **Why Us** | Differentiation | 4–5 differentiators made specific to this client |
| **The Partnership** | What this becomes | Long-term partner, not one-time vendor |
| **Next Steps** | Call to action | 3 specific, named next steps |

**Adjust based on context:**
- Exploratory: lead with intelligence and landscape; keep offering slides light
- Deep proposal: heavier on use cases and layered opportunity
- Board-level: fewer slides, bigger ideas, less operational detail

---

## Step 5: Build the Deck

**Read `/mnt/skills/public/pptx/SKILL.md` before writing any code.**

### Design Principles

- **Color palette:** Use your organization's brand colors; create a consistent accent color pulled from the prospect's brand or industry where appropriate
- **Cover + section dividers:** Dark background, bold white type, minimal decoration
- **Content slides:** Light background, strong typographic hierarchy
- **Every content slide needs a visual element:** stat callout, 2×2 grid, icon row, comparison block, or timeline — never plain text-only
- **Stat callouts:** Large numbers (60–72pt) with small label below for impact metrics
- **Two-column layouts:** Left: narrative/framing; Right: insight cards, stat callouts, or use case grid
- **Consistent motif:** Pick one design element (rounded icon circles, card-style blocks, accent rules) and repeat

### Key Slide Notes

**Cover:** Prospect company name prominently. Proposal title below. Your branding bottom right. Clean, premium, minimal.

**The Challenge:** Split layout — left: company-specific pain bullets from intelligence scan; right: your answer framing the primary offering.

**Use Cases:** Grid layout — 2×3 or 3×2. Each cell: icon + title + 2-sentence description. Tag each card with a functional area (OPERATIONS / FRONT OFFICE / ENABLEMENT / etc.). Ground each use case in the prospect's actual context where known.

**Next Steps:** Numbered 1–2–3. Each step has a bold headline, 2-sentence description, and call-to-action label.

---

## Step 6: QA & Deliver

After building the deck:

1. Extract text and scan for: missing content, placeholder text, wrong names
2. Convert to images and visually inspect for: text overflow, overlapping elements, low contrast
3. Fix any visible issues (one fix-and-verify cycle)
4. Copy final file to `/mnt/user-data/outputs/[CompanyName]_Proposal_v1.pptx`
5. Present the file to the user

**Narrate a brief summary:** what the deck covers, the primary offering recommended, and one sentence on the intelligence-driven angle that makes it specific to this prospect.

---

## Source Integrity

All company-specific facts, statistics, competitive claims, and market signals in the deck must trace to:
- Live retrieved search results from the intelligence layer, OR
- Confirmed facts the user has provided

Do not fabricate competitor capabilities, market share figures, or technology adoption statistics. Use directional language ("competitors are accelerating AI investment") rather than fabricated numbers.

---

## Output Checklist

Before delivering:
- [ ] Intelligence scan completed across all five dimensions
- [ ] Source log maintained — every claim traces to a retrieved source
- [ ] Value framing produced — archetype, service mapping, narrative
- [ ] Deck architecture defined (slide count, narrative arc)
- [ ] Prospect's company name used throughout (no generic placeholders)
- [ ] Use cases grounded in prospect's known context
- [ ] Visual elements on every content slide
- [ ] Stat callouts on at least 2–3 slides
- [ ] QA complete — no overflow, no placeholder text
- [ ] File exported to `/mnt/user-data/outputs/`
- [ ] Presented via `present_files`

---

## Edge Cases

**Minimal prospect context available:**
Run broader industry intelligence; design slides around industry dynamics and typical pain points. Note assumptions inline.

**Prospect is a startup or emerging company:**
Shift narrative toward GTM, commercialization, and ecosystem access rather than enterprise transformation.

**Deck is exploratory / pre-proposal:**
Reduce to 6–8 slides. Lead with landscape intelligence. Keep offering language soft ("here's where we see opportunity") rather than prescriptive.

**Deck is for a board or C-suite audience:**
Maximum 8 slides, larger fonts, prioritize stat callouts and headline insights over operational detail, sharpen the "why now" urgency narrative.
