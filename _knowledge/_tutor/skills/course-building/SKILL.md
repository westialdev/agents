---
name: course-building
description: >
  Build the preparation course for a tutoring session: split the official
  scope into topics, have one teacher agent per topic write a short lesson
  and a verified question bank whose every question carries its likely
  mistake and a variant, and keep the answers private. Trigger after scope
  intake, or when the creator asks to "build the course", "prepare the
  questions", "create the preparation".
---

# Building the course

The course is the tutor's instrument. Each question must be able to teach as
well as test, so it carries its answer, the mistake learners usually make,
and a fresh variant for re-testing.

## The teacher team

Split the official scope into its sections (use the assessment's own section
labels when it has them). If you can spawn agents, start **one teacher per
section, in parallel**, while you begin the session with a warm-up question.
Otherwise, write the sections yourself one after another. Give each teacher a
self-contained brief that includes the learner's level, the assessment
format and instructions, and the section's sub-skills.

Each teacher produces two files:

1. **Lesson**, for the learner and safe to show. It should be short, aimed
   at the learner's level, and contain the key ideas, formulas, a diagram
   where it helps, one or two fully worked examples in the assessment's
   required format, the common traps, and exam tips. It must contain **no**
   bank answers.
2. **Question bank**, private. About ten questions per section, split into
   basic, applied, and exam-hard levels. Each entry has:
   - the exact question text, with a diagram if needed (every dimension
     labelled and consistent);
   - the full worked solution and the final answer with units and rounding;
   - the **likely mistake** and one sentence on why it is wrong;
   - a **variant** (same skill, new numbers and wording; in a text subject,
     a new fact, quotation or extract) with its answer;
   - the **source** of every fact and quotation it relies on (chapter,
     page, section).

## Verification

Every number in the lessons and banks must be **computed, not recalled**.
Use code (for example `python3`) to check answers, rounding, the values of
the likely mistakes, and the consistency of composite diagrams.

Every fact must be **checked, not recalled** (`_tutor` rule 13): plot
events and their order, who says what, dates, definitions, and the exact
wording of quotations. Check them against the learner's own text or the
best available source (`source-of-truth`), and mark anything you could not
check as unverified rather than presenting it as fact. A question that asks
the learner to link events is only as good as the order of those events. Read through
each bank yourself before the first question from it, checking that the
answers are right, the difficulty is labelled correctly, and no question
leaks the answer to another.

## Privacy

Store banks where the learner will not open them, such as a scratch or temp
directory rather than the course folder. Displaying a file can show its
contents on screen, so do not print bank contents in the session. Lessons go
in a learner-visible folder so they can revise from them later.
