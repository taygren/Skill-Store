[README.md](https://github.com/user-attachments/files/28306268/README.md)
# ai-model-handoff

**Category:** Operations  
**Trigger:** Any request to transfer work between AI platforms, or to recommend which platform to use next

---

## What It Does

Packages active working sessions into **platform-native handoff prompts** — formatted, compressed, and configured for the specific AI model or platform receiving the work. Handles forward handoffs (sending work out), return handoffs (receiving work back), platform recommendations, multi-platform comparisons, and chain planning for complex multi-hop workflows.

Every handoff preserves goals, decisions, artifacts, constraints, and re-entry instructions. Every package is formatted to match the receiving platform's conventions, not a generic paste.

---

## The Problem It Solves

Switching AI platforms mid-project normally means starting over. You re-explain context, re-establish decisions, re-paste artifacts. Each hop degrades fidelity. This skill makes switching deliberate and lossless — one command, one copy-paste, full continuity.

---

## Commands

| Command | What It Does |
|---|---|
| `/handoff to [platform]` | Package and send work to a named platform |
| `/handoff recommend` | Recommend the best platform for the next task |
| `/handoff return from [platform]` | Receive work coming back from a platform |
| `/handoff compare` | Show routing options with reasoning |
| `/handoff chain` | Plan a multi-platform workflow |

---

## Platform Registry (12 Profiles)

| Platform | Best For | Profile |
|---|---|---|
| **Claude** | Reasoning, writing, structured analysis | `platforms/claude.md` |
| **Claude Code** | Terminal-native agentic coding, repo-level work | `platforms/claude-code.md` |
| **ChatGPT** | All-purpose, multimodal, broadest tool set | `platforms/chatgpt.md` |
| **Gemini** | Google Workspace, 2M context, multimodal | `platforms/gemini.md` |
| **Copilot** | Microsoft 365 + GitHub enterprise | `platforms/copilot.md` |
| **Perplexity** | Real-time research, citation-required outputs | `platforms/perplexity.md` |
| **Grok** | X/social signals, large context, real-time data | `platforms/grok.md` |
| **DeepSeek** | Transparent reasoning, cost-sensitive, open-source | `platforms/deepseek.md` |
| **Mistral** | EU data residency, multilingual, privacy, edge | `platforms/mistral.md` |
| **Cursor** | AI-native IDE, codebase-aware, multi-file agent | `platforms/cursor.md` |
| **Meta / Llama** | Self-hosted, air-gapped, fine-tunable, open-weight | `platforms/meta-llama.md` |
| **Windsurf** | Cursor alternative, Cascade multi-file, JetBrains | `platforms/windsurf.md` |

---

## How a Handoff Works

```
1. User runs: /handoff to Cursor

2. Skill scans the session:
   — Current goal and sub-goals
   — Artifacts produced (with locations and status)
   — Decisions made (with reasoning)
   — Hard constraints

3. Loads platforms/cursor.md:
   — Cursor uses .cursor/rules for persistence
   — Agent mode needs file-referenced, acceptance-criteria-driven prompts
   — Credit-based billing: don't bloat the context unnecessarily

4. Assembles the package:
   — Strips narrative context Cursor doesn't need
   — Keeps schema, specs, constraints, file paths
   — Formats for Agent mode, not Chat mode
   — Includes re-entry instructions

5. Delivers a copy-paste block + configuration checklist
```

---

## Memory Anchor Protocol

Every handoff classifies context into three tiers:

**MUST CARRY** — always included regardless of platform
- Current goal, active sub-goals
- Hard constraints (non-negotiables)
- Decisions + reasoning
- Artifacts + locations + status
- What the next platform is asked to do

**SHOULD CARRY** — included when relevant to the next task
- Tone/voice/audience context
- Prior rejected approaches
- Technical environment details

**COMPRESS OR DROP** — platform-dependent
- Raw conversation history → compress to key points
- Exploratory tangents → drop
- IDE platforms (Cursor, Windsurf, Claude Code) → strip narrative, keep specs
- Research platforms (Perplexity, Grok) → strip build context, keep research questions

---

## Real-World Chain Example

```
Claude      → Research + architecture phase
   ↓ /handoff to Cursor
Cursor      → Build the application
   ↓ /handoff to Perplexity
Perplexity  → Verify real-time competitive data
   ↓ /handoff return to Claude
Claude      → Synthesize findings, finalize report
   ↓ /handoff to ChatGPT
ChatGPT     → Generate presentation from report
```

Each transition is one command. Each platform receives only what it needs.

---

## Adding a New Platform

Use `platforms/_template.md` to add a new platform profile. Required sections:
- Strengths, weaknesses, context window behavior
- Memory and persistence model
- System prompt support
- Prompt format conventions
- Handoff receiving template (copy-paste ready)
- Configuration checklist

---

## Repo Placement

```
operations/
├── ai-model-handoff/
│   ├── SKILL.md
│   ├── README.md
│   └── platforms/
│       ├── claude.md
│       ├── claude-code.md
│       ├── chatgpt.md
│       ├── gemini.md
│       ├── copilot.md
│       ├── perplexity.md
│       ├── grok.md
│       ├── deepseek.md
│       ├── mistral.md
│       ├── cursor.md
│       ├── meta-llama.md
│       ├── windsurf.md
│       └── _template.md
```

Sits alongside `session-handoff` and `agent-foundation` — together these three form the repo's **continuity and persistence cluster**.

---

## Running This Skill Outside Claude

This skill is designed with **Claude as the orchestrator**. Here's what that means in practice.

### What Works on Any Platform
The platform profiles and handoff package templates are plain markdown. Any frontier model can read them and assemble a handoff package if you paste the relevant content into the session. The *receiving* end of a handoff always works — a handoff package is just a structured prompt.

### What Doesn't Transfer Cleanly

| Limitation | Why |
|---|---|
| Slash commands (`/handoff to [platform]`) | Not native commands in ChatGPT or Gemini — they work because Claude reads the SKILL.md and treats them as instructions |
| Automatic session scanning | Claude follows the structured extraction workflow more reliably than most platforms |
| Persistent skill loading | Requires Claude Projects or equivalent per-platform setup each session |

### Two Approaches If You Want Cross-Platform Orchestration

**Option A — Configure once per platform**
Load the SKILL.md as a persistent system instruction in each platform's equivalent:
- ChatGPT → Custom GPT with SKILL.md as the system prompt
- Gemini → Gem with SKILL.md as instructions
- Copilot → Agent configuration

Each platform then has native `/handoff` capability without pasting every session. Behavior will vary slightly by platform.

**Option B — Keep Claude as the permanent orchestrator (recommended)**
Claude always initiates and receives handoffs. Every other platform is always the *destination* — never the source. This is what the skill was designed for and produces the most consistent results.

```
Claude (orchestrator) <—> Any other platform (destination)
```

The handoff packages Claude produces are formatted for the destination platform. The return packages those platforms produce are received and processed by Claude. The loop is always Claude-anchored.
