# _continuity

**Choose this use case when** the agent being created works with one human over a **long
collaboration that is interrupted** (end of the day, sleep, trips, other projects), and the
human must be able to step back in quickly. Recognition signals: "where was I", "I'm leaving
for today", "note where I am", "park this for later", "keep a TODO", "don't run it, just note
it", "WHEREIAM", "WIA", "pick up where we left off".

This use case is orthogonal to what the agent produces. Combine it with any other branch: a
developer, a researcher or a tutor can each take `_continuity` as well.

## What it provides

- `AGENTS.md`: the always-on posture. A suggestion is parked rather than run, a pause is met
  with an offer to update the files, and what was written before a gap is checked before it is
  trusted.
- Skills:
  - `where-i-am`: the human's work-in-progress file (default `WHEREIAM.md`, alias "WIA"). It
    holds short notes on what is in progress or must happen first thing next time. The human
    writes them; the agent links each to the context it came from, when there is any.
  - `parked-ideas`: the backlog (default `TODO.md`). It holds what can wait: the human's
    parked ideas and everything the agent or its team suggests, with the decisions that are
    the human's alone at its foot.

## How the two fit together

**The WIA is now; the backlog is later.** A WIA note is immediate and short-lived. A parked
idea waits until it is called. Work moves between them: a parked item that becomes the next
thing to do goes to the WIA, and a WIA note that stops being immediate goes to the backlog.
Only the human moves a note out of the WIA.

The agent never writes its own notes in the WIA. Everything it authors goes in the backlog.

## Provisioning requirements

- **File names and location.** Default: `WHEREIAM.md` and `TODO.md` at the project root.
  Offer the defaults; the human may rename or move them.
