[prompt-auditor.md](https://github.com/user-attachments/files/28345652/prompt-auditor.md)
# Capability: Prompt Auditor

**Command:** `/audit [prompt]`  
**Purpose:** Analyze any prompt and identify token waste without degrading intent or output quality.

---

## Audit Process

### Step 1: Component Parsing

Break the prompt into its structural components and score each:

| Component | Token Efficiency Target | Common Issues |
|---|---|---|
| **Role definition** | 1–2 sentences max | Over-specified personas, theatrical character descriptions |
| **Context block** | Only what the model can't infer | Background the model already knows, repeated facts |
| **Instructions** | Each instruction one line | Redundancy, contradiction, default behavior re-stated |
| **Examples** | Minimum effective count | Too many examples, examples that are too long |
| **Format specification** | Explicit and brief | Described in prose when a template would be shorter |
| **Constraints** | Non-default constraints only | Stating what the model already does by default |
| **Closing remarks** | None needed | "Thank you", "I appreciate your help", "Please try your best" |

---

### Step 2: Waste Pattern Detection

Scan for all of the following. Flag each instance with category, location, and estimated token cost.

---

#### Category 1: Politeness Overhead
Phrases that consume tokens with zero effect on output quality.

**Patterns to flag:**
- "Please", "Could you", "Would you mind", "I would appreciate if"
- "Thank you in advance", "I appreciate your help"
- "Please try your best", "Do your best to"
- "Feel free to", "Don't hesitate to"
- Any sentence that begins with acknowledgment of the AI's capabilities

**Token cost:** 2–8 tokens per instance. Compounds significantly in system prompts applied to every call.

---

#### Category 2: Redundant Instructions
Instructions that duplicate default model behavior or repeat each other.

**Patterns to flag:**
- "Be accurate and factual" — models default to this
- "Don't make things up" — same as above
- "Be helpful" — default behavior
- "Respond in English" — default when prompt is in English
- "Read the instructions carefully" — models read all input
- Same instruction stated twice in different words
- Positive and negative versions of the same rule ("always do X" + "never do not-X")

**Token cost:** 5–20 tokens per instance.

---

#### Category 3: Context Bloat
Background information the model doesn't need or already knows.

**Patterns to flag:**
- Historical context irrelevant to the current task
- Definitions of terms the model knows (explaining what "JSON" is, for example)
- Company background in prompts where it doesn't affect the output
- Repeated context — same information provided twice in different sections
- Hedged context ("you may or may not need this, but just in case...")

**Token cost:** Highly variable — 20–500+ tokens. Highest-impact category.

---

#### Category 4: Verbose Examples
Few-shot examples that are longer than they need to be.

**Patterns to flag:**
- Examples with unnecessary setup or preamble
- Multiple examples demonstrating the same pattern (1–2 is usually sufficient)
- Examples that include the thought process when only the output format matters
- Full documents used as examples when a truncated version would demonstrate the pattern

**Token cost:** 50–500 tokens per over-specified example.

---

#### Category 5: Format Prose
Output format described in paragraph form when a template or schema would be shorter and clearer.

**Patterns to flag:**
- "Please respond with a title, followed by a brief introduction, then three to five bullet points, and a conclusion paragraph" — replace with a format template
- Describing JSON structure in prose — replace with a schema or example
- Multi-sentence format instructions — compress into a format spec

**Token cost:** 20–80 tokens. Also reduces model uncertainty, improving output consistency.

---

#### Category 6: Instruction Contradiction
Instructions that conflict, forcing the model to resolve ambiguity (consuming extra tokens in reasoning).

**Patterns to flag:**
- "Be concise" + "provide comprehensive detail"
- "Use bullet points" + "write in flowing prose"
- Role instructions that conflict with task instructions
- Tone instructions that conflict with format instructions

**Token cost:** Direct token cost is low, but indirect cost (longer model reasoning, inconsistent outputs requiring re-runs) is high.

---

#### Category 7: Over-Specified Role
Role definitions that are more theatrical than functional.

**Patterns to flag:**
- Multi-paragraph persona descriptions for simple tasks
- Character backstories irrelevant to the task
- Emotional or motivational framing ("you are passionate about...", "you deeply care about...")
- Credentials that don't affect output quality for the specific task

**Token cost:** 30–200 tokens. Worst in system prompts applied universally.

---

#### Category 8: Hedge Language
Qualifications and hedges in instructions that reduce clarity and add tokens.

**Patterns to flag:**
- "If possible", "where appropriate", "as needed", "if relevant"
- "Try to", "attempt to", "aim to" — replace with direct instruction
- "Generally speaking", "in most cases", "typically"
- "You might want to consider" — replace with "consider" or a direct instruction

**Token cost:** 3–10 tokens per instance. Death by a thousand qualifications.

---

### Step 3: Efficiency Scoring

Score the prompt across five dimensions:

| Dimension | Score | Criteria |
|---|---|---|
| **Instruction clarity** | 1–10 | Are instructions unambiguous and non-contradictory? |
| **Context necessity** | 1–10 | Is every piece of context load-bearing? |
| **Example efficiency** | 1–10 | Are examples minimum effective length and count? |
| **Format specification** | 1–10 | Is the output format specified concisely? |
| **Overhead elimination** | 1–10 | Is the prompt free of politeness, hedges, and defaults? |

**Overall efficiency score:** Average of five dimensions.

Scores below 7 on any dimension trigger a recommendation to rewrite that component.

---

### Step 4: Audit Output

```
━━━ PROMPT AUDIT ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Original token count: [N] tokens
Estimated waste:      [N] tokens ([X]%)
Recommended mode:     [light / balanced / aggressive]

EFFICIENCY SCORES
Instruction clarity:   [N]/10
Context necessity:     [N]/10
Example efficiency:    [N]/10
Format specification:  [N]/10
Overhead elimination:  [N]/10
Overall:               [N]/10

WASTE DETECTED
[#] [Category] — "[exact phrase]" — [N] tokens — [why it's waste]
[#] [Category] — "[exact phrase]" — [N] tokens — [why it's waste]

HIGHEST IMPACT CHANGES
1. [Highest token saving change] — saves ~[N] tokens
2. [Second highest] — saves ~[N] tokens
3. [Third highest] — saves ~[N] tokens

RECOMMENDATION
Run /rewrite[balanced] to apply all changes, or /rewrite[light]
to remove waste only while preserving original structure.

Est. cost at 1K calls/day ([model]):
  Current:   $[X]/month
  Optimized: $[X]/month
  Savings:   $[X]/month ([X]%)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Audit Rules

1. **Flag, don't remove silently.** Every identified waste item is shown to the user before any rewrite.
2. **Quantify everything.** Every finding includes an estimated token cost.
3. **Distinguish waste from intent.** Some "inefficient" language carries tone or relationship context — flag it but note when it may be intentional.
4. **Score before recommending mode.** The efficiency score determines which rewrite mode to recommend.
5. **Never flag what belongs.** If context is genuinely needed, don't flag it as bloat.
