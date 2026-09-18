# interview-prep

An agent skill that turns a job description into realistic interview practice.

Paste a job posting and get:

- **A role profile.** Seniority, stack, domain, and what the posting is signalling the team cares about.
- **Question sets per round.** Recruiter screen, technical, system design, behavioural. Each question says why they ask it, what a strong answer covers, and the follow-ups a real interviewer would use.
- **A live mock interview.** One question at a time, honest scoring against the target level, feedback after each answer, and a written summary of what to work on.
- **A take-home tech test.** A real scaffolded repo in the stack from the posting, with a brief that reads like a company sent it, a hidden rubric, and a panel-style review when you are done.
- **Curveballs.** Deliberately tricky questions of the kind real interviewers use: code whose output surprises, a design with one real flaw, questions where the obvious answer is wrong or where you should ask before answering.
- **Topic drills.** No posting handy? "Quiz me on caching, senior level" works too.
- **Progress tracking.** Weak areas carry over so the next session targets them.

Ask for "3 interviews" and it generates three rounds that build on each other.

## Why a skill and not a website

The question-generator part exists as dozens of free web tools. What they cannot do is create a real project on your machine, review your actual code, or remember what you got wrong last week. A skill runs inside your coding agent, uses your own model, and has a filesystem.

## Install

**Claude Code**

```bash
git clone https://github.com/Bravilogy/interview-prep ~/.claude/skills/interview-prep
```

Or copy the `interview-prep/` folder into `.claude/skills/` in any project.

**Other agents**

The skill is a folder with a `SKILL.md` and a `references/` directory, following the open agent skills format. Copy `interview-prep/` into wherever your agent loads skills from.

## Usage

Paste a job description and say what you want:

```
Here's a JD for a senior backend role at Acme. Give me the questions they'd ask.
```

```
<job description> — interview me for this, technical round.
```

```
Generate a take-home test for this role and I'll do it tonight.
```

```
Run me through 3 interviews for this posting.
```

```
Drill me on system design for a senior backend role, tricky questions welcome.
```

Everything is written to `interview-prep/<company-role>/` in your current directory.

## Layout

```
interview-prep/
├── SKILL.md                  workflow and principles
└── references/
    ├── rounds.md             how to write each round type, seniority calibration
    ├── scoring.md            running a mock, scoring, end-of-round summary
    └── take-home.md          designing, scaffolding and reviewing a take-home
```

## License

MIT
