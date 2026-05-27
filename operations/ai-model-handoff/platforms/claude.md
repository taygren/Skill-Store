[claude.md](https://github.com/user-attachments/files/28306287/claude.md)
# Platform Profile: Claude (claude.ai / API)

**Provider:** Anthropic  
**Current Flagship:** Claude Opus 4.6 / Sonnet 4.6  
**Interface:** claude.ai chat, Projects, API

---

## Strengths
- Long-form structured reasoning and multi-step analysis
- Writing quality — most natural prose of any frontier model
- Code quality and readability (senior-engineer-caliber output)
- Extended thinking for complex reasoning chains
- Following nuanced, detailed instructions precisely
- Structured output formats (JSON, markdown, schemas)
- Document analysis and synthesis across large contexts
- Consulting-grade deliverables and strategic analysis

## Weaknesses
- No persistent memory across sessions by default (Projects partially addresses this)
- Real-time web data requires web search tool to be enabled
- Cannot execute code natively in standard chat interface
- Less suited for rapid iterative chat loops than IDE-native tools

## Context Window
- Opus 4.6: 200K tokens
- Sonnet 4.6: 200K tokens
- Behavior: Claude handles long context well with strong recall; does not degrade significantly at high token counts

## Memory & Persistence
- **Projects:** Persistent knowledge base within a project; instructions and uploaded files carry across sessions
- **Session memory:** No cross-session memory by default unless Projects or memory features are enabled
- **Handoff note:** For multi-session work, use Claude Projects with a persistent CLAUDE.md or system prompt

## System Prompt Support
- ✅ Full system prompt support via API
- ✅ Project instructions function as a persistent system prompt in claude.ai
- System prompts are highly effective; Claude follows detailed, structured instructions reliably

## Tool Availability
- Web search (when enabled)
- File reading and analysis
- Code execution (via artifacts in claude.ai)
- MCP connectors (in claude.ai with connected integrations)

## Prompt Format Conventions
- Responds best to clearly structured prompts with explicit role, context, and task sections
- Handles XML tags well: `<context>`, `<task>`, `<constraints>`, `<examples>`
- Benefits from explicit output format specification
- Detailed instructions outperform vague ones — more specificity = better results
- Works well with step-by-step task decomposition in the prompt

## Ideal Task Types
- Research synthesis and strategic analysis
- Long-form writing and editing
- Architecture decisions and technical planning
- Structured document production (reports, SOWs, proposals)
- Code review and explanation
- Complex reasoning chains with multiple dependencies
- Any task where output quality and precision matter more than speed

---

## Handoff Receiving Template

```
=== CLAUDE HANDOFF PACKAGE ===
Project: [name]
Handed off from: [platform] ([phase])
Receiving: Claude ([phase])

<system>
You are continuing work on [project name]. The [prior phase] is complete.
Your role for this phase: [specific role — analyst / writer / architect / reviewer].
Operating constraints: [key constraints].
</system>

<context>
[2–4 sentences: what this project is, who it's for, what matters most]
</context>

<current_goal>
[One sentence outcome]
</current_goal>

<sub_goals>
- [Sub-goal 1] — [status]
- [Sub-goal 2] — [status]
</sub_goals>

<artifacts>
- [Artifact name] | [type] | [location] | [status]
</artifacts>

<decisions>
[Decision]: [choice made] | Reason: [why] | Constraint: [what this means going forward]
</decisions>

<context_register>
[Named list of things established over time that must not be re-litigated]
</context_register>

<task>
[Explicit instruction for this phase. First, second, third.]
</task>

<must_not_change>
[Hard constraints — non-negotiables]
</must_not_change>

<re_entry>
When complete or blocked, run: /handoff return from Claude
Include: [specific outputs], decisions made, blockers hit
</re_entry>
=== END ===
```

## Configuration Checklist
- [ ] Open in a Project if this is ongoing work (preserves context across sessions)
- [ ] Enable web search if real-time data is needed
- [ ] If pasting into a new session, include full context block — Claude has no prior memory
