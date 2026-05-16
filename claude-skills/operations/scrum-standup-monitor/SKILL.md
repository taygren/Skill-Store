---
name: scrum-standup-monitor
description: >
  Scrum standup process monitoring system. Activate this skill whenever a user provides a daily standup transcript, meeting notes, or scrum update — even partial or informal ones. Produces a clean dashboard and 1-page tear sheet covering sprint progress, individual commitments, blockers, and accountability signals. Use this skill when the user says "here's our standup", "process this scrum", "track our sprint", "generate a standup summary", or pastes any text that resembles team member daily updates (what they did, what they're doing, any blockers). Also trigger when the user asks to "update the dashboard" or "add today's standup" — this skill maintains a running, cumulative view across standups.
---

# Scrum Standup Monitor

Transforms raw standup transcripts into a structured dashboard and 1-page tear sheet for progress tracking, accountability, and project monitoring.

---

## Input

The user will typically provide a **verbatim Zoom or Teams transcript** with speaker labels (e.g., `[John Smith] 00:01:23`). Also accept:
- Lightly cleaned transcripts with names prefixed
- Meeting notes or bullet points per person
- Pasted async written updates

**Transcript parsing notes:**
- Ignore filler, crosstalk, and non-standup chatter (greetings, tech issues, side conversations)
- Focus on standup signal: what someone did, what they're doing, what's blocking them
- Speaker labels are the primary signal for attribution — use the name as stated

If context from prior standups exists in the conversation, incorporate it into the running dashboard.

---

## What to Extract

Parse the transcript for these core scrum signals:

### Per Team Member
- **Name / Role** (if mentioned)
- **Yesterday** — what they completed or worked on
- **Today** — what they're committing to
- **Blockers** — anything blocking progress (explicit or implied)
- **Carry-overs** — items they mentioned yesterday that didn't get done (if prior standup context exists)

### Sprint-Level
- **Sprint goal** (if stated or inferable)
- **Days remaining** (if mentioned)
- **Overall momentum** — on track / at risk / blocked (your assessment based on signals)
- **Open blockers count**
- **Items completed today vs. committed**

---

## Output Format

Produce two clearly labeled sections:

---

### SECTION 1: LIVE DASHBOARD

A compact, scannable table or structured layout. Use markdown tables. Keep it tight.

```
📅 Standup: [Date or "Day N"]
🏃 Sprint: [Name/Number if known] | Days Remaining: [X]
🎯 Sprint Goal: [Goal or "Not stated"]
⚡ Status: [ON TRACK / AT RISK / BLOCKED]

─────────────────────────────────────────────────────────
TEAM MEMBER  | YESTERDAY          | TODAY              | BLOCKERS
─────────────────────────────────────────────────────────
[Name]       | [What they did]    | [What they'll do]  | [Blocker or —]
[Name]       | ...                | ...                | ...
─────────────────────────────────────────────────────────

🚧 OPEN BLOCKERS ([N] total)
  • [Blocker] — Owner: [Name] | Since: [Day if known]

📌 CARRY-OVERS (items not completed from prior day)
  • [Item] — Owner: [Name]

✅ COMPLETED TODAY
  • [Item] — Owner: [Name]
```

---

### SECTION 2: 1-PAGE TEAR SHEET

A narrative summary in plain language. 3–5 short paragraphs or bullet groups. Audience: a project manager or stakeholder who wasn't in the meeting.

Structure:
1. **Sprint Snapshot** — Where are we overall? On track? Key risks?
2. **Today's Commitments** — What the team is focused on today, summarized
3. **Blockers & Watch Items** — Any blockers, risks, or items needing attention
4. **Accountability Flags** — Carry-overs, repeated blockers, or items that seem stalled (flag with care, no blame)
5. **Next Standup Focus** — What to watch for or follow up on tomorrow

Keep the tear sheet to ~200–300 words. No filler. Plain language.

---

## Audience

This output serves multiple audiences simultaneously:
- **Team members** — need to see their commitments and blockers clearly
- **Project manager / team lead** — needs accountability signals, carry-overs, and sprint health at a glance
- **Executives / stakeholders** — need the tear sheet: plain language, no jargon, quick read

Design the dashboard for the team and PM. Design the tear sheet for leadership.

---

## Tone & Behavior

- Be neutral and factual. Don't editorialize about individuals.
- If a blocker has appeared across multiple standups, flag it as **persistent**.
- If someone mentions a commitment and it doesn't appear resolved in a subsequent standup, quietly note it as a carry-over — don't accuse.
- If the transcript is ambiguous, make your best inference and note it with `[inferred]`.
- If sprint goal, dates, or other metadata aren't stated, mark as `Not stated` — don't fabricate.

---

## Running Across Multiple Standups

If prior standup outputs exist in the conversation:
- Update the dashboard cumulatively (don't start fresh)
- Track carry-overs and persistent blockers across days
- Note velocity trends if enough data exists (e.g., "3 days of carry-overs on [item]")

---

## Output Delivery

1. **Render both sections inline** in chat using markdown — always. This gives the user an immediate, readable view.
2. **Always also export a Word document (.docx)** using the `docx` skill. The Word doc should contain both the dashboard and the tear sheet, cleanly formatted. Read `/mnt/skills/public/docx/SKILL.md` before generating the file.
   - File naming: `standup-[date or day-number].docx`
   - Present the file via `present_files` so the user can download it.
