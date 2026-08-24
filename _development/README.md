# _development

**Choose this use case when** the agent being created will write, modify, or
review software of any kind. This is the base development use case; every
development sub-use-case below builds on top of it and is combined with it.

## What it provides

- `AGENTS.md` — core project rules (development guidelines, ubiquitous
  language, README workflow).
- Skills: `development-guidelines`, `done`, `stack-skill-sourcing`.

`stack-skill-sourcing` turns the project's technology stack into a vetted
shortlist of technology skills for the target agent to carry, ranking sources by
proximity to the technology's owner (official first) and verifying each
candidate before trusting it. It applies to every development sub-use-case: the
pathfinders invoke it once the stack is known, and it runs again whenever a main
technology later enters the project.

## Narrow it further

- `_greenfield` — starting a project from scratch.
- `_brownfield` — developing inside an existing codebase you have access to.
- `_review` — reviewing code.
- `_hacker` — security, hacking, and adversarial understanding of third-party
  web systems.
