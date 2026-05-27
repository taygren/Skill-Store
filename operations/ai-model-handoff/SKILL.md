[SKILL.md](https://github.com/user-attachments/files/28306245/SKILL.md)
---
name: ai-model-handoff
version: 1.0.0
description: >
  AI Model Handoff Orchestrator — activate when a user wants to transfer active work from one
  AI platform or model to another while preserving full context, decisions, and continuity.
  Trigger when the user says "/handoff to [platform]", "/handoff recommend", "/handoff return
  from [platform]", "/handoff compare", "switch this to [platform]", "continue this in
  [platform]", "hand this off", or any variation of wanting to move work between AI tools
  without losing context. Packages the active session into a platform-native handoff prompt
  formatted, compressed, and configured for the specific receiving platform. Handles forward
  handoffs (sending work out), return handoffs (receiving work back), recommendation routing
  (choosing the best platform for the next task), and chain orchestration (multi-hop workflows
  across platforms). All handoff packages include re-entry instructions so work can always
  return cleanly.
---

# AI Model Handoff Orchestrator

Transfers active work between AI platforms with full context preservation. Packages sessions into **platform-native handoff prompts** — formatted, compressed, and configured for the specific receiving platform's conventions, strengths, and interface.

Every handoff is a deliberate, structured transition — not a copy-paste. The receiving platform gets exactly what it needs, in the format it works best with, and nothing it doesn't need.

---

## Commands

```
/handoff to [platform]           → Package and send work to a named platform
/handoff recommend               → Recommend the best platform for the next task
/handoff return from [platform]  → Receive work coming back from a platform
/handoff compare                 → Show routing options with reasoning for current task
/handoff chain                   → Plan a multi-platform workflow for a complex task
```

---

## Platform Registry

Supported platforms and their primary routing signal:

| Platform | Route Here When... |
|---|---|
| **Claude** | Long-form reasoning, structured analysis, writing, extended thinking |
| **Claude Code** | Terminal-native agentic coding, repo-level autonomous work |
| **ChatGPT** | All-purpose work, multimodal tasks, broadest tool ecosystem |
| **Gemini** | Google Workspace integration, multimodal (video/audio), 2M token context |
| **Copilot** | Microsoft 365 / Teams / GitHub enterprise environment |
| **Perplexity** | Real-time web research, citation-required outputs |
| **Grok** | Real-time X/social signals, large context summarization |
| **DeepSeek** | Transparent step-by-step reasoning, cost-sensitive, open-source |
| **Mistral** | Privacy-sensitive/on-premise, multilingual, edge deployments |
| **Cursor** | Active codebase work, multi-file editing, IDE-native agent tasks |
| **Meta / Llama** | Self-hosted, fine-tunable, air-gapped, open-weight deployments |
| **Windsurf** | IDE alternative to Cursor, Cascade multi-file editing |

Full platform profiles are in the `/platforms/` folder. Read the relevant profile before assembling any handoff package.

---

## Workflow Overview

1. **Identify the handoff type** — Forward, return, recommend, compare, or chain
2. **Scan the session** — Extract goals, context, artifacts, decisions, blockers
3. **Build the Memory Anchor set** — Classify what must carry, should carry, and can compress
4. **Load the target platform profile** — Read formatting conventions, context behavior, system prompt support
5. **Assemble the handoff package** — Structured, platform-native, with re-entry instructions
6. **Deliver** — Copy-paste ready output with a brief configuration checklist if needed

---

## Step 1: Identify Handoff Type

### Forward Handoff (`/handoff to [platform]`)
Work is leaving the current platform for a named destination. The user knows where it's going.
→ Proceed to Step 2 with the named target platform.

### Return Handoff (`/handoff return from [platform]`)
Work is coming back from another platform. The user pastes output from the other platform.
→ Read the pasted output. Extract: what was completed, what changed, any decisions made, any blockers hit.
→ Reconstruct the session state and resume as if the work never left.
→ Produce a "Return Summary" confirming what was received and what the current state is.

### Recommendation (`/handoff recommend`)
The user doesn't know which platform to use next.
→ Assess the next task type against the platform routing matrix.
→ Recommend 1 primary platform and 1 alternative, with reasoning.
→ Offer to produce the handoff package for the recommended platform immediately.

### Comparison (`/handoff compare`)
The user wants to see routing options before deciding.
→ Evaluate the current task against all relevant platforms.
→ Produce a comparison table: platform, fit score, key reason, tradeoff.
→ Wait for user selection before producing the package.

### Chain Planning (`/handoff chain`)
The user has a complex multi-platform workflow.
→ Map the full task into phases.
→ Assign the optimal platform per phase.
→ Produce the first handoff package and note the planned chain.

---

## Step 2: Session Scan

Read the full conversation before writing anything. Extract:

**Goal Layer**
- Current goal (one sentence, outcome-focused)
- Sub-goals and their status (complete / in progress / blocked / not started)

**Context Layer**
- What took multiple turns to establish
- Constraints that cannot be violated
- Audience, tone, or format requirements
- Anything the next platform would not know without being told

**Artifact Layer**
- Every file, document, code block, schema, or output produced
- Location (in conversation / file path / external link)
- Status (final / draft / placeholder)

**Decision Layer**
- Significant choices made and the reasoning behind them
- Rejected alternatives worth remembering
- Open decisions still pending

**Blocker Layer**
- What is unresolved, stuck, or waiting on input
- What the next platform will need to resolve or work around

---

## Step 3: Memory Anchor Protocol

Before assembling the package, classify every piece of context:

### MUST CARRY — Always included
- Current goal and active sub-goals
- Hard constraints (things that cannot change)
- Decisions made with their reasoning
- Artifacts produced with locations and status
- What the next platform is being asked to do

### SHOULD CARRY — Include if relevant to next task
- Tone, voice, and audience context
- Prior attempts and why they were rejected
- Relationship or stakeholder context
- Technical environment details

### COMPRESS OR DROP — Platform-dependent
- Raw conversation history (compress to key points)
- Exploratory tangents that didn't lead anywhere
- Superseded drafts and intermediate outputs
- Background context the platform doesn't need for its specific task

**Compression rules are platform-specific.** Check the target platform profile before deciding what to include:
- Large context platforms (Gemini 2M, Claude 200K): can carry more
- Chat-native platforms (ChatGPT, Perplexity): tighter briefs perform better
- IDE platforms (Cursor, Windsurf, Claude Code): strip narrative; keep schema, specs, constraints
- Research platforms (Perplexity, Grok): strip build context; keep research questions and existing findings

---

## Step 4: Load Platform Profile

Before writing the handoff package, read the relevant file in `/platforms/`.

Each profile specifies:
- How to structure the system prompt for that platform
- What context format performs best
- Memory and persistence behavior
- Tool availability
- Formatting conventions
- The platform's handoff receiving template

**Never write a handoff package without reading the target platform profile.** Handoff packages that ignore platform conventions produce worse results than starting fresh.

---

## Step 5: Assemble the Handoff Package

Every handoff package uses this structure, adapted per platform profile:

```
=== [PLATFORM] HANDOFF PACKAGE ===
Project: [name]
Handed off from: [source platform] ([phase completed])
Receiving: [target platform] ([phase beginning])
Timestamp: [date]

--- SYSTEM CONTEXT ---
[Platform-native system prompt. Sets up the model's role and operating context.
Format and length per platform profile conventions.]

--- CURRENT GOAL ---
[One sentence. Outcome-focused.]

--- SUB-GOALS ---
[Table or list with status per item]

--- WHAT EXISTS ---
[Artifacts: name, type, location, status]
[Compress or expand per platform context tolerance]

--- DECISIONS MADE ---
[Decision name]: [what was decided] | Why: [reasoning] | Implies: [what this forecloses]
[Include only decisions relevant to the receiving platform's task]

--- CONTEXT REGISTER ---
[Named list of things that took time to establish and must not be re-litigated]

--- YOUR TASK ---
[Explicit, specific instruction for the receiving platform.
Not "continue the work" — exactly what to do first, second, third.]

--- MUST NOT CHANGE ---
[Hard constraints. Non-negotiables. Exactly as established.]

--- BLOCKERS / OPEN ITEMS ---
[What's stuck or unresolved that the receiving platform should know about]

--- RE-ENTRY INSTRUCTIONS ---
When this phase is complete (or if blocked), run:
/handoff return from [target platform]

Include in the return:
• [Specific output 1 to bring back]
• [Specific output 2]
• Any decisions made
• Any new blockers

=== END HANDOFF PACKAGE ===
```

---

## Step 6: Delivery

After producing the handoff package:

1. **Present the package** — formatted as a clean code block for easy copy-paste
2. **Add a configuration checklist** if the target platform requires setup before pasting:
   - e.g., "Enable web search before pasting" (Perplexity)
   - e.g., "Open in a new Project with no prior context" (Claude)
   - e.g., "Paste into Agent mode, not Chat mode" (Cursor)
3. **Confirm the re-entry path** — remind the user how to bring the work back

---

## Routing Decision Matrix

Use this when running `/handoff recommend` or `/handoff compare`:

| Task Characteristic | Best Platform(s) |
|---|---|
| Deep research + synthesis | Claude, Gemini, Perplexity |
| Real-time web data required | Perplexity, Grok, ChatGPT |
| Active codebase / multi-file changes | Cursor, Claude Code, Windsurf |
| Code generation + explanation | Claude, ChatGPT, Cursor |
| Complex multi-step reasoning | Claude, DeepSeek R1, Gemini |
| Google Workspace integration | Gemini, Copilot |
| Microsoft 365 / Teams integration | Copilot |
| GitHub repo integration | Copilot, Claude Code, Cursor |
| Multimodal (image / video / audio) | Gemini, ChatGPT |
| Privacy / on-premise / air-gapped | Mistral, Meta Llama, DeepSeek |
| Multilingual / non-English | Mistral, Gemini, Qwen |
| Cost-sensitive at scale | DeepSeek, Mistral, Meta Llama |
| Social / market signal analysis | Grok |
| Citation-required research output | Perplexity |
| Long document / massive context | Gemini (2M), Claude (200K), Grok (2M) |
| Autonomous agentic task completion | Claude Code, Cursor, ChatGPT |
| Presentation / document creation | ChatGPT, Copilot, Gemini |

---

## Consistency Guardrails

These travel with every handoff regardless of platform:

- **Tone and voice** — established in the originating session must persist
- **Naming conventions** — file names, variable names, entity names don't change mid-project
- **Format standards** — output format decisions made early don't get re-decided by a new platform
- **Constraint log** — hard limits (stack choices, brand rules, deadline constraints) appear in every package under MUST NOT CHANGE

If a receiving platform produces output that violates a guardrail, the return handoff flags the violation explicitly before resuming.

---

## Quality Checklist

Before delivering any handoff package:
- [ ] Session fully scanned — no significant context missed
- [ ] Memory Anchor classification complete (must / should / compress)
- [ ] Target platform profile read and formatting applied
- [ ] Current goal is outcome-focused, not task-focused
- [ ] Every artifact has a location and status
- [ ] Every decision includes reasoning, not just the choice
- [ ] MUST NOT CHANGE section is complete and accurate
- [ ] Re-entry instructions specify exactly what to bring back
- [ ] Package is a clean copy-paste block with no surrounding explanation needed
- [ ] Configuration checklist included if platform requires pre-paste setup

---

## Edge Cases

**Target platform has no system prompt support:**
Move system context into the first user message. Note in the package header: "No system prompt support — context block is in the user turn."

**Session has produced no artifacts:**
Note explicitly in the package. The receiving platform needs to know whether it is starting work or continuing it.

**User wants to handoff to a platform not in the registry:**
Use the `_template.md` in `/platforms/` to build an ad-hoc profile. Note the gaps in the package header.

**Work involves sensitive or confidential data:**
Flag in the package header. Recommend against platforms with broad data retention (check platform profiles for retention policies). Recommend Mistral, Meta Llama, or DeepSeek for sensitive work.

**Multiple platforms are equally suited:**
Surface both in the recommendation with the deciding factor clearly stated (usually: ecosystem integration, cost, or which platform the user already has open).

**Return handoff brings back conflicting decisions:**
Flag the conflict explicitly. Do not silently merge. Present both states and ask the user to resolve before continuing.

**Chain involves more than 3 hops:**
Produce the first handoff package and the full chain plan. Don't pre-generate all packages — context will evolve with each hop.
