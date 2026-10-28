# _continuity

**Choose this use case when** the agent being created works with one human over a
**long collaboration that is interrupted** (sleep, trips, other projects), and the human's
train of thought must survive the gaps. Recognition signals: "I lose my ideas when I pause",
"park this for later", "where were we", "keep a TODO of what you suggest", "don't run it, just
note it", "a post-it file", "WHEREIAM", "WIA", "pick up where we left off".

This use case is orthogonal to what the agent produces. Combine it with any other branch: a
developer, a researcher or a tutor can each take `_continuity` as well.

## What it provides

- `AGENTS.md` — the always-on posture: a suggestion is parked rather than run, a pause is met
  with an offer to update the files, and the boundary between the two files is never crossed.
- Skills:
  - `parked-ideas` — the human's post-it file (default `WHEREIAM.md`, alias "WIA"). The notes
    are the human's alone. The agent only links each note to the context it refers to.
  - `suggestion-backlog` — the agent's parking lot (default `TODO.md`). Everything the agent
    or its team suggests waits here until the human calls it, with the decisions that are the
    human's alone at its foot.

## The one rule that joins them

**Two authors, two files.** The ideas file holds only what the human wrote, plus the agent's
`→` links beneath it. Everything the agent authors (suggestions, decisions, state, queues)
goes in the backlog. Mixing them is the failure this use case exists to prevent: once the
agent's text sits among the human's notes, the human can no longer tell which ideas are their
own.

## Provisioning requirements

- **File names and location.** Default: `WHEREIAM.md` and `TODO.md` at the project root.
  Offer the defaults; the human may rename or move them.
