# Working with the sibling skills

Three arm-pz skills share the same subject, so they must not share triggers. The one-line division:

- **recruiter-lens judges** ("tell me what is wrong")
- **job-lens produces** ("write me the better version")
- **application-pilot coordinates** ("what should I apply to, where does it stand, what happens next")

Command and mode names below were checked against the installed skills in October 2026. Where an installed skill behaves differently, trust the installed skill.

## Who answers what

| Question | Owner | Notes |
|---|---|---|
| What roles match me, where are they posted, which are new? | application-pilot mode 2 | the other two never search |
| Is this role worth applying to? | application-pilot mode 3 | rubric over the user's own evidence |
| How well does my resume cover this JD? | recruiter-lens `gap-analysis`, `tailor` | coverage verdict; feeds mode 3's gap column |
| Write the tailored resume, bullets, summaries, LinkedIn, answers | job-lens modes 1 to 6 | mode 4 hands the target back here |
| Will an ATS parse it, what is the 6-second impression, red flags? | recruiter-lens `ats-check`, `scan`, `critique`, `red-flag-review`, `reject-reasons` | run before the user sends |
| What may I use AI for in a job search? | recruiter-lens `ai-guidelines` | takes precedence over all three skills' defaults |
| Keep my list of applications, dates, follow-ups | application-pilot modes 5 and 6 | neither sibling owns a tracker |
| Brief me before Thursday's interview | application-pilot mode 7 | assembles job-lens mode 6 and recruiter-lens `predict-questions` |
| Is my search working? What do I change? | application-pilot mode 8 | funnel from the user's own rows |
| Cover letters, offer and salary negotiation, relocation or visa advice | none | answer normally; do not force it through a skill |

## Hand-off wording

One line, then the call: "This is material writing, so I am handing it to `job-lens` mode 1." If the environment can invoke a skill by name, do it; otherwise give the command, for example `/job-lens` or `/recruiter-lens ats-check`. Take their findings as given: this skill turns verdicts into next actions, it does not re-judge them.

Never let the tracker imply work that has not happened. A `ready` row means a packet exists; only the user makes it `submitted`.

## Standalone fallback

If a sibling is not installed, say so once and keep going with a short note that the sibling does it better. Do not imitate their full output. Offer:

```
npx skills add arm-pz/job-lens --skill job-lens
npx skills add arm-pz/recruiter-lens --skill recruiter-lens
```

## Reciprocal boundary wording

For the other two skills' descriptions, so all three state the same split:

> Not for running the search itself (finding roles, the application tracker, follow-ups, interview briefings): use the application-pilot skill.

And the matching non-activation group in both `tests/test-discovery.md` files:

- "Find me backend roles posted this week."
- "Build/update my application tracker."
- "Which of my applications went quiet past seven days?"
- "Write the follow-up for the ones with no reply."
- "Brief me before Thursday's interview."

All five belong to application-pilot.
