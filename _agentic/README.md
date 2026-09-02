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

- `AGENTS.md` — the cross-cutting rules of agentic work: asymmetric roles and a
  single spawner, least privilege for every delegate, the reversibility gate
  (act on what can be undone, ask before what cannot), delegation briefs passed
  verbatim rather than re-summarized, one channel of record so the system is
  auditable, and the duty to log decisions and hand-offs.

## Narrow it further

- `_minime` — the Minime agentic team: a development team that drives itself
  from a work-item tracker, with a human owner on top.
