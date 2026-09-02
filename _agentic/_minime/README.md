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

**Do not hardcode a particular team's behavior.** Statuses, gates, comment
conventions and role names belong to the installation and are still evolving.
Read the installation's own documentation and the tracker's own record; treat
what you find there as the truth, and this README as orientation only.

What is stable enough to rely on:

- **The tracker is the channel.** Every instruction, question, answer and
  delivery is a work-item comment or a status change. Nothing meaningful happens
  in chat, and what is not written on the item did not happen.
- **The human owner is the top of the hierarchy** and the only one who accepts
  or rejects a delivery.
- **Plan before code.** The team states what it intends to build before building
  it, so a misaligned plan is caught before a delivery is built on top of it.
- **Roles are asymmetric.** One agent orchestrates and spawns; the rest are
  scoped, least-privilege, and cannot spawn.
- **Reversible work is autonomous; irreversible work is confirmed** by the owner.

## What it provides

- `AGENTS.md` — working with a Minime team: tracker-as-channel discipline,
  reading the installation before assuming its protocol, and the rule that a
  status change is a signal to another agent, never bookkeeping.

## Narrow it further

- `_owner` — the human owner's own agent: the vehicle through which the owner
  thinks, writes, and acts on the team.
