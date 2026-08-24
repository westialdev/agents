# _development/_greenfield

**Choose this use case (in addition to `_development`) when** the agent being
created will start a project from scratch — a clean slate with no existing
codebase to respect. Recognition signals: "new project", "bootstrap",
"greenfield", "from zero", "set up a fresh repo".

## What it provides

- Skills: `greenfield-pathfinder`.

`greenfield-pathfinder` runs once at kickoff and charts the project: it
interrogates the developer and lays the foundation (README, AGENTS.md,
ubiquitous language, scaffold, ADRs, evaluation scenarios). Once it has
confirmed the stack in area 4, it invokes `stack-skill-sourcing` — inherited
from `_development` — to source the technology skills the project's agents
should carry.
