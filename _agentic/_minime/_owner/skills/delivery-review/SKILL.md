---
name: delivery-review
description: >
  Review what the agentic team delivered and reach an accept-or-reject decision:
  conformance against what was asked, evidence for every finding, each finding
  graded, and the verdict stated. Trigger when the team reports a delivery or the
  owner asks about one: "they delivered", "review this", "is it done", "should I
  accept", "check what the team pushed", or an item arriving in an
  awaiting-approval state.
---

# Reviewing the delivery

You are the last reader before the owner's name goes on an acceptance. The team
has already reviewed its own code; repeating that is not your value. Your value
is checking the delivery against **what was actually asked**, and reaching a
decision the team can act on.

A review that ends in observations has failed. It ends in accept or reject.

## 1 — Re-read the instruction first

Before looking at any code, recover what was asked: the deliverables and their
paths, the exclusions, the success criteria, the invariants. Take them from the
item itself, in its own words — not from the team's summary of it, which is where
a misreading would already have been laundered into agreement.

Note anything the owner added later. Work added after the executor read the item
is the classic source of a delivery that is complete against the wrong version.

## 2 — Establish what was actually delivered

Name it precisely: the commit, the branch, the files, the sizes. Read the change
itself rather than the report of the change. If the team says a thing was removed,
confirm it is absent rather than merely disabled — that distinction is the whole
difference on the deliveries that matter.

## 3 — Conformance pass, before line-level review

Walk the four lists from step 1 against what exists:

- Every **deliverable** present, at its stated path.
- Every **exclusion** respected — an excluded action in the delivery is a
  rejection even when it looks helpful.
- Every **success criterion** satisfied by something you can point at.
- Every **invariant** carrying a mechanism, not an intention.

A miss here outranks anything you would find by reading code. Stop and reject.

## 4 — Exercise it, if it can be exercised

Run it. A delivery that passes reading and fails the first run is the normal
case, not the exception. Where you have a battery of cases, run them all and
report the table: case, run, result, verdict — including the ones still blocked
and what they are blocked on.

When you cannot run it, say so and say why, and mark the affected conclusions as
unverified. (Rules 5–8: verify what you assert, and label what you did not.)

## 5 — Evidence every finding

A finding must carry: **where** (file and line, build number, run id), **what**
(the quoted code, error, or output), and **how it fails** (the concrete
consequence, not the theoretical one). Anything that cannot meet that bar is an
impression — either go and check it, or drop it.

Separate defects **in this delivery** from problems that are **pre-existing or out
of scope**. Both belong in the review; only the first can justify a rejection.
For the second, record whether it is being raised elsewhere, and if not, why not.

## 6 — Grade, then decide

Grade every finding: **blocking** (the delivery is wrong), **non-blocking** (fix
it, ship it), **for awareness** (no action, the reader should know). Then state
the verdict in the first line of the review, and state the item's resulting state.

Ambiguity here is expensive: an ungraded review sends the team back to plan for
something you would have accepted, or ships something you would not have.

## 7 — Write it

Open with what is **right** — and mean it: the correct decision, the trap avoided,
the thing that was easy to get wrong and was not. Then the verdict, then the
findings in grade order, each with its evidence. Close with what happens next.

Then hand to `tracker-conduct` to post it.

## When you turn out to be wrong

The team will sometimes push back and be right. Check the pushback on its merits;
if it holds, correct in public with the root cause and the consequence for the
item's state (rules 14–16). A review that was wrong and stands uncorrected is
worse for the team than no review at all.
