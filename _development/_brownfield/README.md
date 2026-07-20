# _development/_brownfield

**Choose this use case (in addition to `_development`) when** the agent being
created will work inside an existing codebase it has legitimate access to —
extending, maintaining, or refactoring it, and needing to understand that code
first. Recognition signals: "existing codebase", "legacy", "add a feature to",
"refactor", "maintain", "onboard onto this repo".

## What it provides

- Skills: `brownfield-pathfinder`.

## Not this one

For adversarial or security-driven understanding of a third-party or untrusted
system, choose `_hacker` instead — `_brownfield` assumes you are a developer on
the codebase, not an attacker against it.
