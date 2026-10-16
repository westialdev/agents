---
name: review-beyond-the-stubs
description: >
  Review pass for the bugs a green test suite cannot see: clocks, latency against
  a deadline, deployment artifacts, durable state, external-data units, and metered
  cost. Trigger after tests pass and after the refactor-focused review, before
  committing anything that runs unattended, touches money, or talks to an external
  system.
---

# Review beyond the stubs

**Tests stub the world. This pass reviews the gap between the stub and the world.**

Every item below is a bug that reached production in a codebase with a green suite —
1,600+ passing scenarios in the cases that produced this list. **Not one was a
refactoring problem**, which is why a review briefed on duplication, naming and
abstraction leaks found none of them.

Run this **in addition to** the refactor review, not instead of it. They look for
different things.

---

## How to run it

For each section, answer the question against the actual diff. **"The tests pass"
is never an answer** — the whole premise is that they passed while the bug shipped.

Report findings as: what breaks, under what real-world condition, and what the
green suite saw instead.

---

## 1. Clocks and time

**Question: can a naive datetime meet an aware one?**

- Does any use-case code build an instant itself — `datetime.combine`,
  `datetime.now`, `date.today`, `utcnow` — instead of asking an injected clock?
  **An injected clock only helps if nothing constructs time beside it.**
- Is there a test that drives the path with a **genuinely timezone-aware** clock?
  A frozen double is internally consistent — naive-vs-naive compares fine — so it
  is **structurally blind** to the mismatch.
- Is DST covered on **both sides** of a transition? An offset that is right in
  July and wrong in January is the normal shape of this bug.
- Does a deadline comparison mix a wall-clock instant with a config `time`?

> *Incident: an availability guard compared an aware `now_et` against a naive
> `datetime.combine(...)`. It crashed on all 15 ticks inside a 15-minute window,
> on the first armed night. The clock ABC already existed and was bypassed.*

---

## 2. Latency against a deadline

**Question: has the cost been measured against the real deadline, or estimated?**

- Does the change loop over an external call where a **batched** form exists?
  Per-item round-trips are invisible in tests and fatal against a window.
- Is there a **measured wall clock** on real infrastructure — not a projection?
- Does the deadline path have a **guard that refuses rather than acting late**?
- Does the measurement use the **heaviest realistic input**, not a convenient one?

> *Incident: a nightly fetch made one API call per symbol — 627 seconds against a
> 120-second auction window. It would have missed every night, silently. Every test
> stubbed the gateway, so latency did not exist in the suite. Batched: 7.9 seconds.*

---

## 3. Deployment artifacts versus source

**Question: does the running artifact contain this change?**

- Is there a frozen venv, wheel, image or bundle that must be **rebuilt** before the
  fix is live? A committed fix is not a deployed fix.
- After rebuilding, is a **symbol from the change verified present** in the artifact?
  Not "the install succeeded" — check for the thing you added.
- Could a stale build be selected accidentally (`ls -t`, `latest`, a cached layer)?

> *Incident: a rebuild used a wheel built minutes earlier, before the fix committed.
> The install reported success and the artifact still crashed. Caught only by probing
> for the new method by name.*

---

## 4. Durable state written from unavailable inputs

**Question: can "not available yet" be persisted as a real observation?**

- If an input is missing because it **does not exist yet**, does the code write a
  zero, an empty, or a default into durable state? **"No data" is not a value.**
- Does a rolling window, running total or history get polluted by such a write?
  A single bad entry can corrupt a statistic for its whole window length.
- Is there a **guard that HOLDS** — no fetch, no computation, no persistence —
  before the input can exist?
- On a degraded path, is the append **skipped**, not merely flagged?

> *Incident: a tick fired before the minute bar it reads had closed, so every name
> returned nothing, breadth read 0, and a first-write-wins append stamped that zero
> into a 125-night rolling quantile. Every night. Nothing in the logs looked wrong.*

---

## 5. Observability must not change behaviour

**Question: can the monitoring break the thing it monitors?**

- Is any monitor, metric or log call on the **critical path** between a decision and
  its action?
- If the monitoring backend is slow, throttled or down, does the system behave
  **identically**? Is there a test that proves it — a monitor that raises, and a
  byte-identical decision?
- Does monitoring consume a **deadline budget** it should not?

**Note the deliberate tension with "errors must explode":** observability is the one
place where swallow-and-log is correct, *because* the alternative is a monitoring
outage becoming an outage. State that exception explicitly where it is taken, or the
next reader will read it as a guideline violation — which it otherwise is.

---

## 6. Metered cost and unbounded cardinality

**Question: does any per-item value become a key in something you pay for?**

- Metrics priced per unique name+dimension: is a **rotating identifier** — symbol,
  user, request, tenant — used as a dimension? That is unbounded growth, billed
  monthly, for series written once.
- Do dashboards, alarms or annotations get **rewritten per event**? Definition
  bodies have size limits and will silently stop accepting.
- Is retention set explicitly, or is it "forever" by default?
- Does enabling the feature start spend, and is it **default-off**?

> *Incident: nearly shipped symbol-as-a-dimension on a book holding twenty rotating
> names a night — thousands of metrics a year, each written once, each billed.*

---

## 7. Persisted configuration versus code configuration

**Question: what happens when a constant changes and state holds the old value?**

- Is a config or consent value **copied into durable state**? Then a code change
  makes the two disagree.
- Does the system **detect** the disagreement and fail closed, or act on the stale one?
  (Failing closed is right — but then amending the constant requires a state migration
  or reset, and that path should exist deliberately rather than be discovered.)
- Is there a documented way to amend it while the system is live?

> *Incident: a consent envelope persisted in the journal. Raising a cap in code made
> the machine refuse every tick — correctly — until the journal was reset. Fine while
> flat; genuinely awkward mid-position.*

---

## 8. Units, bases and ratios in external data

**Question: are both sides of every comparison on the same basis?**

- A **ratio** of two prices, sizes or times: same adjustment, same currency, same
  timezone, same units? Mixing bases inside a ratio does not error — it produces
  plausible, wrong numbers.
- Split/dividend adjustment, sampling interval, inclusive/exclusive bounds, and
  time-of-day conventions all differ between endpoints of the same vendor.
- Is the basis **stated at the boundary** where data enters?

> *Incident: a fade ratio nearly mixed a raw intraday high with a split-adjusted
> price. On split days it would have manufactured enormous fake signals — and looked
> like a stronger edge, not an error.*

---

## 9. The meta-check

**Ask: what does this code assume about the world that no test in this repo can check?**

Then say so in the review, even without a fix. **The value is naming the assumption**,
because that is what nobody wrote down and what the next incident will be about.

---

## What this pass is NOT

Not style, not naming, not duplication, not architecture — the refactor review owns
those. **If a finding here would survive a perfect refactor, it belongs here. If it
would not, it belongs there.**
