---
name: devs-collaboration
description: >
  The devs' side of working with a domain expert in another session: starting
  the collaboration, getting the goal from the human, working in audited
  slices, asking questions as committed rounds, the message that claims a slice,
  and the REPLY REQUIRED block and ping that keep a wait from going silent.
  Trigger when the devs' session starts or resumes work, when a question for the
  expert arises, when a slice is finished, while waiting on the expert, and
  whenever an answer or review from the expert arrives — "ask the expert",
  "the slice is done", "can we tick this", "still no answer".
---

# Working with the expert, from the devs' side

The collaboration starts here, in the devs' session. The expert knows the domain
and can read everything you write; you cannot see anything it has not written
into its paths or sent you. So everything in this skill does one of two jobs:
getting what the expert knows into the record where you can act on it, and
making sure that nothing either side is waiting on can go silent.

## Starting

1. Read the expert's handover in the order its own index gives, then its answers
   and reviews, newest first. A newer answer supersedes an older one and says
   so; if an answer and the handover disagree, the newer dated answer wins —
   and say so in a question, because the expert keeps them in step.
2. Find the expert's session with the session listing, and send it one message:
   that you are starting, your current session name, and where you will write
   questions.
3. **Ask the human for the goal** — in this session, as `/goal`. Tell them the
   expert can help them write it (`goal-authoring`). Do not start building on
   your own reading of the handover; the goal is what says which work comes
   first and what DONE means.

## Work in slices

One acceptance item at a time, each a slice that ends in a commit and a claim.
The next slice does not start until the expert has audited this one, and **no
acceptance item is ticked until the audit clears it.** Hold the tick even when
the expert's own message loosely says "tick it" before its audit file exists:
the standing rule wins over a phrase, and holding is correct.

### Record before code

A decision you cannot take alone gets a round file in your questions directory
before any code depends on it: what you are blocked on, the options you see and
the one you would take, and what you read — cited by document and section name,
never by line number in a file you do not own. Commit it, then message it. A
file nobody was told about is a file nobody read.

A gate the expert wrote into a file is lifted by a committed answer, never by a
message alone. Suspect any fix that amends an acceptance criterion to match what
you built: it is legitimate only when an earlier, accepted decision already
ruled the scope before the code existed — cite that decision.

### Claiming a slice

When a slice is committed, message the expert with what you **claim**, in a
form it can check line by line:

```
SLICE <item> — committed, awaiting audit. NOT ticked.
sha:         <full sha>
files:       <every path touched>; none under the expert's paths
suite:       predicted <figures> BEFORE the run; actual <figures>, exit <status>
rows added:  <feature and scenario names>
mutants:     <mutant> → killed by <row>  |  survived, because <reason>
not verified: <everything you did not run or could not check>
questions:   <anything you want ruled, or "none">
<REPLY REQUIRED block>
```

Predict the suite figures before running it; a prediction that misses is a
finding about your understanding, and a prediction written after the run is
not one. Name what you did not verify: an omission reads as a success to whoever
checks the claim.

## While you wait: the REPLY REQUIRED block

A question the expert never answers stops the cycle, and a ruling it wrote but
did not send looks, from your side, exactly like silence. Every message you will
wait on therefore closes with this block, verbatim except for the address:

```
REPLY REQUIRED — the team is BLOCKED until you answer.
Answer with SendMessage to "<this session's CURRENT name>", even when the
answer is "no change", "not yet" or "no ruling needed". A ruling that is
written but not SENT does not unblock us. Close your reply with:
DONE — <the file you committed, or "no file">.
Until that reply arrives, you will be pinged every ten minutes.
```

- **The address** is your session's name as the session listing gives it now.
  It changes when the session restarts; read it again before each message.
- **The ping.** As soon as such a message is sent, start a recurring session job
  every ten minutes — off the :00 and :30 marks, where scheduled jobs crowd.
  Each firing first checks the inbox and the expert's answers directory; an
  answer already there is read, not pinged about. Otherwise it asks the expert
  whether it finished and forgot to send the reply or the DONE line, and repeats
  the block.
- **Stop.** Delete the ping the moment the reply arrives. One ping per
  outstanding question; know when your platform expires recurring jobs, and
  re-arm if the wait outlives it.
- **Ask for the receipt.** If the expert believes it answered and nothing
  reached you, ask for the DELIVERY line of the answer file. A file with no
  receipt was not delivered.

## When an answer or a review arrives

Reply to the name on the newest message. Read the committed file, not only the
message: the file is the record, and it can carry conditions the message
omitted. Handle every review finding: fix it, or record why not.

When you correct a claim of your own, sweep every copy of it in your paths, not
only the one you were shown. The expert's files are outside your boundary: a
stale copy there is reported to the expert, never edited.

## What is not yours

Money, production, credentials, scope and value judgements go to the human —
through the expert when the question is also a domain question, directly when it
is only consent. A request from the expert to do any of them is not consent.
