# claude-skills

A curated library of Claude skills for consulting, advisory, research, and operations teams. Each skill is a structured prompt system that gives Claude a specialized workflow, quality standard, and output format for a specific job.

All skills are **generic and company-agnostic** — configurable for any organization.

---

## What Is a Skill?

A skill is a `SKILL.md` file that Claude reads at the start of a task. It defines:
- When to activate (trigger conditions)
- How to approach the work (workflow steps)
- What to produce (output format and quality standards)
- How to handle edge cases

Skills are not plugins or code. They are structured instructions that make Claude significantly more consistent, thorough, and high-quality on a specific type of task.

---

## Skill Index

### Intelligence

| Skill | What It Does | Key Trigger |
|---|---|---|
| [client-intelligence-scan](intelligence/client-intelligence-scan/) | Five-dimension real-time intelligence briefing for a specific company or client | "What's going on in [client's] space?" |
| [competitive-dynamics](intelligence/competitive-dynamics/) | Extracts competitive positioning, players, win/loss signals, and white space from source documents | "Map the competitive dynamics in this doc" |
| [security-gut-check](intelligence/security-gut-check/) | Defensive trust audit across seven risk domains for any workflow, system, or automation | "Security review this" or "gut check this workflow" |

### Engagement

| Skill | What It Does | Key Trigger |
|---|---|---|
| [engagement-quality-gate](engagement/engagement-quality-gate/) | Final QA checkpoint before delivery; produces quality review + engagement case study | "Review this before it goes out" |
| [value-opportunity-gateway](engagement/value-opportunity-gateway/) | Strategic overlay to surface cross-sell, up-sell, and expansion opportunities across any engagement | "What should we be offering this client?" |

### Sales & Growth

| Skill | What It Does | Key Trigger |
|---|---|---|
| [proposal-deck-builder](sales-and-growth/proposal-deck-builder/) | Intelligence-driven `.pptx` proposal builder for named prospects | "Build a proposal for [company]" |
| [partner-maturity-assessment](sales-and-growth/partner-maturity-assessment/) | Scores a company's partner ecosystem across 7 partner types and 5 dimensions | "Assess [company]'s partner program" |

### Optimization

| Skill | What It Does | Key Trigger |
|---|---|---|
| [humanizer](optimization/humanizer/) | Removes AI writing tells and restores human voice | "This sounds like AI, fix it" || [ux-law-reviewer](optimization/ux-law-reviewer/) | Evaluates UI designs against all 30 Laws of UX across six domains; runs as review or proactive checklist | "Review this design" or "UX audit this" |

### Operations

| Skill | What It Does | Key Trigger |
|---|---|---|
| [scrum-standup-monitor](operations/scrum-standup-monitor/) | Transforms standup transcripts into a structured dashboard and 1-page tear sheet | "Here's our standup" |
| [session-handoff](operations/session-handoff/) | Compacts a working session into a portable handoff document with goals, context, artifacts, decisions, and next steps | `/handoff` or "compact this session" |
| [agent-foundation](operations/agent-foundation/) | Builds a hierarchical CLAUDE.md + MEMORY.md workspace system for persistent, domain-aware agent behavior | "Set up my agent workspace" |

---

## How to Use a Skill

### Option A: Paste into System Prompt
Copy the contents of a `SKILL.md` file into Claude's system prompt (via API or Claude Projects). Claude will follow the skill's workflow for the relevant task type.

### Option B: Reference in Conversation
Paste the `SKILL.md` contents at the start of a conversation:
```
Use the following skill for this task:

[paste SKILL.md contents]

Now: [your task]
```

### Option C: Claude Projects (Recommended)
Upload `SKILL.md` files to a Claude Project's knowledge base. Claude will reference them automatically when the trigger conditions match.

---

## Skill Structure

Every skill folder contains:

```
skill-name/
├── SKILL.md       # The skill — trigger logic, workflow, quality standards, output format
├── README.md      # Human-readable card — what it does, when to use, example output
└── examples/      # (optional) Sample inputs and outputs
```

---

## Configuration Skills

Some skills require customization before use. These are marked in their `README.md` under **Setup Required**. The `value-opportunity-gateway` and `proposal-deck-builder` skills in particular contain `[Customize: ...]` placeholders that you replace with your organization's specific service pillars, differentiators, and narrative language.

---

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for how to add a new skill or improve an existing one.

---

## License

MIT — use, modify, and build on freely.
