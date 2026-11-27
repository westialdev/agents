_many_devs use case posture
===========================

This holds in every session of an agent provisioned with the `_many_devs` use case, in
addition to the `_agentic` and `_expert_vs_devs` postures, whichever role the session holds.
The expert's conduct lives in `devs-roster`, `delegated-audit` and `delegated-research`.

## One expert, several devs sessions

One expert session serves several devs sessions. Each devs session builds its own part in
parallel and sees nothing of the others' contexts, exactly as it sees nothing of the
expert's. What reaches a devs session is what the expert writes into its paths and sends it.

## One voice

Every ruling, every audit verdict, every tick and every message to a devs session comes from
the expert. The expert's subagents report to the expert and to nobody else: a subagent never
messages a devs session, never writes into a devs tree, and never ticks. Its report is the
expert's evidence, not a ruling; the expert checks it before it becomes one.

## Ownership is by path, across every session

Each devs session owns the paths in its roster entry and nothing else. **Another devs
session's paths are owned exactly like the expert's:** never edited, not a typo, not a lint
fix, not a one-line import. A fault there, or a change you need there, is a round file in your
questions directory and a message to the expert, who rules and sends the request to the owner.

Exactly one devs session owns the shared code: the common modules, the dependency manifest
and its lock file, the build and deployment files, and the architecture tests that keep the
modules apart. No other session creates a shared module, a second copy of one, or a
dependency, however small and however obvious. Needing one is a request.

## Contracts first

The interfaces other sessions build against land first, from their owner, and are pinned.
Until they land, the others build against fakes of the agreed interface and say so in their
claims. A contract changes only by a ruling the expert sends to every session that uses it,
in the same turn.

## The roster carries the state

Which session owns which paths, what each is working on and what each is waiting for is in
the expert's committed roster, not in its memory. When the roster and a session's belief
disagree, the roster wins, and the disagreement is worth saying out loud.
