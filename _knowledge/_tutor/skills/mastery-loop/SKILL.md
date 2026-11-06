---
name: mastery-loop
description: >
  Run the tutoring session: draw each question from a shuffled queue that
  mixes topics and assessment sections, mark the attempt, teach the
  correction, re-test failed skills with spaced variants, raise difficulty
  on success, switch to quick-fire rounds for breadth when time is short,
  and close with a killer round of every previously failed item. Trigger on every
  turn of a tutoring session once the course exists: "next question", "I'm
  ready", a learner's answer.
---

# The mastery loop

## Shuffle: a non-linear journey

The course is written topic by topic, but the session must **not** follow
it. Before the first question, build a **shuffled queue** that interleaves
every topic (lesson) with every assessment section, and draw from it:

- **Never two questions in a row from the same topic.** Rotate the
  assessment sections too (for example A → C → B), so each topic is met
  through recall, application and data.
- **Breadth first.** Every topic gets one question before any topic gets
  its second, apart from re-tests.
- **Space the re-tests.** A missed skill's variant comes back after one or
  two questions from other topics, not immediately (see *Choose next*).
- **Quick-fire batches span three different topics**, never three questions
  from one lesson.
- **Don't announce the topic.** Ask the question as the exam would, so the
  learner must recognise which concept it needs.

Why it matters:

- The real assessment mixes topics. A lesson-ordered session gives the
  topic away, so the learner practises recall but not the skill of
  recognising *which* idea a question needs.
- A spaced re-test checks that the fix holds, not just that the learner can
  echo the correction they read a moment ago.
- Sessions end early: the creator steps in, or the learner tires. Shuffled
  from the start, an early end still leaves "a bit of everything". Lesson
  order leaves whole topics untested, usually the ones in the last lessons.

Keep the queue in the private progress file (`progress-report`) so the
next session continues the same shuffle.

## Each turn

1. **Ask**: one question, or a short batch in quick-fire mode, with the
   expected format stated (working, units, rounding).
2. **Mark**: compare the attempt with the bank's answer. Score method and
   format separately, or per criterion for written work
   (`exam-conditions`). For a written assessment, end the reply with the
   language check (`writing-accuracy`).
3. **Teach**: say what was right before what was wrong. Then give the
   correct worked answer in exam layout, name the trap in one sentence, and
   add a one-line rule to remember. When it helps, add a picture or
   metaphor ("imagine an ant walking all the way round the shape").
4. **Choose next**:
   - On a **miss**, put the bank variant of the same skill one or two
     places further down the queue, so a question from another topic comes
     first. Point out the trap in the question text if this is the second
     miss.
   - On a **hit**, take the next question from the shuffled queue, which is
     on a different topic. Raise that topic's level for its next turn.
   - If an incomplete message looks accidentally cut off, ask the learner to
     finish it. Do not mark it.
5. **Update the score line** (`progress-report`).

## Learner-led drills

A learner may skip the plan and ask for a drill directly ("give me a
sentence and I'll connect it"). If it is within the official scope, run it:
a learner who asks for practice is engaged. But (`_tutor` rule 14):

- note which steps it skipped (scope intake, lessons, uncovered scope) and
  return to them in the same session;
- an improvised question needs the same checks as a bank question
  (`_tutor` rule 13). If you can't check a fact behind it, don't ask it.

## Difficulty

Start each topic at the applied level. Raise its level after a correct
answer and lower it after a miss. The shuffle decides *which* topic comes
next; the difficulty rule decides *how hard* that topic's next question is.

## Quick-fire mode

When the session window is short or the creator asks for more coverage,
switch to batches of three short questions, each from a different topic and,
where possible, a different section, each answerable in a line. Coverage per minute rises a lot. The format rules still apply:
the final number and the unit are still required.

## Re-test list

Keep a list of every failed skill. A skill leaves the list only when the
learner gets a variant right. A skill that fails twice in different forms
(for example, borders added once on both a frame and a rug) is a **pattern**.
Name it to the learner as a pattern rather than as another single slip.

## Killer round

Near the end, or when the creator asks, run every item still on the re-test
list in a row, each with new numbers, in shuffled order rather than the
order in which they failed. Announce it as a challenge ("each one
has a trap"), let the learner answer in any grouping, and show a
before → now table afterwards. Any item still failing goes into one final
"boss" variant.

## Engagement

Learners tire and push back ("why would anyone need this?", "you do the
calculation", "I think I'm ready"). Answer briefly, with warmth and humour,
then hold the line: a sentence of real-world context, a polite refusal of
work they must do themselves, and no ending before the creator decides.
