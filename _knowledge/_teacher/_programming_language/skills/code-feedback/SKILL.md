---
name: code-feedback
description: >
  Review a learner's code attempt the way a good senior reviews a junior:
  run it, run the tests and the official linters, then give feedback in
  priority order (does it work, is it correct at the edges, is it
  idiomatic, is it well designed) pointing at lines, without rewriting the
  solution. Trigger whenever the learner submits code: "done", "check my
  solution", "why doesn't this work", a pasted snippet, or a finished
  exercise.
---

# Code feedback

## 1. Run before you read

Run the build, the tests, the formatter check and the official linters on the
learner's code (`_programming_language` rule 5). Report the real output in a
short block. Never judge "this would work" by eye. Run it.

If it does not build, stop there. Ask the learner what the first error says
(`_programming_language` rule 4) before saying anything else.

## 2. Feedback in priority order

1. **What works**: one sentence of genuine, specific credit.
2. **Correctness**: failing tests, edge cases the tests missed (empty input,
   zero, nil or null, very large values, concurrency), and wrong results.
   Each one gets the line, the input that breaks it and the observed result.
3. **Idiom**: what a fluent programmer in this language would do
   differently, such as naming, error handling, the standard-library function
   that already exists, or the formatter's output. Name the false friend when
   a habit comes from the learner's background language (`_programming_language`
   rule 7).
4. **Design**: only once the above are clean. This covers function size,
   responsibilities and testability.

At most three points per round. Pick the ones that matter most for the
current module, and put the rest in the journal for later.

## 3. How to say it

- Point at the line, quote the fragment, say what is wrong and why, and give the
  rule to remember. Do **not** paste the corrected solution
  (`_programming_language` rule 3). A corrected *single line* is fine for
  syntax the learner has not met yet.
- Ask a question when the learner can find it themselves ("what happens on
  line 12 when the slice is empty?").
- After the learner's fixes pass, you may show the idiomatic reference for
  comparison and name the one or two differences worth learning.

## 4. Record

Record recurring mistakes and false friends in the journal's review queue
(`learning-journal`). The same mistake a third time is a **habit**. Tell the
learner, and make it a predict or fix exercise in the next session.
