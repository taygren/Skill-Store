---
name: agent-foundation
version: 1.0.0
description: >
  Agent Foundation — activate when a user wants to set up a structured, persistent workspace
  system for an AI agent (Claude, Cowork, or similar) to operate in over time. Trigger when
  the user says "set up my agent workspace", "create a workstation for", "build my Claude OS",
  "help me structure my agent environment", "set up a [area] workspace", "create a CLAUDE.md",
  "I want my agent to remember my preferences", or any request to configure a durable, organized
  environment where an AI agent will work repeatedly across sessions. Produces the full folder
  structure, CLAUDE.md instruction files, MEMORY.md scaffolds, and a behavioral analysis pass
  that extracts the user's actual patterns from existing work. Designed to make agent behavior
  consistent, compounding, and tailored — not generic across every session.
---

# Agent Foundation

Builds a **structured, persistent workspace system** that gives an AI agent durable context, behavioral rules, and a memory layer — so it behaves consistently across sessions, learns from corrections, and adapts to the specific domain it's operating in.

The system is hierarchical: a root layer sets global defaults, workstation layers specialize by domain, and project layers handle one-off work. Rules stack automatically — more specific layers override less specific ones.

---

## Core Architecture

```
[Root Workspace]/
├── CLAUDE.md              ← Global voice, model, and behavior defaults
├── MEMORY.md              ← Root-level corrections and learned patterns
│
├── [Workstation A]/       ← e.g., "Research HQ", "Client Work", "Finance"
│   ├── CLAUDE.md          ← Domain-specific rules (stack on top of root)
│   ├── MEMORY.md          ← Workstation-level corrections
│   └── Resources/         ← Reference materials, templates, assets
│
├── [Workstation B]/
│   ├── CLAUDE.md
│   ├── MEMORY.md
│   └── Resources/
│
└── Projects/              ← One-off work
    └── [Project Name]/    ← e.g., "Q4 Strategy", "Vendor Evaluation"
        ├── CLAUDE.md      ← Project-specific overrides
        └── MEMORY.md      ← Project-specific corrections
```

---

## How the Layers Work

**Root CLAUDE.md** — The constitution. Establishes the agent's default voice, output format preferences, model selection logic, and universal behavioral rules. Everything in root applies everywhere unless overridden downstream.

**Workstation CLAUDE.md** — Domain specialization. Rules here stack on top of root and apply whenever the agent is operating in this workstation. A workstation is a persistent area of work — something you return to repeatedly (not a one-time project).

**Project CLAUDE.md** — Task-specific overrides. A project is bounded, one-off work. Its CLAUDE.md can override anything from root or workstation for the duration of the project.

**MEMORY.md files** — The learning layer. Written by the agent whenever the user corrects it, provides new preferences, or establishes a pattern worth keeping. Corrections compound — the agent gets better at this domain over time. Never delete MEMORY.md content; append.

---

## Workflow Overview

1. **Intake** — Understand the user's work domains and what they need the agent to do
2. **Design the structure** — Map workstations and projects based on the user's domains
3. **Build root CLAUDE.md** — Establish global defaults
4. **Build workstation scaffolds** — One CLAUDE.md + MEMORY.md per domain
5. **Pattern extraction** — Analyze existing work to populate workstation rules with real behavioral data
6. **Verify with the user** — Confirm extracted patterns before locking them in
7. **Create project scaffolds** — If any active projects need their own layer
8. **Document the setup** — Produce a system map the user can reference

---

## Step 1: Intake

Gather the following before building. Extract from context first; ask only for what's missing.

### Required
- **Agent platform** — What tool will read these files? (Cowork, Claude Projects, custom setup, other)
- **Root workspace path** — Where does this live? (e.g., `/Documents/Agent OS`, `~/Workspaces/Claude`)
- **Domains / workstations needed** — What are the recurring areas of work? (e.g., Client Work, Research, Finance, Writing, Operations)

### Useful
- **Sample work** — Existing documents, emails, notes, or outputs the agent can analyze to extract behavioral patterns
- **Known preferences** — Tone, formality level, output format, things the agent should always/never do
- **Active projects** — Any bounded, one-off work that needs a project-level layer right now
- **Model preferences** — Any existing preferences for when to use faster vs. more capable models

If the user has no existing work to analyze, build scaffolds with placeholder rules and note that MEMORY.md will populate through use.

---

## Step 2: Design the Structure

Before creating any files, confirm the workstation map with the user:

```
Proposed Structure:

Root: [path]/
├── CLAUDE.md + MEMORY.md
│
├── [Workstation 1]: [Name] — [1-sentence description of what work lives here]
├── [Workstation 2]: [Name] — [description]
├── [Workstation 3]: [Name] — [description]
│
└── Projects/ (for one-off work)
    └── [Any active projects to create now]
```

Get confirmation before building. It's easier to adjust the map than to restructure files after creation.

---

## Step 3: Build Root CLAUDE.md

The root file should stay **under 300 lines**. It establishes universals — things that should be true everywhere. Don't put domain-specific rules here; they belong in workstation files.

### Root CLAUDE.md Template

```markdown
# [Agent Name] — Root Configuration
*Last updated: [Date]*

---

## Identity & Purpose
[1–2 sentences on what this agent is for and who it serves]

---

## Voice & Tone (Global Defaults)
- **Formality:** [e.g., Professional but direct; never stiff or corporate]
- **Length bias:** [e.g., Prefer concise; expand only when complexity requires it]
- **Perspective:** [e.g., First-person where natural; avoid passive constructions]
- **What to avoid:** [e.g., Filler phrases, excessive hedging, em dash overuse]

---

## Output Format Defaults
- **Default format:** [e.g., Prose with minimal headers; use bullets only for lists of 4+]
- **Default length:** [e.g., Match the complexity of the task; don't pad]
- **File naming:** [e.g., kebab-case, date-prefixed for time-sensitive work]

---

## Model Selection
- **Default model:** [e.g., Sonnet — fast, capable, appropriate for most tasks]
- **Use stronger model when:** [e.g., Task has 3+ dependent steps; high-stakes deliverable; complex reasoning required]
- **Use faster model when:** [e.g., Drafting, formatting, simple lookups, iteration]

---

## Universal Behavioral Rules
- [Rule 1 — e.g., Always confirm scope before starting a task over 30 minutes of work]
- [Rule 2 — e.g., Never fabricate citations, sources, or statistics]
- [Rule 3 — e.g., Flag ambiguity rather than making silent assumptions]
- [Rule 4 — e.g., Ask one clarifying question at a time, not a list]
- [Rule 5]

---

## What I Always Do
- [e.g., End complex outputs with a "What's next?" or "Open items:" section]
- [e.g., Include source URLs when pulling from web research]

## What I Never Do
- [e.g., Send drafts without flagging they're drafts]
- [e.g., Make permanent changes to files without confirming]

---

## Memory Protocol
When the user corrects me, provides a preference, or establishes a pattern:
1. Apply the correction immediately
2. Write the learning to the relevant MEMORY.md
3. Confirm what was written

MEMORY.md files are append-only. Never delete prior entries.
```

---

## Step 4: Build Workstation Scaffolds

For each workstation, create:
- `CLAUDE.md` — domain-specific rules that stack on root
- `MEMORY.md` — starts empty (or populated via Step 5)
- `Resources/` — subfolder for reference materials

### Workstation CLAUDE.md Template

```markdown
# [Workstation Name] — Configuration
*Workstation path: [path]*
*Stacks on: Root CLAUDE.md*
*Last updated: [Date]*

---

## Domain Context
[1–2 sentences on what work happens in this workstation and who the outputs are for]

---

## Voice & Tone Overrides
[Only include what differs from root. If root's defaults apply, don't repeat them.]
- [Override 1 — e.g., "More formal than default; this workstation produces client-facing work"]
- [Override 2]

---

## Output Format Overrides
- [e.g., "All outputs in this workstation get a header block with date, project, and audience"]

---

## Domain-Specific Rules
- [Rule specific to this workstation's work type]
- [Rule specific to recurring stakeholders or relationships in this domain]
- [Rule specific to quality standards in this domain]

---

## Recurring Patterns
[Populated via pattern extraction (Step 5) or through use over time]
- [Pattern 1 — e.g., "When writing to [person/type], always lead with X"]
- [Pattern 2]

---

## Resources
Key reference materials in `/Resources`:
- [File name] — [what it is]
```

### Empty MEMORY.md Template

```markdown
# Memory: [Workstation Name]
*Append-only. Written by agent when corrections or patterns are established.*

---

[Entries added here over time, each with date and context]
```

---

## Step 5: Pattern Extraction

If the user has existing work to analyze (documents, emails, prior outputs, notes), run a pattern extraction pass before locking in workstation rules.

### Extraction Process

1. **Ingest the sample work** — Read the provided files, emails, or outputs
2. **Identify recurring patterns** — Look for:
   - Opening conventions (how they start things)
   - Closing conventions (how they end things)
   - Formality signals (vocabulary level, sentence structure)
   - Structural preferences (bullets vs. prose, headers vs. flowing text)
   - Relationship-specific patterns (different behaviors with different people or contexts)
   - Things they consistently do that aren't obvious defaults
   - Things they consistently avoid

3. **Draft the Editorial Rules** — Translate patterns into explicit rules for the workstation CLAUDE.md

4. **Write a verification paragraph** — Before locking anything in, produce:

> *"Based on [N] samples of your work, here's what I learned about how you operate in [workstation name]: [2–4 sentences describing the dominant patterns]. Does this match how you want to continue working? I'll lock these in as your Editorial Rules once you confirm."*

**Never write patterns into CLAUDE.md before the user confirms them.** Unverified patterns become wrong defaults.

### Patterns to Look For by Work Type

**Written communications (email, messages, memos):**
- Typical opener style (direct / contextual / relational)
- Sign-off style and formality
- How they handle asks (explicit vs. implied)
- Paragraph length and density
- Phrases they use repeatedly with specific people

**Research and analysis outputs:**
- How they structure findings (bottom-line-up-front vs. narrative)
- How they handle uncertainty (hedged vs. direct)
- What they always include (exec summary, sources, recommendations)
- What they never include

**Creative or editorial work:**
- Voice (first person vs. removed)
- Sentence rhythm preferences
- Vocabulary register
- How they use examples

---

## Step 6: Verify with the User

Before finalizing any workstation CLAUDE.md:

1. Present the extracted patterns as a verification paragraph (see Step 5)
2. List the proposed Editorial Rules explicitly
3. Wait for confirmation or corrections
4. Apply corrections and note them in MEMORY.md
5. Only then finalize the CLAUDE.md

This step is not optional. Patterns that go in unchecked create compounding drift.

---

## Step 7: Create Project Scaffolds (If Needed)

For any active projects the user identifies, create:

```
Projects/[Project Name]/
├── CLAUDE.md    ← project-specific overrides
└── MEMORY.md    ← project-specific corrections
```

### Project CLAUDE.md Template

```markdown
# Project: [Name]
*Project path: [path]*
*Stacks on: [Workstation] → Root*
*Active: [Start date] — [End date or "ongoing"]*

---

## Project Overview
[2–3 sentences: what this project is, what it needs to produce, and when it ends]

---

## Project-Specific Rules
[Only rules unique to this project. Everything from workstation and root still applies.]

---

## Key Constraints
- [Deadline or timeline]
- [Stakeholder or audience specifics]
- [Format or delivery requirements]

---

## Open Items
[Running list of things to track within this project]
```

---

## Step 8: Produce the System Map

After building all files, produce a **System Map** the user can reference:

```markdown
# Agent Workspace System Map
*Root: [path] | Built: [date]*

## Structure
[Directory tree showing all workstations and projects]

## How to Use This System
- To work in a domain: open the relevant workstation folder
- To start a project: create a new subfolder under Projects/ with CLAUDE.md + MEMORY.md
- To teach a correction: tell the agent the correction; it writes to MEMORY.md automatically
- To update rules: edit the relevant CLAUDE.md directly

## Active Workstations
| Workstation | Purpose | Pattern Source |
|---|---|---|
| [Name] | [Description] | [Analyzed from X samples / Placeholder — populate through use] |

## Active Projects
| Project | Status | Path |
|---|---|---|
| [Name] | [Active / Complete] | [path] |

## Rule Hierarchy (Most → Least Specific)
Project CLAUDE.md → Workstation CLAUDE.md → Root CLAUDE.md

## Memory Locations
| Scope | Path | Last Updated |
|---|---|---|
| Root | [path]/MEMORY.md | — |
| [Workstation] | [path]/MEMORY.md | — |
```

---

## Quality Checklist

Before delivering the completed setup:
- [ ] Root CLAUDE.md is under 300 lines and contains only universal rules
- [ ] Each workstation CLAUDE.md only contains rules that differ from or extend root
- [ ] Pattern extraction verified with the user before locking in Editorial Rules
- [ ] Every MEMORY.md exists and starts empty (or with verified initial entries only)
- [ ] No unverified assumptions are written into any CLAUDE.md
- [ ] System Map produced and accurate
- [ ] User knows how to: add a workstation, start a project, trigger a memory write

---

## Edge Cases

**User has no existing work samples:**
Build scaffolds with explicit placeholder sections labeled `[Populate through use — agent will fill this in as you work]`. The MEMORY.md layer means the system improves organically even without an initial analysis pass.

**User wants to start with just one workstation:**
Build root + one workstation. Don't over-engineer upfront. Note that adding workstations later is additive — new folder, two files, done.

**User is setting this up for a team (not individual):**
Root CLAUDE.md should define shared team voice and standards. Individual workstations can exist per team member for personal preferences. Shared workstations (e.g., "Client Deliverables") hold cross-team standards.

**The agent platform doesn't support CLAUDE.md natively:**
Adapt the output — the same content can be delivered as system prompts, project knowledge base files, or prefixed context. Note the adaptation clearly in the System Map.

**User has existing CLAUDE.md files already:**
Read them before building. Extend, don't replace. Flag any conflicts with what you're proposing.

**User wants to connect external tools (calendar, email, documents):**
Note the connector in the relevant workstation CLAUDE.md under a `## Connected Tools` section. Define what the tool enables and any rules about how it should be used (e.g., "Use calendar connector to check availability before scheduling tasks; never create calendar events without confirming").
