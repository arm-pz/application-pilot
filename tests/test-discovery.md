# Discovery tests

These check that application-pilot activates for search-orchestration requests and stays out of the way of applicant-kit (producing material), recruiter-lens (judging material), and job-application-agent (automated filling and submission). Run each prompt with all four skills installed, then repeat the "should not activate" and "ambiguous" groups with only application-pilot installed.

## Should activate application-pilot

- "Set up a job search for senior backend roles, remote, starting from my resume."
- "Find roles matching my brief that were posted in the last 7 days, with links."
- "Score these 20 postings for fit and tell me which to skip."
- "Turn this list of applications into a tracker with status and follow-up dates."
- "Which of my applications are past 7 days with no reply? Draft the follow-ups."
- "Brief me before Thursday's interview at Acme."
- "How is my search going this month and what should I change?"
- "These ten links look like the same role twice, merge them in my tracker."

## Should not activate application-pilot (applicant-kit produces)

- "Rewrite my resume bullets for this role."
- "Decode this JD and tailor my resume to it."
- "Write me five summary options."
- "Rewrite my LinkedIn headline and About section."
- "Give me my interview answers for this role, based on my resume."

## Should not activate application-pilot (recruiter-lens judges)

- "Why am I not getting interviews?"
- "Will this resume pass an ATS?"
- "Give me a 6-second recruiter scan."
- "What are the red flags in my resume?"
- "How well does my resume cover this JD?"
- "Audit my LinkedIn profile."
- "Is it okay to use AI to write my resume?"

With only application-pilot installed, both groups above should get the one-line "that belongs to applicant-kit / recruiter-lens, which is not installed" note plus the short standalone fallback, not an imitation of either skill's full output.

## Should not activate application-pilot (job-application-agent automates)

- "Fill out and submit these 40 applications for me."
- "Set up unattended applying while I sleep."
- "Check my ledger for whether I already applied to this requisition id."
- "Grant this agent continuing autonomy so I stop getting prompts."
- "Import my job-search profile into a durable ledger with outcomes."

With only application-pilot installed, these get the packet-plus-approval flow (mode 4) and one line saying automated submission is not what this skill does, plus the terms and privacy note from `references/siblings.md`. The skill must not add a submit path, drive a browser through forms, or imitate the ledger.

## Ambiguous: expected routing

| Prompt | Expected routing |
|---|---|
| "Here is my resume. Help me get a job." | application-pilot mode 1 confirms the brief, then modes 2, 3, 5; hands mode 4 work to applicant-kit |
| "Apply to the 500 highest-compatibility roles while I sleep." | application-pilot declines the unattended submit, explains the board terms and detection risk, offers the reviewed shortlist plus ready-to-send packets |
| "Find this job and write me a resume for it." | application-pilot modes 2 and 3 to identify it, then applicant-kit mode 1 to write it |
| "Prepare me for my interview." | application-pilot mode 7 assembles the briefing, using applicant-kit mode 6 for answers and recruiter-lens `predict-questions` for the list |
| "Which roles should I prioritise?" | application-pilot mode 3 (rubric over evidence), using recruiter-lens `gap-analysis` per role when it is available |
| "Track my applications and check each one for ATS problems." | application-pilot owns the tracker; recruiter-lens `ats-check` runs per material before the user sends |
| "Find good roles and then apply to them." | application-pilot modes 1 to 3 decide the shortlist; job-application-agent fills and submits if the user wants that; applicant-kit writes the packet in between |
| "Keep a record of everywhere I applied." | application-pilot mode 5 for a reviewable CSV or Markdown file; job-application-agent's ledger when they want it queryable across agents and rounds |

## Out of scope for all four skills

- Cover letters, offer and salary negotiation, relocation or visa advice, and tax or contract review. Answer these normally; do not force them through a skill.
- Anything that submits, messages, or sends on the user's behalf without their per-action approval.
