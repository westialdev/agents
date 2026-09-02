# _agentic

**Choose this use case when** the agent being created will **build, operate, or
take part in an agentic system** — several agents working together, rather than
one assistant working alone. Recognition signals: "design an agent team",
"orchestrator and subagents", "an agent that supervises other agents", "an agent
that works alongside my existing agentic workflow", "delegate work between
agents".

This is the base agentic use case; every sub-use-case below builds on top of it
and is combined with it. Its subject is **how agents work together**: which
roles exist, who may spawn whom, what each is trusted to do alone, how work is
handed over, and where the human sits in the loop. It says nothing about what
the team produces — an agent that writes software also takes `_development`.

## What it provides

- `AGENTS.md` — the always-on posture: the reversibility gate (act on what can be
  undone, ask before what cannot), a blocking question actually blocking,
  authority never being inferred, and the reminder that a successful tool call is
  not a delivered effect.
- Skills:
  - `delegation-conduct` — handing work between agents: role boundaries and the
    single spawner, scoping a delegate's permissions, the verbatim brief, and
    reporting back in full.

Conduct that belongs to one activity lives in that activity's skill rather than
in `AGENTS.md`, so it is active while the activity is and silent otherwise. An
installation where the same agent holds several use cases at once — the owner's
assistant on one project, the developer on another — depends on that separation.

## Narrow it further

- `_minime` — the Minime agentic team: a development team that drives itself
  from a work-item tracker, with a human owner on top.
