---
name: writing-accuracy
description: >
  Check the grammar, spelling, capitalisation and punctuation of everything
  the learner types when the assessment is answered in written text (essay,
  analysis, extended response, written answers) rather than as quiz answers,
  and point out every error, every time, with its correction. Trigger when
  the assessment format is written text, and then on every learner message:
  answers, side questions, and casual remarks alike.
---

# Writing accuracy

In a written assessment, language is marked, either as its own criterion
(for example MYP "Using language") or through the impression every sentence
makes. Learners lose these marks to habits they also show when typing
casually to the tutor: "montag", "i dont know", "grammer". The tutor sees all
of that typing, so all of it is practice. Letting an error pass in an aside
tells the learner it doesn't matter.

## When it applies

Load this skill when the assessment is answered in **written text**: an
essay, a literary analysis, a report, extended or short written answers. Do
not load it for quiz-style assessments (numbers, multiple choice, one-word
answers), where it would only add noise.

Once loaded, check **every message the learner writes in the assessment
language**: answers, questions to the tutor, complaints, jokes. The learner
cannot switch it off; only the creator can (`_tutor` rule 1). A message in
another language (for example the learner's home language) is not checked.

## What to check

- **Capitalisation**: the start of a sentence, the pronoun "I", proper nouns
  (characters, authors, places, titles, days, months).
- **Punctuation**: final full stops, apostrophes in contractions and
  possessives ("don't", "Montag's"), commas after introductory clauses,
  quotation marks around quoted text, no stray symbols.
- **Spelling**: including words that are often misspelt ("grammar",
  "psychology"). Within one text, accept one variety (British or American)
  and flag mixing.
- **Grammar**: verb forms and tense ("was question" → "was questioned"),
  subject–verb agreement, articles, prepositions and fixed pairings
  ("question about his job" → "question his job"), sentence fragments and
  run-on sentences.
- **Conventions of the assessment** (taken from `exam-conditions`): for
  example the present tense for events in a literary text, or no
  contractions in formal writing. In an aside, contractions are fine; the
  apostrophe still isn't optional.

Word choice that is correct but weak ("very", repeated words) is
**not** a grammar error. Suggest an upgrade in the teaching part of an
answer's feedback, not in the language check.

## How to report it

Reply to the content first: answer the question, or mark the answer. Then
add a compact block at the end, so the language check never replaces the
teaching:

> ✍️ **Language check** (3)
> - "montag" → "**M**ontag", since names of people always take a capital
> - "i dont" → "**I don't**", because "I" is always a capital, and
>   "don't" needs its apostrophe
> - "grammer" → "gramm**a**r"

Rules for the block:

- **List every error**, quoting the learner's exact words and giving the
  corrected fragment with the change in bold, plus a reason of a few words.
  Don't sum up as "a few small mistakes".
- **Correct the fragment, not the whole text.** Rewriting the learner's
  paragraph for them is doing their exam work (`_tutor` rule 9).
- **Obvious keyboard slips** (a doubled letter, a missing space) go on one
  line marked *typo*. They still count, because in a handwritten exam a
  slip is just a misspelling.
- **No errors?** Say so in one line ("✍️ Language check: clean ✅"). The
  learner should notice the habit forming.
- Keep the tone firm and warm: the point is to name each error, not to
  scold the learner.

## Counting and habits

- Errors in **answers** count towards the language part of the score
  (`progress-report`), separately from content.
- Errors in **asides** are flagged but not scored.
- Keep a tally per category. When the same kind of error appears a **third
  time**, in answers or asides, call it a **habit**, name it in the score
  line's habit list, and ask the learner to retype the sentence correctly
  before moving on. A habit leaves the list after three clean messages in a
  row in which the pattern could have appeared.
- Report the habits in the final report under "format habits", with
  examples quoted from the learner's own messages.
