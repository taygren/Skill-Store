[_template.md](https://github.com/user-attachments/files/28306382/_template.md)
# Platform Profile: [Platform Name]

**Provider:** [Company]  
**Current Flagship:** [Model name / version]  
**Interface:** [Web / API / IDE / CLI / other]

---

## Strengths
- [Strength 1 — specific capability]
- [Strength 2]
- [Strength 3]

## Weaknesses
- [Weakness 1 — specific limitation]
- [Weakness 2]

## Context Window
- [Model]: [token count]
- Behavior: [How it handles long context — degrades / holds well / truncates]

## Memory & Persistence
- [Memory feature 1]: [description]
- [No cross-session memory / describe what persists]
- **Handoff note:** [How to ensure context survives across sessions on this platform]

## System Prompt Support
- ✅ / ⚠️ / ❌ [Interface type]: [notes on system prompt behavior]
- [Additional notes]

## Tool Availability
- [Tool 1] ([native / via plugin / not available])
- [Tool 2]
- [Tool 3]

## Prompt Format Conventions
- [Convention 1 — how prompts should be structured for best results]
- [Convention 2]
- [Convention 3]

## Ideal Task Types
- [Task type 1 — specific, not generic]
- [Task type 2]
- [Task type 3]

---

## Handoff Receiving Template

```
=== [PLATFORM NAME] HANDOFF PACKAGE ===
Project: [name]
Handed off from: [platform] ([phase])
Receiving: [Platform Name] ([phase])

[System context — format per this platform's conventions]

Context: [2-sentence project description]
Your role: [specific role]

Current goal: [one sentence outcome]

What exists:
- [Artifact 1] — [status]

Decisions already made:
- [Decision]: [choice] — [reasoning]

Your task:
1. [First action]
2. [Second action]

Must not change:
- [Hard constraints]

Re-entry: When complete, provide full output + summary.
Run: /handoff return from [Platform Name]

=== END ===
```

## Configuration Checklist
- [ ] [Pre-paste setup step 1]
- [ ] [Pre-paste setup step 2]
- [ ] [Model selection note if relevant]

---

## Notes for Profile Author
When completing this template:
- Strengths should be specific capabilities, not marketing language
- Weaknesses must be honest — a profile that hides weaknesses produces bad handoffs
- Context window behavior matters more than the raw number — note how quality degrades
- Handoff receiving template should be copy-paste ready, not a description of a template
- Configuration checklist should include only things that actually matter before pasting
