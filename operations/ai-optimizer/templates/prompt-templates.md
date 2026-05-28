[prompt-templates.md](https://github.com/user-attachments/files/28345752/prompt-templates.md)
# Template: Efficient System Prompt

**Use for:** Any persistent system prompt applied across many calls.  
**Target:** < 500 tokens for standard assistants, < 1,500 for complex agents.

```
# ROLE
[One sentence. Title + 1–2 functional behavioral instructions.]

# TASK
[What this assistant does. 1–3 sentences max.]

# CONTEXT
[Only what the model can't infer. Company, product, audience — only if it affects output.]

# RULES
- [Non-default constraint 1]
- [Non-default constraint 2]
- [Non-default constraint 3]
[Keep to 3–7 rules. Remove anything that's already default model behavior.]

# FORMAT
[Output format specification. Use a template or schema, not prose description.]
[Example: Respond in JSON: {"field1": type, "field2": type}]
[Or: Structure: SUMMARY (2 sentences) → ANALYSIS (bullets) → RECOMMENDATION (1 sentence)]
```

**Token target:** 100–400 tokens  
**What to exclude:** Credentials, backstory, politeness, default behavior instructions, hedged constraints

---

---

# Template: Minimal Effective Few-Shot

**Use for:** Teaching output format via example.  
**Rule:** 1–2 examples for simple patterns. 2–3 for complex ones. Never more than 3.

```
# FORMAT
[Brief schema or template description]

# EXAMPLE
Input: [minimum representative input]
Output: [exact format you want — nothing more]

# EXAMPLE 2 (only if pattern has meaningful variation)
Input: [input that demonstrates a different case]
Output: [output for that case]
```

**What makes a good example:**
- As short as possible while still demonstrating the pattern
- Output only — no explanation of why the output looks that way
- Covers edge cases only if they're genuinely likely in production

**What to avoid:**
- Preamble: "Here is an example to help you understand..."
- Explanation: "Notice how the output includes..."
- More than 3 examples (3 is the maximum; 1–2 is usually enough)

**Token target per example:** 30–100 tokens  
**Savings vs. verbose examples:** 40–70% reduction

---

---

# Template: Chain-of-Thought with Token Controls

**Use for:** Reasoning tasks where you want the model to show its work without producing an essay.

```
# TASK
[What to reason about — 1–2 sentences]

# CONTEXT
[Only what's needed for the reasoning — no background noise]

# REASONING APPROACH
Think step by step. Show each step briefly (1–2 sentences per step).

# OUTPUT FORMAT
STEPS:
1. [step]
2. [step]
3. [step]
ANSWER: [final conclusion — 1–2 sentences]
CONFIDENCE: [high / medium / low] — [one-sentence rationale]
```

**Token controls built in:**
- "1–2 sentences per step" caps step verbosity
- Explicit format spec prevents model from writing narrative prose
- CONFIDENCE field captures uncertainty without a paragraph of hedging

**When to use extended thinking instead:**
- If the problem genuinely requires deep multi-path reasoning (math proofs, complex architecture decisions)
- Extended thinking tokens are cheaper than equivalent reasoning in the visible output on Claude
- Use `thinking: {budget_tokens: N}` API parameter to cap thinking token spend

**Token target for reasoning task:**
- Simple (3–5 steps): 400–800 total tokens
- Complex (5–10 steps): 800–2,000 total tokens
- If reasoning output exceeds 2,000 tokens: consider whether the task needs Tier 3 or whether the format is too loose
