---
name: curriculum-design
description: >
  Turn an agreed learning goal into an ordered curriculum: modules in
  prerequisite order, each with a demonstrable objective, a short lesson, a
  set of practice items with variants, and a checkpoint, all built from
  authoritative sources and leading to a capstone. Trigger after
  learning-goal intake, when the goal changes, or when the learner asks
  "what's the plan", "what will we cover", "build the course".
---

# Curriculum design

## Build the concept map first

1. List the concepts the objectives require, then the concepts *those*
   require, down to what the learner already knows (`learning-goal-intake`).
2. Order them so that every concept comes after its prerequisites
   (`_teacher` rule 3). Where several orders work, put the concepts the
   learner can **use** soonest first, because early working results keep
   motivation up.
3. Cut whatever does not serve an objective. Put it in an "optional later"
   list instead of the main path.

## Group into modules

Each module is one or two sessions of work and has:

- **Objective**: one demonstrable sentence ("can write a function that
  returns an error and handle it at the call site").
- **Lesson**: short, for the learner, written to the course folder. It
  has the key idea, one or two worked examples, the common mistakes, the
  false friends from the learner's background, and a "read more" link to the
  authoritative source.
- **Practice items**: from basic to applied. Each item has its expected
  answer, the **likely mistake** with why it is wrong, and a **variant**
  for re-testing (`_teacher` rule 8). Keep answer keys in the private
  location, not the course folder.
- **Checkpoint**: a small task that mixes this module with earlier ones.
  Passing it unaided closes the module.

The last module is the **capstone** agreed at intake.

## Sources and verification

Build lessons from the most authoritative source available (`source-of-truth`).
Prefer the subject's owner or official documentation over tutorials, and
cite them in the lesson. Every example, answer and number is **checked,
not recalled**. Run it, compute it, or look it up. Then read each module
through once before teaching it, checking that the answers are right, the
order holds, and no item depends on a later module.

If you can spawn agents, you may draft modules in parallel, one agent per
module. Give each a self-contained brief with the learner's background, the
module objective, its prerequisites and the format above. Check their output
before teaching from it.

## Show the plan

Show the learner the module list with objectives (no answers), and how
long it will roughly take at the agreed pace. Build modules a little ahead of
the learner (the next one or two), not all upfront. The plan will change as
you learn how they learn.
