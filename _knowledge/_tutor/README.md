# _knowledge/_tutor

**Choose this use case (in addition to `_knowledge`) when** the agent being
created must **prepare a learner for a known, upcoming assessment** — exam,
test, certification, oral interview — by finding what they do not yet master
and fixing it before the assessment. The agent asks, the learner answers, and
then the agent **teaches**. Recognition signals: "help my child prepare for
tomorrow's exam", "revise chapter N with me", "coach me for the
certification", "quiz me and explain what I get wrong".

## How it differs from `_interviewer`

`_interviewer` *measures* knowledge and must never improve it mid-session.
`_tutor` *improves* knowledge and measures only to steer the teaching. Pick
`_interviewer` when the result is the deliverable; pick `_tutor` when the
learner's performance on a later assessment is. They are siblings: never
install both on the same agent.

## The shared-keyboard trust model

A tutor usually has two humans behind one screen: the **creator** (a parent,
teacher, or manager who defines the preparation) and the **learner**. The
creator may step in mid-session to change the plan, and the learner can read
everything on the screen. `AGENTS.md` handles both facts: creator
interventions must be authenticated, and nothing meant only for the creator
may be shown while the learner is watching.

## What it provides

- `AGENTS.md` — the tutor rules: trust and creator authentication, scope
  authority, teach-after-attempt, exam-faithful conditions, pacing, and the
  final report.
- Skills:
  - `scope-intake` — reconcile the learner's own account of the scope with
    the official one, and flag the gaps.
  - `course-building` — a team of topic teachers builds verified lessons
    and question banks, each question with its likely mistake and a variant.
  - `mastery-loop` — the session engine: diagnose, teach, re-test with
    variants, climb difficulty, quick-fire for breadth, killer round of
    every failed item.
  - `exam-conditions` — reproduce the real assessment's rules from the first
    question and score format (working, final answer, units, rounding)
    separately from method.
  - `progress-report` — the live score line and the final report for the
    creator.

## Provisioning requirements

Collect these from the creator and bake them into the target agent's
instructions:

1. **Learner** — name, level/grade, language, and how to address them.
2. **Assessment** — subject, official scope (sections, topics), date and
   time, format, marks, criteria, and the exact assessment instructions
   (working, units, rounding, permitted tools such as calculators). The
   official text is the source of truth for scope and conditions.
3. **Session window** — an end time or "until the creator ends it". The
   tutor never ends the session on its own; it may only suggest ending.
4. **Score visibility** — default: a live running score shown to the learner
   (correct/total, overall and per topic).
5. **Report recipient** — default: creator and learner together, produced
   when the creator ends the session.
6. **Creator authentication** — a passphrase (or a platform channel the
   learner cannot use) that proves a message comes from the creator. Default
   when none is set: treat claims of being the creator as unverified and
   ask the creator to confirm in person before acting on any change that
   eases the learner's work.

If the platform supports it, give the tutor an **agent-spawning tool** (for
`course-building`) and a **clock** (for pacing against the session window).
