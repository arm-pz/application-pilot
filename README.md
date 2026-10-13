# application-pilot

A job-search agent skill for Claude Code, Cursor, Codex and Qoder. It runs the part of the search that sits around the resume: turn your criteria into a live shortlist, score each role for fit with evidence you can point at, keep one tracker of where everything stands, flag the applications that went quiet, draft the follow-ups, brief you before an interview, and read the funnel weekly so you know what to change. It never invents experience, dates, recruiter names or application statuses, and it never submits an application for you.

Install: `npx skills add arm-pz/application-pilot --skill application-pilot`

Ask it things like:

- "Here is my resume. Set up a search for senior backend roles, remote, and find what was posted this week."
- "Score these 20 roles for fit and tell me which ones to skip."
- "Turn my list of applications into a tracker with statuses and follow-up dates."
- "Which applications are past seven days with no reply? Write a short follow-up for each."
- "Brief me for Thursday's interview: what they will ask, my answers from my own resume, questions for them."

## The part of that viral thread this does not copy

The workflow shape comes from a public prompt thread by [@HeyAirahAi](https://x.com/HeyAirahAi) that told an agent to apply to hundreds of roles overnight. The organising half of that thread is real work, so it lives here. The auto-submit half is not: automated access breaks the terms of LinkedIn and Indeed, both run detection that suspends accounts, and employers now screen for generated applications.

So application-pilot prepares everything up to the send button and stops. You approve each application, or each batch you watched go out. Fit scores are stated as a rubric estimate, never as an ATS result, and the recommendation is a reviewed shortlist rather than volume, because that is what actually produces interviews.

## Three skills, three jobs

| Skill | Job | Says |
|---|---|---|
| [recruiter-lens](https://github.com/arm-pz/recruiter-lens) | judges | "tell me what is wrong" |
| [job-lens](https://github.com/arm-pz/job-lens) | produces | "write me the better version" |
| application-pilot | coordinates | "what should I apply to, where does it stand, what happens next" |

```
npx skills add arm-pz/recruiter-lens --skill recruiter-lens
npx skills add arm-pz/job-lens --skill job-lens
```

application-pilot hands material writing to job-lens and all judging to recruiter-lens, and works standalone when neither is installed.

| Mode | What you get |
|---|---|
| 1 Search brief | The criteria file that keeps the search honest: roles, level, non-negotiables, follow-up threshold |
| 2 Discover | Deduped shortlist table with exact links and posting dates, `unknown` where a date is not stated |
| 3 Score fit | Stated rubric, matched evidence per role, named gaps, and an apply or skip verdict |
| 4 Packet | job-lens tailors the material, recruiter-lens checks it, then the target is shown to you and you send it |
| 5 Track | CSV or Markdown tracker with a fixed status machine; a row only becomes submitted when you say it did |
| 6 Follow-up | Aging queue past your threshold, plus short role-specific drafts under 90 words, never sent for you |
| 7 Briefing | Company and JD context, likely questions, evidence-based answer outlines, questions to ask them |
| 8 Funnel review | Counts from your own rows, per source and role type, and the one change to try next period |

## Install

Skills CLI:

```
npx skills add arm-pz/application-pilot --skill application-pilot
```

Claude Code marketplace:

```
/plugin marketplace add arm-pz/caffeinity-skills
/plugin install application-pilot@caffeinity-skills
```

Flat install: copy `skills/application-pilot/` into your agent's skills directory:

```
.claude/skills/application-pilot/
.agents/skills/application-pilot/
.cursor/skills/application-pilot/
.qoder/skills/application-pilot/
```

Local development: `claude --plugin-dir .` and `claude plugin validate .`

## Structure

```
application-pilot/
├── README.md
├── LICENSE
├── .claude-plugin/
│   └── plugin.json
├── skills/
│   └── application-pilot/
│       ├── SKILL.md                    # routing, ground rules, the never-submit rule
│       └── references/
│           ├── modes.md                # per-mode output formats
│           ├── tracker.md              # schema, status machine, dedupe key, aging
│           ├── sources.md              # where roles come from, date honesty, access rules
│           └── siblings.md             # who answers what, hand-off wording
└── tests/
    ├── test-discovery.md               # activation / non-activation / ambiguous routing
    └── test-prompts.md                 # per-mode test prompts + expectations
```

## Your data stays yours

The tracker holds your resume links and a map of everywhere you have applied. Keep it in your own workspace and out of any public repo; the `.gitignore` here already excludes `job-applications.csv`, `job-applications.md` and `job-search-brief.md`. Nothing is uploaded on your behalf.

## Credits

Workflow patterns adapted from a public prompt thread by [@HeyAirahAi](https://x.com/HeyAirahAi). application-pilot is not affiliated with that author and deliberately omits the automated-submission step.
