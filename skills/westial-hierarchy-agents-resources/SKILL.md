---
name: westial-hierarchy-agents-resources
description: >
  How to consume the Westial hierarchy-style agents resources catalog
  (https://github.com/westialdev/agents). Trigger whenever an agent must
  create, configure, or provision another agent using resources from this
  catalog: "create an agent", "set up an agent for <use case>", "install
  agent resources from the catalog". Teaches how to discover the use-case
  hierarchy, interrogate the developer to find the best-matching branch,
  and accumulate and install every resource along that branch.
---

# Westial Hierarchy Agents Resources

This skill turns you into a competent consumer of the **agents resources
catalog**: a repository that organizes reusable agent resources — skills,
instructions, and configuration — into a hierarchy of *use cases*. Your job,
when this skill triggers, is to find the use-case branch that best matches the
agent being created, collect every resource along that branch, and install
those resources into the target agent.

This skill is **consume only**. Never modify the catalog itself: do not edit,
add, or remove anything inside it. If a needed use case is missing, tell the
developer and stop.

## The catalog at a glance

- Directories prefixed with an underscore (`_`) are **use cases**. They form a
  hierarchy: a parent use case applies to all its descendants, and each
  subdirectory narrows the scope further.
- A use-case directory may contain any of:
  - `skills/` — one subdirectory per skill, each with a `SKILL.md` (some are
    git submodules).
  - `AGENTS.md` — instructions/rules for agents working under that use case.
  - `.agents/` — configuration for the agent platform.
  - `README.md` — extra explanation of the directory's purpose, when needed.
- **Simple accumulation.** Resources combine from root to leaf: a child adds
  to its parents, it never replaces or overrides them. Everything found along
  the chosen branch gets installed.

**Example:** an agent for a greenfield development project takes the branch
`_development` → `_development/_greenfield`, and therefore receives the
resources of *both* directories.

## Step 0 — Obtain the catalog

If a local checkout is not already available, clone it **with submodules**
(some skills are git submodules and are empty without them):

```sh
git clone --recurse-submodules git@github.com:westialdev/agents.git
```

If a checkout exists but skill directories are empty, run
`git submodule update --init --recursive` inside it.

## Step 1 — Map the hierarchy

From the catalog root, list every underscore-prefixed directory recursively to
build the use-case tree, and read the `README.md` files you find along the way
— the root one first, then any local ones. Note which directories contain
`skills/`, `AGENTS.md`, or `.agents/`.

## Step 2 — Find the best-matching branch

Do not guess the use case. **Interrogate the developer**, one level of the
hierarchy at a time:

1. Present the top-level use cases and ask which one matches the agent being
   created. Describe each briefly, using what you read in Step 1.
2. Descend into the chosen use case. If it has child use cases, present them
   and ask whether one of them narrows the match — or whether the parent alone
   is the right scope.
3. Repeat until you reach a leaf or the developer stops at an inner node.
4. Confirm the final branch explicitly (e.g. "`_development` →
   `_development/_greenfield`") before installing anything.

If no top-level use case matches, report the gap to the developer and stop —
do not improvise resources and do not add anything to the catalog.

## Step 3 — Accumulate the resources along the branch

Walk the confirmed branch **from root to leaf** and collect, in that order:

1. Every skill directory under each `skills/` (including submodule skills,
   with their reference files and assets).
2. Every `AGENTS.md`, kept in parent-first order.
3. Every `.agents/` configuration file.

Accumulation is additive: never drop, dedupe, or override a parent's resource
because a child has one of the same kind.

## Step 4 — Install into the target agent

Map the accumulated resources onto the target platform's conventions. Stay
platform-neutral: the catalog does not assume a specific agent product.

- **Skills** — copy each collected skill directory, whole, into wherever the
  target agent loads skills from.
- **Instructions** — install the collected `AGENTS.md` contents parent-first
  into the target agent's instructions document. When concatenating multiple
  files into one, precede each part with a comment or heading naming the use
  case it came from.
- **Configuration** — apply the collected `.agents/` files to the target
  agent's configuration location, translating file layout if the platform
  uses a different convention.

Copy — never symlink into the catalog checkout, and never point the target
agent at catalog paths, unless the developer explicitly asks for a linked
setup.

## Step 5 — Report

Tell the developer, concisely:

- the branch that was chosen and why;
- every skill, instructions file, and configuration file installed, with its
  source use case and destination path;
- anything expected but missing (e.g. an empty submodule).
