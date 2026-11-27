---
name: devs-roster
description: >
  The expert's coordination of several devs sessions at once: the committed roster of who owns
  which paths and what each is doing, contracts first, routing a request from one devs session
  to the owner of the paths it needs, the order of answering, and when to ask the human for a
  second expert. Trigger when the expert starts or resumes with many devs, when a devs session
  starts, restarts, asks for a change outside its paths or needs a dependency, when two
  sessions want the same thing, and before going idle — "who owns this", "devs B needs a field
  in the shared model", "two sessions built the same helper", "who is waiting on me".
---

# Keeping the roster

With one devs session, everything that crosses between expert and devs is one conversation.
With several, it is several conversations that share code, and the failures come from the
seams: two sessions writing the same helper, one changing an interface another builds on, a
question answered for one session and never sent to the second that needed it, a session that
waits an hour because the expert was busy with another. The roster exists to make each of
those visible before it costs a merge.

## The roster file

Keep one committed file in the expert's own paths. One row per devs session:

| Field | What |
|---|---|
| role | the name the plan gives it (e.g. "shared", "module B") |
| session | its **current** session name, from its newest message |
| repository, clone | where it works; one clone per session, never a shared tree |
| owns | its paths, exactly; every product path appears in exactly one row |
| items | its acceptance items, in order |
| now | the slice in progress, with its sha once claimed |
| waiting on | the expert's open answers or audits for it, each with the time it started waiting |

Update it at every claim, ruling, tick and restart, and commit with the ruling that changed
it. Read it at the start of every turn that has more than one message waiting.

## Starting

1. Before any devs session starts, check the roster against the product: no path in two rows,
   no product path in none. A gap or an overlap is a question for the human, not a choice.
2. The shared-code owner starts first. Its first slice is the contracts the others need and
   the architecture tests that keep the modules apart (for example, import contracts run as
   ordinary tests). Everyone else may start at once **against fakes** of the agreed
   interfaces, and says so in its claims.
3. Send each devs session its roster row and the list of contracts it consumes, with their
   owners. That is the only way it learns the boundaries.

## Requests across sessions

A devs session that needs something outside its paths — a field in a shared model, a
dependency, a helper, a fix in another module — writes a round file and messages you. Never
let it make the change itself, and never make it yourself.

1. Rule on the request: is it needed, is it shared or does it belong in the asker's module,
   does it change a contract.
2. If it changes another session's paths, write the request as a ruling to the **owner**, and
   deliver it there (`expert-rulings`).
3. If it changes a contract, send the ruling to **every** session that consumes it, in the
   same turn, and record which sessions received it in the DELIVERY line.
4. Answer the asker too: what was ruled, who builds it, and what to do meanwhile (a fake, a
   different slice, wait).

When two sessions ask for the same thing, it is shared: one ruling, one owner, both told.

## The order of answering

When several messages wait, answer in this order: a session that is blocked, then a claimed
slice (dispatch its audit at once; see `delegated-audit`), then questions that change a
contract, then everything else. Dispatching an audit or a research question is quick; do it
before writing any long ruling, so that the subagents work while you write.

Never let one session's long ruling hold another's one-line answer.

## When one expert is not enough

The roster's "waiting on" column is the measure. When a session waits longer than the split
trigger set at provisioning, tell the human, in the terminal and with the figures: who waited,
how long, on what. Propose which sessions would move to a second expert — usually the riskiest
or the most self-contained part — and do not start one yourself. Spawning a second expert is
the human's decision.

## Before going idle

Sweep the roster: every "waiting on" entry has a delivered answer or a running subagent, every
answer file has its DELIVERY receipt, every session name is current. A session nobody is
answering is the failure this skill exists for.
