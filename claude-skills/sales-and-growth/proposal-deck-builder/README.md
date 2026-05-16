# proposal-deck-builder

**Category:** Sales & Growth  
**Trigger:** Any request to build a proposal deck, pitch presentation, or client-facing PowerPoint for a prospect

---

## What It Does

Produces a polished, company-specific `.pptx` proposal by orchestrating three steps: live five-dimension client intelligence research, value/service framing mapped to the prospect's situation, and a fully built PowerPoint following a standard 8–12 slide narrative arc. The result is a bespoke pitch grounded in the prospect's actual market context — not a generic template with names swapped in.

---

## When to Use

- A sales conversation is progressing to a formal proposal
- You want to send a deck before a first meeting
- You're building a pitch for a named prospect or client
- You need an intelligence-driven, visually polished deck fast

---

## Trigger Phrases

- "Build a proposal for [company]"
- "Create a deck for [prospect]"
- "Put together a pitch for [company]"
- "Make a proposal deck for [client]"
- "We're pitching to [company] — build the deck"

---

## Key Inputs

| Input | Required? | Notes |
|---|---|---|
| Prospect / company name | ✅ | |
| Industry / vertical | ✅ | |
| Proposed offering or engagement type | ✅ | What are you selling? |
| Known pain points or priorities | Optional | Sharpens use cases |
| Tone / audience level | Optional | Default: executive-appropriate |

---

## Output

A `.pptx` file with:
- Cover, positioning, challenge, strategic opportunity, approach, use cases, layered opportunity, differentiators, partnership, next steps
- Visual elements on every content slide (no text-only slides)
- Stat callouts, two-column layouts, icon grids
- All claims sourced from live web research

---

## Configuring for Your Organization

Before first use, update the `SKILL.md` with:
- Your brand colors and design system
- Your service offerings and pillar names
- Your differentiator language
- Your archetype narrative framing

The slide structure and intelligence workflow are universal; the content specifics are yours to define.

---

## Dependencies

- Requires `pptx` skill for deck generation
- Requires web search for intelligence layer
- Works best when paired with `value-opportunity-gateway` for service framing
