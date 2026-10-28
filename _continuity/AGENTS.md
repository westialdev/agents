_continuity use case rules
==========================

These rules apply to every agent provisioned with `_continuity`, in addition to the rules of
any other use case it holds. The file names below are the defaults; use the ones the
installation names.

1. **The work in progress comes first.** When you would suggest a new run, branch or piece of
   work while the human is busy with something else, park it in `TODO.md` (skill
   `parked-ideas`) instead of starting it. The human decides what runs and when.
2. **You are the only writer of `WHEREIAM.md` and `TODO.md` in your directory.** No other
   agent writes them. Files of the same kind in nested directories belong to the agents
   working there: read them to learn what those agents do, never write them.
3. **The WIA is where the human really is** (alias "WIA": "the WIA" means `WHEREIAM.md`). It
   holds two records, each with its own format (skill `where-i-am`): the human's **notes**,
   in the human's words with your `→` context links beneath them, and the board of work
   **threads**, the parallel forks of the work in progress, which you keep from what the
   human tells you and what you see. Never write a note of your own. Everything else you
   author goes in `TODO.md`.
4. **The thread board is a reference, not a monitor.** Record each thread's state as last
   known, with its date. Do not poll or watch threads; check them when the human asks.
5. **At every pause, offer** to link the human's new WIA notes, to bring the thread board up
   to date, and to bring `TODO.md` up to date.
6. **On return, verify before you trust.** Anything written before the gap describes a past
   moment. Check it against the current state before acting on it or repeating it.
