# AI Token & Usage Optimizer

Reduces AI costs and improves performance by optimizing prompts, managing context, routing tasks to the right model, and auditing workflows for inefficiency. Token efficiency is a first-class concern — without sacrificing output quality.

Integrates with [ai-model-handoff](../ai-model-handoff/) for platform-aware routing and seamless task transfer.

---

## The Problem

AI costs scale with usage in ways that are easy to ignore until they aren't. The same task can cost 10x more depending on how it's prompted, which model handles it, whether context is trimmed, and whether outputs are structured efficiently. Most teams optimize for output quality but never optimize for the cost of producing it.

**Three layers where cost accumulates:**
```
Prompt layer    → Verbose prompts paying for tokens that add nothing
Session layer   → Unmanaged context windows that compound on every turn
Workflow layer  → Wrong models, uncached content, redundant steps
```

This skill addresses all three.

---

## Quick Start

**Optimize a prompt before sending:**
```
/audit [paste your prompt]
/rewrite[balanced] [paste your prompt]
```

**Find the right model for a task:**
```
/route Write a weekly sales pipeline summary from CRM data
```

**Compress a long session:**
```
/compress
```

**Audit a workflow for cost inefficiencies:**
```
/analyze-workflow We use GPT-5 to classify support tickets, then Claude Opus 
to draft responses, then GPT-5 again to check tone. Runs 5,000 times/day.
```

**Build a monthly budget:**
```
/budget $500/month
```

---

## Commands

| Command | What It Does |
|---|---|
| `/audit [prompt]` | Analyze a prompt for token waste — diff view with savings estimate |
| `/rewrite[mode] [prompt]` | Rewrite a prompt for efficiency (light / balanced / aggressive) |
| `/route [task]` | Recommend the best model for cost-to-capability fit |
| `/compress` | Compress current session context to reduce per-turn cost |
| `/compress[keep: X]` | Compress while explicitly preserving named items |
| `/analyze-workflow [desc]` | Audit a workflow or agent pipeline for cost inefficiencies |
| `/budget [$target]` | Build a token budget plan for a monthly spend target |
| `/estimate [task]` | Estimate token cost before executing |
| `/compare [A] vs [B] on [task]` | Side-by-side model cost and capability comparison |
| `/handoff to [platform]` | Transfer work to another platform via ai-model-handoff |
| `/handoff recommend` | Recommend best platform for the current task |

---

## Optimization Modes

All rewrite and audit commands run in one of three modes. Default is `[balanced]`.

| Mode | What It Does | Typical Savings |
|---|---|---|
| `[light]` | Removes waste only — politeness, redundancy, defaults. Preserves all structure and phrasing. | 10–25% |
| `[balanced]` | Removes waste + restructures for clarity and efficiency. Trims examples, lifts context, compresses roles. | 25–45% |
| `[aggressive]` | Full restructure for maximum compression. Rebuilds from intent. Review before use. | 45–70% |

```
/rewrite[light] [prompt]        → Safe, minimal changes
/rewrite[balanced] [prompt]     → Recommended default
/rewrite[aggressive] [prompt]   → Maximum savings, review output carefully
```

---

## Diff-Style Output

Every audit and rewrite produces a side-by-side comparison:

```
━━━ PROMPT REWRITE ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Mode: balanced

BEFORE                              AFTER
──────────────────────────────────  ──────────────────────────────────
You are an expert senior financial  You are a senior financial analyst.
analyst with 20 years of experience Be precise, data-backed, actionable.
at top-tier investment banks...

Token count: 89 tokens              Token count: 14 tokens

SAVINGS
Tokens removed: 75 (84%)
Cost at 1K calls/day (Sonnet): $3.38/month saved

CHANGES MADE
1. Role Compression: Removed credentials/backstory — saved 68 tokens
2. Hedge Elimination: "always back your analysis" → "data-backed" — saved 7 tokens

WHAT WAS PRESERVED
Role title and 3 functional behavioral instructions — load-bearing context
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Model Routing

The routing system matches task complexity to model capability — not just capability to task.

### Model Tiers

| Tier | Models | Best For | Cost Range (per 1M tokens) |
|---|---|---|---|
| **Tier 1** Fast/Cheap | Gemini Flash, GPT-4o mini, Haiku, Mistral 7B | Extraction, classification, formatting, template filling | $0.10–$0.80 input |
| **Tier 2** Balanced | Sonnet 4.6, GPT-4o, Gemini Pro, Mistral Large | Writing, analysis, code, multi-step instructions | $1.25–$3.00 input |
| **Tier 3** Frontier | Opus 4.6, GPT-5, Gemini Ultra, DeepSeek R1 | Complex reasoning, architecture, extended thinking | $0.55–$15.00 input |
| **Specialized** | Perplexity, Grok, Cursor, Claude Code, Copilot | Real-time search, IDE work, M365 tasks | Varies |

### Quick Routing Reference

| Task | Route To | Why |
|---|---|---|
| Classify support tickets | Tier 1 | No reasoning needed |
| Draft professional emails | Tier 1–2 | Depends on stakes |
| Write production code | Tier 2 | Quality matters |
| Complex multi-step analysis | Tier 3 | Reasoning required |
| Real-time market research | Perplexity / Grok | Don't pay frontier rates for search |
| Multi-file codebase changes | Cursor / Claude Code | Chat models are wrong tool |
| 500K+ token document analysis | Gemini (2M context) | Context window is the constraint |
| Privacy-sensitive at scale | Mistral / Llama self-hosted | Data sovereignty |

---

## Context Window Management

Context costs compound. Every message is re-sent on every turn.

```
Turn 1:   500 tokens input
Turn 10:  5,000 tokens input (history accumulating)
Turn 20:  10,000 tokens input
Turn 20 costs 20x more than Turn 1 — for the same new content
```

`/compress` applies the Memory Anchor Protocol:

| Tier | Action |
|---|---|
| **Must Carry** | Goal, decisions, constraints, artifacts — always preserved |
| **Should Carry** | Tone, rejected approaches, technical context — preserved if relevant |
| **Compress/Drop** | Process, tangents, superseded drafts, error trails — removed |

**Context health thresholds:**

| Usage | Status | Action |
|---|---|---|
| < 40% of window | 🟢 Healthy | No action |
| 40–65% | 🟡 Monitor | Consider compressing |
| 65–80% | 🟠 Warning | Run /compress now |
| > 80% | 🔴 Critical | Compress immediately |

---

## AI Model Handoff Integration

This skill integrates with `ai-model-handoff` for platform-aware cost optimization.

**How it works:**
- `/route` identifies when a specialized platform would reduce cost
- `/analyze-workflow` flags steps where platform switching saves money
- `/handoff to [platform]` invokes the full handoff skill with token-efficiency context built in

**The division of responsibility:**
- `ai-token-optimizer` decides **whether** to switch platforms (cost basis)
- `ai-model-handoff` handles **how** to switch (context, format, platform conventions)

**Example integration:**
```
/route Analyze real-time competitor pricing from the web and produce a summary report

→ Recommendation: Perplexity for research phase, Claude Sonnet for synthesis
→ Cost savings vs. using Claude Opus for full task: ~$45/month at current volume
→ Run /handoff to perplexity to transfer the research phase
```

---

## Real-World Examples

### Example 1: Prompt Audit
**Scenario:** System prompt running on 2,000 calls/day feeling expensive.

```
/audit

[PASTE SYSTEM PROMPT]

→ Audit finds: 340 tokens of waste across 6 patterns
→ Cost impact: $6.12/day, $183/month on Sonnet 4.6
→ Recommended fix: /rewrite[balanced]
→ After rewrite: 127 tokens, $2.29/day — saves $3.83/day / $115/month
```

---

### Example 2: Model Routing
**Scenario:** Team using Claude Opus for all tasks including simple ones.

```
/route Classify incoming support tickets into 12 predefined categories

→ Recommendation: Gemini Flash 2.0 (Tier 1)
→ Current cost (Opus): $1,575/month at 5K calls/day
→ Optimized cost (Flash): $18/month at 5K calls/day
→ Savings: $1,557/month (99% reduction)
→ Quality note: Classification tasks don't require frontier reasoning
```

---

### Example 3: Workflow Audit
**Scenario:** 5-step agent pipeline costing $800/month.

```
/analyze-workflow
Step 1: Claude Opus — classify customer intent (5K calls/day)
Step 2: Claude Opus — draft response (5K calls/day)  
Step 3: Claude Opus — check tone (5K calls/day)
Step 4: GPT-5 — translate if needed (500 calls/day)
Step 5: Claude Opus — final review (5K calls/day)

→ Finding #1: Steps 1 and 3 are classification/checking tasks → downgrade to Tier 1
→ Finding #2: Step 5 duplicates Step 3 — eliminate
→ Finding #3: Full conversation history passed to every step — pass output only
→ Finding #4: System prompt not cached — enable prompt caching

→ Current: $2,340/month
→ Optimized: $340/month
→ Savings: $2,000/month (85% reduction)
```

---

### Example 4: Budget Planning
**Scenario:** $300/month target, multiple use cases.

```
/budget $300/month

→ Allocation:
   Customer support (high volume, simple)  → Gemini Flash  → $45/month
   Content generation (medium volume)      → Sonnet 4.6    → $120/month
   Strategic analysis (low volume)         → Opus 4.6      → $90/month
   Research tasks (real-time data)         → Perplexity    → $30/month
   Buffer                                              →  $15/month
   Total: $300/month

→ Alert thresholds: $150 (50%), $225 (75%), $270 (90%)
```

---

## File Structure

```
ai-token-optimizer/
│
├── SKILL.md                              ← Master orchestration — load into system prompt
├── README.md                             ← This file
│
├── capabilities/
│   ├── prompt-auditor.md                 ← Token waste detection and scoring
│   ├── context-manager.md                ← Context compression and Memory Anchor Protocol
│   ├── model-router.md                   ← Cost-to-capability routing matrix
│   ├── prompt-rewriter.md                ← Rewriting strategies by mode
│   └── workflow-analyzer-budget.md       ← Pipeline audit + token budget planner
│
├── reference/
│   ├── model-pricing.md                  ← Pricing for top 8 platforms + tiers
│   └── benchmarks-and-patterns.md        ← Token benchmarks + optimization pattern library
│
└── templates/
    └── prompt-templates.md               ← System prompt, few-shot, and CoT templates
```

---

## Key Numbers to Know

| Fact | Why It Matters |
|---|---|
| System prompts are paid on **every call** | A 1,000-token system prompt at 10K calls/day = 10M tokens/day in input alone |
| Context window costs **compound** | Turn 20 costs 20x more input tokens than Turn 1 for the same new content |
| Prompt caching cuts input costs by **50–90%** | Highest-ROI single optimization for high-volume workflows |
| Tier 3 vs Tier 1 = **10–150x cost difference** | Most tasks don't need Tier 3 |
| Politeness overhead ≈ **$30/month** per prompt at 1K calls/day | Completely zero-value spend |

---

## Design Principles

**Show the math.** Every recommendation includes a cost estimate. Savings are quantified, not asserted.

**Diff-style always.** Never present a rewritten prompt without the original alongside it. The user decides; the tool shows the comparison.

**Never sacrifice quality for savings.** If a compression would degrade output, flag it rather than apply it silently.

**Pricing is volatile.** Every cost estimate includes a verification reminder. Model pricing changes — sometimes dramatically and without notice.

**Integration over duplication.** This skill routes, optimizes, and audits. ai-model-handoff handles platform transfer. They work together, not in parallel.

---

*Part of the AI Operations cluster: `agent-foundation` · `session-handoff` · `ai-model-handoff` · `ai-token-optimizer`*
