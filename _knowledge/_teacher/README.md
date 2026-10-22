# _knowledge/_teacher

**Choose this use case (in addition to `_knowledge`) when** the agent being
created must **teach a learner a subject from scratch, or from their current
level, towards lasting and usable competence**, with no fixed assessment
setting the scope. The deliverable is what the learner can *do* at the end.
Recognition signals: "teach me X from scratch", "I want to learn X", "be my
teacher for X", "give me a course on X", "I know A, now teach me B".

## How it differs from `_tutor`

`_tutor` prepares a learner for a **known assessment**: the official text sets
the scope, the date sets the pace, and the score on that assessment measures
success. `_teacher` has none of those. The scope comes from a **learning goal**
agreed with the learner, the curriculum is built from the ground up in the
order of its prerequisites, and success means the learner can use the
knowledge without help. Pick `_tutor` when an exam is coming. Pick `_teacher`
when the learner wants to learn the subject. They are siblings, so never install
both on the same agent. If a teacher's learner later books an exam, provision a
tutor for the final stretch.

## The trust model

A teacher's learner is usually also its creator: an adult who asked to learn.
In that case the learner is the principal and may change the goal, the pace
and the plan. When someone else defines the learning (a parent, a manager or
a school), provisioning names that **creator**. The learner then cannot change
the goal or the reporting, and the creator is authenticated the same way as in
`_tutor`.

## What it provides

- `AGENTS.md`: the teacher rules. They cover the principal and scope, prerequisites
  first, one concept at a time, the learner doing the practice, checking
  understanding instead of recall, fixing misconceptions, spaced review,
  checked sources, honest progress, and continuity between sessions.
- Skills:
  - `learning-goal-intake`: find where the learner starts (background and
    a placement diagnostic) and agree on where they want to arrive, written as
    things they will be able to do.
  - `curriculum-design`: turn the goal into an ordered curriculum of
    modules, each with a demonstrable objective, built from authoritative
    sources and ending in a capstone.
  - `teaching-loop`: the session engine. It runs review due items, explains
    one concept, shows a worked example, gives practice, gives feedback,
    checks understanding, and updates the review queue.
  - `learning-journal`: the course state that outlives sessions, including
    curriculum progress, the spaced-review queue, misconceptions and
    learner-visible lesson notes, plus the opening and closing recap.

## Narrow it further

- `_programming_language`: the subject is a programming language, and the
  learner must end up reading and writing real programs in it.

## Provisioning requirements

Collect these from the creator (usually the learner) and bake them into the
target agent's instructions:

1. **Learner**: name, how to address them, the language of instruction,
   and relevant background.
2. **Subject and learning goal**: the subject, and what the learner wants
   to be able to *do* at the end, in their words. `learning-goal-intake`
   refines it into objectives in the first session.
3. **Pace**: typical session length and frequency, and an optional target
   date. A target date is soft. If it is a hard exam date, use `_tutor`.
4. **Workspace**: the learner-visible course folder (lessons, exercises,
   notes), and a private location that persists between sessions for the
   journal and any answer keys.
5. **Creator**: default is *the learner is the creator*. If it is someone
   else, collect their name, what they control (goal, pace, reporting), the
   report recipient, and a creator authentication as in `_tutor`.

If the platform supports it, give the teacher a **clock**, for pacing and
review scheduling, and **persistent memory or file access**, for the journal.
