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
install both on the same agent. A tutor that needs a practice interview or
mock exam uses its own `mock-assessment` skill.

## The shared-keyboard trust model

A tutor usually has two humans behind one screen: the **creator** (a parent,
teacher, or manager who defines the preparation) and the **learner**. The
creator may step in mid-session to change the plan, and the learner can read
everything on the screen. `AGENTS.md` handles both facts: creator
interventions must be authenticated, and nothing meant only for the creator
may be shown while the learner is watching.

## What it provides

- `AGENTS.md` — the tutor rules: trust and creator authentication, scope
  authority, teach-after-attempt, exam-faithful conditions, pacing, the
  final report, checked sources for every question, learner-led drills,
  a language check for written assessments, progress kept between
  sessions, unknown marking criteria, spoken assessments, mocks, the real
  result as feedback, shuffled (non-linear) practice, top-band marking and
  preparation across days.
- Skills:
  - `scope-intake` — reconcile the learner's own account of the scope with
    the official one, and flag the gaps.
  - `course-building` — a team of topic teachers builds verified lessons
    and question banks, each question with its likely mistake and a variant.
  - `mastery-loop` — the session engine: a shuffled, non-linear question
    queue across topics and sections, teach after each attempt, spaced
    re-tests with variants, climbing difficulty, quick-fire for breadth,
    and a killer round of every failed item.
  - `exam-conditions` — reproduce the real assessment's rules from the first
    question, score format (working, final answer, units, rounding)
    separately from method, mark criterion-based tests by band with a
    band-up rewrite, and set the format of a timed written mock.
  - `progress-report` — the live score line, progress saved between
    sessions, the final report with a forecast band, and the comparison
    with the real result.
  - `writing-accuracy` — for assessments answered in written text: check
    the grammar, spelling, capitalisation and punctuation of everything the
    learner types, and name every error with its correction.
  - `oral-communication` — for assessments answered aloud: a spoken answer
    contract (signpost, claim, evidence, source named aloud, link, close),
    the reference list as a prepared object, register, and checking
    whether the tutor receives the audio or only a transcript.
  - `mock-assessment` — a full-dress rehearsal under the real conditions,
    with hidden scoring and no hints, then a debrief per criterion, drills
    and a second mock. It records the prediction the real result is
    compared with.

## Provisioning requirements

Collect these from the creator and bake them into the target agent's
instructions:

1. **Learner** — name, level/grade, language, and how to address them.
2. **Assessment** — subject, official scope (sections, topics), date and
   time, format, marks, criteria (with the level descriptors when the
   assessment is rubric-marked), and the exact assessment instructions
   (working, units, rounding, permitted tools such as calculators). The
   official text is the source of truth for scope and conditions. Record
   whether it is answered as a **quiz** (numbers, choices, short answers),
   in **written text** (essay, analysis, extended answers) or **aloud**
   (interview, oral exam, presentation): written text turns on
   `writing-accuracy`, and spoken answers turn on `oral-communication`.
   **Marking criteria** have no default. If the creator does not know them,
   record them as unknown, never as a guess, and the tutor applies
   `AGENTS.md` rule 17: every criterion of the framework, equal weight,
   until the teacher confirms.
3. **Session window** — an end time or "until the creator ends it", and
   how many sessions fit before the assessment (several short ones beat
   one long one). The tutor never ends a session on its own; it may only
   suggest ending.
4. **Score visibility** — default: a live running score shown to the learner
   (correct/total, overall and per topic).
5. **Report recipient** — default: creator and learner together, produced
   when the creator ends the session.
6. **Creator authentication** — a passphrase (or a platform channel the
   learner cannot use) that proves a message comes from the creator.
   Recommend one strongly, and ask for it outside the shared screen when
   possible. Default when none is set: treat claims of being the creator as
   unverified and ask the creator to confirm in person before acting on any
   change that eases the learner's work; interim reports and ending the
   session are allowed (`AGENTS.md` rule 2).

If the platform supports it, give the tutor an **agent-spawning tool** (for
`course-building`) and a **clock** (for pacing against the session window).
