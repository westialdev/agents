---
name: where-i-am
description: >
  Keep the human's work-in-progress file (default WHEREIAM.md, alias "WIA"): short notes on
  what the human is doing right now or must do next, left at the end of a day or before a gap
  so they can step straight back in. The agent links each note to the context it came from,
  when there is any. Trigger when the human writes or mentions a note in WHEREIAM.md or "the
  WIA", says "where was I", "where did I leave it", "I'm leaving for today", "note where I
  am", or comes back after a gap.
---

# Where I am: the human's work in progress

When the human leaves the office, goes to sleep or switches to another project, the thread of
what they were doing is easy to lose. Before going, they leave a note in the WIA. The next day
they open it and see where they left the work, without scrolling back through yesterday.

**The WIA holds what is live, not what is parked:**
- work the human is in the middle of;
- things to do first thing next time, which are immediate rather than long-term.

Ideas and suggestions that can wait belong in the backlog (skill `parked-ideas`, default
`TODO.md`). A WIA note that stops being immediate has outgrown the WIA.

## Who writes what

**The human writes the note.** It is short, in the human's own words, and often the only
context it needs is what it says.

**The agent adds a `→` link beneath it when the note came out of shared work**: the context it
was created from, so it reloads the human's head fast.

```markdown
**finish the retry test, the timeout case is still red**

> **→** `tests/features/retry.feature`, scenario "a call that times out twice"; red since the
> backoff change in `a1b2c3d`. Next step: the double still answers instantly, so it never times
> out. Make it wait past the deadline.
```

A good link is brief, because this is a resume point and not a report:
- **where**: the file, the record, the branch, the command, the line;
- **the state** when the note was left: what was green, red, running or waiting;
- **the next step**, if the work made it clear.

When a note needs no context beyond its own words, leave it bare. Source every fact in a link:
a wrong resume point sends the human the wrong way first thing in the morning.

## What the agent never does

- Never writes a note of its own. The agent's suggestions go to the backlog.
- Never rewrites, reorders or merges the human's sentence.
- Never clears a note on its own. When a note's work is done, or it has stopped being
  immediate, **offer** to clear it, or to move it to the backlog. The human decides.

## On return

1. Show the notes, newest first.
2. **Check every link against the current state before relying on it.** It describes the
   moment the note was left. Say what has changed since: a test that went green, a run that
   finished, a branch that moved.
3. Pick up the note the human chooses. The order is theirs.
