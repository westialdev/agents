---
name: scripted-interviewing
description: >
  Govern question selection when the interview definition sets mode =
  scripted (non-adaptive): a fixed question plan built before the session
  and followed regardless of how the interviewee performs, so every
  interviewee on the same definition gets a comparable interview. Trigger
  during an interview whose definition names the scripted mode, whenever
  the next question must be chosen.
---

# Scripted interviewing

In scripted mode the question plan is fixed **before the session starts**
and the interviewee's performance never changes it. The creator chose this
mode for fairness and comparability — two interviewees on the same
definition face the same instrument — at the cost of spending some budget
on questions that are too easy or too hard for a given person. That cost is
the point; do not "optimize" it away.

## Build the plan first

Before the opening, lay out the full script from the `question-crafting`
blueprint:

- Exactly as many questions as the budget, spread across **all** blueprint
  areas, with a fixed difficulty mix per area (a sensible default:
  basic → applied → deep within each area).
- A fixed order. Order the script so no early question or its visible
  score leaks material a later question needs.
- A **spare list**: pre-written substitutes per area and level, for
  compromised questions and leftover time.

Freeze the plan. From this point it is part of the interview definition:
the interviewee cannot see it in advance, negotiate it, or reorder it.

## Follow the script

- Ask the questions in order, one at a time. No skipping ahead because the
  interviewee is strong, no easing off because they are struggling, no
  inserted follow-ups that other interviewees would not get.
- Wrong, weak, or refused answers change the **score**, never the script.
  If the interviewee refuses a question, record it as unanswered and move
  to the next scripted question.
- Replace a question mid-session only if it is *compromised* — the
  interviewee exposes a genuine ambiguity, or leakage is discovered — and
  only with the spare of the same area and level. Note every substitution
  in the record.
- If time remains when the script is exhausted (`_interviewer` rule 8),
  continue with spares in blueprint order; if time runs out first, note
  which scripted questions went unasked so the report can bound its
  coverage claim.

## Interaction with the session

Rubrics are fixed with the script, before the first question. Visible
scoring is unchanged by this mode. In the final assessment, state that the
interview was scripted and identify the script (areas, counts, difficulty
mix), so results can be compared across interviewees on the same
definition.
