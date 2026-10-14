# Build log

How this skill was made, step by step, with the commands that were actually run. Written as it happened rather than reconstructed after.

## Why this skill exists

A prompt thread by @HeyAirahAi went viral in October 2026: seven steps that turn a chat agent into a job-search machine, ending in a few hundred automated applications overnight and nine interview calls by morning. Two of those steps already had owners in this family: step 1 and the material writing belong to [job-lens](https://github.com/arm-pz/job-lens), the judging to [recruiter-lens](https://github.com/arm-pz/recruiter-lens). Steps 3, 4, 6 and 7 (discovery, tracking, follow-ups, briefing) had no owner. That gap is this skill.

The step it deliberately drops is 4, unattended bulk submission.

## Step 0: Decide the boundary first

Before writing anything, one product decision was made and it shapes every file: the skill prepares, the user sends. Reason, recorded here so it does not need re-deriving:

- LinkedIn's user agreement prohibits automated access to the service; Indeed's terms are similar. Both run automated detection and suspend accounts.
- Employers and ATS vendors now screen for generated applications, so volume at scale reduces quality rather than raising reach.
- An agent that submits on a candidate's behalf is acting under their name and reputation, which is not the skill's to spend.

This made the skill an approval-gated copilot instead of an auto-apply tool.

## Step 1: Scaffold

Matched the family layout exactly (repo root README + LICENSE + `.claude-plugin/`, skill under `skills/<name>/`, tests alongside).

```bash
cd ~/Downloads/Qoder
mkdir -p application-pilot/skills/application-pilot/references \
         application-pilot/tests application-pilot/.claude-plugin
cd application-pilot
git init -q && git symbolic-ref HEAD refs/heads/master   # master, like the sibling repos
git branch -M master
```

## Step 2: SKILL.md, then split the weight into references

`SKILL.md` keeps only what must always be loaded: the sibling boundary table, the eight-mode routing table, the ground rules, the loop order, and standalone behaviour. Everything with a format attached went into `references/`, because progressive disclosure is the whole reason references exist.

```bash
git add skills && git commit
```

Four references, each with one job:

| File | Why it is separate |
|---|---|
| `modes.md` | Exact per-mode output formats; only the running mode is read |
| `tracker.md` | Schema, status machine, dedupe key, aging rules: the deterministic core |
| `sources.md` | Where roles come from, date honesty, per-source access rules, the volume argument |
| `siblings.md` | The hand-off table and the wording that keeps three skills from overlapping |

## Step 3: Repo files

`plugin.json` mirrors the sibling manifest (version 0.1.0, `skills: ./skills/`). MIT license reused byte-for-byte from job-lens. README leads with what the skill does, then the section explaining which part of the thread it drops and why, because that is the interesting design decision and hiding it would be dishonest marketing.

`.gitignore` excludes the tracker files a user generates, so a public repo cannot accidentally ship someone's job history.

## Step 4: Tests as the routing contract

`tests/test-discovery.md` states activation, non-activation toward each sibling, and the ambiguous cases with the expected routing. All three skills' test files must describe the same split or the wrong skill fires half the time, so the sibling repos get matching edits in the next step.

## Step 5: Found a collision with a skill already installed

Before registering the skill, the flat install was checked against what the host actually loads. A skill named `job-application-agent` was already installed (`~/.claude/skills/job-application-agent`), and it covers much of the same ground with far more machinery. Its own `SKILL.md` was read this session; what it describes is a Node CLI (`scripts/job-application.mjs`), OS-backed profile storage, a source catalog, `score` gates, append-only NDJSON ledgers, cloud leases, browser form filling and uploads, an autonomy mode that stops prompting per application, and a CAPTCHA vendor helper. Two files in it also state that the skill runs a managed updater that checks npm at login and hourly, and that analytics transmit by default.

Two problems, one fix:

- **Routing.** Both descriptions claimed "find roles, assess, track, follow up", so which skill fires becomes a coin flip.
- **Scope creep.** Building a tracker that competes with a ledger, or a submit path that competes with an autopilot, would mean a worse version of something that already exists.

So application-pilot was narrowed instead of extended. It keeps what the neighbour does not own: the editable search brief, the reviewed shortlist, follow-up drafts, interview briefings, the funnel read, and the hand-offs to job-lens and recruiter-lens. It gains no CLI, no cloud state, no telemetry, no background updater, and no submission path, and now states a scale ceiling (about 40 rows, 25 shortlist items) past which it hands off rather than growing the table. `references/siblings.md` records the precedence rule, and the discovery tests gained a "should not activate, job-application-agent automates" group.

What is said about the neighbour in this repo is limited to what its own documentation states, and its files were only read, never modified.

## Step 6: Contract check across the family

All three job-search skills' descriptions were measured, because the 1024-character frontmatter limit is easy to cross while adding a boundary clause:

| Skill | Before | After |
|---|---|---|
| application-pilot | new | 1002 |
| job-lens | 1027 (already over the limit) | 1000 |
| recruiter-lens | 922 | 997 |

job-lens was over the limit before this work, which the added clause would have made worse; the trim moved the MCP tool names out of the description (they still live in `references/github-mcp.md`) and compressed two clauses. recruiter-lens's test file already routed "finding, evaluating, or submitting job applications" to job-application-agent, so that line was split: search coordination now names application-pilot, automated submission still names job-application-agent. Both `tests/test-discovery.md` files and the SKILL.md descriptions now state the same four-way split, and each repo was committed separately.

Flat installs were re-synced from the clones and verified byte-identical with `diff -rq`.

## Validated

- `SKILL.md` present, name matches folder, frontmatter opens and closes with `---`
- descriptions single-line and within 1024: application-pilot 1002, job-lens 1000, recruiter-lens 997
- bodies well under 500 lines (80 / 68 / 105), no `TODO:` markers, no extraneous files in the skill folders
- `marketplace.json` parses, nine plugins, `application-pilot` resolves to `arm-pz/application-pilot`

## Step 7: Discovery audit before the remote exists

Ran the `findable` skill's audit on the not-yet-public repo, because this is the only moment a rename is free. Findings in `docs/discovery-kit.md`; the one that changes the plan is the name. "application pilot" is an aviation job title, so the phrase returns crop-duster listings rather than software, `Obada-barakat/ApplicationPilot` already does application tracking under that name, `-pilot` is the busiest suffix in the agent-skill namespace, and it rhymes with a 156-star incumbent (`vaibhavarora14/job-application-agent`, the skill installed on this machine). Audit surfaced three further gaps: no remote, no site page, no release. Kit drafted with About at 346 characters and 12 topics, verified with `check_listing.py`, nothing applied.

## Open

- **Decide the name** (`docs/discovery-kit.md` section 2). Renaming is free right now and expensive after the push.
- Create the `arm-pz/<name>` remote and push. Four repos carry unpushed commits: application-pilot (4), job-lens (1), recruiter-lens (1), caffeinity-skills (1).
- `gh` on this machine is the npm shim and crashes with a TypeError, so repo creation needs either a working `gh` or the browser.
- Run the discovery tests for real: install all four skills in one session and check which fires for each prompt in `tests/test-discovery.md`.
- Test mode 2 against a live search, where the date-honesty rules actually bite.
- job-lens has no `argument-hint` or `user-invocable` keys while recruiter-lens and application-pilot do, so `/job-lens` may not appear as a slash command. Left as-is pending your call.
