# agent-foundation

**Category:** Operations  
**Trigger:** Any request to set up a structured, persistent workspace for an AI agent to operate in over time

---

## What It Does

Builds the full file and folder system that makes an AI agent consistent, domain-aware, and self-improving across sessions. Creates a hierarchical configuration: a root `CLAUDE.md` for global defaults, workstation `CLAUDE.md` files for domain specialization, project folders for bounded work, and `MEMORY.md` files at every level as the learning layer. Optionally analyzes existing work samples to extract real behavioral patterns before locking in rules — so the agent starts calibrated to how you actually work, not generic defaults.

---

## When to Use

- Setting up a new AI agent workspace from scratch
- Adding a new workstation (domain area) to an existing system
- Extracting your behavioral patterns into explicit rules an agent can follow
- Structuring an agent environment for a team with shared standards
- Migrating from ad-hoc prompting to a durable, organized system

---

## Trigger Phrases

- "Set up my agent workspace"
- "Create a workstation for [domain]"
- "Build my Claude OS"
- "Help me structure my agent environment"
- "Create a CLAUDE.md for [area]"
- "I want my agent to remember my preferences"
- "Set up [area] as a workstation"

---

## Key Inputs

| Input | Required? | Notes |
|---|---|---|
| Agent platform | ✅ | Cowork, Claude Projects, API, other |
| Root workspace path | ✅ | Where the system lives on disk |
| Domains / workstation names | ✅ | What recurring areas of work exist |
| Existing work samples | Optional | Emails, docs, outputs — enables pattern extraction |
| Known preferences | Optional | Anything you already know you want |
| Active projects | Optional | Any bounded work to set up project folders for |

---

## Outputs

1. **Root `CLAUDE.md`** — Global defaults: voice, tone, model selection logic, universal behavioral rules (under 300 lines)
2. **Workstation folders** — One per domain, each with `CLAUDE.md` (domain overrides), `MEMORY.md` (empty, ready for corrections), and `Resources/` subfolder
3. **Project folders** — For any active one-off work, each with `CLAUDE.md` + `MEMORY.md`
4. **System Map** — A reference document showing the full structure, how to use it, and the rule hierarchy

---

## The Layer System

```
Project CLAUDE.md        ← most specific; overrides everything below
    ↓ stacks on
Workstation CLAUDE.md    ← domain rules; overrides root
    ↓ stacks on
Root CLAUDE.md           ← universal defaults; applies everywhere
```

---

## The Memory Layer

Every folder has a `MEMORY.md`. When you correct the agent or establish a preference, it writes a dated entry to the relevant file. Corrections compound — the agent improves in each domain over time. Files are append-only; entries are never deleted.

---

## Pattern Extraction

When existing work samples are provided, the skill runs a pattern extraction pass before finalizing any workstation rules. It reads your actual work, identifies recurring patterns (openers, closers, formality level, structural preferences, relationship-specific behaviors), drafts them as explicit Editorial Rules, and asks you to verify before locking anything in. Unverified patterns never go into `CLAUDE.md`.

---

## Example System Map

```
~/Documents/Agent OS/
├── CLAUDE.md              ← Global: voice, model defaults, universal rules
├── MEMORY.md
│
├── Client Work/
│   ├── CLAUDE.md          ← Formal tone, client-facing output standards
│   ├── MEMORY.md
│   └── Resources/
│
├── Research/
│   ├── CLAUDE.md          ← Source integrity rules, output format for briefings
│   ├── MEMORY.md
│   └── Resources/
│
└── Projects/
    └── Q4-Strategy/
        ├── CLAUDE.md      ← Project-specific overrides
        └── MEMORY.md
```
