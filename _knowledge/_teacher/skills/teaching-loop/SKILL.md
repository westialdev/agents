---
name: teaching-loop
description: >
  Run a teaching session once the curriculum exists: open with the due
  review items, then cycle explain → worked example → learner attempt →
  feedback → understanding check through the current module, and close with
  a recap. Trigger on every turn of a teaching session: "let's continue",
  "next", "I'm ready", a learner's attempt or question.
---

# The teaching loop

## Opening a session

1. Read the journal (`learning-journal`) and tell the learner in two lines
   where they are: the current module and what they did last time.
2. Run the **review items that are due**, as short attempt-first questions,
   before anything new (`_teacher` rule 9).

## Each step

1. **Explain** one concept (`_teacher` rule 4) in a few sentences, contrasting
   it with something the learner knows when that helps. Point to the lesson
   file for the full version.
2. **Show** one worked example that has been checked, not recalled.
3. **Practice**: give one item from the module. State exactly what a
   complete answer looks like. Then wait. No hints before the first attempt.
4. **Feedback** (`_teacher` rule 6): what's right, what's wrong and why, and
   a rule to remember.
   - On a miss, if it reveals a misconception, name it as one and give the
     variant now or later in the session. Then add it to the review queue.
   - On a hit, move on, or raise the difficulty one level.
   - If the learner asks for help instead of attempting, give the next
     graded hint (`_teacher` rule 5), not the answer.
5. **Check understanding** before leaving the concept (`_teacher` rule 7):
   ask for a prediction, an explanation in their own words, or a new case.
6. **Update** the journal.

## Pace and difficulty

- Two hits in a row on the same concept: go to the next concept.
- Two misses in a row: step back. Re-explain from a different angle (a
  picture, an analogy, a smaller example) before another attempt. Check
  whether a prerequisite is missing.
- Close the module with its **checkpoint**. A failed checkpoint names the
  weak concept, and that concept gets one more round before you move on
  (`_teacher` rule 11).

## Learner questions

Answer in-scope questions briefly, even if they run ahead. Say "we'll see
it properly in module N". Park tangents in the journal's "optional later"
list (`_teacher` rule 2). A good question deserves a word of credit, because
curiosity is what you want more of.

## Closing a session

End with a **recap** of at most three bullets of what was learned, the
misconceptions fixed or still open, and the **next step**. If the learner
wants homework, make it an exercise for the next concept or a review item.
Save the journal.
