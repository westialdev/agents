---
name: westial-agents-resources-hierarchy
description: >
  How to consume Westial Agents Resources Hierarchy
  (https://github.com/westialdev/agents). Trigger whenever an agent must
  create, configure, or provision another agent using resources from this
  project: "create an agent", "set up an agent for <use case>", "install
  agent resources". Teaches how to discover the use-case hierarchy,
  interrogate the developer to find the best-matching branch, and
  accumulate and install every resource along that branch.
---

# Westial Agents Resources Hierarchy

This skill turns you into a competent consumer of **Westial Agents Resources
Hierarchy**: a repository that organizes reusable agent resources — skills,
instructions, and configuration — into a hierarchy of *use cases*. Your job,
when this skill triggers, is to find the use-case branch that best matches the
agent being created, collect every resource along that branch, and install
those resources into the target agent.

This skill is **consume only**. Never modify the repository itself: do not
edit, add, or remove anything inside it. If a needed use case is missing, tell
the developer and stop.

## The repository at a glance

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

## Step 0 — Obtain the repository

If a local checkout is not already available, clone it **with submodules**
(some skills are git submodules and are empty without them):

```sh
git clone --recurse-submodules git@github.com:westialdev/agents.git
```

If a checkout exists but skill directories are empty, run
`git submodule update --init --recursive` inside it.

## Step 1 — Map the hierarchy

From the repository root, list every underscore-prefixed directory recursively to
build the use-case tree, and read the `README.md` files you find along the way
— the root one first, then any local ones. Note which directories contain
`skills/`, `AGENTS.md`, or `.agents/`.

Each use-case directory carries a `README.md` whose **"Choose this use case
when"** line is its *selection hook*: a plain description of the kind of agent
that use case is for, with recognition signals. That hook is what you match the
agent being created against in Step 2 — read every one before interrogating the
developer. If a use-case directory has no such hook, fall back to its directory
name and contents, and note the missing hook in your Step 6 report.

## Step 2 — Find the best-matching branch

Do not guess the use case. **Interrogate the developer**, one level of the
hierarchy at a time:

1. Present the top-level use cases and ask which one matches the agent being
   created. Describe each briefly using its selection hook from Step 1, and
   compare the agent's intended purpose against each hook's recognition
   signals.
2. Descend into the chosen use case. If it has child use cases, present them
   and ask whether one of them narrows the match — or whether the parent alone
   is the right scope.
3. Repeat until you reach a leaf or the developer stops at an inner node.
4. Confirm the final branch explicitly (e.g. "`_development` →
   `_development/_greenfield`") before installing anything.

For example, an agent that must find web vulnerabilities, run an authorized
web-application penetration test, or scrape and recon a third-party web
system matches the branch `_development` → `_development/_hacker`, and so
receives the base development resources plus the `_hacker` browser MCP, rules
of engagement, and web skills.

If no top-level use case matches, report the gap to the developer and stop —
do not improvise resources and do not add anything to the repository.

## Step 3 — Collect the provisioning requirements

A use case may declare a **"Provisioning requirements"** section in its
`README.md`: settings the target agent is not viable without (for example,
`_knowledge/_interviewer` requires an interview definition — topic,
duration, mode, and so on). Check every use case along the confirmed
branch:

1. For each declared requirement, take the value from what the developer
   has already said, or ask the developer for it. Where the requirement
   states a default, offer it; otherwise the developer must decide. Never
   invent a value, and never leave a requirement unset.
2. Record the collected values as the use case's **provisioning
   definition** — you will bake it into the target agent's instructions in
   Step 5.

If the branch declares no provisioning requirements, skip this step.

## Step 4 — Accumulate the resources along the branch

Walk the confirmed branch **from root to leaf** and collect, in that order:

1. Every skill directory under each `skills/` (including submodule skills,
   with their reference files and assets).
2. Every `AGENTS.md`, kept in parent-first order.
3. Every `.agents/` configuration file.

Accumulation is additive: never drop, dedupe, or override a parent's resource
because a child has one of the same kind.

## Step 5 — Install into the target agent

Map the accumulated resources onto the target platform's conventions. Stay
platform-neutral: the repository does not assume a specific agent product.

- **Skills** — copy each collected skill directory, whole, into wherever the
  target agent loads skills from.
- **Instructions** — install the collected `AGENTS.md` contents parent-first
  into the target agent's instructions document. When concatenating multiple
  files into one, precede each part with a comment or heading naming the use
  case it came from. Append each provisioning definition collected in
  Step 3, under a heading naming its use case.
- **Configuration** — apply the collected `.agents/` files to the target
  agent's configuration location, translating file layout if the platform
  uses a different convention.

Copy — never symlink into the repository checkout, and never point the target
agent at repository paths, unless the developer explicitly asks for a linked
setup.

## Step 6 — Report

Tell the developer, concisely:

- the branch that was chosen and why;
- every skill, instructions file, and configuration file installed, with its
  source use case and destination path;
- the provisioning definition collected in Step 3, if any, as installed;
- anything expected but missing (e.g. an empty submodule).
