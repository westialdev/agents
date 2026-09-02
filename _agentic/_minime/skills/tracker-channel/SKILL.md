---
name: tracker-channel
description: >
  Working through the tracker as the team's only channel: what belongs on the
  work item, what a state change means to the agent that reads it, writing for
  the human and the literal reader at once, never rewriting an entry to carry new
  information, and confirming an entry landed. Trigger whenever something is
  about to be written to a work item or its state changed — posting a comment or
  a plan, answering a question, moving an item, or reading an item to find out
  where the work stands.
---

# The tracker is the channel

A Minime team has one channel, and it is the work item. Every instruction,
question, answer, plan, delivery and decision goes there. Nothing meaningful
happens in a chat window, and what is not written on the item did not happen —
whoever remembers it, and however recently.

This is not bureaucracy. The team is a set of processes that wake up, read the
item, act, and forget; the item is their shared memory. A fact that lives only in
a session is a fact the next agent will not have.

## What belongs on the item

Everything the next reader must act on, in full, on the item itself. Do not carry
meaning in a side channel, an attachment nobody will open, or a reference to a
conversation that is not on the record.

Log the joints as they happen: decisions, delegations, state transitions and
errors, with enough context to reconstruct them later. This is how anyone answers
"who is doing what" — including you, at your next wake-up, with no memory of the
last one.

## A state change is a signal

Moving an item is how another agent learns there is something to do. It is
addressed to a reader, not to a filing system.

So move an item when its meaning changes — needs work, needs an answer, needs a
decision, accepted — and never as tidying up. And take the meanings from the
installation you were provisioned with rather than from a state's name, which is
frequently a poor description of what the team does when it sees it.

Two failures are worth naming because both are quiet: an item left in a working
state while it waits on a person, which stalls until somebody happens to look;
and an item left in a waiting state after the answer arrived, which stalls in
exactly the same way while looking correct.

## Write for two readers at once

Every entry is read by a human who must decide and by an agent that will act on
it literally. Put the decision the human needs at the top, and the specifics the
agent needs, in full, below it.

Write the specifics so they cannot be interpreted two ways. The literal reader
will not notice the ambiguity, will resolve it, and will not tell you which way
it went.

## Never rewrite an entry to carry new information

A revised entry reaches nobody who has already read it — and the reader you most
need is the one who read it first. Add a new entry instead.

This holds for the agents as much as for the people: an executor that read the
original has, from its side, nothing new to do, and will happily report the work
complete against the version it saw.

## Confirm it landed

A tool that returns success has told you it accepted the call. Read the entry
back and check it is what you sent, in the form you sent it. Trackers that accept
a structured payload they cannot parse are common, and they do it without an
error — see `tracker-conduct` for the shape that failure takes and how to repair
it.
