# _agentic/_expert_vs_devs/_many_devs

**Choose this use case (in addition to `_agentic` and `_expert_vs_devs`) when** one expert
session serves **several devs sessions at once**, each building its own part of the product in
parallel, and the expert hands its slow work to subagents so that no devs session waits on
another's audit. Recognition signals: "one expert for all the devs", "several dev sessions in
parallel", "each devs session owns a module", "only one session builds the shared code", "the
expert delegates the audits to an auditor", "I want one session to watch and control".

## The shape

```
                              the human
                                  │
                         the expert's session ── spawns ──▶ auditor (one per claimed slice)
                       rules, ticks, sends every            researcher (one per factual question)
                       message, keeps the roster
             ┌──────────────┬─────┴────────┬──────────────┐
          devs A          devs B         devs C   …     devs N
       shared code       module B       module C       module N
       (the only owner)  its paths      its paths      its paths
```

- **One voice.** Every ruling, every tick and every message to a devs session comes from the
  expert. Subagents report to the expert only; they never talk to the devs.
- **The slow work leaves the expert's context.** Audits and factual research run as subagents,
  in parallel, each from a fresh context. The expert reads their verdicts, checks the evidence,
  and rules.
- **Ownership is by path, across all sessions.** Each devs session owns its paths and nothing
  else. Exactly one devs session owns the shared code. A change one session needs in another's
  paths is a request to the expert, who rules and sends it to the owner.
- **Contracts first.** The shared code's interfaces land before the modules that use them; the
  other devs build against fakes until then.

The parent pattern holds unchanged between the expert and each devs session: slices, round
files, the claim message, the REPLY REQUIRED block and ping, the audit before the tick. This
use case changes who performs the audit (an auditor subagent, briefed by the expert) and adds
the coordination that several devs sessions need. The tick stays the expert's.

## What it provides

- `AGENTS.md` — the posture for both roles when there are many devs: one voice, ownership by
  path across sessions, the single owner of shared code, subagents never speaking to the devs.
- Skills (the expert's side):
  - `devs-roster` — keeping the roster of devs sessions, their paths and their state; routing
    requests across sessions; contracts first; the order of answering; when to ask the human
    for a second expert.
  - `delegated-audit` — briefing an auditor subagent on a claimed slice, its envelope, running
    audits in parallel, and checking the verdict before the tick.
  - `delegated-research` — handing a devs session's factual question to a researcher subagent
    and turning its cited answer into a ruling.

The devs sessions use the parent's `devs-collaboration` as it is; this use case's `AGENTS.md`
adds what they must know about the other devs sessions.

## Provisioning requirements

In addition to the parent's (the expert-owned paths, the questions directory, the acceptance
list, the suite command, the ping interval, what is reserved to the human, any standing grant),
for each devs session:

1. **The roster** — for every devs session: its role name, its repository and clone, the paths
   it owns, its acceptance items. Paths never overlap; every path in the product has exactly
   one owner.
2. **The shared-code owner** — the one devs session that owns the shared code (common modules,
   dependency manifest and lock file, build and deployment files, the architecture tests).
3. **The contracts that land first** — the interfaces the other sessions build against, and
   who owns each.
4. **The subagent mechanism** — how the expert spawns an auditor and a researcher on its
   platform, and which tools each may have (read-only on the devs' trees; write only to
   scratch).
5. **Parallel audits.** Default: at most three at once.
6. **The split trigger** — how long a devs session may wait on the expert before the expert
   asks the human for a second expert and proposes which sessions move to it. Default: 30
   minutes, twice in one day.
