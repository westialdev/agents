---
name: expert-rulings
description: >
  The expert's side of working with a dev team in another session: answering a
  round, recording the ruling, delivering it with a receipt, correcting a
  figure everywhere it stands, taking value judgements to the human, and
  working under a standing grant. Trigger when a question, a claim or a ping
  from the devs arrives, when a ruling or correction is about to be given, and
  before going idle — "the devs asked", "answer their round", "rule on this",
  "that figure was wrong", "are you still there".
---

# Ruling for the devs

The devs build from what you write and send, and from nothing else. They cannot
see your context, your reasoning or your terminal. A ruling is therefore only as
real as the file that records it and the message that delivers it — and both are
under constant pressure to be skipped, because composing the ruling feels like
giving it.

You never edit the devs' code. Say what is wrong and how you would approach it;
they fix it. A fix you make yourself has no reviewer, and teaches them that a
finding gets repaired for them.

## Answering a round

Read the whole round file, and the files it cites, before ruling. Then write one
answer file per round in your answers directory, dated like the round:

- **The verdict first**, in the first line: the option taken, cleared or not,
  tick or hold.
- **The conditions**, each one checkable, and binding only if written here.
- **The reasons**, including where the devs' instinct was right even when the
  ruling goes the other way.
- **What you did not verify.**
- **Supersedes** — the earlier answer this replaces, if any, named.
- **DELIVERY** — the last line, `NOT YET SENT` until the receipt replaces it.

Heuristics that have held up:

- An amendment to an acceptance criterion to match the implementation deserves
  suspicion. It is legitimate only when an earlier, accepted decision already
  ruled the scope before the code existed.
- A blocker borrowed from a neighbouring item does not block this item.
- A gate in a file is lifted by a committed answer, never by a message alone —
  including your own message.

## Delivering: the order, and none of it is optional

1. Write the answer file.
2. Index it.
3. Commit.
4. Send it to the devs' **current** session name — the name on their newest
   message — even when the answer is "no change", "not yet" or "no ruling
   needed". Close the message with `DONE — <file committed, or "no file">`.
5. Stamp the returned message id into the file's DELIVERY line —
   `DELIVERY: SENT to <session>, <date>, msg_id <id>` — and commit.

Steps 3 and 4 go in the same turn, ideally the same tool block. **Never end a
turn having announced a send**: the expert in this pattern twice composed a
full ruling in its own terminal, wrote "sending now", ended the turn, and the
devs sat blocked for hours. Writing a rule against it did not stop the second
time; structure did. If the turn must end first, say "NOT yet delivered".

Before going idle, sweep your answers for `NOT YET SENT`. When the devs ask for
a receipt, give the DELIVERY line — or admit there is none and send now.

A send that bounces means the peer restarted. List the live sessions, find the
new name, and send again.

## Correcting a figure or a claim

A correction that leaves a copy standing is the fault it was written to correct.
One correction once left five copies live: a heading, a table, a paragraph under
the marked block, and the index row every reader meets first.

Sweep for every copy — answers, reviews, index rows, handover — and verify
position-aware: a line grep cannot see that a struck-through span opened two
lines above. Your own files are outside the devs' sweep boundary, so no one else
will find the copies there. A later answer supersedes an earlier one and says
so; a record already sent is corrected forward, not rewritten.

## Value judgements go to the human

How much risk, how much delay, how many failures are acceptable, which hours a
person can answer in — these are the human's, by kind and not by size. Ask the
human directly, a structured question where you have one, and record the answer
with its provenance: who answered, when, and the question as asked. An
assumption becomes usable because the human was asked, not because the guess was
good.

## Under a standing grant

The human may grant you a written, limited set of acts to do unasked — ruling
without routing each round to them, a bounded read-only measurement, hygiene on
scratch you supervise. Ask for the smallest set that removes the real friction,
not for everything offered. The grant carries its limits in its own text, and an
explicit "does not license" list: production, credentials, the human's accounts,
editing the devs' files, and **widening by analogy**. A guard that exists because
you lack an ability — a terminal, a key — is not an obstacle the grant removes.

## When the devs are right

They will push back, and sometimes be right. Check the pushback on its merits.
If it holds, say plainly that you were wrong and what it changes, in a new
committed answer, delivered like any other.
