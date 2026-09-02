---
name: tracker-conduct
description: >
  Act on the work tracker safely and in the owner's name: choose between a new
  comment and an edit, use state changes as signals, make sure the intended
  reader is actually notified, and verify what was posted arrived as written.
  Trigger whenever something is about to be written to or changed on a work item:
  "post this", "reply to them", "move the ticket", "add this to the task",
  "tell the team", or before publishing anything produced by the other
  `_owner` skills.
---

# Acting on the tracker

The tracker is the only channel the team has. Everything real happens here, and
the failures here are quiet: a message nobody was notified about, an edit nobody
saw, a record overwritten, a state that says the wrong thing. None of them
returns an error. All of them cost a delivery.

You are acting **in the owner's name**, on the owner's account. Post as if the
owner will be asked to defend every sentence, because they will be.

## Choosing the action

### The owner sees the text first

Show the owner the exact text before it is posted, unless they have said to post
directly. The reversibility gate does not catch this — a comment can be deleted
and a state can be moved back — but what it costs is not reversible: the message
went out over the owner's name, and the team has already read it and acted.

Posting directly is a standing permission the owner grants, for a kind of message
or for a session. It is not something to infer from their having liked the last
three.

### Adding work is always a new message

If the content adds anything the reader must act on, post a **new** message and
re-apply the state change. Never edit.

`tracker-channel` says why: a rewritten entry reaches nobody who has already read
it. The owner-side consequence is the part that gets forgotten — **re-apply the
state change too.** An earlier transition carries no signal about work added
after it, so an item that already moved once will sit exactly where it is while
the new work goes unread.

Edit only to correct something in work that has **not started**: a typo, a wrong
path, a broken link. Anything else is a new message.

### Know which call you are making

In many trackers, posting with an existing entry's identifier is an **update that
replaces the body**, not a reply. Read the API you are about to use, and check
whether the identifier you are passing means "in reply to" or "instead of".
Getting this wrong destroys a record that other people are working from.

Before any call that can overwrite, have the current content saved.

### The state is a signal

Moving an item is how another agent learns there is something to do. Move it when
the meaning changes — needs an answer, needs work, needs a decision — and never as
tidying. Leaving an item in a working state while it waits on a person is how
work silently stalls; so is leaving it in a waiting state after the answer landed.

State what state you are leaving the item in, in the message itself. The reader
should not have to check.

## Writing the message

- **One message, one purpose.** A review, a new instruction and a question are
  three messages. Merged, the reader acts on the first and misses the rest.
- **Lead with the decision.** The first line says what this is and what it means:
  accepted, rejected, blocked on an answer, new work added. The specifics follow.
- **Address the reader you need.** If a person must act, mention them the way the
  tracker actually notifies — a name typed as text notifies nobody.
- **Keep it self-contained.** Carry the essentials inline. A message that only
  works if the reader re-reads a long earlier one will be acted on without it.

## Formatting hazards

Prefer the simplest format the tracker accepts, and reserve the structured
document format for the part that genuinely needs it — usually only a mention.

When you must hand-build a structured payload, treat it as code:

1. **Validate it before sending.** Parse the payload with a real parser. Never
   send something you have only looked at.
2. Escaping is where this breaks. A single stray escape sequence — from a code
   sample, a shell snippet, a Windows path — makes the payload invalid.
3. **A tracker that cannot parse your payload may accept it as plain text and
   return success.** The result is a wall of raw markup where your message should
   be, and any mention inside it never becomes a mention, so nobody is notified.

## Verify after posting

Read back what you posted, every time:

- It rendered as intended, and is not raw markup.
- The mention exists as a mention.
- The state is what you intended to leave.

On failure, repair the same entry in place — correcting a broken post is exactly
the case where an edit is right — and never post a second copy alongside the
first. Then note that it was repaired, so the log reflects what actually reached
the reader.
