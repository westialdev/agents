---
name: done
description: >
  Completion workflow: run tests, code-review with subagent for refactor opportunities,
  optionally refactor, then commit. Trigger when user says a change is done, finished,
  or asks to commit. Also handles post-test-writing review with a separate subagent.
---

# Done — Change Completion Workflow

Run this skill when the user says a change is finished, completed, or asks to commit.

## Rules

1. **Tests must pass** before a change is considered complete.
2. **Code review** — after green tests, spawn a subagent to review the changed code for refactor opportunities.
3. **Test review** — after writing a new test, spawn a subagent to evaluate test quality.
4. **Commit** — only after tests pass (and any approved refactor passes tests again).

---

## Step 1 — Run tests

Run the project's test command. For this project: `pnpm run test`.

- If tests **fail**: stop. Report failures. Do not proceed to review or commit.
- If tests **pass**: proceed to Step 2.

---

## Step 2 — Code review (subagent)

Spawn a **code-review subagent** focused on the changed files (use `git diff` to identify them).

Brief the subagent:

> Review the following changed files for refactoring opportunities. Focus on: duplication, overly complex logic, naming clarity, abstraction leaks, and opportunities to simplify without changing behavior. Do NOT suggest adding features or changing architecture unless there is a clear maintainability problem. Return a concise list of specific suggestions with file paths and line numbers. If nothing meaningful can be improved, say so explicitly.

Subagent returns findings.

- If **no meaningful improvements**: skip to Step 4.
- If **improvements found**: go to Step 3.

---

## Step 3 — Present refactor plan

Present the subagent's findings to the user as a numbered plan. Ask:

> "The reviewer found these refactor opportunities. Do you want to proceed with any of them? [Y/N or select numbers]"

- If user **declines**: skip to Step 4.
- If user **approves**: implement the approved items, then re-run tests (Step 1). If tests fail after refactor, fix before proceeding. Once green, go to Step 4.

---

## Step 4 — Commit

The commit message must:
- Start with the task key, followed by a space and then the message. Extract that key from the branch name; it is a {word}-{number}, like `SK-1234`.
- Summarize *what* changed
- Include a short body explaining *why* if the reason isn't obvious from the subject line

---

## Test review (when a new test was just written)

If the user just wrote a test (or asks to review a test), spawn a **test-review subagent** before Step 2.

Brief the subagent:

> Review this test for quality. Check: (1) Does it test behavior, not implementation details? (2) Does it cover a realistic path a user or system would actually trigger? (3) Is it stable — would it pass consistently without relying on timing, order, or mocks that don't reflect real behavior? (4) Is it effective — would it catch a real regression? (5) Is it free of redundancy with existing tests? Return specific findings with file and line references. If the test is solid, say so.

Present findings to user. If the subagent finds the test is weak or brittle, ask user whether to revise before proceeding.

---

## Notes

- Never commit with failing tests.
- Never skip the code review subagent step — even for small changes.
- If `npm test` is not the right command for the project, use whatever the project's test script is.
- If there are no staged or changed files, ask the user what they want to commit before proceeding.
