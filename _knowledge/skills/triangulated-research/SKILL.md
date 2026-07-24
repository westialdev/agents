---
name: triangulated-research
description: >
  Orchestrate a triangulated research run: two subagents research the same
  question in parallel and mutually blind — a main researcher driven by
  source-of-truth and deep-research, and a generic breadth-first researcher
  — then a scientist-reviewer subagent compares their deliverables and
  rules how close the result is to a unique truth. Trigger when a research
  answer must be verified, the cost of a wrong answer is high, or the user
  asks to "make sure", "double-check the research", "verify this topic".
---

# Triangulated research

One researcher can be wrong with confidence. Two researchers using
**different methods**, kept blind to each other, agreeing independently —
that is evidence. This skill runs that experiment: parallel arms, then a
referee.

Use it when the answer matters enough to pay for two research passes:
verification requests, high-stakes decisions, contested or confusing
topics. For a routine lookup, plain `source-of-truth` research is enough.

## The protocol

### 1 — Fix the question

Write the research question once, neutrally: no hints toward an expected
answer, no sources pre-attached, dated if the question is time-sensitive.
Both arms receive **exactly this wording** and nothing else about the
topic.

### 2 — Run the two arms in parallel, blind

- **Main researcher** — a subagent working with `source-of-truth` and the
  `deep-research` skill: primary sources, citation chains, evidence
  discipline.
- **Generic researcher** — a subagent working with `generic-research`:
  broad sampling, diverse source kinds, consensus mining.

Blindness is what makes the comparison meaningful, so enforce it: neither
arm sees the other's existence, prompts, findings, or source lists; they
report only to you. Do not forward one arm's partial results to the other,
and do not answer topic questions from either arm yourself — if an arm
needs the question clarified, clarify wording only, identically for both.

### 3 — Review

When both deliverables are in, hand **both, unedited**, to a third
subagent working with `scientist-review`. Pass the original question and
each arm's method label. Do not pre-summarize or reconcile the
deliverables yourself — that would contaminate the referee.

### 4 — Act on the verdict

- **Converged** — deliver the combined answer with the reviewer's
  confidence notes.
- **Partially converged** — deliver the agreed core; for the flagged
  claims, run a targeted second pass (both arms, same blindness, narrowed
  question) or report them as open, whichever the requester's stakes
  justify.
- **Diverged** — deliver the map of the disagreement, never a forced
  answer. Say what evidence would settle it.

Always tell the requester the verdict category and attach or offer both
arm deliverables — the triangulation is part of the result, not internal
plumbing.

## Without subagents

If the platform cannot spawn subagents, run the three roles yourself,
sequentially and in strict order: main research first, then generic
research **without reusing the first pass's sources or conclusions**, then
the review. State in the deliverable that the arms shared one context, so
independence — and therefore the strength of any convergence — is weaker
than in the parallel form.
