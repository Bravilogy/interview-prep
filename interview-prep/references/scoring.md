# Running and scoring a mock interview

## Conduct

You are the interviewer for the duration of the round. Stay in that frame:

- One question at a time. Ask it, then stop and wait. Do not show the list.
- Do not answer your own question. If the user stalls, do what a real interviewer does: rephrase once, or ask "what would you look at first?" Then wait again.
- Follow up when a real interviewer would. If the answer was strong, push one level deeper. If the answer was vague, ask for a specific example. If the answer was wrong, do not correct it yet. Note it and move on, or probe once to see if they catch it.
- Keep the interviewer's tone: neutral, polite, brief. No "great answer!" between questions. Feedback comes after each answer in a clearly separated block, then you return to interviewer mode.
- If the user asks to skip a question, let them, score it as skipped, and move on.
- If the user breaks frame to ask a meta question ("how am I doing?", "what's the answer?"), answer briefly and return to the interview.

## Scoring each answer

Score 1 to 4 and say which:

| Score | Meaning |
|---|---|
| 4 | Would clearly pass at this level. Specific, correct, shows judgment. |
| 3 | Would probably pass. Correct but missed a dimension a strong candidate would cover. |
| 2 | Borderline. Partially correct, vague, or answered a different question. |
| 1 | Would not pass. Wrong, empty, or a red flag. |

After the score, give feedback in this shape, and keep it to a few lines:

```
**Score: 3/4**
What worked: you identified the idempotency key approach and explained where to store it.
What was missing: a real interviewer would expect you to mention what happens when the key store itself is unavailable.
Stronger version: "...one sentence of what a 4 sounds like."
```

Then continue: the follow-up if there is one, otherwise the next question.

## Calibrating the score

Score against the level in the role profile, not against perfection. A mid-level candidate who gives a clean, correct answer without discussing failure modes gets a 4 for a mid role and a 3 for a senior role. Say which level you are grading against at the start of the round.

Be honest. A user who gets a 4 on everything learns nothing. If most answers are 2s, say so plainly in the summary; that is useful information before the real interview.

## End-of-round summary

Write to `interview-prep/<slug>/round-<n>-<type>-results.md`:

```markdown
# Round 2 results: Technical — <date>

Graded against: Senior

| Q | Topic | Score |
|---|---|---|
| 1 | Idempotent payment retries | 3 |
| 2 | ... | ... |

Average: 2.8 / 4

## Would this pass?
One honest paragraph. Yes, borderline, or no, and why.

## Work on these three things
1. Specific gap, with what a strong answer includes.
2. ...
3. ...

## Questions to revisit
List the question numbers scoring 2 or below so they can be re-asked next session.
```

Then append a line to `progress.md`: date, round type, average score, the three weak areas as short tags. Later sessions read this to bias question selection.

## Non-interactive mode

If there is no user to answer (for example, the skill is being run to generate material rather than to interview), do not simulate a fake candidate. Produce the question set instead and note that the mock needs a live session.
