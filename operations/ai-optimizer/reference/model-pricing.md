[model-pricing.md](https://github.com/user-attachments/files/28345722/model-pricing.md)
# Reference: Model Pricing

**Last verified:** May 2026  
⚠️ **Model pricing changes frequently. Always verify against provider pricing pages before budgeting.**

---

## Pricing by Tier

### Tier 1 — Fast / Economical

| Model | Provider | Input (per 1M tokens) | Output (per 1M tokens) | Context Window |
|---|---|---|---|---|
| Claude Haiku 3.5 | Anthropic | $0.80 | $4.00 | 200K |
| GPT-4o mini | OpenAI | $0.15 | $0.60 | 128K |
| Gemini Flash 2.0 | Google | $0.10 | $0.40 | 1M |
| Gemini Flash 2.0 (8B) | Google | $0.04 | $0.15 | 1M |
| Mistral 7B | Mistral | $0.10 | $0.30 | 32K |

### Tier 2 — Mid-Tier / Balanced

| Model | Provider | Input (per 1M tokens) | Output (per 1M tokens) | Context Window |
|---|---|---|---|---|
| Claude Sonnet 4.6 | Anthropic | $3.00 | $15.00 | 200K |
| GPT-4o | OpenAI | $2.50 | $10.00 | 128K |
| Gemini Pro 3.1 | Google | $1.25 | $5.00 | 2M |
| Mistral Large | Mistral | $2.00 | $6.00 | 128K |
| Grok 4.1 | xAI | $3.00 | $15.00 | 2M |

### Tier 3 — Frontier / Premium

| Model | Provider | Input (per 1M tokens) | Output (per 1M tokens) | Context Window |
|---|---|---|---|---|
| Claude Opus 4.6 | Anthropic | $15.00 | $75.00 | 200K |
| GPT-5 | OpenAI | $10.00 | $40.00 | 1M |
| Gemini Ultra 3.1 | Google | $10.00 | $40.00 | 2M |
| DeepSeek R1 | DeepSeek | $0.55 | $2.19 | 128K |
| Grok 4.0 | xAI | $5.00 | $25.00 | 2M |

### Specialized / Open-Weight

| Model | Provider | Pricing Model | Notes |
|---|---|---|---|
| Meta Llama 4 (self-hosted) | Meta | Infrastructure cost only | No per-token cost once deployed |
| Mistral (self-hosted) | Mistral | Infrastructure cost only | Open weights available |
| DeepSeek V3 (self-hosted) | DeepSeek | Infrastructure cost only | Open weights available |
| Perplexity Pro | Perplexity | ~$5/1K queries | Search-native; not per-token |
| Cursor | Anysphere | Credit-based (~$20/mo base) | IDE-native; credits deplete by model |
| Windsurf | Codeium | $15/mo base | IDE-native; similar to Cursor |
| GitHub Copilot | Microsoft | $10–19/user/mo | Repo-integrated; not per-token |
| M365 Copilot | Microsoft | $30/user/mo | M365-embedded; not per-token |

---

## Cost Calculation Reference

### Formula
```
Cost per call = (input_tokens / 1,000,000 × input_price) + (output_tokens / 1,000,000 × output_price)
```

### Quick Reference — Cost per 1K Calls

Assumes 1,000 input tokens + 500 output tokens per call (typical):

| Model | Cost per 1K calls | Cost per 1M calls |
|---|---|---|
| Gemini Flash 2.0 | $0.30 | $300 |
| GPT-4o mini | $0.45 | $450 |
| Claude Haiku 3.5 | $2.80 | $2,800 |
| Gemini Pro 3.1 | $3.75 | $3,750 |
| GPT-4o | $7.50 | $7,500 |
| Claude Sonnet 4.6 | $10.50 | $10,500 |
| GPT-5 | $30.00 | $30,000 |
| Claude Opus 4.6 | $52.50 | $52,500 |

### Context Window Cost Impact

The cost of a long context window compounds across every call:

| Context Length | Sonnet 4.6 cost per call | Daily cost at 1K calls |
|---|---|---|
| 1,000 tokens | $0.003 | $3.00 |
| 5,000 tokens | $0.015 | $15.00 |
| 20,000 tokens | $0.060 | $60.00 |
| 50,000 tokens | $0.150 | $150.00 |
| 100,000 tokens | $0.300 | $300.00 |

**This is the core argument for context compression.** A 50K context window that can be compressed to 10K saves $120/day at 1K calls.

---

## Prompt Caching Discounts

Some providers offer significant discounts for cached (repeated) prompt prefixes:

| Provider | Cache Discount | Min Cache Size |
|---|---|---|
| Anthropic (Claude) | 90% off cached input tokens | 1,024 tokens |
| OpenAI | 50% off cached input tokens | 1,024 tokens |
| Google (Gemini) | ~75% off cached tokens | 32K tokens |

**Caching is the single highest-ROI optimization for high-volume workflows with consistent system prompts.**

Example: 4,000-token system prompt on Claude Sonnet at 10K calls/day:
- Without caching: $120/day
- With caching: $12/day
- **Savings: $108/day / $3,240/month**

---

## Provider Pricing Pages

Always verify before budgeting:
- Anthropic: https://www.anthropic.com/pricing
- OpenAI: https://openai.com/api/pricing
- Google: https://ai.google.dev/pricing
- Mistral: https://mistral.ai/technology/#pricing
- xAI (Grok): https://x.ai/api
- DeepSeek: https://platform.deepseek.com/api-docs/pricing
- Perplexity: https://www.perplexity.ai/pro
