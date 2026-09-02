---
name: solution-widening
description: >
  Open the solution space before the owner commits to an approach, then close it
  with a reasoned recommendation. Produces genuinely distinct options, the
  trade-off each one carries, what each forecloses, and one pick with its
  reasons. Trigger before any instruction is written for the team, and whenever
  the owner arrives with a solution already in mind: "we should do X", "tell the
  team to X", "what do we do about X", "is X the right approach", "I want a job
  that does X".
---

# Widening the solution

The owner arrives with an itch and, usually, with the first solution that came to
mind. That first solution is not wrong — it is unexamined. Your job is to open
the space around it, then close the space again with a recommendation. Widening
that ends in a menu has failed: the owner asked for help deciding, not for more
to decide.

**Do this before `work-item-authoring`, never after.** Once an instruction is
written the owner is committed, and reopening it costs a delivery.

## 0 — Recover the actual want

Separate three things the owner has fused into one sentence:

- **The itch** — what is going wrong, in observable terms.
- **The want** — the state of the world they are asking for.
- **The proposal** — the mechanism they had in mind.

Only the itch and the want constrain the answer. If you cannot state the itch
without naming the proposal, ask; you do not yet know what you are solving.

## 1 — Establish the ground truth

Widening on top of an assumption manufactures options that cannot exist. Before
generating anything, check the cheap facts: does the thing the owner believes is
broken actually behave that way; does the mechanism they proposed already exist
somewhere; who owns the system that would have to change. Verification rules 5–8
apply here, not only in review.

## 2 — Generate genuinely distinct options

Three to five. The test for distinctness is that they **fail differently** — two
options that break in the same way are one option with two spellings.

Always consider, explicitly, whether these belong on the list:

- **Do nothing**, and what it costs. Sometimes the honest answer.
- **The smallest thing that would tell us more** — when the disagreement is
  really about a fact nobody has checked.
- **Move the fix upstream**, to whoever owns the thing that produces the problem.
- **The owner's own proposal**, stated fairly. It is on the list like the others,
  and it may well win.

## 3 — Stress each option

For each, in one or two lines:

- What it costs, and who pays — which team, which system, whose time.
- How reversible it is. Cheap-and-reversible outranks elegant-and-permanent when
  the ground truth is thin.
- **What it forecloses.** The decision behind the decision, and the one the owner
  will not see coming.
- Where it would live — which repository, which job, whose scope. An option that
  lands outside the owner's scope is a request to someone else, and must be
  labelled as one.

## 4 — Recommend

Pick one. Say why it wins over the closest runner-up, and name the condition
under which you would change your mind. If the owner's original proposal loses,
say so directly and say what it was right about.

Where you genuinely cannot choose, say what fact would decide it and how to get
that fact — that is itself a recommendation, for option two above.

## 5 — Hand over

Once the owner picks, the chosen option goes to `work-item-authoring`. Carry
forward the two things the instruction will need and that only exist here: the
options that were **rejected and why**, and what the choice **forecloses**. Both
become the "does not do" list, and without them the team will helpfully rebuild
the option you discarded.
