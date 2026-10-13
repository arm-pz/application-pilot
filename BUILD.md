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

## Next

- Flat install to `~/.qoder/skills/application-pilot` (skill contents only, no README at that level).
- Marketplace entry in `arm-pz/caffeinity-skills`.
- Routing edits in job-lens and recruiter-lens so all four skills state the same split.
- Validate against the skill checklist, then real-world test on a live search.
