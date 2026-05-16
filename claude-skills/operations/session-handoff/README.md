# session-handoff

**Category:** Operations  
**Trigger:** User wants to preserve and transfer working context before ending or handing off a session

---

## What It Does

Compacts an active working session into a portable handoff document that fully transfers context to the next person or session. Scans the full conversation to extract the goal hierarchy, established context (especially things that took multiple turns to build), artifacts produced, decisions made and why, current blockers, and specific next steps. The output must be complete enough that someone with zero prior context could continue intelligently.

---

## When to Use

- Ending a long session and wanting to pick it up later
- Handing work off to another person or team member
- Switching from one Claude session to another
- Creating a checkpoint before a context window gets too long
- Documenting a work session for project records

---

## Trigger Phrases

- `/handoff`
- "Compact this session"
- "Create a handoff document"
- "I need to hand this off"
- "Write a session summary for continuity"
- "Picking this up later — save the context"

---

## Key Inputs

| Input | Required? | Notes |
|---|---|---|
| Active conversation history | ✅ | The skill reads the full session |
| Recipient context | Optional | If handing to a specific person, adjust depth of background |

---

## Output

A clean markdown document with:
- **Current Goal** — one sentence, outcome-focused
- **Sub-Goals table** — each with ✅ / 🔄 / ⏳ / ⚠️ status
- **Context Register** — named list of things that took multiple turns to establish
- **Artifacts table** — every file, doc, or output with location and status
- **Decisions Made** — what was decided, why, and what it implies
- **Blockers & Open Items** — what's stuck vs. what's deferred
- **Suggested Next Steps** — specific and actionable, not "continue the work"

---

## What Makes This Different From a Summary

A summary tells you what happened. A handoff tells you what you need to know to continue. The Context Register is the key differentiator — it captures the shared understanding that accumulated over multiple turns and would take significant effort to re-establish without the conversation history.

---

## Example Context Register Entry

```
**Confidence scoring cap for vendor-authored documents**
The source bias rule caps all player self-assessments at MODERATE confidence when
the document is VENDOR_AUTHORED. This was established in turn 12 after the user
rejected a HIGH-confidence finding that was sourced from the vendor's own white paper.
All subsequent scoring must respect this constraint.
```
