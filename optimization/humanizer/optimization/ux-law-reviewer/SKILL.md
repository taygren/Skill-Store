[ux-law-reviewer-SKILL.md](https://github.com/user-attachments/files/28010367/ux-law-reviewer-SKILL.md)
---
name: ux-law-reviewer
version: 1.0.0
description: >
  UX Law Reviewer — activate whenever a user presents a UI design, app wireframe, component,
  user flow, screen description, or design specification for review. Also activate when starting
  any new app or UI design to use as a proactive checklist. Trigger when the user says "review
  this design", "UX review", "check this UI", "design audit", "does this follow UX best
  practices", "apply the Laws of UX", "evaluate this flow", "check my wireframe", or begins
  designing or describing any interface. Evaluates designs against all 30 Laws of UX sourced
  from lawsofux.com, organized into six design domains. Produces findings with severity ratings,
  specific violations, and actionable fixes. Can run as a review (against existing design) or
  as a proactive checklist (before/during design).
---

# UX Law Reviewer

Evaluates any UI design, wireframe, user flow, or screen description against all **30 Laws of UX** — the complete set of cognitive psychology and behavioral design principles from [lawsofux.com](https://lawsofux.com). Produces findings organized by design domain, with severity ratings and specific, actionable fixes.

Runs in two modes:
- **Review mode** — Audit an existing design against the laws and surface violations
- **Checklist mode** — Use the laws proactively during design to ensure compliance from the start

---

## The 30 Laws of UX — Complete Reference

All 30 laws are organized into six design domains. Each law includes the core principle and the specific design rules it generates.

---

### Domain 1: Cognitive Load & Decision-Making
*Reduce the mental effort required to understand and use the interface.*

**1. Hick's Law**
Decision time increases with the number and complexity of choices.
- Minimize choices at every decision point; reduce options to only what's necessary for the current step
- Break complex tasks into smaller sequential steps rather than presenting everything at once
- Highlight recommended options to guide users toward a decision without eliminating choice
- Use progressive onboarding — hide advanced features until users are ready for them
- Never simplify to the point of abstraction; meaningful choices must remain

**2. Miller's Law**
The average person holds 7 (±2) items in working memory.
- Chunk content into groups of 5–9 items maximum; smaller groups (3–4) reduce cognitive stress
- Organize navigation, menus, and option lists into logical categories rather than flat long lists
- Don't weaponize "the magic number 7" to justify arbitrary limitations — chunking is the goal, not the ceiling
- Account for working memory variation: novice users and high-stress contexts need fewer items

**3. Cognitive Load**
The amount of mental resources required to understand and use an interface must be minimized.
- Eliminate unnecessary elements — every element that doesn't serve the user's goal adds cognitive tax
- Use familiar patterns and conventions instead of novel interactions that require learning
- Reduce extraneous cognitive load (caused by poor design) while preserving germane load (caused by meaningful learning)
- Progressive disclosure: show only what's needed for the current step; reveal complexity on demand

**4. Chunking**
Information grouped into meaningful units is easier to process and remember.
- Group related content visually using proximity, borders, or background differentiation
- Apply chunking to forms (group related fields), navigation (group related pages), and data displays (group related rows or columns)
- Use white space as a chunking tool — adequate spacing between groups signals separation as powerfully as borders

**5. Choice Overload**
Too many options leads to paralysis, poor decisions, and decision fatigue.
- Cap option sets at meaningful limits; if more options are needed, use filtering, search, or categorization
- Surface defaults and recommendations prominently — reduce the number of items the user must actively evaluate
- Consider reducing a large catalog's visible options at entry points, with progressive expansion available

**6. Occam's Razor**
The simplest solution that works is correct. Remove everything that doesn't serve the user.
- For every element in the design, ask: "What does the user lose if this is gone?" If the answer is "nothing," remove it
- Prefer simple interaction patterns over clever ones; cleverness requires explanation, simplicity doesn't
- Audit designs for decorative elements that add visual complexity without adding meaning or function

---

### Domain 2: Visual Perception & Gestalt
*Design what the eye naturally sees and groups.*

**7. Law of Proximity**
Objects near each other are perceived as related.
- Place related elements close together; separate unrelated elements with clear space
- Use proximity to define groups without relying solely on borders or color
- In forms, place labels directly adjacent to their inputs; in navigation, cluster related links

**8. Law of Common Region**
Elements within a defined boundary are perceived as belonging together.
- Use cards, containers, borders, and background fills to group content that belongs together
- Don't place unrelated items inside the same container — shared region implies shared relationship
- Common region is stronger than proximity; use it deliberately for primary groupings

**9. Law of Similarity**
Similar-looking elements are perceived as related.
- Apply consistent visual treatment (color, shape, size, style) to elements that belong to the same category
- Use visual dissimilarity to distinguish elements that are different in type or function
- Avoid making different things look alike — similar styling implies similar behavior

**10. Law of Uniform Connectedness**
Visually connected elements are perceived as more related than elements with no connection.
- Use lines, arrows, or shared visual properties to indicate strong relationships (e.g., a line connecting a tooltip to its trigger)
- Connection implies stronger relationship than proximity or similarity alone — use it for the tightest relationships
- Avoid decorative connective elements that imply relationships that don't exist

**11. Law of Prägnanz**
People perceive complex or ambiguous images in the simplest form possible.
- Design for the interpretation that requires the least cognitive effort — users will take the path of least resistance
- Ambiguous layouts will be misread as the simpler, more familiar pattern; remove ambiguity by making structure explicit
- Prefer clean geometric shapes and clear spatial relationships; complexity must be intentional and meaningful

---

### Domain 3: Memory & Learning
*Design for how people actually remember and learn.*

**12. Working Memory**
Working memory temporarily holds and manipulates information needed to complete tasks — it's limited and fragile.
- Never require users to remember information from one step to carry it to another; display it persistently
- Reduce the number of things a user must hold in mind simultaneously
- Minimize interruptions during multi-step tasks; each interruption flushes working memory

**13. Serial Position Effect**
Users best remember the first and last items in a list or sequence.
- Place the most important navigation items, actions, and options first or last — never bury them in the middle
- In navigation bars, use first and last positions for primary and secondary calls-to-action
- In long lists, consider repeating the most critical item or using visual differentiation to counteract serial position bias

**14. Zeigarnik Effect**
People remember incomplete or interrupted tasks better than completed ones.
- Use progress indicators, completion percentages, and "X of Y steps" counters to surface incomplete tasks and pull users back
- Design onboarding and setup flows to be deliberately incomplete at first — incompleteness creates the pull to return
- Be careful: incomplete states that are frustrating or confusing create anxiety rather than engagement

**15. Goal-Gradient Effect**
Users accelerate effort as they approach a goal — the closer they are, the harder they push.
- Show progress clearly throughout multi-step flows; users will complete tasks faster when they can see they're close
- Design progress indicators that make progress feel meaningful even in early stages (artificial advancement)
- In gamification, reward systems, and completion flows, proximity to completion is itself a motivator

**16. Mental Model**
Users approach your interface with a pre-existing model of how it should work, built from past experience.
- Align your interface to the mental models users already hold — violating expectations creates confusion and friction
- Use familiar metaphors (shopping carts, folders, inboxes) that map to real-world or prior digital experience
- When you must deviate from convention, provide explicit explanation — don't assume users will discover new patterns

---

### Domain 4: Interaction & Performance
*Design interactions that feel fast, responsive, and effortless.*

**17. Fitts's Law**
The time to reach a target is determined by its size and distance from the current cursor/touch position.
- Make interactive targets (buttons, links, form controls) large enough to hit reliably, especially on touch devices
- Place interactive targets close to where the user's attention and cursor/finger are likely to be
- Increase target size for destructive, high-stakes, or frequently used actions
- Avoid small touch targets (below ~44px × 44px on mobile) and insufficient spacing between adjacent targets
- Edge and corner targets are fastest to hit (the screen edge acts as an infinite edge); use this for primary actions

**18. Doherty Threshold**
Productivity peaks when system response time stays under 400ms. Above that, users disengage.
- Target sub-400ms response for all interactions; optimize for perceived performance if actual performance can't hit the mark
- Show immediate feedback (loading states, spinner, skeleton screens, progress bars) for any operation that takes longer than 400ms
- Use animation to maintain perceived responsiveness during background processing
- Never leave the user staring at a blank or static screen — motion signals the system is working
- Progress bars manage wait perception even when their accuracy is imperfect; use them

**19. Postel's Law**
Be liberal in what you accept; be conservative in what you send.
- Accept flexible user input — handle varied date formats, phone number formats, spacing, capitalization variations
- Don't fail on minor formatting differences that the system can normalize; fail only on genuinely invalid input
- Be strict and consistent about what you output — use standardized, predictable formats for all system output
- Error handling should be forgiving and helpful, not punitive; guide users to correction rather than blocking them

**20. Parkinson's Law**
Tasks expand to fill the available time.
- Set clear deadlines and time limits for user tasks to focus effort and prevent scope creep in form-filling and workflows
- For time-sensitive tasks (auctions, bookings, limited availability), display explicit time constraints
- Keep forms and multi-step flows as short as the task genuinely requires; length signals "this will take a while"

---

### Domain 5: Experience & Emotion
*Design the emotional arc of the experience, not just its steps.*

**21. Aesthetic-Usability Effect**
Aesthetically pleasing designs are perceived as more usable — even when they're not.
- Invest in visual polish; a beautiful interface gives users more patience with minor usability friction
- Use aesthetics strategically: a high-quality visual impression buys goodwill during user learning curves
- Critical warning: beautiful design can mask usability problems and fool usability testing — test both aesthetics and functional usability separately

**22. Peak-End Rule**
Users judge an experience by its peak emotional moment and its final moment — not the average.
- Identify the emotional peak of your product (the moment of delight, relief, achievement, or insight) and design it deliberately
- Design the end state of every flow with care — confirmation screens, success states, and empty states are the final impression
- Address pain points at peak-stress moments (checkout, error states, long waits) — these are the moments that define the memory of the experience
- Negative emotional peaks are remembered more vividly than positive ones; eliminate or soften the worst moments before amplifying the best

**23. Flow**
Optimal experience occurs when challenge and skill are in balance — the user is fully immersed and focused.
- Remove distractions from task-focused interfaces; every unnecessary element is a potential flow-breaker
- Calibrate task difficulty to user skill: too easy creates boredom, too hard creates anxiety, balanced creates engagement
- Provide immediate, clear feedback for every action so users always know the result of what they did
- Design for context: mobile users, distracted environments, and multi-tasking contexts require simpler flows

**24. Paradox of the Active User**
Users never read documentation. They start using the product immediately.
- Design for the user who skips instructions — the interface must teach itself through good design, not manuals
- Use onboarding that is embedded in the interface itself (tooltips, contextual hints, empty states that explain)
- Never require users to read documentation before they can accomplish their first meaningful task
- Write UI copy that explains as it instructs; labels and error messages are the documentation

**25. Pareto Principle**
80% of effects come from 20% of causes. Most users use most of your product's value from a small set of features.
- Identify the 20% of features that deliver 80% of user value and optimize those ruthlessly
- Surface the most-used features prominently; bury rarely-used features in secondary navigation
- Use analytics to discover which features actually get used — design reflects intended behavior, not always actual behavior

---

### Domain 6: Information Architecture & Navigation
*Design how information is organized, labeled, and traversed.*

**26. Jakob's Law**
Users spend most of their time on other products. They expect yours to work like those products.
- Default to established design conventions before inventing novel patterns — convention is not laziness, it's respect for existing mental models
- Navigation placement (top or left), icon meanings, form conventions, and interaction patterns should match what users already know
- When redesigning, allow users to transition gradually — provide the old design as an option before forcing the new one
- Document intentional convention-breaking explicitly and design extra affordances to help users discover novel patterns

**27. Von Restorff Effect**
When similar items are present, the one that differs is most likely to be remembered.
- Use visual differentiation (color, size, shape, weight) to highlight the single most important action or element on each screen
- Don't overuse differentiation — if everything is highlighted, nothing is; visual emphasis requires contrast against a calm baseline
- Use the Von Restorff Effect for primary CTAs, warnings, and critical information — not for decoration

**28. Tesler's Law (Law of Conservation of Complexity)**
Every system has an irreducible amount of complexity. It cannot be eliminated — only transferred.
- Accept that complexity exists and decide consciously where it lives: in the interface (user bears it) or in the system (design/engineering bears it)
- Err toward bearing complexity in the system rather than the user — make the hard things easy, even if that's hard to build
- Don't over-simplify: some complexity belongs to the user because it represents meaningful choice or necessary understanding

**29. Selective Attention**
Users focus only on a subset of available information — usually what relates to their current goal.
- Design to match the user's attention at the moment of use; irrelevant information is invisible to a focused user
- Don't rely on users noticing important information that isn't in their goal-directed path of attention
- Use visual hierarchy, position, and motion to guide attention toward what matters at each moment
- Warning messages, error states, and critical information must break through selective attention — use visual disruption intentionally

**30. Cognitive Bias**
Systematic errors in thinking influence how users perceive and interact with interfaces.
- Anchoring: the first number or option a user sees influences all subsequent judgments — use it deliberately (e.g., pricing page order)
- Confirmation bias: users interpret ambiguous information to confirm what they already believe — design clearly to prevent misreading
- Status quo bias: users resist change; minimize disruption when updating designs and provide transitions
- Social proof: users look to others' behavior to guide their own — display usage statistics, reviews, and popularity signals where relevant
- Loss aversion: users fear losses more than they value equivalent gains — frame choices in terms of what is preserved, not just what is gained

---

## Workflow Overview

1. **Intake** — Understand what's being reviewed and at what fidelity
2. **Domain scan** — Evaluate the design against each of the six domains
3. **Findings** — Document violations and confirmations with severity ratings
4. **Synthesis** — Identify the highest-priority issues and systemic patterns
5. **Render** — Produce the review as a structured artifact

---

## Step 1: Intake

Before reviewing, establish:

### Required
- **What is being reviewed** — Screen, flow, component, wireframe, or design description
- **Mode** — Review (auditing existing design) or Checklist (guiding new design)

### Useful Context
- **Platform** — Web / mobile / desktop / responsive (affects Fitts's Law, touch targets, layout conventions)
- **User type** — Novice / expert / mixed (affects cognitive load thresholds and onboarding needs)
- **Task type** — High-frequency routine task vs. rare complex task (affects simplicity vs. power tradeoff)
- **Design stage** — Concept / wireframe / prototype / production (calibrates depth of feedback)

If the design is described in text rather than shown visually, proceed with the description and note assumptions explicitly.

---

## Step 2: Domain Scan

Evaluate the design systematically against each domain. For each law within a domain, assess:
- **Status:** ✅ Satisfied / ⚠️ Partially satisfied / ❌ Violated / — Not applicable
- **Evidence:** What in the design indicates this status?
- **Finding:** If violated or partial, what specifically is wrong and what is the fix?

Do not skip domains. A domain with no violations gets a brief confirmation note — silence is not the same as passing.

---

## Step 3: Findings Format

For every ⚠️ or ❌ finding, produce:

**[SEVERITY] [Law Name] — [Short finding title]**

- **What's wrong:** Specific, concrete description of the violation in this design. Not generic.
- **Why it matters:** What user behavior or outcome this will cause.
- **Fix:** Specific, actionable change. Not "improve the design" — describe exactly what to change.

### Severity Levels

| Severity | Criteria |
|---|---|
| 🔴 **Critical** | Will cause task failure, user drop-off, or significant frustration for most users |
| 🟠 **High** | Will cause friction or confusion for many users; measurably degrades experience |
| 🟡 **Medium** | Will affect a subset of users or cause minor friction; degrades polish and perception |
| 🟢 **Low / Polish** | Good practice; addressing it improves quality but won't meaningfully affect task success |

---

## Step 4: Synthesis

After completing the domain scan:

### Priority Summary Table

| Finding | Law | Severity | Fix Effort |
|---|---|---|---|
| [Short title] | [Law name] | 🔴/🟠/🟡/🟢 | Low / Medium / High |

### Systemic Patterns
Identify if multiple violations trace to a single root cause (e.g., "five findings are all caused by insufficient information architecture — fix the nav structure and most resolve"). Pattern-level insights are more actionable than a list of isolated fixes.

### What's Working
Note where the design demonstrably satisfies laws well. A balanced review is more credible and helps the designer know what not to change.

### Top 3 Priority Fixes
If only three things get fixed, these should be them. Rank by impact-to-effort ratio, not severity alone.

---

## Step 5: Render

**Default output:** Structured markdown review organized by domain.
**For comprehensive audits:** HTML artifact with a visual summary table, domain cards, and priority matrix.
**For checklist mode:** A pre-design checklist organized by domain with pass/fail checkboxes and design prompts for each law.

---

## Checklist Mode — Pre-Design Reference

When designing a new interface from scratch, use this checklist before and during design:

### Cognitive Load & Decision-Making
- [ ] Have I limited choices at each decision point? Are all options necessary?
- [ ] Is content chunked into groups of 5–9 or fewer meaningful items?
- [ ] Is every element earning its presence? Have I removed what doesn't serve the user?
- [ ] Are related items visually grouped? Is white space being used as a grouping tool?
- [ ] Is onboarding progressive — hiding complexity until the user is ready?
- [ ] Have I highlighted recommended options where relevant?

### Visual Perception & Gestalt
- [ ] Are related elements placed close together and unrelated elements separated?
- [ ] Am I using containers (cards, regions, borders) to communicate grouping?
- [ ] Do similar-looking elements behave similarly? Do different-looking elements behave differently?
- [ ] Are visual connections (lines, arrows, shared properties) used deliberately and accurately?
- [ ] Is the visual structure unambiguous — does it have one clear reading?

### Memory & Learning
- [ ] Does the design avoid requiring users to remember information across steps?
- [ ] Are the most important items placed first or last in lists and navigation?
- [ ] Am I using progress indicators and completion signals to surface incomplete tasks?
- [ ] Is there a clear progress arc that shows users how close they are to completion?
- [ ] Does the design align with the mental models users bring from familiar products?

### Interaction & Performance
- [ ] Are all touch targets at least 44×44px with adequate spacing between them?
- [ ] Are high-frequency and high-stakes actions placed near the user's natural attention zone?
- [ ] Is there system feedback within 400ms for every user action?
- [ ] Are loading states, skeleton screens, or progress indicators in place for operations over 400ms?
- [ ] Does the interface accept flexible, forgiving input and handle formatting variations gracefully?
- [ ] Is the form or flow as short as the task genuinely requires?

### Experience & Emotion
- [ ] Is the interface visually polished enough to create a positive first impression?
- [ ] Have I designed the emotional peak moment deliberately — the moment of delight or achievement?
- [ ] Does the final state of every flow (confirmation, success, completion) create a positive last impression?
- [ ] Are the highest-stress moments in the flow (checkout, errors, waits) given extra care?
- [ ] Does the interface teach itself — can a user accomplish their first task without reading anything?
- [ ] Have I identified the 20% of features that deliver 80% of value and optimized those?

### Information Architecture & Navigation
- [ ] Does navigation follow established conventions for this platform?
- [ ] Is there exactly one visually differentiated element per screen drawing primary attention?
- [ ] Is complexity being borne by the system rather than the user wherever possible?
- [ ] Is critical information positioned in the user's goal-directed attention path?
- [ ] Am I using visual hierarchy, position, and motion to guide attention to what matters?
- [ ] Are cognitive biases (anchoring, social proof, loss aversion) used deliberately and ethically?

---

## Quality Checklist

Before delivering the review:
- [ ] All six domains evaluated — no domains skipped without documented reason
- [ ] Every finding includes: what's wrong, why it matters, specific fix
- [ ] Severity ratings are calibrated to actual user impact, not design preference
- [ ] Systemic patterns identified where multiple findings share a root cause
- [ ] What's working is documented alongside violations
- [ ] Top 3 priority fixes identified by impact-to-effort ratio
- [ ] No generic feedback ("make it more usable") — every fix is specific and actionable

---

## Edge Cases

**Design is described in text, not shown visually:**
Proceed with text description and flag assumptions explicitly. Note which laws can be fully assessed vs. which require visual inspection to verify.

**Design is at concept/sketch stage:**
Calibrate findings to the stage — flag structural and architectural issues (information architecture, cognitive load, mental models) heavily; deprioritize pixel-level polish feedback (aesthetics, target sizes). Use checklist mode to guide rather than critique.

**Design is production-ready for release:**
Raise the bar for severity ratings. Issues that are Medium at wireframe stage become High or Critical at production stage if they've survived to shipping.

**Only one screen or component provided, not a full flow:**
Review what's available thoroughly and note which laws require flow context to assess (Goal-Gradient Effect, Peak-End Rule, Zeigarnik Effect require seeing the full user journey). Flag the gaps explicitly.

**Design intentionally breaks a convention:**
Acknowledge the break explicitly and evaluate whether the deviation is justified and adequately supported by compensating affordances. Jakob's Law violations are not automatically wrong — they require explanation and mitigation.

**Design is for an expert/power user audience:**
Adjust cognitive load thresholds upward — experts can handle more complexity. But Fitts's Law, Doherty Threshold, and memory laws apply regardless of expertise. Note the audience calibration in the review header.
