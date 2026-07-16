---
name: brownfield-pathfinder
description: >
  Step-0 pathfinder for the FULL refactor/restructuring of an entire existing
  project — replacing whole parts of a legacy system, incrementally, without
  rewriting it from scratch and without ever taking it offline. Autonomously maps
  the existing code, interrogates the developer about scope and hard constraints,
  recovers the domain language, plans the safety nets (missing end-to-end tests
  that cover every use case, plus characterization tests), and lays out a strict
  strangler-fig replacement strategy of ordered, always-shippable slices.
  Stack-agnostic. Trigger at the very start of a whole-project refactor:
  "full refactor", "restructure the project", "modernize the codebase",
  "break up the monolith", "strangle the legacy", "big migration". NOT for
  partial or localized refactors — those belong to the lower-range refactor skill.
---

# Brownfield Pathfinder

The **pathfinder** runs once, at the very start of a **full refactor of an entire
project**, before you change a single line of the legacy system. It does not
perform the refactor. Its job is to find the path through terrain that is already
built and already running: understand the existing system, pin its behavior with
safety nets, and lay out an incremental plan to replace whole parts without ever
taking the system offline.

Think of it as surveying occupied ground. `development-guidelines` builds each new
part on it (TDD); `done` completes each part.

**Scope.** This pathfinder is only for the *whole-project* refactor — the widest
range of change. A partial, localized, or single-component refactor is **not**
this skill's job; defer those to the dedicated lower-range refactor skill.

**Prime directive.** The system stays working, green, and shippable at every step.
We strangle the legacy part by part — we **never** big-bang rewrite it.

## When to run

- A **full refactor / restructuring of an entire project** is about to begin.
- No restructuring map, ADRs, or safety-net plan exist yet for this effort.
- The developer says "full refactor", "restructure the project", "modernize the
  codebase", "break up the monolith", "strangle the legacy", or "big migration".

## When NOT to run

- The change is **partial or localized** (one module, one component, a contained
  cleanup) → defer to the **lower-range refactor skill**, not this pathfinder.
- A restructuring map already exists for this effort → resume under
  `development-guidelines`.

## Guiding principles

1. **Keep it running.** Behavior preservation is the prime directive. The system
   must stay green and shippable after every slice. No step leaves it broken.
2. **Understand before you touch.** The existing code is the specification. Do
   reconnaissance first; never propose changes to code you have not mapped.
3. **Safety net before surgery.** Before changing behavior, pin the *current*
   observable behavior with tests — first the end-to-end tests that cover every
   use case, then characterization (golden-master) tests at the seams. Green net
   first, change second.
4. **Strangle, don't rewrite.** Replace incrementally and *only* incrementally.
   Stand the new implementation up alongside the old, route to it, and retire the
   old part only once the new one is proven. No big-bang rewrite. Never delete the
   old path before the new one works.
5. **Recover the language, don't invent it.** The Ubiquitous Language is
   *recovered* from the existing code and the developer's words. Where the code's
   names and the domain's meaning disagree, pin the truth.
6. **Seams over edits.** Find the seams — points where behavior can be altered
   without editing the legacy in place — and insert new behavior there (branch by
   abstraction, anti-corruption layer, facade). Minimize edits to untested legacy.
7. **One part at a time.** Each replaced part is its own slice with its own
   red-green-refactor cycle, handed to `development-guidelines`. Never batch
   multiple parts into one move.
8. **Ask, never assume.** Stack-agnostic. Never presume the target architecture,
   the parts in scope, or what may change. Recommend only when asked or when
   laying out trade-offs.
9. **Confirm before scaffolding.** Produce the map and the plan, get explicit
   approval, and only then create artifacts.

---

## The expedition — five phases

Walk the phases in order. Phase 1 is investigation the agent performs; phase 2 is
interrogation of the developer; phase 3 recovers the language; phases 4–5
synthesize the safety nets and the strategy. Confirm each phase's output back to
the developer before moving to the next. On a large codebase, fan out phase-1
reconnaissance across parallel `general-purpose` subagents (one per subsystem) and
consolidate their findings.

### 1. Reconnaissance — map the existing terrain (autonomous, then confirm)

The agent investigates on its own, then presents a written **system map** for the
developer to correct. Do not ask the developer to narrate the code first — map it,
then have them fix what you got wrong. Cover:

- **Stack & tooling** — languages, frameworks, build tool, package manager, and
  the exact **test command** and how to run the app. Detect from the repo.
- **Structure & dependencies** — modules/packages, layering, entry points, and the
  dependency edges between parts. Note cycles and tight coupling.
- **Hotspots** — via git archaeology (churn, age, ownership) and size, find the
  parts that change most, break most, or concentrate complexity.
- **Existing test coverage** — what is tested and what is not, with special
  attention to **end-to-end coverage of use cases**: which user journeys have E2E
  tests and which do not. This directly feeds phase 4.
- **Replacement candidates** — the parts plausibly in scope, and the seams around
  each.

Present the map. Revise it against the developer's corrections before continuing.

### 2. Scope & hard constraints (ask the developer)

Interrogate the developer on exactly these four areas. Batch related questions
with `AskUserQuestion`, one area at a time; echo back a summary before moving on.

- **In-scope vs frozen parts** — which parts of the project may be replaced, and
  which are explicitly off-limits / frozen.
- **What must not change** — public API contracts, DB schema, wire formats,
  observable behavior, performance envelope.
- **Constraints & definition of done** — must-stay-shippable, no downtime,
  deadlines, data migration, compliance — and the concrete definition of done for
  the whole refactor.
- **Missing end-to-end coverage** — walk the use cases the system must keep
  supporting and, against the phase-1 coverage findings, identify **which E2E
  tests are missing to cover all the use cases**. This list is the backbone of the
  safety net planned in phase 4.

### 3. Recovered Ubiquitous Language & target architecture

- **Recover the Ubiquitous Language**: extract the domain terms already present in
  the code, confirm each against the developer's own vocabulary, and reconcile
  mismatches (code name vs. true domain meaning). These seed `doc/UBIQUITOUS.md`.
- Confirm the intended **end state** — the target architecture/structure. Surface
  trade-offs if the developer wants them. Every significant choice becomes an ADR.

### 4. Safety nets — cover every use case, then pin the seams

- **First, the E2E net.** For every use case identified in phase 2 as lacking
  coverage, plan the missing **end-to-end test** that pins its current observable
  behavior. Full E2E coverage of all use cases is the net that lets internals be
  replaced freely — it is the primary safety net for a whole-project refactor.
- **Then, characterization tests** at the seams of individual parts, where finer
  behavior pinning is needed before that part is touched.
- Identify the **seam** where each characterization test attaches and where the new
  implementation will later be swapped in.

Safety nets are the one exception to "the pathfinder writes no code": a green net
must exist before any legacy behavior is touched (see artifacts).

### 5. Restructuring strategy — the path

- Choose the **replacement technique per part**: strangler fig (facade/route new
  callers to the new implementation), branch by abstraction (introduce an
  abstraction, migrate implementations behind it, remove the old), anti-corruption
  layer (isolate new code from legacy models), or extract-and-replace.
- Break the work into **independently shippable slices**, ordered by
  risk/value/dependency. Each slice: confirm the net is green → replace one part →
  route to it → retire the old path → stay green. Each slice is its own
  `development-guidelines` cycle.
- State explicitly how the system stays shippable between slices. No slice may
  leave the system unshippable, and no big-bang cutover is permitted.

---

## Confirm before scaffolding

Synthesize everything into a short written summary: the system map, the confirmed
scope and hard constraints, the recovered language and target architecture, the
E2E + characterization safety-net plan, and the ordered slice sequence — plus the
list of artifacts you intend to create. Present it and ask for explicit approval.
Revise until the developer confirms. **Only then** create files.

---

## Artifacts to produce

Create or reconcile these in the **target project** (not in this config
directory), honoring the project rules in `_development/CLAUDE.md`. Where an
artifact already exists in the legacy repo, **reconcile** with it rather than
overwrite blindly.

1. **`README.md`** — create or update. Add/refresh a **"Current task"** section
   naming the refactor effort (CLAUDE.md rules 5 & 6 read and update this).
2. **`CLAUDE.md`** — create or reconcile: pointers to `development-guidelines` and
   `done`, the discovered stack/tooling and **test command**, the **hard
   constraints** (what must not change), and branch/commit conventions.
3. **`doc/UBIQUITOUS.md`** — the recovered Ubiquitous Language glossary, using the
   developer's exact terms, with any code-vs-domain mismatches pinned.
4. **`doc/restructuring-plan.md`** — the living plan: the system map, the safety-net
   inventory (missing E2E tests per use case + characterization seams), and the
   ordered slice sequence with each slice's replacement technique, its net, and its
   shippable boundary.
5. **Architecture Decision Records** — under `doc/adr/`: the current-state
   assessment, the target architecture, and each major strategy decision (e.g. why
   strangler fig, why this slice order). Context → decision → consequences.
6. **Safety-net scaffolding** — the missing end-to-end tests that cover the use
   cases, plus the first characterization test(s) at the seams of the first slice
   — or at minimum the net plan and the first failing E2E test. This is the
   exception to "no code": nets come before surgery.
7. **Agent resources (when required)** — only if discovery surfaced a real need:
   project-specific skills and/or MCP configuration, *in addition to* what
   `_development` and `_brownfield` already provide.

Whenever a new crucial domain term surfaces while producing artifacts, add it to
`doc/UBIQUITOUS.md` (CLAUDE.md rule 4).

---

## Hand off

Once the map, the safety-net plan, and the slice sequence are confirmed and
written:

1. Summarize what was created and where, and restate the ordered slice sequence.
2. Point at the **first slice** as the starting point: get its safety net (E2E +
   characterization) green, then replace that one part.
3. Explicitly hand off: from here each slice is built under
   `development-guidelines` (TDD, red-green-refactor, errors-must-explode) and
   completed under `done`, and the system stays green and shippable after every
   slice.

The pathfinder's job ends at the map, the nets, and the plan. Do not begin
performing the refactor.
