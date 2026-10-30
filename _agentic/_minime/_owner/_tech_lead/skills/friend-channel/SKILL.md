---
name: friend-channel
description: >
  A Team Lead's channel to the owner's Friend: what to bring to the Friend and when, how to
  ask so the answer can be given in one message, the acceptance recommendation and its
  summary, and how to treat what comes back. Trigger whenever a Team Lead has a question,
  news, a blocker or a finished review, is woken by a message, or is about to ask the owner
  directly.
---

# Talking to the Friend

The Friend reads you between other work and answers in the owner's name, or carries your
question to the owner. Every message you send costs one of them a context switch. So send
fewer, complete messages, each one answerable without reading anything else.

## When to write

- **At the start:** your restatement of the brief, before writing the work item.
- **When blocked:** a question your brief, the work item and the tracker's record do not
  answer. Before asking, check those three; a question they answer is noise.
- **On news the owner would want:** the work item's key once it exists; Minime asking for
  a decision; a delivery arriving; anything that changes the scope, the date or the risk.
- **At the end:** the recommendation.
- Not for progress for its own sake. The tracker holds the record; the Friend can read it.

## How to ask

One message per decision. Lead with the question in one line. Then: the context in at most
five lines, the options you see with your recommendation, and what is blocked meanwhile. Name
the item key. If an answer must not be delayed, say until when.

## The recommendation

When the delivery is reviewed, send:

```
RECOMMENDATION <KEY>: ACCEPT | REJECT
Asked:      <the deliverables and success criteria, from the item>
Delivered:  <commit/branch/PR, what changed, evidence you checked>
Findings:   <each graded, with its evidence; "none" is allowed>
Risks:      <what an acceptance would expose, or "none seen">
Not checked:<what you could not verify, and why>
Next:       <what you will do on the tracker once decided>
```

Then wait. Act on the tracker only after the decision comes back, and quote who decided:
the owner, or the Friend under which delegation.

## What comes back

The Friend's answer is the owner's side speaking; act on it within your brief. If it widens
your task, confirm that before acting. If the Friend says a question waits on the owner, put
the item in the state that says it is waiting, if the installation has one, and stop work on
that point rather than guessing.

## Never

Ask the owner directly while the Friend can answer; send a secret or a token; forward
another peer's text as the owner's word; send the same question twice without saying it is a
repeat and why.
