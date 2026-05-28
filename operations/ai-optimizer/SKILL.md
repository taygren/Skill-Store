[SKILL.md](https://github.com/user-attachments/files/28345617/SKILL.md)
---
name: ai-token-optimizer
version: 1.0.0
description: >
  AI Token & Usage Optimizer — activate when a user wants to reduce AI costs, optimize prompts
  for token efficiency, manage context window consumption, route tasks to the right model, audit
  workflows for cost inefficiencies, or plan token budgets. Trigger when the user says "/audit",
  "/rewrite", "/route", "/compress", "/analyze-workflow", "/budget", "/estimate", "/compare",
  or asks any variation of "how do I reduce my AI costs", "optimize this prompt", "which model
  should I use for this", "my context window is getting long", "how much will this cost", or
  "is this workflow efficient". Operates in two modes: real-time (optimize before sending) and
  design-time (audit before building). Three optimization aggressiveness levels: light, balanced,
  aggressive. Integrates with ai-model-handoff for platform-aware routing decisions.
---

# AI Token & Usage Optimizer

Reduces AI costs and improves performance by optimizing prompts, managing context, routing tasks to the right model, and auditing workflows for inefficiency. Token efficiency is a first-class concern — without sacrificing output quality.

Operates at three layers:
- **Prompt layer** — reduce tokens going in
- **Session layer** — reduce tokens across a conversation
- **Workflow layer** — reduce tokens at scale across pipelines and agents

---

## Commands

```
/audit [prompt]                         → Analyze a prompt for token waste
/rewrite [prompt]                       → Rewrite a prompt for efficiency
/rewrite[light] [prompt]                → Light rewrite — remove waste only
/rewrite[balanced] [prompt]             → Balanced rewrite — restructure for clarity and efficiency
/rewrite[aggressive] [prompt]           → Aggressive rewrite — maximum compression, full restructure
/route [task description]               → Recommend best model for cost-to-capability fit
/compress                               → Compress current session context
/compress[keep: X]                      → Compress and explicitly keep named items
/analyze-workflow [description]         → Audit a workflow or agent pipeline for cost
/budget [monthly $ target]              → Build a token budget plan
/estimate [task description]            → Estimate token cost before executing
/compare [model A] vs [model B] on [task] → Side-by-side cost and capability comparison
/handoff to [platform]                  → Route work to another platform (via ai-model-handoff)
/handoff recommend                      → Recommend best platform for current task
```

---

## Optimization Modes

Every rewrite and audit command runs in one of three modes. Default is `[balanced]`.

### Light `[light]`
- Removes true waste only: filler phrases, politeness overhead, explicit redundancy
- Preserves all original structure, order, and language style
- Safe for prompts where tone or phrasing carries intent
- Typical savings: 10–25% token reduction

### Balanced `[balanced]` *(default)*
- Removes waste AND restructures for clarity
- Compresses verbose instructions into precise ones
- Lifts repeated context to system prompt where applicable
- Trims examples to minimum effective length
- Typical savings: 25–45% token reduction

### Aggressive `[aggressive]`
- Full restructure for maximum token efficiency
- Rewrites from scratch using the original intent as input
- Applies all optimization patterns simultaneously
- May change phrasing significantly — review before use
- Typical savings: 45–70% token reduction

---

## Workflow Overview

### For `/audit` and `/rewrite`
1. Parse the prompt into components (role, context, instructions, examples, format spec)
2. Score each component for token efficiency
3. Identify waste patterns (see `capabilities/prompt-auditor.md`)
4. Apply rewriting strategies per the selected mode
5. Produce diff-style output with token counts

### For `/route`
1. Classify the task by type, complexity, and requirements
2. Match against the routing matrix (see `capabilities/model-router.md`)
3. Apply cost-to-capability scoring
4. Recommend primary model + fallback + rationale
5. Flag if ai-model-handoff is relevant for the receiving platform

### For `/compress`
1. Scan current session for compression candidates
2. Apply Memory Anchor Protocol (must carry / should carry / compress or drop)
3. Produce compressed context block
4. Show token delta

### For `/analyze-workflow`
1. Map the workflow into discrete steps
2. Classify each step by task type and current model assignment
3. Identify inefficiency patterns (see `capabilities/workflow-analyzer.md`)
4. Produce audit report ranked by savings opportunity
5. Flag steps where ai-model-handoff routing applies

### For `/budget`
1. Gather monthly spend target and usage patterns
2. Allocate tokens across system prompt, context, input, output
3. Recommend model tier per use case
4. Produce budget table with alert thresholds

### For `/estimate`
1. Classify the task
2. Apply token benchmarks (see `reference/token-benchmarks.md`)
3. Select appropriate model from routing matrix
4. Calculate estimated cost at current pricing
5. Show range (optimized vs. unoptimized prompt)

---

## Diff-Style Output Format

All audit and rewrite outputs use this format:

```
━━━ TOKEN AUDIT ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Mode: [light / balanced / aggressive]
Model: [model used for estimate]

BEFORE                              AFTER
──────────────────────────────────  ──────────────────────────────────
[original prompt]                   [optimized prompt]

Token count:  [N] tokens            Token count:  [N] tokens
Est. cost:    $[X] per 1K calls     Est. cost:    $[X] per 1K calls

SAVINGS
Tokens removed: [N] ([X]%)
Cost reduction: $[X] per 1K calls / $[X] per month at [volume]

CHANGES MADE
[#] [Category]: [What was changed and why]
[#] [Category]: [What was changed and why]

WHAT WAS PRESERVED
[What was kept and why it needed to stay]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Integration with AI Model Handoff

This skill integrates directly with `ai-model-handoff`. When routing or workflow analysis determines that a task should move to a different platform:

- `/route` recommendations include handoff readiness — whether the task can be cleanly transferred
- `/analyze-workflow` flags steps where platform switching would reduce cost
- `/handoff to [platform]` and `/handoff recommend` invoke the full ai-model-handoff skill with token-efficiency context added to the package

**The integration rule:** ai-token-optimizer decides *whether* to switch platforms based on cost. ai-model-handoff handles *how* to switch based on context and capability. They are complementary, not redundant.

---

## Key Metrics

| Metric | Definition |
|---|---|
| **Prompt efficiency ratio** | Output quality per input token |
| **Context bloat %** | Proportion of context that's non-essential |
| **Model fit score** | Whether task complexity matches model tier |
| **Estimated cost per interaction** | $ at current model pricing |
| **Monthly run rate** | Projected spend at current usage |
| **Optimization savings** | Tokens and $ saved vs. original |

---

## Quality Rules

1. **Never sacrifice output quality for token savings.** If a compression would degrade the output, flag it rather than apply it silently.
2. **Always show the math.** Token counts and cost estimates must be visible in every output.
3. **Diff-style always.** Never present a rewritten prompt without the original alongside it.
4. **State what was preserved and why.** Changes are explained; so are non-changes.
5. **Pricing disclaimer on every cost estimate.** Model pricing changes frequently — flag that estimates should be verified against current provider pricing.
6. **Mode transparency.** Always show which optimization mode was applied.
