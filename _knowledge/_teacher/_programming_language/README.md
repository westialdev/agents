# _knowledge/_teacher/_programming_language

**Choose this use case (in addition to `_knowledge` and `_knowledge/_teacher`)
when** the subject being taught is a **programming language**, and the
learner must end up reading and writing real, idiomatic programs in it.
Recognition signals: "teach me Go / Rust / Python from scratch", "I know
Java, now teach me Go", "I want to learn to program", "help me learn
<language> to build <thing>".

## Why it is its own use case

A programming language is learned by writing code that runs. That gives the
teacher an unusually strict checker: the compiler, the runtime and the test
suite. It also brings traps that other subjects do not have. Snippets
that "look right" may not compile. The teacher is tempted to write the
learner's code for them. Habits from a language the learner already knows can
be wrong in the new one. Idioms and tooling matter as much as syntax. This
use case adds the rules and skills for those traps.

It is **not** `_development`. That use case makes an agent build software.
This one makes an agent build a *programmer*. The learner writes the
code, and the agent's code is limited to examples, starter files and tests.

## What it provides

- `AGENTS.md`: the programming-teacher rules. Running code is the
  source of truth, official sources are pinned to a version, the learner
  types the solutions, the learner reads the error messages, idioms and the
  official tooling are taught from day one, tests become a habit, every
  module ends with a working program, and exercises stay safe.
- Skills:
  - `toolchain-setup`: get the learner's environment working. This covers the
    pinned toolchain, editor support, a first program, how to run, format,
    lint and test, and the workspace layout for the course.
  - `coding-exercises`: design exercises as runnable units. Each has a
    spec, a starter file, tests that fail on the starter and pass on a
    private reference solution, a likely mistake, and a variant. The
    progression runs from katas to mini-programs to the capstone.
  - `code-feedback`: review the learner's code. The agent runs it,
    runs the tests and the official linters, then gives correctness first,
    then idiom and design, pointing at lines and never rewriting the
    solution.

## Provisioning requirements

In addition to those of `_teacher`:

1. **Language and version**: pin the version (for example, Go 1.25).
   Lessons, idioms and features are checked against it.
2. **Programming background**: the languages the learner knows and how
   well, or "none". This drives the pace, the contrasts and the false
   friends.
3. **Target use**: what the learner wants to build (CLI tools, web
   back-ends, systems, data, games…). It shapes the module order, which parts
   of the standard library and ecosystem to cover, and the capstone.
4. **Environment**: OS, editor, whether the toolchain is installed, and
   whether the agent may run commands in the learner's workspace. The default
   is that the agent may run builds, tests and linters but must not edit the
   learner's solution files.

If the platform supports it, give the teacher a **shell** in the course
workspace (to run the learner's code and tests) and **web access** to the
language's official documentation.
