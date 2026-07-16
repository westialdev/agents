---
name: development-guidelines
description: >
  Development philosophy for all source code generation: error handling and
  TDD (red-green-refactor). Trigger whenever writing, generating, or modifying
  code in any programming language: functions, modules, classes, packages,
  scripts, or any other unit of source code.
---

# Development Guidelines

Apply these rules to every piece of code generated or modified.

## Examples — read only your language's file

Code examples live in [`examples/`](examples/), one file per language, each
mirroring the section headings below:

- [`examples/typescript.md`](examples/typescript.md)
- [`examples/python.md`](examples/python.md) — testing examples use Gherkin with [behave](https://behave.readthedocs.io/)

**Load only the file for the language you are writing.** If the task is in
Python, open `examples/python.md` and do not open the others; if it is in
TypeScript, open `examples/typescript.md`. The pointers under each section below
("see the per-language example files") mean *your* language's file only — they
are not an instruction to read every file. This keeps context small: the base
guidance is always loaded, but per-language examples load on demand.

When adding a new language, add a matching `examples/<language>.md` that mirrors
these same sections.

## Core principle: errors must explode

An error is an error. Never treat an error condition as a warning and continue
normal execution.

When the runtime detects an invalid state — null/None where a value is required,
a missing key, a failed assertion, an unexpected type, an out-of-range value, or
any other broken invariant — the process must raise an exception immediately.

**Never**: log a warning and continue. Never return a default value to silently
paper over a missing required input. Never swallow an exception and proceed as
if nothing happened.

**Always**: raise. Hard. Make the failure visible and traceable.

---

## Exception strategy

### Use a custom exception when:

- The error is domain-specific and callers may want to catch it selectively.
- The error carries context that a generic exception cannot express (e.g.,
  which field was null, which ID was not found, what invariant was violated).
- The module/package has its own exception hierarchy.

In these cases, define or use an existing custom exception class and raise it
with a descriptive message and any relevant context values. See the
["Exception strategy — custom exception"](examples/) section in the per-language
example files.

### Use a runtime/built-in exception when:

- The condition represents a programmer error (wrong argument, contract
  violation) rather than a recoverable domain condition.
- No custom hierarchy exists and defining one would be premature.
- The goal is to crash the process loudly and immediately.

Use the language's standard hard-fail mechanism:

| Language   | Preferred mechanism                                        |
|------------|------------------------------------------------------------|
| TypeScript | `throw new Error(...)`                                     |
| Python     | `raise ValueError(...)` (bad value) / `raise TypeError(...)` (wrong type) |

---

## Null / None / missing value checks

Every required value received from outside the current function's control
(parameters, config, external API responses, database results) must be
validated before use. See the ["Null / None / missing value checks"](examples/)
section in the per-language example files.

Do not rely on the language to throw a NullPointerException / AttributeError
downstream — check early, fail early, with a message that names the missing
value.

---

## What NOT to do

The banned patterns — silently continuing with broken state, swallowing an
exception, and logging-and-returning-null — plus the GOOD "raise immediately
with context" counterpart are shown in the ["What NOT to do"](examples/) section
of the per-language example files.

---

## Summary rules — error handling

1. **Validate early** — check required values at the entry point of the function.
2. **Raise with context** — include the offending value and what was expected.
3. **Custom exception for domain errors** — use or define one when the caller
   might need to distinguish this failure from others.
4. **Runtime exception to crash** — use built-in hard-fail types when the error
   is a programmer contract violation.
5. **Never swallow** — bare `except: pass`, silent `catch`, or `recover()` that
   discards the error are banned unless there is an explicit documented reason.
6. **Never warn-and-continue** — a log line is not error handling.

---

## Enums for classification values

When a value belongs to a **fixed, known set of classification options**, model it
as an enum — never as a bare string, magic number, or free-form constant. If the
use case is clear, reach for an enum instead of a primitive.

### Create an enum when:

- The value is one of a **repeating, finite set of categories** — a type, kind,
  status, stage, family, mode, or role (e.g. `ModelFamily`, `JobKind`, `Stage`).
- The same set of literal values appears in **more than one place**, or is
  compared against string/number literals scattered through the code.
- The value maps to a **term in the Ubiquitous Language** (`doc/UBIQUITOUS.md`) —
  the enum members should carry the exact glossary names.
- Invalid values should be **impossible to construct**, not merely validated at
  runtime.

Prefer string-backed enums so the serialized value stays readable and stable.
See the ["Enums for classification values"](examples/) section in the
per-language example files for the magic-string (BAD) vs closed-set (GOOD)
contrast.

### Do NOT force an enum when:

- The set of values is **open-ended or user-supplied** (free text, arbitrary
  identifiers, external IDs).
- There is a **single, one-off** value with no sibling categories and no
  repetition.
- The values come from an **external system** whose set you do not control and
  which may add members without warning — validate at the boundary instead.

### Rules — enums

1. **Repeating classification → enum** — if a value names a category and recurs,
   it is an enum, not a string.
2. **Name from the glossary** — enum members use Ubiquitous Language terms; add
   new crucial terms to `doc/UBIQUITOUS.md`.
3. **String-backed** — back enums with stable, readable strings for
   serialization.
4. **Exhaustive handling** — switch/branch over all members; make unhandled
   members a compile-time or hard-fail error, never a silent fall-through.

---

## Test-driven development — red-green-refactor

All new code must be written test-first. No production code without a failing
test that justifies it.

### The cycle (ONE TEST AT A TIME)

**CRITICAL**: You work on ONE test at a time. Never write multiple tests before
implementing. Never implement multiple tests' worth of code at once.

For each test:

1. **Red** — write ONLY ENOUGH of ONE test to fail (compilation failures count).
   The test must fail for the right reason (missing behavior, not a syntax error
   or wrong import). Run the test suite and verify this specific test fails.

   **Rule**: Write no production code unless it makes a failing unit test pass.

2. **Green** — write ONLY ENOUGH production code to make THIS test pass. No more.
   Write only enough code to pass the current failing test. Run the test suite
   and verify this test now passes.

   **Rule**: Write only enough production code to pass the one failing test.

3. **Refactor** — clean up both production code and test code if needed. Run the
   FULL test suite and verify ALL previous tests still pass. If any test breaks,
   fix it immediately or revert the refactor.

4. **Repeat** — Move to the next test. Start at step 1.

**Three Laws of TDD**:
1. Write no production code unless it makes a failing unit test pass.
2. Write only enough of a unit test to fail (compilation failures count as failures).
3. Write only enough production code to pass the one failing test.

Never skip red. Never write multiple tests before implementing. A test written
after the code is not TDD — it is documentation at best, false confidence at worst.

For a worked red→green→refactor cycle in each language, see the
["Test-driven development"](examples/) section of the per-language example files.

---

### Planning TDD tasks — how to structure todo lists and task plans

When breaking down work into tasks or todos, **mirror the cycle exactly**. Each
behavior gets its own RED→GREEN pair. Tasks are never batched by phase.

**WRONG — phases batch multiple behaviors together:**
```
- [ ] Write all RED tests for feature X
- [ ] Implement all production code (GREEN)
- [ ] Refactor
```

**CORRECT — each behavior is its own cycle:**
```
- [ ] RED: write test for [behavior 1] — run it, verify it fails for the right reason
- [ ] GREEN: implement [behavior 1] — run tests, verify this test passes
- [ ] RED: write test for [behavior 2] — run it, verify it fails for the right reason
- [ ] GREEN: implement [behavior 2] — run tests, verify this test passes
- [ ] REFACTOR: clean up if needed — run full suite, verify all green
```

Each RED task is immediately followed by its GREEN task. **Never create a task
that says "write all tests", "write multiple tests", or "implement all X".** If
you catch yourself writing such a task, split it into individual behavior cycles.

A task plan that groups all tests before all implementation is not TDD planning —
it is waterfall with test files.

---

### Test pyramid — priority order

1. **Unit tests** — fast, isolated, no I/O. Test one unit of behavior.
   These are the majority of the test suite.
2. **Integration tests** — test collaboration between two or more real
   components (e.g., service + real DB, two modules talking to each other).
   Fewer than unit tests.
3. **End-to-end tests** — test the full system from the outside.
   Fewest. Expensive. Only for critical paths.

Default to unit tests. Reach for integration only when the interaction between
components is the thing under test. Reach for E2E only for high-value user
journeys.

---

### Mocking — what to mock and what not to

Mock **irrelevant actors**: external services, I/O boundaries (HTTP clients,
database drivers, file system, message queues, clocks), and collaborators
outside the unit under test.

Do **not** mock the subject under test. Do not mock value objects or pure
functions. Do not mock just to avoid writing real code.

**The key test**: if the mock is the only thing being exercised, the test is
worthless. A test that asserts `mock.returns(x)` and then verifies `result == x`
proves nothing. Every test must verify real behavior of real code. The
mock-return (BAD) vs real-logic (GOOD) contrast is shown in the
["Mocking — what to mock and what not to"](examples/) section of the
per-language example files.

Use high-level mocking libraries:

| Language   | Preferred mocking tool                          |
|------------|-------------------------------------------------|
| TypeScript | Jest (`jest.fn()`, `jest.spyOn()`) / Vitest     |
| Python     | `unittest.mock` (`Mock`, `MagicMock`, `patch`)  |

---

### Architecture for testability

Design code to be testable from the start. The two tools that make this
possible are **dependency injection** and **polymorphism**.

**Dependency injection**: pass collaborators in — do not instantiate them
inside the unit. A constructor or function that creates its own database
connection, HTTP client, or clock is untestable in isolation. See the
["Architecture for testability — dependency injection"](examples/) section in
the per-language example files for the hardwired (BAD) vs injected (GOOD)
contrast.

**Polymorphism**: depend on interfaces/abstract types, not concrete
implementations. In tests, pass a fake or mock that implements the same
interface. In production, pass the real implementation. See the
["Architecture for testability — polymorphism"](examples/) section in the
per-language example files.

When a class or function is hard to test, treat that as a design smell — not
a reason to write fewer tests. Refactor toward DI and interfaces.

---

## Summary rules — TDD

1. **Red first** — no production code without a failing test.
2. **Minimum green** — write only enough code to pass the test.
3. **Refactor freely** — tests are the safety net; keep them green.
4. **Unit > integration > E2E** — default to the fastest, most isolated layer.
5. **Mock boundaries, not behavior** — mock I/O and irrelevant actors; never
   mock the thing you are trying to test.
6. **No mock-return tests** — a test that only verifies a mock's return value
   is not a test.
7. **DI and interfaces** — design for injection from day one; hard-to-test code
   is a design problem.
