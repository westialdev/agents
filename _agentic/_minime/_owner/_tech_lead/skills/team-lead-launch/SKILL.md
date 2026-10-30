---
name: team-lead-launch
description: >
  The Friend starting a Team Lead for one task: deciding the task is ready, writing the
  brief, launching the Team Lead with the installation's launcher, and recording it as a
  thread. Also stopping one. Trigger when the owner says "start a Team Lead", "give this
  ticket to a Team Lead", "delegate this", or when a task he assigned needs one, and when a
  Team Lead's task is closed.
---

# Starting a Team Lead

A Team Lead knows only its brief, the item and what it can read. Whatever the owner meant and
did not say, the brief must carry, or the Team Lead will ask, or worse, will guess.

## 1 — Is it ready?

Start a Team Lead only when the owner asked for one, for a task he named. Check you know:
the outcome he wants, the repository, the deadline if any, and what is out of scope. If one
is missing, ask the owner first. Starting a Team Lead is cheap; un-starting a work item
written in his name is not.

## 2 — The brief

Write it in the owner's voice, short, in this order:

- **Task:** the key (or "new item") and one line of outcome.
- **Why:** the reason, so the Team Lead can judge trade-offs.
- **Scope:** what is in, what is explicitly out.
- **Repository and environment:** which repo; what the runtime can and cannot reach (no
  production, no deploys).
- **Decisions already taken** by the owner, verbatim where it matters.
- **Delegations:** which questions the Friend may answer alone (cite the standing answers),
  and whether the **acceptance** is delegated to the Friend for this task. Default: not.
- **Contact:** "Questions and the recommendation go to `friend` first."
- **Done when:** the success criteria the review will judge.

Show the brief to the owner before launching unless a standing answer lets you launch alone.

## 3 — Launch

Use the installation's launcher (for example `tl-start <repo> <KEY> < brief`). Check it
reported the peer address and the session, and that the Team Lead's first message, its
restatement of the brief, arrives. A launch is done when that message is read, not when the
command returned.

## 4 — Record it

Open a thread on the owner's WIA for the Team Lead: the task key, the peer address, where it
runs (container, tmux session), the delegations, and the next expected event.

## Stopping

When the item is closed and the Team Lead says it is done, stop its session with the
installation's command, keep its record, and close the thread with the outcome.
