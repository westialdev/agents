# _continuity

**Choose this use case when** the agent being created works with one human over a **long
collaboration that is interrupted** (end of the day, sleep, trips, other projects) or **split
into parallel threads of work** (agents coding one thing while the human thinks about another,
waits for an approval, or handles an organisational task), and the human must be able to step
back into any of them quickly. Recognition signals: "where was I", "I'm leaving for today",
"note where I am", "what are we working on", "open a thread", "park this for later", "keep a
TODO", "don't run it, just note it", "WHEREIAM", "WIA", "pick up where we left off".

This use case is orthogonal to what the agent produces. Combine it with any other branch: a
developer, a researcher or a tutor can each take `_continuity` as well.

## What it provides

- `AGENTS.md`: the always-on posture. The agent is the only writer of its directory's files,
  a suggestion is parked rather than run, a pause is met with an offer to update the files,
  and what was written before a gap is checked before it is trusted.
- Skills:
  - `where-i-am`: the human's work-in-progress file (default `WHEREIAM.md`, alias "WIA"), the
    single source of truth for where the human is. It holds two records: the human's notes on
    what is in progress or must happen first thing next time, in the human's words, each
    linked to the context it came from; and the board of work threads, the parallel forks of
    the work in progress, each with its kind, its last known state and where it lives.
  - `parked-ideas`: the backlog (default `TODO.md`). It holds what can wait: the human's
    parked ideas and everything the agent or its team suggests, with the decisions that are
    the human's alone at its foot.

## How the two fit together

**The WIA is now; the backlog is later.** A WIA note or thread is live. A parked idea waits
until it is called. Work moves between them: a parked item the human calls goes to the WIA as
a note or a thread, and a note or thread that stops being live goes to the backlog. Only the
human decides when a note leaves the WIA.

**One writer per directory.** The agent provisioned with `_continuity` is the only writer of
its directory's WIA and backlog. It writes the human's notes in the human's words, never notes
of its own, and keeps the thread board itself. Other agents keep their own files in nested
directories; the owner may read those, never write them.

**A reference, not a monitor.** The thread board records each thread's last known state, with
its date. It answers "what are we working on?"; it does not watch the threads.

## Provisioning requirements

- **File names and location.** Default: `WHEREIAM.md` and `TODO.md` at the project root,
  and `WHEREIAM.archive.md` beside them once the WIA needs an archive. Offer the defaults; the
  human may rename or move them.
