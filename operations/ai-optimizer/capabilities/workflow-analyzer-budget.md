[workflow-analyzer-budget.md](https://github.com/user-attachments/files/28345698/workflow-analyzer-budget.md)
# Capability: Workflow Cost Analyzer

**Command:** `/analyze-workflow [description]`  
**Purpose:** Audit a described AI workflow or agent pipeline for cost inefficiencies. Rank findings by savings opportunity. Flag where ai-model-handoff routing applies.

---

## Workflow Decomposition

Before auditing, map the workflow into discrete steps:

```
Step [N]: [Name]
  Input: [what enters this step]
  Model: [what model currently handles it]
  Output: [what this step produces]
  Downstream: [what consumes this output]
```

---

## Inefficiency Pattern Library

### Pattern 1: Frontier Model Overuse
**What it is:** Using Tier 3 (frontier) models for tasks that Tier 1 or Tier 2 handles equally well.

**Detection signals:**
- Step is classification, extraction, formatting, or template filling → should be Tier 1
- Step is standard writing, summarization, or code generation → should be Tier 2
- Model is Claude Opus / GPT-5 / Gemini Ultra for a task with no multi-step reasoning

**Cost impact:** 10–50x cost premium over appropriate tier. Highest-impact finding in most pipelines.

**Fix:** Downgrade model to appropriate tier. Run quality comparison before committing.

---

### Pattern 2: Context Passed Unnecessarily
**What it is:** Full conversation history or large documents passed to every step when only a subset is needed.

**Detection signals:**
- Every pipeline step receives the full conversation history
- A document is re-passed to each step instead of being summarized once upstream
- A step only uses 10% of the context it receives

**Cost impact:** Linear with context size. A 50K token context passed to 5 steps = 250K tokens in context costs alone.

**Fix:** Pass only the output of the prior step, not the full history. Summarize large inputs upstream. Use targeted extraction before routing to downstream steps.

---

### Pattern 3: Sequential Steps That Could Be Parallel
**What it is:** Independent steps executed one-at-a-time when they could run simultaneously.

**Detection signals:**
- Step B and Step C both consume the output of Step A but don't depend on each other
- Multiple research or analysis tasks queued sequentially

**Cost impact:** No token cost reduction — but reduces wall-clock time and therefore cost in time-sensitive workflows. Parallel execution can cut pipeline time by 50–70%.

**Fix:** Identify independent branches. Run them in parallel. Merge outputs in a final synthesis step.

---

### Pattern 4: Re-Processing Inefficiency
**What it is:** One step produces output that a downstream step immediately transforms or summarizes — when the upstream step could have produced the right format directly.

**Detection signals:**
- Step 3 summarizes the output of Step 2, which could have been produced as a summary in Step 2
- A formatting step follows every generation step because outputs aren't formatted at source
- A validation step re-reads and re-evaluates everything the prior step produced

**Cost impact:** Doubles the token cost of affected steps.

**Fix:** Specify output format in the upstream step. Eliminate redundant transformation steps.

---

### Pattern 5: Cacheable Outputs Not Cached
**What it is:** Identical or near-identical inputs being processed repeatedly when the output could be cached.

**Detection signals:**
- The same document is being summarized on every pipeline run
- The same system prompt is being processed with identical preamble on every call
- FAQs, reference documents, or static context are re-ingested every run

**Cost impact:** Proportional to call volume. At 1,000 calls/day, caching a 2,000-token preamble saves ~$3/day on Sonnet.

**Fix:** Implement prompt caching (Claude, OpenAI support this natively). Cache static context outside the model call. Pre-compute outputs for deterministic inputs.

---

### Pattern 6: Missing Human Checkpoint
**What it is:** Error-prone steps proceeding without human review, leading to downstream rework that costs more tokens than a checkpoint would have.

**Detection signals:**
- High-variance generation steps (creative, strategic, subjective) feeding directly into irreversible downstream steps
- Pipelines where a wrong output in Step 2 causes all subsequent steps to fail and restart

**Cost impact:** Rework multiplies token cost. A 10-step pipeline that fails at Step 8 and restarts wastes 8 steps of compute.

**Fix:** Place human checkpoints at high-variance steps before irreversible downstream actions. This reduces tokens, not increases them — catching errors early is always cheaper.

---

### Pattern 7: Wrong Platform for the Task
**What it is:** Using a general chat model for a task that belongs on a specialized platform.

**Detection signals:**
- Pipeline steps requiring real-time web data are running on Claude or GPT without search enabled
- Code changes to an actual codebase are being generated in chat and copy-pasted manually
- Document editing is being done by pasting Word/Excel content into a chat model instead of using Copilot natively

**Cost impact:** Indirect — chat models used for search tasks produce lower quality outputs, requiring more correction iterations. IDE tasks via chat are slower and error-prone.

**Fix:** Route to the appropriate platform via ai-model-handoff. Flag which steps should move.

---

## Workflow Audit Output

```
━━━ WORKFLOW COST AUDIT ━━━━━━━━━━━━━━━━━━━━━━━━━
Workflow: [name/description]
Steps analyzed: [N]
Current estimated cost: $[X]/run | $[X]/month at [volume]

EFFICIENCY SCORE: [N]/10

FINDINGS (ranked by savings opportunity)

🔴 #1 — [Pattern Name] — [Step(s) affected]
   Issue: [Specific description of the inefficiency]
   Current cost contribution: ~$[X]/month
   Fix: [Specific recommendation]
   Savings potential: ~$[X]/month ([X]%)
   Effort: [Low / Medium / High]
   Handoff required: [Yes → /handoff to [platform] / No]

🟠 #2 — [Pattern Name] — [Step(s) affected]
   [same structure]

🟡 #3 — [Pattern Name] — [Step(s) affected]
   [same structure]

TOTAL SAVINGS OPPORTUNITY
Conservative: $[X]/month | Aggressive: $[X]/month
Current run rate: $[X]/month | Optimized run rate: $[X]/month

RECOMMENDED ACTION ORDER
1. [Highest ROI fix first — specific action]
2. [Second action]
3. [Third action]

PLATFORM ROUTING RECOMMENDATIONS
[Steps that should move to a different platform via ai-model-handoff]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

---

# Capability: Token Budget Planner

**Command:** `/budget [monthly $ target]`  
**Purpose:** Design AI usage within a defined monthly spend target. Allocate tokens intelligently across use cases, recommend model tiers, and set alert thresholds.

---

## Budget Planning Process

### Step 1: Usage Inventory

Gather current or planned usage:
- Primary use cases (list each distinct task type)
- Estimated call volume per use case per day
- Current model assignment per use case
- Typical token count per call (input + output)

### Step 2: Spend Decomposition

Break down where the budget goes:

```
Use Case          | Model  | Calls/Day | Tokens/Call | Cost/Day | Cost/Month
──────────────────|────────|───────────|─────────────|──────────|───────────
[Use case 1]      | [model]| [N]       | [N]         | $[X]     | $[X]
[Use case 2]      | [model]| [N]       | [N]         | $[X]     | $[X]
Total             |        |           |             | $[X]     | $[X]
```

### Step 3: Optimization Pass

For each use case, ask:
1. Is this the right model tier for this task?
2. Is the prompt optimized (run /audit if not)?
3. Are outputs being cached where possible?
4. Is context being passed efficiently?

### Step 4: Budget Allocation

Allocate the monthly budget across use cases based on value and volume:

```
BUDGET ALLOCATION PLAN
Monthly target: $[X]

High-value / high-volume (allocate 50–60%):
  [Use case] → [model] → $[X]/month

Standard operations (allocate 25–35%):
  [Use case] → [model] → $[X]/month

Exploratory / one-off (allocate 10–15%):
  [Use case] → [model] → $[X]/month

Buffer for overruns: 10%

Total allocated: $[X] / Budget: $[X]
```

### Step 5: Alert Thresholds

Set spending alerts at:
- **50% of budget** — review and confirm on track
- **75% of budget** — assess if high-value use cases are consuming disproportionate share
- **90% of budget** — restrict non-essential calls for the remainder of the period

---

## Token Budget Per Call

For any given call, allocate tokens across four components:

| Component | Conservative | Balanced | Liberal |
|---|---|---|---|
| System prompt | < 500 tokens | 500–1,500 | 1,500–3,000 |
| Context / history | < 2,000 tokens | 2,000–8,000 | 8,000–20,000 |
| User input | < 500 tokens | 500–2,000 | 2,000–5,000 |
| Expected output | < 500 tokens | 500–2,000 | 2,000–5,000 |
| **Total per call** | **< 3,500** | **3,500–13,500** | **13,500–33,000** |

**System prompt is the highest-leverage component.** It's paid on every single call. A 2,000-token system prompt at 1,000 calls/day costs $90/month on Sonnet pricing for input alone — before any user input or output.

---

## Budget Output Format

```
━━━ TOKEN BUDGET PLAN ━━━━━━━━━━━━━━━━━━━━━━━━━━━
Monthly target: $[X]
Usage profile: [description]

CURRENT STATE
Estimated current spend: $[X]/month
Primary cost drivers: [top 2–3 use cases]

OPTIMIZED ALLOCATION
[Use case table with model, volume, and cost per use case]

TOTAL: $[X]/month | Δ from current: $[X] ([X]%)

MODEL RECOMMENDATIONS BY USE CASE
[Use case]: [model recommendation with rationale]

PROMPT OPTIMIZATION PRIORITY
High priority (optimize first — biggest savings):
  [Use case] → run /audit and /rewrite[balanced]

ALERT THRESHOLDS
50% ($[X]): [Date estimate at current rate]
75% ($[X]): [Date estimate]
90% ($[X]): [Date estimate] — restrict non-essential calls

MONTHLY SAVINGS VS. UNOPTIMIZED
Conservative estimate: $[X]/month
Aggressive estimate:   $[X]/month

⚠️ Pricing verified as of [date]. Review monthly — model pricing changes.
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
