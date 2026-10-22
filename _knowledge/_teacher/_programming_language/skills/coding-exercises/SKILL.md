---
name: coding-exercises
description: >
  Design programming exercises as runnable units: a short spec, a starter
  file that compiles, tests that fail on the starter and pass on a private
  reference solution, the likely mistake, and a variant for re-testing,
  progressing from katas through mini-programs to the capstone. Trigger
  when building a module's practice items, when the learner asks for
  "an exercise", "more practice", "a challenge", or when a review item needs
  a coding variant.
---

# Coding exercises

These exercises are the programming form of `curriculum-design`'s practice
items. The tests are the marking scheme, and the compiler is the first
examiner.

## Kinds, in order of the course

- **Predict**: read a short snippet and predict its output or the error,
  then run it. This is best for new semantics and false friends.
- **Fix**: a snippet with one bug tied to this module's concept. The learner
  finds and fixes it.
- **Kata**: one function to implement, with tests provided.
- **Extend**: add a feature to a working program from an earlier module. This
  builds the skill of reading existing code.
- **Mini-program**: the module checkpoint. It is a small complete program
  (a CLI, a server, a tool) with a spec and acceptance tests, and part of the
  tests are written by the learner once testing has been taught
  (`_programming_language` rule 8).
- **Capstone**: the learner's own target project, specified together and
  built over several sessions.

## Each exercise

In the course folder, which the learner can see, under `exercises/NN-name/`:

- `README.md`: the goal in two or three sentences, the exact input and output
  contract, an example, the command to run the tests, and the concepts used
  (all already taught, per `_teacher` rule 3).
- A **starter** that compiles and runs, with the function signatures in place
  and the bodies left for the learner.
- **Tests** with clear names that describe the behaviour, including at least
  one edge case. Failure messages say what was expected and what was got.

In the private location:

- **Reference solution**: idiomatic, formatted, and lint-clean.
- **Likely mistake**: the bug a learner with this background is most likely to
  write, and why it is wrong.
- **Variant**: the same concept with a different surface, for re-testing.

## Verification (`_programming_language` rule 1)

Before giving an exercise to the learner, run the following and confirm every
expected result:

1. The starter builds, and its tests **fail** (or do not pass) for the
   right reason.
2. The reference solution passes every test and is clean under the formatter
   and the linters.
3. The likely mistake **fails** at least one test. If it passes, the tests
   are too weak, so add one.

## Difficulty

Start each module with predict or fix exercises, then katas, then the
checkpoint. Raise the difficulty after a clean pass, and lower it or switch to
a predict exercise after two failed attempts (`teaching-loop`).
