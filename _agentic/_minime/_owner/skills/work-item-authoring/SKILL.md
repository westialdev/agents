---
name: work-item-authoring
description: >
  Turn the owner's decided intent into a work item the team can execute without
  guessing: context, the change itself, deliverables with their target paths,
  explicit exclusions, success criteria, and the invariants that must survive.
  Trigger when the owner is ready to instruct the team: "write the ticket",
  "tell the team to…", "ask them to fix…", "add this to the task", "post the
  plan", or after `solution-widening` has settled on an approach.
---

# Authoring the work item

An agentic team executes what is written, faithfully and fast. That is the
benefit and the whole risk: an instruction with a hole in it does not produce a
question, it produces a confident delivery built around the hole. Your job is to
leave no hole worth filling by guesswork.

Write for two readers at once — the human who may need to judge this later, and
the agent that will act on it literally.

## The five parts

Every item carries these. Short is fine; missing is not.

### 1 — Why

The context that makes the change make sense: what is going wrong, what was
already tried, what the owner decided and what they rejected. An executor that
understands the intent recovers from an ambiguity; one that does not, invents.

### 2 — Deliverables, with their target paths

Every file, component, module, configuration and repository the work must
produce or change, **each named with the exact path it lands at**, grouped by
repository. "Add a health check" is a wish. `test/healthcheck/run.sh`, new, in
this repository, is a deliverable.

### 3 — What it must not do

The exclusions, each with its reason: the options rejected in widening, the
files and systems that may not be touched, the helpful-looking action that is
out of scope. Carry the reason, not just the prohibition — an unexplained "do
not" is the first thing a capable executor argues its way past.

This is the part owners skip and the part that saves the delivery.

### 4 — How it will be judged

The success criteria, in observable terms: what someone runs, sees, or checks to
know it is done. Each criterion must map to a deliverable in part 2. A criterion
with no deliverable is a gap you have handed to the executor; a deliverable with
no criterion is work nobody will verify.

### 5 — What must stay true

The invariants — the properties the change must not break, especially the ones
that make it dangerous. Each needs a **mechanism**, not an intention: a guard, a
check, an ordering, a test. "Be careful not to destroy the database" is not a
mechanism. "The destroy path is absent from the file, not merely disabled" is.

## Stop at the change

Give the context, the change, and the traps that affect **how to write it
correctly** — escaping hazards, ordering constraints, a gap the implementer must
fill from the current source. Then stop.

Leave out merge instructions, deployment steps, "run it and confirm X", and
end-to-end test procedures. Those are checks on the executor's own process, they
are disciplined about it, and dictating them wastes the item's attention budget
on the part nobody needed. (Rule 11.)

## One item, one intent

If the owner's request contains two changes that could ship separately, say so
and let them decide. Coupled workstreams in one item make the delivery all-or-
nothing and the review impossible to grade.

## Before you post

Re-read the item as the executor: is there any point at which you would have to
decide something the owner has an opinion about? That point is either a sentence
you still owe, or a question to ask before starting.

Then hand to `tracker-conduct` to post it — including when you are adding to an
item that already exists, which is never an edit.
