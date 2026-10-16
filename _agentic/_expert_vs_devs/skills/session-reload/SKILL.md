---
name: session-reload
description: >
  Bringing either session back after a restart: the reload prompt the human
  pastes, what the restarted session must read before acting, and the checks
  that catch what the restart dropped. Trigger when a session starts fresh on
  work already in progress, when the human is about to restart one, or when a
  message bounces — "restart the session", "reload", "where were we", "write me
  a restart prompt", a peer name that no longer answers.
---

# Reloading a session

Sessions get restarted, and a restarted session remembers nothing. The record
carries the state; memory never did. A reload is therefore a reading order plus
a handful of checks, and it is written so the human can paste it without
editing anything but the placeholders.

A restart also changes the session's name. The first thing a reloaded session
sends tells the peer its new name.

## Before the restart

If you are the session about to be restarted, commit what is in flight, send
anything written and not yet sent — or say in the record that it is NOT yet
delivered — and offer the human an up-to-date reload prompt.

## Reload prompt — the devs

```
You are the devs on <project>. You are resuming work in progress; you remember
nothing, and the record is the state.

1. Load devs-collaboration. Read <project instructions> and the acceptance list
   at <path>.
2. Read the expert's answers and reviews, newest first, down to the last one
   you have acted on: <answers dir>, <reviews dir>. Read the files, not only
   the index rows.
3. Read your own questions directory, newest first. For every question with no
   committed answer: it is still open.
4. `git log` since <sha or date>: what was committed, and which slice is
   claimed but not yet cleared. Do not tick anything the record does not show
   as cleared.
5. List the live sessions. Send the expert one message: you restarted, your
   new session name, and what you believe is outstanding. If a question is
   open, close the message with the REPLY REQUIRED block and start the ping.
6. The goal is: <paste the current /goal, or "ask the human for it">.
Then continue with <the next step>, or wait if you are blocked.
```

## Reload prompt — the expert

```
You are the expert on <project>. You are resuming; you remember nothing, and
the record is the state.

1. Load expert-rulings and slice-audit. Read your own instructions and any
   standing grant at <path> — its "does not license" list included.
2. Sweep your answers and reviews for DELIVERY lines reading NOT YET SENT.
   Each one is a ruling the devs do not have: send it, stamp it, commit.
3. Read the devs' questions directory newest first; any round with no
   committed answer is waiting on you.
4. `git log` since <sha or date>: any slice claimed and not yet audited is
   the next thing to audit.
5. List the live sessions. Reply to the devs' CURRENT name, and tell them
   yours.
Then continue with <the next step>.
```

## After the reload, before acting

- **A silence is not agreement.** If the peer has not replied, list the live
  sessions before assuming anything; it may have restarted too.
- **An empty listing is an answer about the instrument** until shown otherwise.
  If the answers directory reads empty, check you are looking where the record
  says answers go.
- **Do not trust a summary of the state**, including this prompt's. Where the
  prompt and the record disagree, the record wins; say so.
