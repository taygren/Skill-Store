[README.md](https://github.com/user-attachments/files/28011363/README.md)
# ux-law-reviewer

**Category:** Optimization  
**Trigger:** Any UI design, wireframe, user flow, or app description presented for review — or any new design project requiring a best-practice checklist

---

## What It Does

Evaluates UI designs against all 30 Laws of UX from [lawsofux.com](https://lawsofux.com) — the complete set of cognitive psychology and behavioral design principles. Organizes the laws into six actionable design domains, evaluates each systematically, and produces findings with severity ratings (🔴 Critical → 🟢 Polish), specific violations, and concrete fixes. Also operates as a proactive design checklist for new builds.

---

## When to Use

- Reviewing a wireframe, mockup, prototype, or production UI before release
- Starting a new UI build and wanting to design with best practices from the beginning
- Auditing an existing product for UX debt
- Evaluating a third-party design or vendor-provided UI
- Any time "does this follow good UX practice?" is the question

---

## Trigger Phrases

- "Review this design"
- "UX audit this"
- "Does this follow UX best practices?"
- "Apply the Laws of UX to this"
- "Check my wireframe"
- "Design checklist for this app"
- "What are the UX issues with this?"

---

## The 30 Laws — Organized Into 6 Domains

| Domain | Laws Covered |
|---|---|
| **Cognitive Load & Decision-Making** | Hick's Law, Miller's Law, Cognitive Load, Chunking, Choice Overload, Occam's Razor |
| **Visual Perception & Gestalt** | Law of Proximity, Law of Common Region, Law of Similarity, Law of Uniform Connectedness, Law of Prägnanz |
| **Memory & Learning** | Working Memory, Serial Position Effect, Zeigarnik Effect, Goal-Gradient Effect, Mental Model |
| **Interaction & Performance** | Fitts's Law, Doherty Threshold, Postel's Law, Parkinson's Law |
| **Experience & Emotion** | Aesthetic-Usability Effect, Peak-End Rule, Flow, Paradox of the Active User, Pareto Principle |
| **Information Architecture & Navigation** | Jakob's Law, Von Restorff Effect, Tesler's Law, Selective Attention, Cognitive Bias |

---

## Two Modes

**Review Mode** — Audit an existing design. Produces a domain-by-domain evaluation with findings, severity ratings, and priority fixes.

**Checklist Mode** — Guide a new design. Produces a per-domain checklist with pass/fail checkboxes and design prompts for every law before a line is drawn.

---

## Key Inputs

| Input | Required? | Notes |
|---|---|---|
| Design / wireframe / description | ✅ | Screenshot, Figma link, written description |
| Platform (web / mobile / desktop) | Optional | Affects Fitts's Law and interaction standards |
| User type (novice / expert / mixed) | Optional | Calibrates cognitive load thresholds |
| Design stage | Optional | Calibrates depth and severity of feedback |

---

## Output Structure

**Review Mode:**
- Domain-by-domain scan with ✅ / ⚠️ / ❌ status per law
- Findings: what's wrong, why it matters, specific fix
- Priority Summary table (finding × law × severity × fix effort)
- Systemic patterns (root causes behind multiple violations)
- What's working
- Top 3 priority fixes

**Checklist Mode:**
- Six domain checklists with a design prompt per law
- Pass/fail checkboxes ready to work through

---

## Example Finding

```
🔴 Critical — Hick's Law — Navigation exposes 14 top-level options

What's wrong: The main navigation presents 14 items at equal visual weight
with no grouping or hierarchy. Users must evaluate all 14 before deciding
where to go.

Why it matters: Decision time increases logarithmically with options. 14
undifferentiated choices creates meaningful hesitation and increases drop-off
at the navigation layer.

Fix: Group the 14 items into 4–5 logical categories. Use a mega-menu or
progressive disclosure to reveal subcategories on demand. Visually weight
the 2–3 most-used destinations above the rest.
```

---

## Source

All 30 laws sourced from [lawsofux.com](https://lawsofux.com) by Jon Yablonski.  
Licensed under [CC BY-NC-ND 4.0](https://creativecommons.org/licenses/by-nc-nd/4.0/).
