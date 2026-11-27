---
name: delegated-audit
description: >
  The expert's slice audit performed by an auditor subagent: when to dispatch it, the brief
  and the envelope it gets, running several audits in parallel, and checking the auditor's
  verdict before writing the review, ticking and delivering. Trigger when a devs session claims
  a slice ("slice done", "awaiting audit", a claim message with a sha), when an auditor
  reports back, and when an audit has run longer than expected.
---

# Delegating the audit

The parent pattern has the expert audit every slice itself. With several devs sessions that
puts every session's next slice behind every other session's audit. Here the expert dispatches
the audit to an auditor subagent and keeps what is the expert's: the brief, the check of the
verdict, the review file, the tick and the delivery. A fresh auditor also gives a reading that
is not anchored on the expert's own; that is a benefit only if the brief does not hand it the
expert's conclusion.

## Dispatch at once

When a claim arrives, dispatch its audit before anything else you are writing (`devs-roster`,
the order of answering). Note it in the roster's "waiting on" column with the time. Tell the
devs session it is under audit; that message is short and needs no REPLY REQUIRED block.

Run at most the number of parallel audits set at provisioning. Beyond that, queue in claim
order.

## The brief

Pass, verbatim, without summarising:

1. **The claim message** as the devs sent it.
2. **The `slice-audit` skill**, whole: the auditor follows it, steps 1 to 4. Step 5 (rule and
   deliver) is yours, not the auditor's.
3. **Where:** the repository, the devs' clone path, the claimed sha, the suite command as the
   project documents it, the acceptance item and its text.
4. **The rulings it must check against:** the answer files that bind this slice, and the
   contracts the session consumes, with their owners. Name them; do not paraphrase them.
5. **The roster row** of the session: the paths it owns. Any file touched outside them is a
   finding.

Do not pass your own opinion of the slice, or what you expect the verdict to be.

## The envelope

- Read-only on every devs tree. Writes only to scratch the auditor owns, outside every
  repository.
- No messages to any session; no commits; no ticks; no further subagents.
- It records `HEAD` and the working-tree status of the devs' clone before and after, and
  reports both.

## What comes back, and what you check

Require the report in this order: the verdict proposed (CLEARED or NOT CLEARED), the
reproduced figures with the exit status captured directly, the asserted file count of the
extract, `HEAD` and status before and after, each finding graded (blocking, non-blocking, for
awareness) with its evidence by file and name, and what it did not reproduce.

The report is model output, the auditor's and not yours. Before it becomes your review:

- **Check the instrument figures yourself** where they are cheap: the extract's file count is
  not zero, the exit status was captured directly, the devs' tree did not change.
- **Check every blocking finding against the code** before you put your name under it. A
  finding you could not confirm goes in as the auditor's, labelled so, or not at all.
- **Read what it did not reproduce.** An audit that skipped the suite has not cleared the
  slice, however clean the rest reads.
- A report that is missing a required part is a failed audit: dispatch again with the gap
  named, or audit that part yourself.

## Rule and deliver

Write the review file yourself, as `slice-audit` step 5 describes, citing the auditor's
evidence where you rely on it. Tick or hold. Deliver as `expert-rulings` describes: index,
commit, send to the session's current name, receipt. Update the roster.

## When the audit goes wrong

An auditor that returns nothing, runs long past its peers, or reports that it changed the
devs' tree: stop it, tell the devs session the audit is delayed and why, and decide whether
to dispatch again or audit yourself. A changed devs tree is reported to its owner at once.
