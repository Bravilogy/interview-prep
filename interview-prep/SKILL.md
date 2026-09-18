---
name: interview-prep
description: Turn a job description into realistic interview practice. Builds a role profile from a pasted or linked job posting, generates tailored question sets across rounds (recruiter screen, technical, system design, behavioural), runs a live mock interview one question at a time with honest scoring and feedback, and scaffolds a real take-home tech test as a working repo with a brief, rubric and code review. Also runs topic drills with no job description: "quiz me on caching", "tricky Go questions", "senior system design practice". Use this whenever the user pastes or links a job description, job posting, or role and wants to prepare, practise, rehearse, or test themselves, or asks for interview questions, a mock interview, a coding challenge, or a take-home for a role, or wants to drill or be quizzed on a technical topic at a given level, even if they never say "interview prep".
---

# Interview Prep

The user is preparing for a real interview and wants practice that feels like the real thing. Everything this skill produces should be traceable back to the job description in front of you. Generic "tell me about a time you failed" lists are what the free web tools already do. The value here is specificity: questions this team would plausibly ask, calibrated to this seniority, probing the things this posting is signalling it cares about.

## Workflow

### 1. Build the role profile

**No job description?** If the user names a topic and a level instead ("drill me on caching, senior", "tricky Go questions"), skip the posting and write a short profile from what they said: topic, level, and any stack or domain they mention. Ask for the level if they gave none, since it changes every question. Use a topic slug such as `topic-caching-senior`. Everything below then works the same, with the topic standing in for the posting's signals.

Read the job description first. If the user gave a URL, fetch it. If it is a screenshot or PDF, read it. Extract:

- **Role and seniority.** Title, and the seniority the responsibilities imply (a "Senior" title with junior responsibilities is a mid role; grade it on the responsibilities).
- **Stack and tools.** Everything named, plus what is strongly implied (a Kubernetes mention implies containers, networking, observability).
- **Domain.** Fintech, healthcare, ad tech, developer tools. Domain shapes the questions as much as the stack does.
- **What they are signalling.** Postings leak priorities. "Fast-paced", "ownership", "0 to 1" means they will probe autonomy and shipping under ambiguity. Repeated mentions of "reliability" or "scale" means system design questions about those. "Mentoring" means leadership questions. Note the three or four strongest signals.
- **Likely interview shape.** From the company size and role, guess the rounds. Startups often skip the recruiter screen and go straight to a founder call. Large companies almost always have a behavioural round with a leadership-principles flavour.

Write this to `interview-prep/<slug>/role-profile.md` where `<slug>` is the company and role, for example `acme-senior-backend`. Show the user a five-line summary and ask if anything is off, because a wrong seniority read wastes the whole session. When running non-interactively (no user to answer), state your assumptions in the profile and proceed.

### 2. Confirm what they want

Offer these, or infer from the request:

| Mode | What it produces | When |
|---|---|---|
| **Question sets** | One file per round with questions and what a strong answer covers | "give me questions", first session, revision |
| **Mock interview** | Live back-and-forth, one question at a time, scored | "interview me", "quiz me", "practise" |
| **Take-home** | A scaffolded repo with brief, rubric and later a review | "tech test", "coding challenge", "take-home" |
| **Full loop** | All rounds in sequence, as question sets or as mocks | "N interviews", "the whole process" |
| **Topic drill** | A round or mock on one topic at one level, no posting needed | "quiz me on X", "drill me on Y" |

The user may ask for a number of interviews. Treat that as the number of rounds to generate and map them to the round types from the role profile. Three interviews for a backend role usually means technical, system design, behavioural. Five adds a screen and a second technical or a pairing session.

### 3. Generate the round

Read `references/rounds.md` before writing any questions. It covers each round type, how to calibrate for seniority, and what separates a good question from a generic one.

Each round gets its own file: `interview-prep/<slug>/round-<n>-<type>.md`. Rounds build on each other: the system design round should reference the technical round's topics, and the behavioural round should probe the signals from the profile. Do not repeat a question across rounds.

Number of questions per round, unless the user says otherwise:

- Screen: 6 to 8, short
- Technical: 8 to 10, mix of conceptual and practical, including 1 or 2 curveballs
- System design: 1 to 2 large prompts with 4 to 6 follow-up probes each
- Behavioural: 6 to 8, each tied to a signal from the profile

### 4. Run the mock (if asked)

Read `references/scoring.md` before starting a mock. The short version:

- Ask one question. Stop. Wait for the answer. Do not list the remaining questions, do not hint at the answer, do not ask two things at once.
- After each answer, score it, give two or three lines of feedback, and ask one follow-up if a real interviewer would. Then move on.
- Play the interviewer honestly. A real interviewer is polite but does not fill silence or rescue a weak answer. If the user asks "is that right?", say you will cover it in the feedback and continue.
- At the end, write a summary to `interview-prep/<slug>/round-<n>-<type>-results.md` with per-question scores and the three things to work on.

### 5. Scaffold the take-home (if asked)

Read `references/take-home.md` first. Take-homes are the part no web tool can do because they need a real filesystem. Build it as a working project in `interview-prep/<slug>/take-home/`: a brief that reads like a real company sent it, a starter with the stack from the JD, a hidden rubric, and a time budget. When the user says they are done, review their submission against the rubric the way a hiring panel would.

### 6. Track progress

Append to `interview-prep/<slug>/progress.md` after every mock or take-home review: date, round, score, weak areas. At the start of a later session, read it and bias the next round toward the weak areas. Say so when you do, so the user knows why the questions are skewed.

## Principles

**Specific beats clever.** A question that name-checks the exact stack, domain, and scale from the posting is worth more than a beautifully phrased generic one. If the JD says "event-driven services on Kafka handling payments", ask about idempotency and exactly-once delivery in payment flows, not "explain message queues".

**Calibrate hard on seniority.** Junior questions test whether they can do the work. Senior questions test judgment: trade-offs, what they would push back on, what they got wrong before. Staff questions test scope: cross-team influence, technical strategy, what they would kill. Asking a junior about org-wide migration strategy is wasted; asking a staff engineer to reverse a linked list is insulting.

**Keep answers out of the chat summary.** When you hand over a question set, list the topics, not the answers. A closing message that says "Q2 is about the outbox pattern and consumer dedup" has just told the user what Q2 is testing. Point them at the file and let them try it cold.

**Do not leak the answer in the question.** "How would you handle the race condition when two workers pick up the same job?" tells them there is a race condition. "Two workers pull from the same queue. Walk me through what could go wrong" does not.

**Be honest in feedback.** The user is here to find gaps before a real interviewer does. Soft feedback wastes their time. Say what was missing, what a strong candidate would have said, and whether that answer would pass at this level.

**Do not fabricate company facts.** You can infer priorities from the posting. You cannot know the company's internal architecture, interview panel, or culture unless the user tells you or you fetched it. Frame guesses as guesses.
