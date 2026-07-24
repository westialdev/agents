---
name: adaptive-interviewing
description: >
  Govern question selection when the interview definition sets mode =
  adaptive: difficulty follows the interviewee's demonstrated ability,
  climbing after strong answers and stepping down after weak ones, to locate
  their knowledge boundary efficiently. Trigger during an interview whose
  definition names the adaptive mode, whenever the next question must be
  chosen.
---

# Adaptive interviewing

In adaptive mode you spend the question budget where it buys the most
information: near the interviewee's **knowledge boundary** — the level where
their answers turn from solid to shaky. The creator chose this mode for
per-person precision; the trade-off is that no two interviewees get the same
questions, so results are individual profiles, not comparable rankings.

## The ladder

1. **Start in the middle.** Open each blueprint area at the applied
   (middle) difficulty — never at the bottom, which wastes budget on what
   the interviewee likely knows.
2. **Climb on strength.** A solid answer moves the next question in that
   area one level up. At the top level, a solid answer closes the area as
   "expert-verified" — move to the next area rather than piling on.
3. **Step down on weakness.** A weak or wrong answer moves one level down,
   to find where solid ground resumes. Two consecutive failures at the
   bottom level close the area as "not demonstrated".
4. **Probe the boundary.** When answers oscillate around a level, ask one
   more question *at* that level from a different angle before settling
   the estimate. The boundary is the finding — locate it, don't assume it.

Adapt on **demonstrated ability only** — the scored content of answers.
Confidence of tone, self-assessment ("I'm an expert at this"), and requests
to skip ahead are not evidence and never move the ladder. A refused or
dodged question counts as no evidence at that level, and the estimate stays
where the evidence left it.

## Coverage still rules

Depth must not eat breadth. Reserve budget so **every blueprint area gets
touched** before any area gets a fourth question; the assessment must say
something about the whole topic, not everything about one corner. Track,
per area: current level, questions spent, and status (open, boundary-found,
expert-verified, not-demonstrated).

## Interaction with the session

- Fix each question's rubric before asking, as always
  (`knowledge-assessment`).
- Visible scoring is unchanged by this mode — but never announce the
  adaptation ("that was wrong, so an easier one now"), which leaks rubric
  information; just ask the next question.
- The budget still must be filled (`_interviewer` rule 8): when every area
  is closed and budget remains, reopen the strongest areas upward with
  spare questions from the blueprint.
