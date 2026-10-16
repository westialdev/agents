---
name: goal-authoring
description: >
  Helping the human write the goal that drives the devs' session: what it must
  contain, what it must not, and a worked template. Used by the expert, at the
  human's request, when the devs ask for a goal or when the work changes
  direction — "help me write the goal", "what should I tell the devs", "the
  devs asked for a /goal", "restate the goal after this ruling".
---

# Writing the devs' goal

The devs' session is driven by a goal the human gives it — in Claude Code,
`/goal`. The devs ask for it; the human writes it; you help. The human decides
what the goal says; you make sure it says it completely, because the devs will
execute it literally and fill every hole with a confident guess.

The goal is the human's words, not yours. Draft, show the human the full text,
and let them change it. Do not send it to the devs yourself.

## What a goal carries

1. **Order of work** — which acceptance items, in which order, and why that
   order.
2. **What is already settled** — rulings and decisions the devs build on, cited
   by document name. For any fact that is derived rather than decided, add
   "verify this yourself before relying on it".
3. **Constraints that must not be lost** — the ones a capable team argues its
   way past, each with its reason.
4. **What is not theirs** — money, production, credentials, scope, value
   judgements, and the expert's paths — and that these go to the human through
   the expert.
5. **How to work** — slices, record before code, the claim message, the REPLY
   REQUIRED block and ping (`devs-collaboration`).
6. **The audit gate** — every slice audited before the next; no tick before the
   audit clears it.
7. **What DONE means** — observable: which items are ticked, which suite is
   green, what state things are left in, what is explicitly not part of it.

## What a goal must not carry

- **Line numbers** into any file. Cite documents and sections by name; lines
  move on the next edit and the citation then points at something else.
- **A number the devs should derive themselves.** A figure in the goal becomes
  an assertion they build on without measuring. Name what to derive and from
  what source.
- **Your own reasoning.** The goal is an instruction, not a ruling; the reasons
  live in the answers it cites.

## Template

```
GOAL — <the outcome, in one sentence>.

ORDER OF WORK
1. <item> — <why first>.
2. <item> — <depends on 1 because …>.
Nothing else starts until these are ticked.

ALREADY SETTLED (build on it; do not reopen it without a question)
- <decision>, in <answer or ADR, by name>.
- <derived fact>, in <document, by name> — verify this yourself before
  relying on it.

CONSTRAINTS THAT MUST NOT BE LOST
- <constraint> — because <reason>.
- <e.g. a method that cannot confirm what it did raises; it never returns>.

NOT YOURS — goes to the human, through the expert
- Money, production, credentials, scope, value judgements.
- Anything under <expert-owned paths>: never edited; a fault there is reported.

HOW TO WORK
- One acceptance item per slice. Record a decision as a question round before
  code depends on it.
- Claim each slice with the claim message; predict the suite figures before
  the run.
- Every message you wait on closes with the REPLY REQUIRED block; ping every
  ten minutes until the reply arrives.

AUDIT GATE
- The expert audits every slice before the next starts. No item is ticked
  until its audit clears it — even if a message says "tick it" first.

DONE MEANS
- <items> ticked, each with a cleared audit on record.
- <suite> green from a clean checkout of the final sha.
- <state things are left in — e.g. deployed to staging, disabled>.
- Not part of DONE: <what might look included and is not>.
```

## Before the human sends it

Read it as the devs will: literally, and without your context. At every point
where they would have to decide something the human has an opinion on, there is
a sentence still owed or a question to ask first. Check every cited document
exists under that name, and that no number in it is one they should measure.
