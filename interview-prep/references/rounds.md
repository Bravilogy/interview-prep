# Round types

How to write questions for each round. Read the role profile first: every question here should be shaped by the stack, domain, seniority and signals you extracted.

## Question file format

Each round file follows this shape so results and progress files can refer back to question numbers:

```markdown
# Round 2: Technical — Acme, Senior Backend Engineer

Format: 60 minutes, one engineer, screen share likely.
Focus: Go services, Postgres, Kafka, payments domain.

## Q1. <question as the interviewer would say it>
**Why they ask it:** one line on what this probes.
**Strong answer covers:** 3 to 5 bullets. Concrete, not "demonstrates understanding".
**Follow-ups:** 1 to 3 probes a real interviewer would use if the first answer was good.
```

The "why they ask it" line matters. Candidates who understand what a question is testing answer it better, and it keeps you honest about whether the question is actually testing anything.

## Recruiter or hiring manager screen

20 to 30 minutes. The goal is fit and motivation, not depth.

- Why this role, why this company, why now. Tie to what the posting emphasises.
- Walk through the CV with a focus on the most relevant role.
- Salary expectations and logistics (include one so the user rehearses it).
- One or two light technical sanity checks: "what did you build most recently with X".
- What questions the candidate should ask back. Include three good ones based on the posting.

Keep answers short. The strong-answer bullets for this round are about structure and framing, not technical content.

## Technical

45 to 60 minutes. Tests whether they can do the job described.

Mix these, weighted by seniority:

- **Conceptual.** "Explain how X works" questions on the core stack. Juniors get more of these.
- **Applied.** "You have this situation, what do you do." Use scenarios from the domain: a payments company gets a double-charge scenario, an ad tech company gets a bidding latency scenario.
- **Debugging.** Describe a symptom, ask them to reason toward causes. Good for all levels.
- **Code reading or writing.** A short snippet in the JD's language with a bug or a smell. Keep it small enough to hold in the head.
- **Judgment.** "Would you use X or Y here, and why not the other." Seniors and above get more of these.

Avoid brain teasers and trivia. "What is the default heap size of the JVM" tests memory, not ability.

## Curveballs

Real interviewers use a few questions designed to catch candidates who pattern-match instead of think. Include one or two per technical round, and more if the user asks for "tricky" questions. Mark them in the file so the user can practise recognising the shape. Four kinds work well:

- **The obvious answer is wrong.** The question invites a textbook response that does not survive the specifics. "We cache user permissions in Redis with a 5 minute TTL. A user is removed from an admin group. What happens?" The textbook answer is "it expires in 5 minutes"; the real answer is about what that 5 minutes costs and how to invalidate.
- **Predict the output.** A short snippet in the posting's language where the result is surprising: a closure capturing a loop variable, a nil interface that is not nil, a float comparison, a mutation through a shared reference. Keep it under 15 lines. The point is not trivia but whether they read code carefully.
- **Find the flaw.** A design or code sketch that looks reasonable and has one real problem. A retry loop with no jitter, a unique constraint the application enforces instead of the database, a queue consumer that acks before it writes. Do not say there is a flaw; ask what they would change.
- **Ask before answering.** A question where the right first move is a clarifying question, because the answer depends on something unstated. "Should we shard this table?" with no size, growth rate or access pattern given. Strong candidates ask; weak ones pick a side.

For each, the strong-answer bullets should name the trap and what recognising it sounds like. In a mock, if the user falls into the trap, let them finish, then probe once ("and if the TTL were an hour?") to see whether they catch it before you reveal it in feedback.

## Topic drills

When there is no posting, the profile is just a topic and a level. Build the round the same way, with two adjustments:

- Pick a plausible domain yourself and use it consistently, because questions without context become textbook questions. "Caching for a product catalogue at a retailer with flash sales" produces better questions than "caching".
- Cover the topic's breadth deliberately. For caching that means invalidation, consistency, stampedes, TTL choice, what not to cache, and cache-aside versus write-through. Say which sub-areas the round covers so the user knows what it does not.

## System design

45 to 60 minutes. One large open-ended prompt, sometimes two.

Write the prompt as a real interviewer would: a short product description and a scale hint, then silence. Then list the probes the interviewer will use to steer:

- Clarifying questions a strong candidate should ask before designing
- The core components they should identify
- The two or three hard parts specific to this domain (consistency for payments, fan-out for social, freshness for search)
- Scale and failure probes: what breaks first at 10x, what happens when component X dies
- Trade-off probes: "why not just use Y"

Pick the prompt from the domain in the posting. If the company builds a scheduling product, the design question is a scheduling system, not a URL shortener.

Calibration:
- Mid: can they produce a coherent design and justify the main choices.
- Senior: do they identify the hard part unprompted and handle failure modes.
- Staff: do they scope the problem, push back on requirements, and talk about migration and operational cost.

## Behavioural

30 to 45 minutes. Each question should map to one of the signals from the role profile.

Write the mapping explicitly in the file so the user sees it:

```
Signals from the posting: ownership, cross-team work, mentoring, shipping under ambiguity.
```

Then questions like "Tell me about a time you owned something end to end that was not going well" map to ownership, and so on. Include one or two negatives: conflict, failure, a decision they would reverse.

For the strong-answer bullets, describe the shape of a good story for this level rather than a script: what the situation should show, what the candidate's specific action should be, and what a credible result looks like. Note the common failure: telling a team story with no personal "I".

Large companies often use named principles (leadership principles, core values). If the posting or company is known for this, map questions to those and say so.

## Pairing or practical session

Some processes include live coding on a small task. If the profile suggests this, describe the likely format (build a small feature, extend a codebase, fix a bug under observation) and give one or two tasks with the same shape. The take-home reference covers scaffolding these into real code if the user wants to practise for real.

## Seniority calibration cheat sheet

| Level | Technical questions test | Design questions test | Behavioural questions test |
|---|---|---|---|
| Junior | Can they use the stack correctly | Usually skipped or very light | Learning, collaboration, taking feedback |
| Mid | Can they solve problems independently | Coherent design, main trade-offs | Ownership of features, handling setbacks |
| Senior | Judgment, trade-offs, what they would avoid | Hard parts, failure modes, operations | Influence without authority, mentoring, disagreement |
| Staff+ | Strategy, what to build vs buy vs kill | Scope, migration, cross-system cost | Org-level impact, setting direction, saying no |

## What makes a question generic (avoid)

- It could be asked for any company in the industry unchanged.
- It has a single textbook answer.
- It names a technology not in the posting and not implied by it.
- The strong-answer bullets say "demonstrates knowledge of" instead of naming the specific things a good answer contains.
