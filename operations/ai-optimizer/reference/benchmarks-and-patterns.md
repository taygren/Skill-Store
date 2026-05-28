# Reference: Token Benchmarks

Typical token counts for common task types. Use for `/estimate` calculations and budget planning.

⚠️ These are directional benchmarks. Actual counts vary with prompt quality, output length, and content complexity.

---

## Input Token Benchmarks

### System Prompts
| System Prompt Type | Typical Range | Optimized Target |
|---|---|---|
| Simple role + task | 50–150 tokens | < 100 tokens |
| Standard assistant | 150–400 tokens | < 250 tokens |
| Detailed behavioral rules | 400–1,000 tokens | < 600 tokens |
| Complex agent persona | 1,000–3,000 tokens | < 1,500 tokens |
| Full skill/SKILL.md | 2,000–8,000 tokens | < 5,000 tokens |

### User Inputs
| Input Type | Typical Range |
|---|---|
| Single question | 10–50 tokens |
| Short task description | 50–150 tokens |
| Paragraph of context | 150–300 tokens |
| Email or short document | 300–800 tokens |
| Long document (1,000 words) | 1,200–1,500 tokens |
| Long document (5,000 words) | 6,000–7,500 tokens |
| Code file (200 lines) | 500–800 tokens |
| Code file (1,000 lines) | 2,500–4,000 tokens |

### Context / Conversation History
| History Length | Approximate Tokens |
|---|---|
| 5 turns (typical exchange) | 500–2,000 tokens |
| 10 turns | 1,000–4,000 tokens |
| 20 turns | 2,000–10,000 tokens |
| 50 turns | 5,000–30,000 tokens |
| Full research session | 20,000–80,000 tokens |

---

## Output Token Benchmarks

### Common Output Types
| Output Type | Typical Range |
|---|---|
| Single sentence answer | 15–40 tokens |
| Short paragraph | 75–150 tokens |
| Email (standard) | 150–400 tokens |
| Executive summary | 200–500 tokens |
| 500-word article | 600–750 tokens |
| Code function (simple) | 100–300 tokens |
| Code function (complex) | 300–1,000 tokens |
| Structured JSON (10 fields) | 100–200 tokens |
| Structured JSON (50 fields) | 500–1,000 tokens |
| Analysis report (1,500 words) | 1,800–2,500 tokens |
| Full document draft | 2,000–6,000 tokens |

---

## Task Type Benchmarks (Total Per Call)

### Tier 1 Tasks (target < 2,000 tokens total)
| Task | Input Est. | Output Est. | Total Est. |
|---|---|---|---|
| Classify a support ticket | 200–400 | 20–50 | 220–450 |
| Extract fields from document | 500–1,500 | 100–300 | 600–1,800 |
| Fill a template | 300–600 | 200–500 | 500–1,100 |
| Translate short text | 200–500 | 200–500 | 400–1,000 |
| Summarize email | 400–800 | 100–200 | 500–1,000 |

### Tier 2 Tasks (target 2,000–8,000 tokens total)
| Task | Input Est. | Output Est. | Total Est. |
|---|---|---|---|
| Draft a professional email | 200–500 | 200–400 | 400–900 |
| Analyze a document | 1,500–4,000 | 400–800 | 1,900–4,800 |
| Write a code function | 300–800 | 300–800 | 600–1,600 |
| Research synthesis (3 sources) | 3,000–6,000 | 500–1,000 | 3,500–7,000 |
| QA a document for errors | 2,000–5,000 | 300–600 | 2,300–5,600 |

### Tier 3 Tasks (expect 8,000+ tokens total)
| Task | Input Est. | Output Est. | Total Est. |
|---|---|---|---|
| Complex multi-step analysis | 2,000–5,000 | 1,000–3,000 | 3,000–8,000 |
| Architecture decision with tradeoffs | 1,000–3,000 | 1,500–4,000 | 2,500–7,000 |
| Full report generation | 3,000–8,000 | 2,000–6,000 | 5,000–14,000 |
| Agent task (5+ steps) | 5,000–15,000 | 2,000–5,000 | 7,000–20,000 |
| Extended reasoning problem | 1,000–3,000 | 2,000–8,000 | 3,000–11,000 |

---

## Tokens Per Word / Character Reference

| Unit | Approximate Tokens |
|---|---|
| 1 word (English) | ~1.3 tokens |
| 100 words | ~130 tokens |
| 1,000 words | ~1,300 tokens |
| 1 character (code) | ~0.25 tokens |
| 1 line of code | ~5–15 tokens |
| 1 paragraph | ~75–150 tokens |
| 1 page (400 words) | ~520 tokens |

---

# Reference: Optimization Patterns

Reusable prompt patterns with token benchmarks. Drop-in replacements for common verbose patterns.

---

## Pattern Library

### Pattern 1: Efficient Role Definition
**Use when:** Setting up an agent or assistant persona.

```
# Verbose (78 tokens)
You are an expert senior software engineer with 15 years of experience at top technology 
companies. You are highly skilled in Python, system design, and best practices. You write 
clean, maintainable, well-documented code and always consider edge cases.

# Optimized (21 tokens)
You are a senior software engineer. Write clean, well-documented Python. Consider edge cases.
```
**Savings:** 57 tokens per call

---

### Pattern 2: Efficient Output Format Spec
**Use when:** Specifying structured output.

```
# Verbose (52 tokens)
Please format your response as a JSON object. The JSON should include the following fields: 
a "title" field containing the title as a string, a "summary" field with a brief summary, 
and a "tags" field containing an array of relevant tags.

# Optimized (17 tokens)
Respond in JSON: {"title": string, "summary": string, "tags": [string]}
```
**Savings:** 35 tokens per call

---

### Pattern 3: Efficient Constraint Block
**Use when:** Setting behavioral constraints.

```
# Verbose (67 tokens)
Please make sure that your response is concise and to the point. Do not include any 
unnecessary information or padding. Please avoid repeating information you have already 
stated. Do not include a preamble or introduction before getting to the answer.

# Optimized (14 tokens)
Be concise. No preamble. No repetition.
```
**Savings:** 53 tokens per call

---

### Pattern 4: Efficient Few-Shot Example
**Use when:** Providing an example for output format.

```
# Verbose (94 tokens)
Here is an example to help you understand the format I'm looking for:
Input: "The customer is very unhappy with the delivery time."
Output: {"sentiment": "negative", "topic": "delivery", "intensity": "high"}

Please follow this exact format for your response.

# Optimized (38 tokens)
Format: {"sentiment": pos/neg/neutral, "topic": string, "intensity": low/med/high}
Example: "Unhappy with delivery" → {"sentiment":"negative","topic":"delivery","intensity":"high"}
```
**Savings:** 56 tokens per call

---

### Pattern 5: Efficient Context Block
**Use when:** Providing background context.

```
# Verbose (89 tokens)
I work at a company called Acme Corp. We are a B2B SaaS company that provides inventory 
management software to mid-market retailers. Our typical customer is an operations manager 
at a retail company with between 50 and 500 employees. Our product has been on the market 
for 3 years and we currently have about 200 customers.

# Optimized (32 tokens)
Company: Acme Corp — B2B inventory SaaS for mid-market retail ops managers.
Stage: 3 years, 200 customers.
```
**Savings:** 57 tokens per call

---

### Pattern 6: Efficient Chain-of-Thought Request
**Use when:** Requesting step-by-step reasoning.

```
# Verbose (42 tokens)
Please think through this problem carefully, step by step, before arriving at your final 
answer. Show your reasoning process.

# Optimized (8 tokens)
Think step by step. Show reasoning.
```
**Savings:** 34 tokens per call

---

### Pattern 7: Efficient Negative Constraints
**Use when:** Telling the model what not to do.

```
# Verbose (remove entirely — 38 tokens wasted)
Please make sure not to make up any information that you are not sure about. Only include 
information that you are confident is accurate and factual.

# Optimized (remove — this is default model behavior)
[delete entirely]
```
**Savings:** 38 tokens per call

---

### Pattern 8: Efficient Length Control
**Use when:** Controlling output length.

```
# Verbose (24 tokens)
Please keep your response brief and concise, ideally no longer than a few sentences.

# Optimized (6 tokens)
Respond in 2–3 sentences.
```
**Savings:** 18 tokens per call — and the optimized version is more precise.

---

## Cumulative Pattern Impact

If a prompt uses all 8 patterns in their verbose form:

| Pattern | Tokens Wasted |
|---|---|
| Role definition | 57 |
| Output format | 35 |
| Constraints | 53 |
| Few-shot example | 56 |
| Context block | 57 |
| Chain-of-thought | 34 |
| Negative constraints | 38 |
| Length control | 18 |
| **Total** | **348 tokens** |

At 1,000 calls/day on Claude Sonnet 4.6:
- 348 tokens × 1,000 calls = 348,000 tokens/day
- 348,000 × $3.00/1M = **$1.04/day = $31.20/month**

From a single prompt, before any output optimization.
