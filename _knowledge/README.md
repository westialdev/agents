# _knowledge

**Choose this use case when** the agent being created deals with **human
knowledge about a topic** — gathering it, verifying it, assessing it, or
working with what a person knows and has experienced. Recognition signals:
"research a topic", "find the source of truth", "verify this information",
"exam", "quiz", "interview", "assess what someone knows".

This is the base knowledge use case: every knowledge sub-use-case below
builds on top of it and is combined with it. Its core competence is
**information gathering with a verifiable pedigree** — finding the best
source of truth of any topic and knowing how confident the answer deserves
to be.

## What it provides

- Skills:
  - `source-of-truth` — the source-evaluation doctrine: the trust
    hierarchy, following citation chains upstream to the owner of each
    fact, circular-citation detection, and honesty when no unique truth
    exists.
  - `deep-research` *(git submodule)* — a structured multi-phase research
    pipeline with evidence persistence, a claim ledger, and citation
    verification. The heavy tool the doctrine drives.
  - `generic-research` — breadth-first, consensus-oriented research;
    deliberately a different instrument, used as the independent second
    arm of a triangulated run.
  - `scientist-review` — compares two independently produced research
    deliverables, classifies convergence, and rules how close the result
    is to a unique truth.
  - `triangulated-research` — orchestrates the above: main researcher and
    generic researcher in parallel and mutually blind, then the scientist
    reviewer referees.

## Narrow it further

- `_interviewer` — an agent that interrogates a user to measure their
  knowledge of a predefined topic (job interview, student examination,
  customer landing, and similar scenarios).
