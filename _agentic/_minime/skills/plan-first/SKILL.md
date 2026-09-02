---
name: plan-first
description: >
  The rule that nothing is built before the intent is written down and available
  to the owner, and the item-by-item check of a plan against the request that
  makes it worth writing. Trigger when work is about to start on a work item,
  when a plan or approach is being drafted, and when a posted plan is being read
  before development — "start on this", "here is the plan", "shall I begin",
  "the plan looks fine", or a plan arriving for approval.
---

# Plan before work

Nothing is built until the intent has been stated in writing and is available to
the owner.

The cost of this is minutes. The cost of skipping it is a complete, competent,
faithfully-executed delivery of the wrong thing — built in the wrong repository,
in the wrong language, missing every named deliverable, because the work
proceeded from a summary nobody outside the agent ever read. That failure does
not announce itself along the way; every step after the misreading is correct.

This step is under permanent pressure to be skipped, because it is the step where
nothing appears to be happening.

## What a plan has to say

Enough that the owner can recognise a misunderstanding from it alone:

- Which repositories and systems the work touches.
- What will exist when it is done, with the paths it lands at.
- The approach, and the decisions inside the approach that could reasonably have
  gone the other way.
- What it deliberately does not do.
- How each stated success criterion will be satisfied.

Post it as a statement, not a question. It is posted whether or not anything is
unclear — its purpose is to let a misaligned plan be caught before a delivery is
built on top of it, and an agent that is not confused is exactly the agent whose
plan needs reading.

## Verify the plan against the request

Not against your reading of the request — against the request itself, in its own
words, item by item. Four kinds of miss, each a question to ask rather than a
silence to keep:

- A **deliverable** named in the request with no place in the plan.
- A **success criterion** that nothing in the plan satisfies.
- An **excluded action** that the plan performs anyway. This one is dangerous
  because the excluded action usually looks helpful.
- An **invariant** with no mechanism — a guard, an ordering, a test. An intention
  to be careful is not a mechanism.

Where the request is large, unfamiliar, spans several systems, or specifies an
architecture, at least one confirming question is worth asking outright. Naming
the architecture out loud in one sentence has caught more misreadings than any
amount of careful reading.

## Carrying the plan into the work

Whoever executes gets the plan as written, alongside the request itself, and
stops on any contradiction between them rather than choosing a side — see
`delegation-conduct`, *The brief*.

When the plan turns out to be wrong mid-flight, the fix is a new plan, not a
patch applied quietly to the code. The owner approved a plan; they should be
looking at the one being built.
