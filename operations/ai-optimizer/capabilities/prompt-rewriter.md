[prompt-rewriter.md](https://github.com/user-attachments/files/28345688/prompt-rewriter.md)
# Capability: Prompt Rewriter

**Commands:** `/rewrite[light]` · `/rewrite[balanced]` · `/rewrite[aggressive]`  
**Purpose:** Rewrite prompts for token efficiency while preserving full intent. Three modes for three levels of aggressiveness.

---

## Rewriting Strategies

All three modes draw from the same strategy library. The mode determines which strategies are applied and how aggressively.

---

### Strategy 1: Instruction Compression
**What it does:** Condenses multi-sentence instructions into precise single statements.

**Before:**
```
When you are writing your response, please make sure that you write in a way that is 
clear and easy to understand. You should avoid using overly complex language or 
technical jargon unless it is absolutely necessary for the task.
```
**After:**
```
Write clearly. Avoid jargon unless required.
```
**Tokens saved:** ~35

---

### Strategy 2: Context Lifting
**What it does:** Moves repeated context from user turns into the system prompt. When the same background appears in every call, it belongs in the system prompt — not re-stated per message.

**Before (user turn, repeated every call):**
```
You are a customer support agent for Acme Corp, a B2B SaaS company that sells 
inventory management software to mid-market retailers. Our customers are typically 
operations managers with limited technical backgrounds.
[actual question]
```
**After (system prompt, set once):**
```
You are a customer support agent for Acme Corp — B2B inventory management SaaS 
for mid-market retail ops managers.
```
**User turn:**
```
[actual question only]
```
**Tokens saved per call:** ~40 (multiplied across every call)

---

### Strategy 3: Example Trimming
**What it does:** Reduces few-shot examples to minimum effective length and count.

**Before:**
```
Here is an example of the kind of output I'm looking for:

Input: "The quarterly revenue increased by 12% compared to last year, reaching $4.2M"
Output: {
  "metric": "quarterly revenue",
  "change_type": "increase",
  "change_value": 12,
  "change_unit": "percent",
  "absolute_value": 4200000,
  "currency": "USD",
  "time_period": "quarterly",
  "comparison": "year-over-year"
}

Here is another example:
Input: "Customer churn dropped from 8% to 5% this month"
Output: {
  "metric": "customer churn",
  "change_type": "decrease", ...
```
**After:**
```
Extract to JSON: metric, change_type, change_value, change_unit, absolute_value.
Example: "Revenue up 12% to $4.2M" → {"metric":"revenue","change_type":"increase","change_value":12,"change_unit":"percent","absolute_value":4200000}
```
**Tokens saved:** ~120

---

### Strategy 4: Format Specification
**What it does:** Replaces prose format descriptions with explicit templates or schemas.

**Before:**
```
Please structure your response with a brief executive summary at the top (2-3 sentences), 
followed by your main analysis organized into clearly labeled sections, and conclude 
with 3-5 specific, actionable recommendations.
```
**After:**
```
Format:
SUMMARY: [2–3 sentences]
ANALYSIS: [labeled sections]
RECOMMENDATIONS:
- [action 1]
- [action 2]
- [action 3]
```
**Tokens saved:** ~30, plus improved output consistency

---

### Strategy 5: Negative Instruction Removal
**What it does:** Removes "don't do X" instructions that duplicate default model behavior.

**Patterns removed:**
- "Don't make up information" → model default
- "Don't be rude or offensive" → model default
- "Don't ignore the instructions" → model default
- "Don't respond in a different language" (when prompt is in English) → model default
- "Don't include any preamble before your answer" → replace with format spec if needed

**Note:** Only remove negatives that are already default behavior. Legitimate constraints ("don't include pricing information") are kept.

---

### Strategy 6: Politeness Removal
**What it does:** Strips all politeness overhead that has zero effect on output.

**Removed patterns:**
- "Please", "Could you", "Would you mind"
- "Thank you in advance", "I appreciate your help"
- "Feel free to ask if you need clarification"
- "Do your best to", "Try your best to"
- Any opening that thanks or acknowledges the AI

**Important:** This strategy is applied in all three modes. Politeness costs tokens on every single call and produces no benefit.

---

### Strategy 7: Role Compression
**What it does:** Condenses verbose persona definitions into functional role statements.

**Before:**
```
You are an expert senior financial analyst with 20 years of experience working at 
top-tier investment banks and consulting firms. You have deep expertise in financial 
modeling, valuation, and strategic analysis. You are known for your ability to 
distill complex financial concepts into clear, actionable insights. You are 
meticulous, detail-oriented, and always back your analysis with data.
```
**After:**
```
You are a senior financial analyst. Be precise, data-backed, and actionable.
```
**Tokens saved:** ~65

**Rule:** Keep the role title and 1–2 functional behavioral instructions. Drop credentials, backstory, and personality description unless they directly affect the output.

---

### Strategy 8: Hedge Elimination
**What it does:** Replaces hedged instructions with direct ones.

| Before | After |
|---|---|
| "Try to be concise where possible" | "Be concise" |
| "If relevant, include examples" | "Include examples" or remove entirely |
| "You might want to consider..." | "Consider..." or state directly |
| "Generally speaking, you should..." | State the rule directly |
| "In most cases, prefer..." | "Prefer..." |

---

### Strategy 9: Structural Reorganization *(Balanced and Aggressive only)*
**What it does:** Reorganizes prompt components into the most efficient order for model processing.

**Optimal order:**
1. Role (1 sentence)
2. Task (what to do)
3. Context (only what's needed)
4. Constraints (non-defaults only)
5. Format spec (template or schema)
6. Examples (if needed — after format spec, not before)

Reordering reduces model uncertainty and often reduces the output tokens needed for the model to orient itself.

---

### Strategy 10: Full Reconstruction *(Aggressive only)*
**What it does:** Discards the original prompt structure entirely and rebuilds from the core intent.

Process:
1. Extract the core task: what output is actually needed?
2. Identify the minimum context required to produce that output
3. Write the most direct possible instruction set
4. Add format spec and minimal examples
5. Verify intent is fully preserved

This strategy produces the highest token reduction but may significantly change the prompt's phrasing. Always review before use.

---

## Mode Application Guide

| Strategy | Light | Balanced | Aggressive |
|---|---|---|---|
| Politeness removal | ✅ | ✅ | ✅ |
| Redundant instruction removal | ✅ | ✅ | ✅ |
| Hedge elimination | ✅ | ✅ | ✅ |
| Instruction compression | — | ✅ | ✅ |
| Context lifting | — | ✅ | ✅ |
| Example trimming | — | ✅ | ✅ |
| Format specification | — | ✅ | ✅ |
| Negative instruction removal | — | ✅ | ✅ |
| Role compression | — | ✅ | ✅ |
| Structural reorganization | — | ✅ | ✅ |
| Full reconstruction | — | — | ✅ |

---

## Rewrite Output Format

```
━━━ PROMPT REWRITE ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Mode: [light / balanced / aggressive]

BEFORE                              AFTER
──────────────────────────────────  ──────────────────────────────────
[original prompt text]              [optimized prompt text]

Token count: [N] tokens             Token count: [N] tokens

SAVINGS
Tokens removed: [N] ([X]%)
Cost at 1K calls/day ([model]): $[X]/month saved

CHANGES MADE
[#] [Strategy name]: [What changed] — saved ~[N] tokens
[#] [Strategy name]: [What changed] — saved ~[N] tokens

WHAT WAS PRESERVED
[Item]: [Why it was kept — load-bearing context, legitimate constraint, etc.]

⚠️ REVIEW BEFORE USE
[Any changes that significantly alter phrasing or structure — flag for user review]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Rewrite Rules

1. **Intent is sacred.** Every rewrite must produce equivalent output from the model. If a change would alter the output, don't make it.
2. **Show every change.** Changes log is non-optional. Every modification is explained.
3. **Flag for review.** Aggressive rewrites that significantly change phrasing are flagged explicitly.
4. **Preserve legitimate constraints.** Don't remove instructions just because they look like negatives — verify they're not load-bearing.
5. **Test the core task.** After rewriting, verify the core task instruction is still clear and unambiguous.
