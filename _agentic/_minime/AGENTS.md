_minime use case rules
======================

These rules apply to every agent provisioned with the `_minime` use case, in
addition to the parent `_agentic` rules. They cover working with a **Minime
agentic team**: a development team that takes work items from a tracker, plans
them, delegates the work to short-lived specialists, and hands the result to a
human owner for approval.

## Read the installation before assuming it

1. A Minime team is an installation, not a fixed product. Before acting, read
   what that installation documents about itself — its roles, its states, its
   conventions — and prefer it over anything you assume, including this file.
2. **Never hardcode another team's behavior.** State names, role names, comment
   markers and timings belong to the installation and change. Refer to them by
   what they mean, discover their current form at run time, and if you cannot
   discover it, ask rather than guess.
3. The team's own record is the truth about the team. When the documentation and
   the tracker disagree, believe the tracker and say that you found the
   discrepancy.

## The tracker is the channel

4. Everything that matters is written on the work item: instructions, questions,
   answers, plans, deliveries, decisions. Do not carry meaning in a side channel
   that the next reader — human or agent — will not see.
5. **A state change is a signal to another agent**, not bookkeeping. Moving an
   item is how the team learns there is something to do, so move it when the
   meaning changes and never as a tidy-up.
6. Write for two readers at once: the human who must decide, and the agent that
   must act. Put the decision the human needs at the top and the specifics the
   agent needs in full below.
7. **Never rewrite an existing entry to carry new information.** Add a new one.
   A revised entry reaches nobody who has already read it, and the reader you
   most need is the one who read it first.

## Plan before work

8. Nothing is built until the intent has been stated in writing and is available
   to the owner. This is what makes a misaligned plan cheap to catch, and it is
   the step under pressure to be skipped.
9. Verify the plan against the request itself, item by item. A deliverable with
   no place in the plan, a criterion nothing satisfies, or an excluded action
   present in the plan is a question to ask — never a silence to keep.
