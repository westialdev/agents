---
name: toolchain-setup
description: >
  Get the learner's programming environment ready before the first lesson:
  install the pinned language toolchain from its official source, set up
  editor support, lay out the course workspace, and have the learner run
  their first program, the formatter, the linter and the test runner. Trigger
  at the start of a programming course, when the toolchain is missing or
  broken, or when the learner asks "how do I install / run / test this".
---

# Toolchain setup

The first lesson is the first program running on the learner's own machine.
Nothing else can be practised until that works.

## Steps

1. **Check what is there.** Ask the learner to run the version command for
   the language, or run it yourself if allowed. Compare the result with the
   pinned version.
2. **Install from the official source** if it is missing or too old. Use
   the language owner's download page or install instructions for the
   learner's OS (`_programming_language` rule 2). Mention the OS package
   manager only if it ships the pinned version. Give the commands, let the
   learner run them (`_programming_language` rule 5), and explain each one in
   a line, including any PATH change.
3. **Editor support.** Recommend the official or most authoritative
   language server and editor extension for the learner's editor, and
   enable format-on-save. If the learner wants to stay with a plain editor,
   respect that and teach the command-line formatter instead.
4. **Lay out the workspace**:
   ```
   <course folder>/
     README.md          learner's index: modules, how to run things
     lessons/NN-topic.md
     exercises/NN-name/ starter + tests, the learner's solution goes here
     playground/        free experiments
     capstone/
   ```
   Answer keys and the journal live in the private location, not here.
5. **First program.** The learner writes and runs "hello, world" by typing it,
   not pasting it. Then they deliberately break it (remove a brace, misspell
   a name) and read the error (`_programming_language` rule 4).
6. **The daily commands.** Show the learner how to run, build, format, lint and
   test, each once, on the hello program. Write them into the course
   `README.md` as a cheat sheet.
7. **Record** the environment and version in the journal.

## When something fails

Read the actual error with the learner. Do not guess. Check the
official troubleshooting documentation before improvising. Never suggest
disabling security features or running the toolchain as root to get
past an install problem.
