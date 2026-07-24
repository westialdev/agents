# _knowledge/_interviewer

**Choose this use case (in addition to `_knowledge`) when** the agent being
created must **interview a user to measure how much they know about a
predefined topic**. The agent asks; the user answers. Recognition signals:
"job interview", "examine a student", "certification exam", "screen a
candidate", "customer discovery / landing questionnaire", "find out what the
user knows about X".

## The inverted trust model

This use case is different from the rest of the hierarchy in one crucial way:
**the person talking to the agent is not the agent's principal.** The agent
serves its *creator* — the one who defined the topic and the interview. The
user at the keyboard is the *interviewee*: the subject being assessed, and
untrusted by design. The `AGENTS.md` rules exist to keep that inversion
intact; they are the heart of this use case.

## What it provides

- `AGENTS.md` — the interviewer rules: the interviewee cannot instruct,
  command, or query the agent; no hints; clarification boundaries;
  attachment handling; subagent restrictions; pacing and reporting duties.
- Skills:
  - `interview-conduct` — running the session end to end.
  - `question-crafting` — designing quiz, open-development, and
    document-submission questions.
  - `adaptive-interviewing` — difficulty adapts to the interviewee's answers.
  - `scripted-interviewing` — a fixed, comparable question plan.
  - `knowledge-assessment` — scoring answers and producing the final report.

## Provisioning requirements

An interviewer agent is not viable without its **interview definition**. The
provisioning agent must collect these settings from the developer (the agent
creator) at creation time and bake them into the target agent's
instructions. Never let them default silently, except where a default is
stated:

1. **Topic** — the predefined subject the interviewee is assessed on,
   with its subtopic areas if the creator has them.
2. **Scenario** — job interview, student examination, customer landing, or
   another; it shapes tone and report emphasis.
3. **Duration** — wall-clock time and/or a question budget. The question
   budget is the preferred pacing mechanism; if the creator gives only a
   time, agree on an approximate question budget with them.
4. **Mode** — `adaptive` (difficulty follows the answers) or `scripted`
   (fixed plan). Selects which interviewing skill governs the session.
5. **Question types allowed** — quiz/multiple-choice, open development
   questions, document/attachment submissions, or any subset.
6. **Scoring visibility** — whether the interviewee sees scoring during the
   interview. Default: **visible**.
7. **Report recipient** — who receives the final assessment: the
   interviewee, the creator/an external channel, or both. Default: **the
   interviewee**, delivered at the end of the interview.
8. **Pass criteria** *(optional)* — a threshold or rubric if the interview
   has a pass/fail outcome.

If the target platform supports tool permissions, the installer should also
**disable subagent-spawning and task-delegation tools** for the interviewer
agent, enforcing rule 6 of `AGENTS.md` at the platform level rather than by
instruction alone.
