# Take-home tech tests

A take-home is the one thing a web tool cannot give the user: a real repo, in the real stack, reviewed the way a hiring panel reviews it. Build it properly.

## Designing the task

Derive the task from the role profile. The task should look like a slice of the actual job:

- **Backend roles:** a small service with a real data model and one or two non-trivial rules. A payments company gets a ledger with idempotent transfers. A logistics company gets a route-assignment service with capacity constraints.
- **Frontend roles:** a small UI against a provided API or fixture data, with one piece of tricky state (optimistic updates, pagination with filters, a form with dependent fields).
- **Full-stack:** a thin vertical slice of both.
- **Data roles:** a pipeline over a provided messy dataset with a couple of quality traps, plus a query or two that need thought.
- **Infra or platform roles:** a deployable thing with a health check, config, and a failure to handle gracefully.

Constraints that make it realistic:

- **Time budget.** Real take-homes say "3 to 4 hours". State one and design for it. The task should be finishable in that time at the target level, with obvious places to go further. Check yourself: a four-hour brief has roughly two core requirements plus tests and a README. If you have listed a grid, a form, optimistic updates, keyboard navigation, and a stretch section, that is a two-day task wearing a four-hour label, and the candidate learns nothing except that they ran out of time. Cut until it fits, and move the rest to "if you have time".
- **One hard part.** A good take-home has one thing that separates candidates. Everything else is table stakes. Identify the hard part before writing the brief and make sure the rubric weights it.
- **Ambiguity on purpose.** Leave one requirement slightly underspecified so the candidate has to make and document a decision. Seniors are expected to notice and call it out.
- **Domain from the posting.** Use the company's domain for the scenario. It makes practice transfer better.

## What to build

Create `interview-prep/<slug>/take-home/` containing:

```
take-home/
├── BRIEF.md            the task as the company would send it
├── README.md           how to run the starter
├── .rubric/RUBRIC.md   hidden grading rubric (tell the user not to read it until after)
└── <starter project>   minimal working scaffold in the JD's stack
```

**BRIEF.md** should read like a real one. Company voice, a short scenario, functional requirements as a list, non-functional expectations (tests, README, how to run), the time budget, what to submit, and what they will evaluate. Do not include hints that a real company would not include.

**The starter** should be minimal but runnable: project file, one entry point, a test setup that runs and passes on an empty test, fixture data if the task needs it. Use the versions and tools the JD names. If the JD is not specific, pick the mainstream choice and say so in the README. Verify it runs before handing it over.

**RUBRIC.md** is what the panel would grade against. Write it before the brief is final so the brief actually tests what the rubric scores. Sections:

- Correctness (does it meet the requirements, does the hard part work)
- Code quality (structure, naming, appropriate abstraction for the size)
- Tests (present, meaningful, cover the hard part)
- Handling of the ambiguous requirement (noticed, decided, documented)
- Communication (README, commit messages if any, notes on trade-offs)
- Level-specific expectations: what a mid, senior, or staff submission looks like differently

Weight the hard part. A rubric where every line is worth the same lets a polished-but-shallow submission win.

## Handing it over

Tell the user:

- Where it is and how to run the starter
- The time budget, and suggest they actually time it
- Not to read `.rubric/` until they are done
- To say "done" or "review my take-home" when finished

## Reviewing the submission

When the user says they are done, review it as a hiring panel would, not as a code reviewer helping a colleague:

1. Read the rubric.
2. Run it. Run the tests. If it does not run, that is the first finding and it is serious.
3. Read the code with the rubric open. Note evidence for each rubric line.
4. Check the ambiguous requirement: did they notice, decide, document.
5. Write the review to `interview-prep/<slug>/take-home/REVIEW.md`:

```markdown
# Take-home review — <date>

Graded against: Senior
Time reported: 3h 40m

## Verdict
Advance / borderline / do not advance. One paragraph on why.

## Rubric
| Area | Score (1-4) | Evidence |
|---|---|---|
| Correctness | 3 | Transfers are idempotent; concurrent transfers on the same account can double-spend (see ledger.go:42) |
| ... | | |

## What a panel would say in the debrief
Three to five bullets in the voice of a hiring panel. Honest.

## If you had another hour
The highest-value things to change, in order.
```

6. Append the result to `progress.md`.

Be direct. A submission that would not advance should be told so, with the specific reasons, because that is exactly what the user needs to hear before the real one.
