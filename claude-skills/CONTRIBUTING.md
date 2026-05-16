# Contributing

## Adding a New Skill

### 1. Choose the right category

| Category | For skills that... |
|---|---|
| `intelligence/` | Research, scan, extract, or analyze information about companies, markets, or competitors |
| `engagement/` | Manage the client engagement lifecycle — planning, quality, value framing |
| `sales-and-growth/` | Support sales, proposals, partner strategy, or business development |
| `ai-enablement/` | Help teams build, configure, or deploy AI tools and frameworks |
| `optimization/` | Improve quality, format, or discoverability of content and assets |
| `operations/` | Support delivery, process management, and team coordination |

If a skill spans categories, place it in the primary category and note dependencies in the README.

### 2. Create the folder

```
[category]/[skill-name]/
├── SKILL.md
└── README.md
```

Use lowercase hyphenated names. Examples: `market-landscape`, `sow-writer`, `meeting-prep`.

### 3. Write the SKILL.md

Every skill must include:

```yaml
---
name: skill-name
version: 1.0.0
description: >
  One paragraph. Start with the activation condition ("Activate when...").
  Cover the primary use cases. List key trigger phrases. Note any skills this
  depends on. End with the quality standard.
---
```

Followed by:
- **Workflow Overview** — numbered steps, 1-sentence each
- **Step-by-step instructions** — enough detail that Claude can execute without guessing
- **Output format** — exact structure, field names, or artifact description
- **Quality checklist** — concrete, verifiable before/after items
- **Edge cases** — the 4–6 most common non-standard situations

### 4. Write the README.md

Use the template in `_templates/skill-template/README.md`. Required sections:
- What It Does (2–3 sentences)
- When to Use
- Trigger Phrases
- Key Inputs table
- Output description
- Any setup required

### 5. Update the master README

Add the skill to the appropriate table in `/README.md`.

---

## Editing an Existing Skill

- Bump the `version` in the frontmatter (patch for fixes, minor for new capabilities)
- Note the change in a `## Changelog` section at the bottom of `SKILL.md` if the change is significant
- Update the README if the interface or outputs changed

---

## Quality Standards for Skills

A good skill:
- **Activates precisely** — trigger conditions are specific enough that Claude knows when to use it and when not to
- **Produces consistent output** — two different Claude sessions running the same skill on the same input should produce structurally identical outputs
- **Handles failure gracefully** — edge cases and low-signal situations are documented; the skill degrades cleanly rather than hallucinating
- **Is honest about uncertainty** — quality checklists and review flags surface gaps rather than hiding them
- **Is generic** — no organization-specific branding, named services, or proprietary content (use `[Customize: ...]` placeholders for anything org-specific)

---

## What Not to Include

- Organization-specific branding, service names, or pricing
- References to internal tools, file paths, or systems that won't exist in other environments
- Skills that are too narrow to be useful outside one specific context
- Skills without a README
