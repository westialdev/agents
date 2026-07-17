Westial Hierarchy Agents Resources
==================================

A collection of personal configurations, skills, and guidelines for AI Agents.

## Installation and usage

Westial Hierarchy Agents Resources is meant to be consumed by agents that
create other agents. The only thing such an agent needs is the
[`westial-hierarchy-agents-resources`](skills/westial-hierarchy-agents-resources/SKILL.md)
skill, located in the root `skills/` directory:

1. Install `skills/westial-hierarchy-agents-resources` into the agent that
   will create agents, wherever that agent loads skills from.
2. That skill carries the full knowledge of how to exploit these resources: it
   clones the repository (with submodules) when no checkout is available,
   interrogates the developer to find the use-case branch that best matches
   the agent being created, accumulates every resource along that branch, and
   installs the resources into the target agent.

The `skills/` directory in the root of this project is not part of the
use-case hierarchy — it holds the skills about the project itself.

## Directory Structure

Directories prefixed with an underscore (`_`) represent use cases. They form a hierarchy: a parent use case directory applies to all its descendants, and each subdirectory narrows the scope further.

**Example:** `_development` contains skills and configuration for software development in general. Inside it, `_greenfield` adds configuration specific to starting a project from scratch. When setting up an agent for a greenfield project, you combine the contents of both `_development` and `_development/_greenfield`.

Local `README.md` files are present in directories where the purpose or content warrants extra explanation.
