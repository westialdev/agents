---
name: source-of-truth
description: >
  Find the best source of truth for any topic or claim: identify the source
  that owns each fact, rank sources by a trust hierarchy, follow citation
  chains upstream, detect circular citation, and say honestly when no unique
  source of truth exists. Trigger when researching a topic, verifying a
  claim, choosing between conflicting sources, or on "what is the
  authoritative source", "is this true", "where does this fact come from".
---

# Finding the source of truth

Every fact has an **owner**: the source where the fact is produced, not
merely repeated. The spec owns what the protocol does. The source code owns
what the program does. The measurement owns the value. The law's text owns
what is legal. The person owns what they said. This skill's whole doctrine
is: **do not stop at a source that heard it — reach the source that owns
it.** It is tool-agnostic: use whatever search, fetch, or archive access
the platform provides; most topics need web reach.

## The trust hierarchy

Rank every source you touch:

1. **Primary — the owner of the fact.** Specifications and standards,
   source code, original datasets and measurements, the original paper
   (for *what the authors found*), legal texts, official announcements,
   first-party documentation, the person or organization itself.
2. **Secondary — reporting on primaries.** Journalism citing named
   primaries, textbooks, review papers, reputable technical write-ups.
   Useful as maps to primaries and for interpretation; not as final
   evidence when the primary is reachable.
3. **Tertiary — aggregation.** Encyclopedias, SEO content, forum answers,
   LLM output, "top 10" listicles. Starting points only. A fact whose best
   available support is tertiary is an **unverified** fact.

Authority is **per class of fact**, not per publisher: a vendor is primary
for what its product is designed to do and weak for how the product
compares to competitors; a paper is primary for its own results and
secondary for its literature review.

## Working the chain

- **Follow claims upstream.** For each claim, ask who the current source
  got it from, and go there — repeat until you reach the owner or the
  chain dies. A chain that dies is a finding: record where and why.
- **Detect circular citation.** Ten sources agreeing is not ten sources if
  they all trace to one origin. Before counting agreement as evidence,
  trace each agreeing source upstream; collapse duplicates into their
  common origin and count *independent* origins only.
- **Version and date everything.** Facts have validity windows. Record the
  source's date/version and prefer, between equally authoritative sources,
  the one matching the time or version the question is about — newest is
  not automatically right for a question about an older state.
- **Prefer proximity.** Between two candidate sources of the same tier,
  prefer the one closer to the fact's production: the changelog over the
  blog post about the changelog, the court ruling over the summary of it.

## When there is no unique source of truth

Some questions genuinely lack one: contested science, active disputes,
matters of interpretation, predictions. The honest output there is not a
picked winner but the **map of positions**: the independent primary
positions, who holds each, on what evidence, and where the disagreement
actually sits. Saying "this is contested, and here is the shape of the
contest" is a successful research result; laundering a contested claim
into a flat fact is the failure mode this skill exists to prevent.

## Output discipline

Every delivered finding carries: the claim, its source, the source's tier
(primary/secondary/tertiary), why that source is authoritative for that
class of fact, its date or version, and — when agreement mattered — the
number of independent origins behind it. A finding you cannot dress this
way is not ready to deliver.
