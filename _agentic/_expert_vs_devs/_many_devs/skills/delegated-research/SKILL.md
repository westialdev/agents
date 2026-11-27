---
name: delegated-research
description: >
  Handing a devs session's factual question to a researcher subagent — how an external API
  behaves, what existing code does, where a value is configured — and turning its cited answer
  into the expert's ruling. Trigger when a round from a devs session asks for a fact that
  needs reading across code, contracts or documents rather than a judgement — "what does the
  API return here", "where is this set today", "does the old service do X" — and when a
  researcher reports back.
---

# Delegating the research

Many questions from the devs are not design questions but facts: what an endpoint accepts,
what the old code does on a retry, which file holds a setting. Answering them means reading
widely, and reading widely fills the expert's context with file dumps that crowd out the
roster and the rulings. A researcher subagent reads instead, and the expert keeps the
conclusion.

## Is it research?

Research when the answer is a fact someone could check in a source: code, a contract, a
document, a record. Not research when the answer is a choice: a design, a trade-off, a scope,
a value judgement. A choice is the expert's, or the human's (`expert-rulings`). A round often
holds both: split it, dispatch the facts, and rule on the choice once they are back.

## The brief

Pass, verbatim: the devs' question as written in their round file, the sources to read (paths,
repositories, documents, by name), and what is out of scope. Ask for:

- the answer, in one or two sentences;
- the evidence: each fact with its source, by file and name (a line number only where the
  file is not the devs' and will not move under them);
- what it could not determine, and every point where it guessed.

Do not pass the answer you expect.

## The envelope

Read-only everywhere. No messages to any session, no commits, no writes to any repository, no
further subagents, nothing outside the sources named unless the brief allows it. It may not
call a live system to find out how it behaves unless the human has granted exactly that.

## Turning the answer into a ruling

The researcher's report is model output, not a fact yet.

1. Check the evidence that the ruling will rest on: open the cited source and confirm it says
   what the report says. A fact you could not confirm is written as *unverified* in the answer
   file, with its source.
2. Write the answer file yourself (`expert-rulings`): the fact, its source, what remains
   unverified, and the ruling if the round also asked for one.
3. Deliver it to the asker. If the fact matters to other devs sessions, deliver it to them too,
   in the same turn, and note them in the DELIVERY line (`devs-roster`).

A fact that contradicts an earlier answer is a correction: sweep every copy, as
`expert-rulings` describes.
