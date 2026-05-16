# scrum-standup-monitor

**Category:** Operations  
**Trigger:** Any standup transcript, scrum update, or daily meeting notes provided for processing

---

## What It Does

Transforms raw standup transcripts (Zoom/Teams, async notes, bullet updates) into a structured dashboard and 1-page tear sheet. Extracts per-person yesterday/today/blocker signals, tracks sprint momentum, surfaces carry-overs and persistent blockers, and produces a cumulative view across multiple standups if run daily.

---

## When to Use

- After a daily standup to create a structured record
- When a PM or stakeholder needs a clean summary of team status
- To track carry-overs and identify stalled items across days
- Anytime standup data exists in a transcript or notes format

---

## Trigger Phrases

- "Here's our standup"
- "Process this scrum"
- "Generate a standup summary"
- "Track our sprint"
- "Update the dashboard with today's standup"

---

## Accepts

- Verbatim Zoom / Teams transcripts with speaker labels
- Lightly cleaned transcripts with names prefixed
- Meeting notes or bullet points per person
- Async written standup updates

---

## Outputs

### Section 1: Live Dashboard
Compact markdown table showing each team member's yesterday / today / blockers, sprint metadata (goal, days remaining, status), open blockers list, carry-overs, and completed items.

### Section 2: 1-Page Tear Sheet
Plain-language narrative summary (~200–300 words) for PMs and stakeholders who weren't in the meeting. Covers sprint snapshot, today's commitments, blockers, accountability flags, and next standup focus items.

**Also exports a `.docx` file** via the `docx` skill for download and sharing.

---

## Example Dashboard Snippet

```
📅 Standup: May 16, 2026
🏃 Sprint: Sprint 12 | Days Remaining: 3
🎯 Sprint Goal: Ship auth module
⚡ Status: AT RISK

TEAM MEMBER  | YESTERDAY              | TODAY                  | BLOCKERS
─────────────────────────────────────────────────────────────────────────
Alex         | Finished login flow    | Starting token refresh | Waiting on design review
Jordan       | API review             | Write unit tests       | —
Sam          | Blocked on credentials | Retry credential setup | Access not provisioned ⚠️

🚧 OPEN BLOCKERS (2 total)
  • Design review not scheduled — Owner: Alex | Since: Day 1
  • Credential access — Owner: Sam | Since: Day 2 [PERSISTENT]
```

---

## Cumulative Tracking

When prior standup outputs exist in the conversation, the skill updates cumulatively — tracking carry-overs across days, flagging persistent blockers, and noting velocity trends.
