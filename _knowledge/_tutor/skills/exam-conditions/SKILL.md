---
name: exam-conditions
description: >
  Make practice match the real assessment: take its instructions (permitted
  tools, working, units, rounding, or the structure and criteria of written
  work) as rules from the first question, score answer format separately
  from method, mark criterion-based tests by band with a "band-up" coaching
  step, and set the format of a timed written mock. Trigger when the assessment
  instructions are known, when marking any answer, when the learner asks
  the tutor to do part of the work, or when a mock is due.
---

# Assessment conditions

Learners often know the method and still lose marks on format. Practice under
the real rules turns format into a habit.

## Set the conditions at the start

From the official instructions, write a short **answer contract** and show it
to the learner before the first question. For a calculator maths exam it
might read:

> formula → numbers substituted → full calculator value → rounded answer +
> unit

Then hold it for the whole session:

- **Permitted tools**: if the learner has a calculator in the exam, they use
  their own in practice. Don't promise to do the arithmetic, not even once.
  One "I'll calculate this time" turns into "you do it" for the rest of the
  session, and the final numbers stop appearing.
- **Rounding**: every question states its rounding instruction. Expect
  trailing zeros (36.0 at 1 d.p.) and rounding at the end.
- **Constants**: use the exact value, such as the π button, unless the
  question says to use an approximation like 3.14.

## Written, rubric-marked assessments

For an essay, a literary analysis or another extended written answer, the
answer contract is the **expected structure**. For a literary analysis it
might read:

> thesis that answers the question → paragraphs of point → embedded
> quotation → technique named → effect explained → link back to the
> question's key idea → conclusion

Hold it the same way:

- **The learner writes every sentence.** Model a paragraph only on a
  different text or extract from the one they are practising on, and never
  "fix" their paragraph by rewriting it; correct the fragments.
- **Conventions are format.** For example, events in a literary text are
  written in the present tense ("Montag realises"), quotations are copied
  exactly and woven into the learner's own sentence, and techniques are
  named precisely.
- **Copyrighted texts**: quote only short passages. For longer practice
  extracts, use text the learner provides from their own copy, or write
  original passages in a similar style, clearly labelled as not the
  author's.
- **Language**: load `writing-accuracy` (`_tutor` rule 15).

## Criterion-marked tests: aim at the top band

Many school tests (MYP sciences Criterion A, for example) are marked with
**level descriptors**, not by adding up points. The bands usually differ in
*depth* and *novelty*, not in how many facts the learner knows: a middle
band can describe and apply in familiar situations, while the top band
explains with the mechanism, applies to **unfamiliar** situations and makes
**judgments supported by data**. A learner who knows the content can still
sit in the middle band. Train the difference explicitly:

- **Get the descriptors.** Ask the creator for the criterion's level
  descriptors and any task-specific clarification the teacher shared. If
  there are none, use the official framework's descriptors for the
  learner's year and say that you did.
- **Command terms decide the depth.** State → describe → explain →
  evaluate are different jobs. Put the command term at the start of every
  question, exactly as the exam would.
- **The explain chain** is the answer contract for an "explain" question:

  > claim → **because** (the mechanism, with the scientific term) →
  > **so** (the consequence) → evidence (a figure quoted from the data,
  > with its unit)

  An answer that stops at the claim is a "describe" answer, whatever its
  length.
- **One point per mark.** A 3-mark question needs three distinct scientific
  points. Before answering, the learner counts the marks and plans the
  points.
- **Evaluate = both sides + a judgment.** Strengths, limitations (sample
  size, missing control, correlation versus cause), then a conclusion that
  quotes the data.
- **Unfamiliar situations.** At least a third of the apply and analyse
  questions are set in a context the class did not study (another disease,
  another dataset), so the learner practises transferring the idea.

Mark every such answer with its band and a **band-up** line: the one or two
sentences that would lift it to the next band ("you said *what* the
antibiotic does; add *why* six months: the bacteria grow slowly, and
survivors become resistant"). Then the learner **rewrites the answer
themselves** (`_tutor` rule 9). The rewrite is scored too; it is how
"describe" turns into "explain".

## Timed mock

Before the assessment, run `mock-assessment` (`_tutor` rule 19), at least a
day before so there is time to fix what it shows (`_tutor` rule 23). For a
timed written test the mock is the full paper: the real duration, the real
section mix and proportion of command terms, the permitted tools, answers
written at exam length (on paper with a photo, if the exam is on paper),
and a band per criterion afterwards. It is the only practice of the clock,
and the best forecast of the band.

## Spoken, rubric-marked assessments

For an interview, oral exam or presentation, the answer contract is the
spoken one in `oral-communication` (`_tutor` rule 18): signpost, claim,
evidence, source named aloud, link, close. Before the assessment, rehearse
it under the real conditions with `mock-assessment` (`_tutor` rule 19).

## Score format separately

For each answer, record two marks: **method** (right approach, right setup)
and **format**. For rubric-marked work, record a mark or band **per
criterion** instead (for example MYP A–D, /8 each): every criterion the
assessment is marked on, or every criterion of the framework while those
are unknown (`_tutor` rule 17). Say which part of the answer earned or lost
each one; a right/wrong mark hides where the marks
were lost. Format faults:

- no final answer (a setup or an expression left as "= ?")
- missing or wrong unit (a cm result labelled m)
- a false working line ("400 × 12 = 4.8 km" with the unit change hidden)
- wrong rounding, or rounding too early in a way that changes the result
- answer only, with no working
- in written work: a missing thesis or conclusion, quotations not embedded or
  not exact, the wrong tense for the text's events, no link back to the
  question

Credit for method can be generous, but point out every format fault, every
time, with the corrected line. When a format fault repeats, call it the
learner's "last enemy" and turn it into a self-check question ("cm? m?
km?").
