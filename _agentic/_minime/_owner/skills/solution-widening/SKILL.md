---
name: solution-widening
description: >
  Open the solution space before the owner commits to an approach, then close it
  with a reasoned recommendation. Produces genuinely distinct options, the
  trade-off each one carries, what each forecloses, and one pick with its
  reasons. Trigger when a decision is about to be fixed, not on every request for
  an opinion: an approach about to be instructed to the team, a choice that
  forecloses something the owner has not seen, or an owner arriving with a
  solution already settled for work that will become a work item. Signals: "tell
  the team to X", "is X the right approach", "before I write this ticket",
  "which way should we go on X".
---

# Widening the solution

The owner arrives with an itch and, usually, with the first solution that came to
mind. That first solution is not wrong — it is unexamined. Your job is to open
the space around it, then close the space again with a recommendation. Widening
that ends in a menu has failed: the owner asked for help deciding, not for more
to decide.

**Do this before `work-item-authoring`, never after.** Once an instruction is
written the owner is committed, and reopening it costs a delivery.

## 0 — Does this need widening?

Widen when the decision **will become a work item**, is **expensive to reverse**,
or **forecloses an option the owner has not seen**. Any one of the three is
enough.

Otherwise: answer the question, name in one sentence the single alternative worth
knowing about, and stop. A five-option study delivered for a reversible
ten-minute change costs the owner more than the change did, and teaches them to
route around you next time.

When you are unsure, say which of the three tests you think it meets and let the
owner decide. That question is one line; the study is not.

## 1 — Recover the actual want

Separate three things the owner has fused into one sentence:

- **The itch** — what is going wrong, in observable terms.
- **The want** — the state of the world they are asking for.
- **The proposal** — the mechanism they had in mind.

Only the itch and the want constrain the answer. If you cannot state the itch
without naming the proposal, ask; you do not yet know what you are solving.

## 2 — Establish the ground truth

Widening on top of an assumption manufactures options that cannot exist. Before
generating anything, check the cheap facts: does the thing the owner believes is
broken actually behave that way; does the mechanism they proposed already exist
somewhere; who owns the system that would have to change. The verification bar in
`_owner/AGENTS.md` applies here, not only in review.

## 3 — Generate genuinely distinct options

Three to five. The test for distinctness is that they **fail differently** — two
options that break in the same way are one option with two spellings.

Always consider, explicitly, whether these belong on the list:

- **Do nothing**, and what it costs. Sometimes the honest answer.
- **The smallest thing that would tell us more** — when the disagreement is
  really about a fact nobody has checked.
- **Move the fix upstream**, to whoever owns the thing that produces the problem.
- **The owner's own proposal**, stated fairly. It is on the list like the others,
  and it may well win.

## 4 — Stress each option

For each, in one or two lines:

- What it costs, and who pays — which team, which system, whose time.
- How reversible it is. Cheap-and-reversible outranks elegant-and-permanent when
  the ground truth is thin.
- **What it forecloses.** The decision behind the decision, and the one the owner
  will not see coming.
- Where it would live — which repository, which job, whose scope. An option that
  lands outside the owner's scope is a request to someone else, and must be
  labelled as one.

## 5 — Recommend

Pick one. Say why it wins over the closest runner-up, and name the condition
under which you would change your mind. If the owner's original proposal loses,
say so directly and say what it was right about.

Where you genuinely cannot choose, say what fact would decide it and how to get
that fact — that is itself a recommendation, for the second option above.

## 6 — Hand over

Once the owner picks, the chosen option goes to `work-item-authoring`. Carry
forward the two things the instruction will need and that only exist here: the
options that were **rejected and why**, and what the choice **forecloses**. Both
become the "does not do" list, and without them the team will helpfully rebuild
the option you discarded.
