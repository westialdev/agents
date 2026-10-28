---
name: where-i-am
description: >
  Keep the human's work-in-progress file (default WHEREIAM.md, alias "WIA"), the single
  source of truth for where the human really is. It holds two records: the human's notes on
  what they are doing now or must do first thing next time, each with the agent's link to
  the context it came from, and the board of work threads, the parallel forks of the work in
  progress (agents coding, thinking, waiting for approval, an organisational task). Trigger
  when the human mentions a note in WHEREIAM.md or "the WIA", says "where was I", "where did
  I leave it", "I'm leaving for today", "note where I am", "what are we working on", "open a
  thread", "fork this", "close that thread", switches from one line of work to another, or
  comes back after a gap.
---

# Where I am: the human's work in progress

The human keeps several lines of work open at once. While agents code one feature, the human
thinks about another, a third waits for an approval and a fourth is an organisational task.
The human also steps away: the end of the day, sleep, another project. The WIA lets them see
at a glance where every line of work stands, and step back into any of them without
scrolling back through yesterday.

**The WIA holds what is live, not what is parked.** Ideas and suggestions that can wait
belong in the backlog (skill `parked-ideas`, default `TODO.md`). A note or a thread that
stops being live has outgrown the WIA.

## Who writes the file

**You, the agent that owns this directory, are the only writer of its WIA.** No other agent
writes it. The human tells you what to record, and you record it in the form below.

WIA or backlog files in nested directories belong to the agents working there. You may read
them to learn what those agents are doing. Never write them.

## The two records

The file holds two sections, in this order. Each has its own format and meaning. Never mix
them: a note is never a thread, and a thread never replaces a note.

```markdown
# Where I am

## Notes
<the human's resume points, newest first>

## Threads
<the board of work threads, newest first>
```

### Notes: the human's resume points

A note is the human's own sentence: what they are in the middle of, or what to do first
thing next time. **Write it in the human's words.** Never rewrite, reorder or merge it, and
never write a note of your own.

Add a `→` link beneath a note when it came out of shared work: the context it was created
from, so it reloads the human's head fast.

```markdown
**finish the retry test, the timeout case is still red**

> **→** `tests/features/retry.feature`, scenario "a call that times out twice"; red since the
> backoff change in `a1b2c3d`. Next step: the double still answers instantly, so it never times
> out. Make it wait past the deadline. Thread: T-003.
```

A good link is brief, because this is a resume point and not a report:
- **where**: the file, the record, the branch, the command, the line;
- **the state** when the note was left: what was green, red, running or waiting;
- **the next step**, if the work made it clear;
- **the thread** it belongs to, if any.

When a note needs no context beyond its own words, leave it bare.

### Threads: the forks of the work in progress

A thread is one line of work running in parallel with the others: a fork or a sub-item of
the work in progress. The board is a reference, not a monitor. It lets the human ask "what
are we working on?" and get a straight answer. It is not kept live: each entry records the
state **as last known, with its date**.

```markdown
### T-003 · Retry backoff for the webhook client
- **Kind:** coding (agents)
- **State:** needs you, as of 2026-10-28: the agent's plan is waiting for approval
- **Where:** repo `webhooks`, branch `feat/retry-backoff`, worktree `../webhooks-retry`
- **Fork of:** T-001
- **Next:** read the plan and approve or redirect it
```

- **ID** `T-NNN`, never reused. A short title in plain words.
- **Kind**: one of coding (agents), coding (human), thinking, waiting for approval,
  organisational, research, or another word that fits better.
- **State**, with its date: *running* (someone else is working on it), *needs you* (it
  waits on the human), *waiting on others* (a person or a system outside), *paused* (nobody
  is on it, but it is still live).
- **Where** it lives: repo, branch, worktree, session name, ticket, document, person. Enough
  to find it again; omit what does not apply.
- **Fork of**: the thread or note it came from, if any.
- **Next**: the next step, if known.

**When to write a thread:**
- **Open** one when the human starts or forks a line of work ("launch agents on X", "I'll
  think about Y", "this waits for Z's approval"), or asks you to.
- **Update** it when the human reports a change, or when you see one yourself in shared
  work. Re-date the state each time. Write only what the human said or what you saw; mark
  anything else *unverified*.
- **Close** it when the human says it is done or dropped: strike the title through, date it
  and add a one-line result with where the result lives. Leave it on the board until the
  human has seen it, then move it to the archive (below).
- **Move it to the backlog** when it stops being live without being finished: a line in
  `TODO.md` that names the thread, and the thread closed with "parked".

## What the agent never does

- Never writes a note of its own, or changes the human's wording.
- Never clears a note on its own. When a note's work is done, or it has stopped being
  immediate, **offer** to clear it or to move it to the backlog. The human decides.
- Never starts, stops or steers a thread because the board says so. The board records; the
  human decides what runs.

## Asked "what are we working on?" or "where was I?"

1. Show the threads that are not closed, those that *need you* first, then the notes,
   newest first.
2. **Check every entry against the current state before relying on it.** It describes the
   moment it was written. Check what can be checked cheaply (a branch that moved, a run that
   finished, a ticket that changed) and say what has changed. Say which entries you could
   not check.
3. Pick up the thread or note the human chooses. The order is theirs.

## Archive

When the file grows unwieldy, move closed threads and cleared notes to a dated archive file
(default `WHEREIAM.archive.md`, newest at the top) and link it from the top of the WIA.
Never delete them.
