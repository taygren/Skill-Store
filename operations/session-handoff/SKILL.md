---
name: session-handoff
version: 1.0.0
description: >
  Session Handoff — activate when a user wants to preserve and transfer the working context of
  a conversation so that another person, another Claude session, or a future self can continue
  without starting over. Trigger when the user says "/handoff", "compact this session",
  "create a handoff", "summarize for continuity", "I need to hand this off", "picking this up
  later", "write a handoff doc", or any variation of wanting to capture session state before
  ending or transferring work. Produces a structured handoff document covering current goals,
  established context, artifacts produced, decisions made, blockers, and recommended next steps.
  The output must be complete enough that someone with zero prior context could continue the
  work intelligently without asking clarifying questions.
---

# Session Handoff

Compacts an active working session into a **clean, portable handoff document** that fully transfers context to the next person or session. The output must stand alone — whoever picks this up should be able to continue intelligently without reviewing the original conversation.

---

## Workflow Overview

1. **Scan** — Read the full conversation to extract all relevant context signals
2. **Reconstruct** — Identify the goal hierarchy, established context, and decision trail
3. **Inventory** — Catalog all artifacts produced with locations and states
4. **Compress** — Distill context that took multiple turns to establish
5. **Assess** — Surface blockers and sharpen next steps
6. **Render** — Produce the handoff document as a clean markdown artifact

---

## Step 1: Scan the Conversation

Before writing anything, read the full conversation history with these extraction goals:

**Goal signals:** What is the person ultimately trying to accomplish? What sub-goals support it?

**Context signals:** What did it take multiple turns to establish? What does the current executor know that a newcomer wouldn't? What assumptions, constraints, or decisions became shared understanding over time?

**Artifact signals:** What was produced? Files, documents, code, decks, analysis outputs — anything with a path, link, or named artifact.

**Decision signals:** What choices were made, and what was the reasoning? Pay attention to forks — places where multiple options were considered and one was selected.

**Blocker signals:** What is unresolved, pending, or stuck? What was deferred?

**Progress signals:** What's done vs. what's still open?

Do not begin writing the handoff until you have read the full conversation. Partial reading produces incomplete handoffs.

---

## Step 2: Reconstruct the Goal Hierarchy

Map the work into a two-level goal structure:

**Current Goal** — The primary outcome this session is working toward. One sentence, outcome-focused, not task-focused.
> *Not:* "Building a competitive intelligence dashboard"
> *Yes:* "Deliver a competitive intelligence dashboard covering Chicago mental health nonprofits for FountainHouse's market entry decision"

**Sub-Goals** — The specific components or milestones that make up the current goal. Each should be:
- Concrete and verifiable (you can tell when it's done)
- Marked with status: ✅ Complete / 🔄 In Progress / ⏳ Not Started / ⚠️ Blocked

If the work has already achieved a current goal and moved to a new phase, reflect that accurately — don't flatten a multi-phase project into a single goal.

---

## Step 3: Extract Established Context

This is the most valuable and most frequently lost part of a session.

Identify every piece of context that:
- Required multiple turns of conversation to establish
- Is not obvious from the task description alone
- Would require significant effort to re-establish without the conversation history
- Represents a constraint, preference, or decision that shapes all future work

**Categories to check:**
- **Technical constraints** — stack, format, file naming, environment, limitations discovered
- **Content decisions** — tone, audience, framing choices, what's in/out of scope
- **Client/stakeholder context** — preferences, sensitivities, prior interactions, relationship dynamics
- **Domain knowledge** — what was explained, what terminology was aligned on
- **Process decisions** — the approach taken, methodology chosen, workflow agreed on
- **Correction history** — what was tried and abandoned, what the person explicitly rejected

Write this as a **Context Register** — a named list of context items, each with a 1–2 sentence explanation of why it matters going forward.

---

## Step 4: Inventory Artifacts

List every artifact produced in the session. For each:

| Artifact | Type | Location / Path | Status | Notes |
|---|---|---|---|---|
| [Name] | [doc / code / deck / analysis / etc.] | [path, URL, or "in conversation"] | ✅ Final / 🔄 Draft / ⏳ Placeholder | [anything a new person needs to know] |

**Artifact types to check for:** files created, code written, documents drafted, decks built, analysis outputs, configurations set, templates established, prompts developed.

If an artifact is in the conversation but not saved to a file, note that explicitly — the next session may need to extract and save it.

---

## Step 5: Document Decisions and Blockers

### Decisions Made
For each meaningful decision (not every micro-choice — the ones that shaped direction):

**[Decision name]**
- **What was decided:** [The choice made]
- **Why:** [The reasoning or constraints that drove it]
- **Implications:** [What this decision forecloses or requires going forward]

Focus on decisions that a new executor might question or reverse without knowing the reasoning. Include rejected alternatives if they're worth remembering.

### Blockers & Open Items
**Blockers** — things actively preventing progress:
- [Blocker description] | Blocked on: [what/who] | Since: [when if known]

**Open Items** — things deferred, unresolved, or needing follow-up:
- [Item] | Status: [deferred / needs decision / needs input / waiting on X]

---

## Step 6: Render the Handoff Document

Produce a **clean markdown artifact** using the structure below. The document should be readable in 3–5 minutes by someone picking up cold.

---

### Handoff Document Structure

```markdown
# Handoff: [Project / Session Name]
*Prepared: [Date] | Session by: [if known, or "AI-assisted session"]*

---

## Current Goal
[One sentence. Outcome-focused.]

## Sub-Goals

| Sub-Goal | Status | Notes |
|---|---|---|
| [Sub-goal 1] | ✅ / 🔄 / ⏳ / ⚠️ | |
| [Sub-goal 2] | | |

---

## Context Register
*What took multiple turns to establish — essential for continuity.*

**[Context item name]**
[1–2 sentences explaining what it is and why it matters going forward.]

**[Context item name]**
[...]

---

## Artifacts

| Artifact | Type | Location | Status | Notes |
|---|---|---|---|---|
| | | | | |

---

## Decisions Made

**[Decision name]**
- Decided: [what]
- Why: [reasoning]
- Implications: [what this means going forward]

---

## Blockers & Open Items

**Blockers:**
- [Blocker] — waiting on [X]

**Open:**
- [Item] — [status]

---

## Suggested Next Steps

1. [First thing the next person should do — specific and actionable]
2. [Second step]
3. [Third step]

*Tip for whoever picks this up: [One sentence of orientation — the most important thing to know before diving in.]*

---

## Raw Context Dump *(optional — include if session was long or complex)*
[Any additional context, background, or notes that didn't fit cleanly into the above sections but would help a new executor.]
```

---

## Quality Checklist

Before delivering the handoff:
- [ ] Goal is outcome-focused, not task-focused
- [ ] Every sub-goal has a status
- [ ] Context Register contains the things that *took multiple turns to establish* — not just background info
- [ ] Every artifact has a location (even if "in conversation") and status
- [ ] Every significant decision includes reasoning, not just what was decided
- [ ] Blockers are distinguished from open items
- [ ] Next steps are specific and actionable — not "continue the work"
- [ ] A person with zero prior context could read this and start working in under 5 minutes

---

## Edge Cases

**Session was very long (50+ turns):**
Prioritize depth of Context Register and Decisions. A long session accumulated a lot of shared understanding — that's what the handoff must preserve. The artifact inventory and next steps can be brief; the context is the asset.

**Session produced no files (all work is in conversation):**
Note each major output in the artifact table with location "in conversation" and enough description that someone can find it by scrolling. Recommend saving key outputs as files as a first step.

**Session ended mid-task (not at a natural stopping point):**
Be explicit in the Current Goal status that work is mid-stream. The Context Register becomes even more critical — capture the working state, not just the end state.

**Multiple independent workstreams in one session:**
Produce a sub-goal table that makes the separation clear. Consider a separate Context Register section per workstream if they're sufficiently independent.

**Handoff is for a different person (not a future self):**
Add a "Who's picking this up" field if known and adjust the orientation tip accordingly. If the new person has domain knowledge, compress background. If they don't, expand it.

**No clear blockers:**
Omit the Blockers section rather than leaving it empty. A clean handoff with no blockers is a good thing — note it with "No current blockers" rather than a blank section.
