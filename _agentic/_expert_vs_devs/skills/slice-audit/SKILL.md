---
name: slice-audit
description: >
  The expert's audit of a slice the devs claim finished: reproducing it from a
  clean extract, checking each claim rather than citing it, judging the rows the
  slice added, and clearing or holding the acceptance tick. Trigger when the
  devs report a slice or ask for a tick — "slice done", "awaiting audit", "can
  we tick", a claim message with a sha — and before anything is cleared.
---

# Auditing a slice

Every slice is audited before the next one starts, and no acceptance item is
ticked until the audit clears it. The devs have already reviewed their own code;
what the audit adds is an independent reproduction and a check of what they
claim, against the tree they committed rather than the one they describe.

## 1 — Leave their tree alone

You read; you never write to their working tree. Record `HEAD` and the working
tree status before and after, and treat any unexplained change as a failed audit.
Old behaviour is seen in a scratch copy outside the repository, never by mutating
the source under review.

## 2 — Reproduce from a clean extract

- **Extract the claimed sha** (for example, `git archive <sha>` run from the
  repository root) into scratch you own.
- **Assert the file count.** An archive run from a subdirectory can match
  nothing and still exit 0; an empty extract then produces a clean run.
- **Run the suite from the extract**, capturing the exit status directly — not
  through a pipe, where it is the last command's status and can read 0 over a
  roster that says "2 failed".
- **Grep the failure markers separately**, and read a zero with suspicion: a
  pattern in the plural misses a singular summary line.
- **Compare with their prediction**, made before their run. Figures that match
  exactly are evidence of understanding; figures that match only after the run
  are not.

## 3 — Check the claims, do not cite them

For each line of their claim, check the thing itself: the files touched are
the files in the diff, and none is in your paths; the rows exist and assert what
their names say; the mutant they say was killed is the mutant the rig actually
built — a matched anchor proves the anchor matched, not that the result is the
mutant named. A figure in their message that you did not reproduce is theirs,
labelled as theirs.

State plainly what you did not reproduce.

## 4 — Judge the rows

- **A kill-set measures what a row catches in this tree, not what it pins.** A
  row no mutant distinguishes still earns its place only if the claim it states
  is currently unfalsifiable **and** no existing row can express it. Ask: what
  would have to change for this row to fail, and can anything else catch that?
  If another row already states it, it is redundant — say so.
- **A fixture that hard-codes what the unit produces cannot test the unit.** It
  passes every mutant while looking green. Fixtures are built by calling the
  unit.
- **A row that errors is not a kill.** An exception raised in a When is a crash
  the rig may score as caught. Capture the failure there and judge it in the
  Then, so a regression fails rather than errors.
- **An empty assertion is an answer.** A step that asserts on a key lookup
  passes when the key is absent; one that asserts on the whole record does not.

## 5 — Rule and deliver

Write the review file: the verdict in the first line — CLEARED or NOT CLEARED,
and TICK or HOLD — then the findings, each graded (blocking, non-blocking, for
awareness) with its evidence cited by file and name, then what was not
reproduced. Findings in your own files are yours to fix, and you say so.

Deliver it exactly as `expert-rulings` describes: index, commit, send, receipt.
An audit reported only to the human, in your terminal, has cleared nothing.
