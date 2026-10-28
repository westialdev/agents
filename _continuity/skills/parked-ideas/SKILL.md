---
name: parked-ideas
description: >
  Keep the human's post-it file (default WHEREIAM.md, alias "WIA"): the human parks an idea
  or something pending in one sentence, and the agent links it to the context it refers to,
  so the note still reloads the human's head weeks later. Trigger when the human writes or
  mentions a note in WHEREIAM.md or "the WIA", says "park this", "note this for later",
  "I'm pausing / going to sleep / travelling", "where was I", or comes back after a gap.
---

# Parked ideas — the human's post-its

During a live collaboration the human's head fills with ideas that grow out of the work on the
table. A pause (sleep, a trip, another project) loses them. So the human parks each one as a
single sentence in the post-it file (WHEREIAM, "WIA" for short), whenever they need to: at a
pause, mid-session, any time.

**The design is a division of labour. The human's sentence is the anchor; the agent's link is
the reload.** The human writes only the idea. The agent supplies what makes it readable weeks
later.

## What the agent writes: one `→` link per note, and nothing else

Beneath each new sentence, add one quoted block that starts with `→`:

```markdown
**try the same filter on the morning session**

> **→** Context: the evening filter kept 31 of 412 names on 2026-10-27
> (`doc/studies/2026-10-27-filter.md`). Connects to the open question on fill size. Acting on
> it takes one rerun of the study with the session switched, about an hour.
```

A good link carries:
- **the numbers that were on the table** when the idea was born, with their source;
- **what it connects to**: the files, records, decisions or other notes;
- **what acting on it would take**: the cost, the first step, and anything it waits on.

Source every fact you put in a link. A link that misstates the context is worse than none,
because the human will trust it on return.

## What the agent never does

- Never writes a note of its own, or suggests one into this file. Agent suggestions belong in
  the backlog (skill `suggestion-backlog`).
- Never rewrites, reorders, merges or deletes the human's sentence. It is the anchor.
- Never adds sections, decisions, state or queues here.
- Never clears a note. Only the human clears one. Before the human clears a note, check that
  any substance existing only in its link has a home elsewhere, and offer to move it.

## The pause-state block: only on request, deleted on return

If the human asks for one, write a dated **STATE AT PAUSE** block at the top: what is running,
what each live process will do during the gap, and where everything is committed.

**Delete it the moment the human returns,** after checking that its substance lives elsewhere.
It is the first thing read on return and the last thing verified, so a stale one is the most
dangerous text in the project. It can describe a failure that never happened, and send the
human into a recovery that is not needed.

## On return

1. Read the file top to bottom with the human.
2. Verify every link against the live state, and say which facts changed.
3. Delete the pause-state block, if one exists.
4. Pick up the note the human chooses. The order is the human's.
