---
name: greenfield-pathfinder
description: >
  Step-0 pathfinder for starting a project from scratch. Interrogates the
  developer about problem, users, scope, domain language, expected end-to-end
  behavior, tech stack, architecture, and tooling — then lays the project
  foundation (README.md, AGENTS.md, doc/UBIQUITOUS.md, folder scaffold + config,
  ADRs, and agent resources). Stack-agnostic. Trigger at the very beginning of a
  greenfield project: "start a new project", "bootstrap", "kickoff", "from
  scratch", "set up a new repo", or an empty/near-empty working directory with
  no existing task in flight.
---

# Greenfield Pathfinder

The **pathfinder** runs once, at the very start of a greenfield project, before a
single line of production code exists. It does not write features. Its job is to
find the path: interrogate the developer, capture their answers as the project's
foundation, and hand off to `development-guidelines` (which owns how code is
written) and `done` (which owns completion).

Think of it as charting the map. `development-guidelines` walks it.

## When to run

- The working directory is empty or contains only scaffolding.
- The developer says they are starting, bootstrapping, or kicking off a new
  project.
- No `README.md` / `AGENTS.md` foundation exists yet.

If a project foundation already exists, **do not run** — defer to the normal
task workflow.

## Guiding principles

1. **Ask, never assume.** This skill is fully stack-agnostic. Never presume a
   language, framework, database, or test runner. Every such choice is the
   developer's to make. Offer recommendations only when asked or when
   explicitly presenting trade-offs.
2. **One area at a time.** Walk the five discovery areas below in order. Confirm
   each area's answers back to the developer before moving to the next. Do not
   fire every question at once.
3. **Capture the developer's words.** Domain terms and scenario descriptions go
   into the artifacts verbatim where possible — they become the Ubiquitous
   Language. Do not paraphrase away the developer's vocabulary.
4. **Scaffold only after confirmation.** Do not create files until the developer
   has confirmed the synthesized picture (see "Confirm before scaffolding").
5. **Foundation, not features.** Produce the map and the empty rooms. The first
   failing test and the first line of production code belong to
   `development-guidelines`, not here.

---

## The interrogation — five discovery areas

Use `AskUserQuestion` to batch related questions within an area; keep questions
open where the answer is genuinely open (domain terms, scenarios) and offer
options only where a small closed set exists. After each area, echo back a short
summary and get a "yes, continue" before proceeding.

### 1. Problem, users & scope

Establish *why* the project exists before anything else.

- What is being built, in one sentence?
- What problem does it solve, and for whom (the users / actors)?
- What is in scope for the first milestone (the MVP)?
- What is explicitly **out of scope** / a non-goal for now?
- What does success look like — how will we know it works?

### 2. Domain & ubiquitous language

Draw out the language of the problem. These answers seed `doc/UBIQUITOUS.md`.

- What are the core concepts / entities in this domain?
- Are there distinct bounded contexts or sub-areas?
- For each key term: the exact name the developer uses and a one-line definition.
- Note any terms that are easily confused or overloaded, and pin their meaning.

### 3. Expected end-to-end behavior (evaluation scenarios)

Capture the observable behavior that will stand up the system for evaluation.
These become the north-star E2E scenarios — the acceptance criteria the finished
system is judged against.

- Walk through the primary user journeys, step by step, as concrete scenarios.
- For each scenario, capture: the actor, the trigger, the steps, and the
  observable expected outcome (Given / When / Then works well).
- Include the critical failure/edge scenarios that must behave correctly.
- These are *evaluation* scenarios — they define "the system does what it
  should," independent of implementation. They will later drive the E2E layer
  of the test pyramid (see `development-guidelines`).

### 4. Tech stack & architecture

Now — and only now — the *how*. Ask; do not decide for the developer.

- Language(s) and runtime?
- Framework(s) / key libraries, if any preference?
- Persistence / storage, if any?
- External services or integrations?
- Architecture style (layered, hexagonal/ports-and-adapters, modular monolith,
  services, …)? Ask the developer's preference; surface trade-offs if they want
  them.
- Any hard constraints (existing infra, team conventions, compliance)?

Every non-trivial choice here becomes an **ADR** (see artifacts).

### 5. Tooling, testing & delivery

- Package manager / build tool?
- Test runner and testing approach? (The project follows TDD per
  `development-guidelines` — confirm the concrete runner the developer wants.)
- Repository layout preference (`src/`, test locations, monorepo vs single)?
- Commit / branch conventions? (Note: `done` extracts a `{WORD}-{NUMBER}` task
  key from the branch name for commit messages — confirm this convention fits.)
- CI / delivery expectations, if any?
- Do any **agent resources** need to be added for this project beyond what
  `_development` and `_greenfield` already provide — e.g. a project-specific
  skill, or an MCP server configuration (a database, an API, a docs source)?
  Only add these when the project genuinely requires them.

---

## Confirm before scaffolding

Synthesize everything into a short written summary covering all five areas and
the list of artifacts you intend to create. Present it and ask for explicit
approval. Revise until the developer confirms. **Only then** create files.

---

## Artifacts to produce

Create these in the **new project** (not in this config directory), aligned to
the confirmed answers. Honor the project rules in `_development/AGENTS.md`.

1. **`README.md`** — project overview: what it is, the problem/users, MVP scope,
   how to set up and run, and a **"Current task"** section (AGENTS.md rules 5 & 6
   read and update this).
2. **`AGENTS.md`** — project instructions for future agents: pointers to the
   guidelines and `done` skills, the confirmed stack/tooling, test command,
   branch/commit convention, and any project-specific rules surfaced during
   discovery.
3. **`doc/UBIQUITOUS.md`** — the Ubiquitous Language glossary, seeded from area 2
   using the developer's exact terms and definitions.
4. **Folder scaffold + config** — the directory layout and configuration files
   for the confirmed stack (build/package config, test runner config, source and
   test directories). Empty and ready for the first failing test — no feature
   code.
5. **Architecture Decision Records** — one ADR per significant choice from areas
   4 & 5, under `doc/adr/` (context → decision → consequences). At minimum: the
   stack choice and the architecture style.
6. **Agent resources (when required)** — only if area 5 surfaced a real need:
   project-specific skills and/or MCP server configuration placed in the
   project's agent directory, *in addition to* the resources inherited from
   `_development` and `_greenfield`.
7. **Evaluation scenarios** — record the area-3 scenarios where the project keeps
   acceptance criteria (e.g. `doc/scenarios.md` or an equivalent), so the E2E
   layer has a source of truth.

Whenever a new crucial domain term appears while producing artifacts, add it to
`doc/UBIQUITOUS.md` (AGENTS.md rule 4).

---

## Hand off

Once the foundation is confirmed and written:

1. Summarize what was created and where.
2. Point at the first evaluation scenario as the natural starting point.
3. Explicitly hand off: from here on, code is written under
   `development-guidelines` (TDD, red-green-refactor, errors-must-explode) and
   completed under `done`.

The pathfinder's job ends at the foundation. Do not begin implementing features.
