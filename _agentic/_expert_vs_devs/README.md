# _agentic/_expert_vs_devs

**Choose this use case (in addition to `_agentic`) when** the agent being
created is **one of two separate sessions that build a project together — a
domain expert and a development team** — talking to each other session to
session, with a human over both. Recognition signals: "an expert session that
reviews my devs", "the devs ask the expert", "two Claude Code sessions on one
repo", "a domain expert that audits every slice", "the team is blocked waiting
for the other session", "help me write the devs' goal".

Provision **both** sessions from this use case; each takes the role named in
its provisioning definition. The skills are scoped by activity rather than by
role, so each session's own work triggers its own skills and the other role's
stay silent.

## The pair

```
                      the human
        (money, production, credentials, scope, value judgements)
             │ goal                              │ questions, grants
             ▼                                   ▼
   the devs' session  ── questions, claims ──▶  the expert's session
   builds the product ◀── answers, reviews ───  reads the whole tree,
   sees only what the      (files + messages)   rules, audits every slice,
   expert writes/sends                          never edits the devs' code
```

- **The collaboration starts in the devs' session**, driven by
  `devs-collaboration` and by a goal the human gives it (Claude Code's `/goal`).
  The devs ask the human for the goal; the expert helps the human write it.
- **Work goes in slices**, one acceptance item each. Every slice is claimed in a
  message, audited by the expert from a clean extract, and only then ticked.
- **Every exchange is a committed file and a message.** Neither alone counts.
  The devs close every message they wait on with a REPLY REQUIRED block and ping
  until the reply arrives; the expert stamps each answer with the receipt of its
  send.

## Why it is shaped like this

Almost every failure this use case was written from was a thing that existed in
one place only. A ruling written in the expert's terminal and never sent; a
question filed in the repository and never messaged; a corrected figure with
five copies still standing; a check that answered plausibly while broken; a
peer that restarted under a new name while the other side read its silence as
agreement. None of them announced itself. So the protocol is built to make
absence visible: the DELIVERY receipt, the DONE line, the ping, the asserted file
count, the audit before the tick.

## What it provides

- `AGENTS.md` — the posture for both roles: two sessions that never share a
  context, ownership by path, the record carrying the state, written not being
  delivered, the human deciding, and the terminal being for the human.
- Skills:
  - `devs-collaboration` — the devs' side, and where the collaboration starts:
    reading in, asking for the goal, slices, question rounds, the claim message,
    holding the tick, and the REPLY REQUIRED block and ping.
  - `expert-rulings` — the expert's side: answering a round, the delivery order
    and its receipt, sweeping every copy of a correction, value judgements to
    the human, and the standing-grant pattern.
  - `slice-audit` — the expert's audit of a claimed slice: clean extract with an
    asserted file count, direct exit status, checking claims rather than citing
    them, and how to judge the rows a slice added.
  - `goal-authoring` — helping the human write the devs' `/goal`, with a worked
    template.
  - `session-reload` — reload prompts for either session after a restart, and
    the checks that catch what the restart dropped.
  - `instrument-discipline` — both sides: suspecting the instrument before the
    subject, counting artefacts not text, citing by name, deriving bounds, and
    sourcing external limits from their owner.

## Provisioning requirements

Each session is not viable without the facts of the pair it belongs to. The
provisioning agent must collect these from the developer and bake them into the
target agent's instructions. Only the items that state a default have one:

1. **This session's role** — `expert` or `devs`.
2. **The shared repository and the devs' tree** — where the product lives.
3. **The expert-owned paths** — its answers directory, its reviews directory
   (if separate), its handover directory, and its own instructions. Everything
   else in the devs' tree is the devs'.
4. **The devs' questions directory and file naming.** Default:
   `YYYY-MM-DD-HHMM-<topic>.md`, one file per round; answers named the same way.
5. **The acceptance list** — the file whose items are ticked, and the mark a
   tick is.
6. **Where the devs' project documents its commands** — the suite command in
   particular, which the expert runs from a clean extract.
7. **The ping interval.** Default: ten minutes.
8. **What is reserved to the human** — by default money, production,
   credentials, the human's accounts, scope and value judgements; the developer
   may add to the list, never shorten it silently.
9. **Any standing grant** — the exact text, with its "does not license" list.
   Default: none.

This use case assumes session-to-session messaging (in Claude Code, sending to a
peer's session name and listing the live sessions) and a recurring session job
for the ping. On another platform, name its equivalents at provisioning; without
them the protocol cannot be kept.
