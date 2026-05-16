# humanizer

**Category:** Optimization  
**Trigger:** Text sounds robotic, AI-generated, or needs voice added — any rewrite request

---

## What It Does

Rewrites prose to remove the statistical fingerprints of LLM-generated text and replace them with genuine human voice. Two jobs: (1) strip AI tells — em dashes, triadic structures, significance inflation, promotional adjectives, hedge-laden constructions; (2) put a real person back in — opinions, rhythm variation, specificity, honest complexity.

Based on Wikipedia's documented "Signs of AI Writing" guide (29 patterns). The skill runs a mandatory audit pass after first draft to catch residual tells before delivering.

---

## When to Use

- Blog posts, essays, LinkedIn content that sound robotic
- Marketing copy or email campaigns with AI-ish phrasing
- Any piece where the output needs to pass as human-written
- Editing your own AI-assisted drafts before publishing

---

## Trigger Phrases

- "Humanize this"
- "This sounds like AI, fix it"
- "Make this sound more natural"
- "Remove the AI feel from this"
- "Rewrite this in my voice" (provide a writing sample)

---

## Key Inputs

| Input | Required? | Notes |
|---|---|---|
| Text to rewrite | ✅ | Any length |
| Writing sample | Optional | Paste or link; enables voice calibration to match your style |

---

## Output

- **Short snippets:** Rewrite only, optionally with one line on what changed
- **Medium pieces:** Draft → audit bullets → final rewrite
- **Long pieces:** Section-by-section with checkpoints

---

## Common AI Tells Removed

`em dashes as dramatic pauses` · `rule of three` · `"vibrant" / "groundbreaking" / "seamless"` · `"marks a pivotal moment"` · `"serves as" instead of "is"` · `hedge stacking ("could potentially possibly")` · `present-participle tails ("...highlighting the broader trend")` · `sycophantic openers` · `generic positive conclusions`

---

## The Audit Pass

After first draft, the skill internally asks: *"What still makes this obviously AI-generated?"* — answers honestly in 2–4 bullets — then rewrites again targeting each one. This is the highest-leverage step and is never skipped.

---

## License

MIT
