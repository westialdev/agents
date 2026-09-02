# _agentic/_minime

**Choose this use case (in addition to `_agentic`) when** the agent being
created **takes part in, drives, or supports a Minime agentic team**.
Recognition signals: "Minime", "my agentic development team", "the agent that
picks up my tickets", "review what my team delivered", "answer my team's
question", "operate my agentic team".

## The team

```
Owner (human) → dispatcher (scheduled) → executive (orchestrator, sole spawner) → mechanics (least-privilege specialists)
```

A Minime team develops software largely on its own initiative: it takes work
items from a tracker, plans them, delegates the actual work to short-lived
specialist subagents, and hands the result back to a human for approval.

## Why so little of it is written down here

A Minime team is an installation, not a product. Its states, role names, comment
markers and timings belong to that installation, and they are still moving.
Anything this repository asserted about them would be stale in some installation
already, and an agent that acted on a stale assertion would be confidently wrong
about the one thing it cannot afford to guess.

So the tree carries only what is structural — the tracker is the sole channel,
the human owner is the only one who accepts a delivery, intent is written before
work starts, roles are asymmetric with a single spawner, reversible work is
autonomous — and the installation's own facts arrive at provisioning time,
below. Everything else is discovered at run time from what the installation
documents about itself, and where that documentation and the tracker's record
disagree, the record wins.

## What it provides

- `AGENTS.md` — the posture: a Minime team is an installation, use the facts you
  were provisioned with, discover the rest, never assume another team's shape.
- Skills:
  - `tracker-channel` — working through the tracker as the team's only channel:
    what belongs on the item, what a state change signals to the agent that reads
    it, writing for the human and the literal reader at once, and why a record is
    never rewritten to carry new information.
  - `plan-first` — nothing is built before the intent is written and available to
    the owner, and the item-by-item check of a plan against the request.

## Provisioning requirements

A Minime-facing agent is not viable without the facts of the installation it
serves. The provisioning agent must collect these from the developer and bake
them into the target agent's instructions. There are no defaults — every value is
installation-specific, and a guess here is the failure this use case is most
exposed to:

1. **Tracker system and base URL** — which tracker, and where it lives.
2. **Project key(s) in scope** — the work the agent may act on, and by omission
   the work it may not.
3. **States and their meanings** — the state names in use, each mapped to what it
   signals: needs work, needs an answer from the human, needs a decision,
   accepted, rejected. The meaning is what the rest of this tree refers to; the
   names are just labels this installation happens to use.
4. **Mention syntax that actually notifies** — how to address a person so they are
   notified, as opposed to how to type their name.
5. **Where the installation documents itself** — the path or URL the agent reads
   to learn the current protocol.

## Narrow it further

- `_owner` — the human owner's own agent: the vehicle through which the owner
  thinks, writes, and acts on the team.
