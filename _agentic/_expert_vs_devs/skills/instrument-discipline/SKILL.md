---
name: instrument-discipline
description: >
  How to trust a check before trusting what it says: suspecting the instrument
  before the subject, counting the artefact instead of the text about it,
  citing by name across an ownership boundary, deriving bounds, and sourcing
  external limits. For both sessions. Trigger whenever a count, a search
  result, a citation, a bound, a wall-clock claim or an external limit is about
  to be stated as a finding — "grep shows", "there are N", "the limit is",
  "nothing matched", "fires at", "see line".
---

# Trusting the instrument

Every finding is produced by an instrument — a search, a count, a script, a
test. The dangerous instrument is not the broken one that errors; that one is
harmless, because it announces itself. It is the broken one that **answers**:
it returns something plausible, and the plausible answer is read as a fact about
the subject. In every case this skill was written from, the subject was sound
and the instrument was wrong.

Two defences worked, and nothing else did: **read the artefact whole** rather
than trusting a pattern match, and **make the instrument assert something about
itself** — a generator that asserts it produced `n` distinct values, an extract
that asserts its file count, a rig that scores a traceback as a failure rather
than a kill.

## An empty answer is an answer

A search that returns nothing, a date filter that did not parse, a count of
zero: each is a claim that the instrument worked. When an instrument returns
nothing, suspect the instrument before the subject — check it against a case you
know must match.

## Count the artefact, never the text about it

A text search cannot tell a configuration key from a comment describing it, an
assertion from a comment quoting it, or a call site from a docstring naming it.
Files that document themselves heavily are exactly where it misleads most. Count
with a parser, or list the items and count the list.

A line-oriented tool cannot see a span across lines: a strike-through opened two
lines above leaves the middle line looking live. Sweep by position against the
spans.

## Matching words are not matching claims

Two sentences that share a phrase — "five minutes after the cross" — may be about
two different events. No search catches this; only reading the subject does.

## Cite by name across an ownership boundary

A line number into a file you do not own dangles on its owner's next edit, and
then points at something else, silently. Cite the document, section, function,
row or scenario by name.

## Derive a bound; never assert one

A bound is derived from a measured distribution or a stated deadline, and shown.
A conservative floor rounds **up**: truncating toward optimism is the one error a
floor may not make. A sample every minute supports an upper bound, not an
instant. "The largest seen" is a maximum only if you looked at all of them.

## Wall-clock claims, in both regimes

When a timezone is involved, compute the claim in both daylight-saving regimes,
and check both transition nights. An hour chosen at one season's offset can hold
for seven months and fail every winter.

## An instrument does not certify the system

An instrument may write a claim about the system into its own output — and then
be read back as evidence for that claim. What an instrument measured is
evidence; what it asserts about the system needs a source outside the
instrument before anything is built on it.

## Change the instrument or compare, not both

Do not change an instrument between two runs and then compare the results. The
difference is as likely to be the instrument as the subject.

## External limits from their owner

A limit of an external service — a retry ceiling, a quota, a maximum age — is
taken from the provider's own documentation or model for the service that owns
the resource, not from memory, and not from a neighbouring service that happens
to share the vocabulary.
