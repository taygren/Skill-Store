[context-manager.md](https://github.com/user-attachments/files/28345667/context-manager.md)
# Capability: Context Window Manager

**Command:** `/compress` or `/compress[keep: X]`  
**Purpose:** Monitor and manage context window consumption across a session. Compress context to extend session utility and reduce token cost.

---

## Why Context Management Matters

Context window costs are cumulative. Every message in a conversation is re-sent to the model on each turn. A 10,000-token conversation history costs 10,000 tokens of input *on every subsequent message* — not just once. In long sessions, unmanaged context is the single largest driver of cost inflation.

**The math:**
```
10 turns × 500 tokens each = 5,000 token history
Turn 11 input cost = 5,000 (history) + new message tokens
Turn 20 input cost = 9,500 (history) + new message tokens
Turn 20 cost = ~19x the cost of Turn 1
```

Compression applied at Turn 10 can reduce Turn 20 costs by 60–80%.

---

## Memory Anchor Protocol

Before compressing, classify every piece of context into one of three tiers:

### MUST CARRY — Always preserved
- Current goal and active sub-goals
- Hard constraints established in the session (things that cannot change)
- Decisions made with their reasoning
- Artifacts produced — names, locations, status
- What the session is currently trying to accomplish
- Named entities (people, companies, products) central to the work

### SHOULD CARRY — Preserve if relevant to next steps
- Tone, voice, and audience context
- Prior rejected approaches and why they were rejected
- Technical environment details that affect future outputs
- Established terminology or naming conventions
- Relationship or stakeholder context

### COMPRESS OR DROP — Reduce or remove
- Raw conversational back-and-forth that led to a decision (keep the decision, drop the path)
- Exploratory tangents that didn't produce anything
- Superseded drafts and intermediate outputs
- Repeated confirmations and acknowledgments
- Error messages and failed attempts (keep the resolution, drop the error trail)
- Verbose explanations already acted upon

---

## Compression Process

### Step 1: Context Inventory

Scan the full conversation and produce an inventory:

| Turn | Content Type | Token Est. | Tier | Action |
|---|---|---|---|---|
| 1–3 | Goal setting and context | ~800 | Must Carry | Compress to summary |
| 4–7 | Exploratory discussion | ~1,200 | Compress/Drop | Compress to decisions only |
| 8–10 | Draft produced | ~2,000 | Should Carry | Keep final draft, drop iterations |
| 11–14 | Revision discussion | ~900 | Compress/Drop | Keep final state, drop path |

### Step 2: Compression

**For Must Carry items:** Rewrite as a structured Context Register — named items with 1–2 sentence descriptions. Far more token-efficient than raw conversation.

**For Should Carry items:** Condense to the key fact. "User prefers direct language without hedging" replaces three turns of tone calibration.

**For Compress/Drop items:** Extract only decisions and final outputs. Delete process.

### Step 3: Compressed Context Block

Output a self-contained context block that can be pasted into a new session:

```
━━━ COMPRESSED CONTEXT BLOCK ━━━━━━━━━━━━━━━━━━━━
Generated: [date/time] | Original: [N] tokens → Compressed: [N] tokens ([X]% reduction)

CURRENT GOAL
[One sentence, outcome-focused]

ACTIVE SUB-GOALS
- [Sub-goal 1] — [status: complete / in progress / blocked]
- [Sub-goal 2] — [status]

CONTEXT REGISTER
[Item name]: [1–2 sentence description of what it is and why it matters]
[Item name]: [description]

ARTIFACTS
- [Name] | [type] | [location or "in conversation"] | [status: final/draft]

DECISIONS MADE
[Decision]: [choice] — Reason: [why] — Implies: [what this forecloses]

CONSTRAINTS (must not change)
- [Constraint 1]
- [Constraint 2]

WHAT WAS DROPPED
[Brief note on what was compressed out — so the user knows what's gone]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Context Health Monitoring

Track estimated token consumption and alert at thresholds:

| Threshold | Status | Recommendation |
|---|---|---|
| < 40% of context window | 🟢 Healthy | No action needed |
| 40–65% of context window | 🟡 Monitor | Consider compressing exploratory content |
| 65–80% of context window | 🟠 Warning | Run /compress now — quality may start degrading |
| > 80% of context window | 🔴 Critical | Compress immediately or start new session |

**Context window sizes by model (approximate):**

| Model | Context Window | Practical Working Window |
|---|---|---|
| Claude Sonnet 4.6 | 200K tokens | ~160K (leave buffer for output) |
| Claude Opus 4.6 | 200K tokens | ~160K |
| GPT-5 | 1M tokens | ~800K |
| Gemini 3.1 Pro | 2M tokens | ~1.6M |
| Grok 4.1 Fast | 2M tokens | ~1.6M |
| Mistral Large | 128K tokens | ~100K |
| DeepSeek V3 | 128K tokens | ~100K |

---

## `/compress[keep: X]` Syntax

When specific items must survive compression regardless of tier:

```
/compress[keep: the schema design, the API decision, Jordan's feedback]
```

Named items are treated as Must Carry regardless of their natural tier. Everything else is compressed normally.

---

## Compression Output

```
━━━ CONTEXT COMPRESSION ━━━━━━━━━━━━━━━━━━━━━━━━━
BEFORE              AFTER
──────────────────  ──────────────────
[N] tokens          [N] tokens
[N] turns           Compressed summary
Est. cost/turn: $X  Est. cost/turn: $X

REDUCTION: [N] tokens ([X]%) | $[X] saved per subsequent turn

WHAT WAS KEPT
[List of Must Carry items preserved]

WHAT WAS COMPRESSED
[List of items condensed with rationale]

WHAT WAS DROPPED
[List of items removed — exploratory tangents, superseded drafts, etc.]

[COMPRESSED CONTEXT BLOCK — paste into new session if needed]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
