# Discovery kit — application-pilot (name pending)

Drafts only. Nothing in section 8 has been run. The name is unresolved, so copy that depends on it uses `<name>`; About and Topics are written to survive a rename unchanged.

## 0. Baseline (audit, 2026-10-13)

Nothing is public yet, so this is a pre-launch baseline rather than a ranking audit.

| Check | Result |
|---|---|
| `github.com/arm-pz/application-pilot` | **404.** No remote created; four local commits only |
| `skills.caffeinity.com/application-pilot` | **404.** No site page |
| Web search, name alone | The phrase is an **aviation job title**. Top results: "Aerial Application Pilot jobs" on Indeed and ZipRecruiter, crop-duster career pages, a CASA pilot-licence application form, an FDOT "web application pilot" (pilot-program sense). Nothing software |
| Web search, name + "agent skill" | No match. Results are unrelated issues and READMEs using "application pilot" as ordinary English, plus a French AI assistant whose name is "Pilot" |
| GitHub repo name search | 103 repos match; almost all are student "pilot application" projects |
| Same-name, same-purpose | **`Obada-barakat/ApplicationPilot`** — "An intelligent job application tracking system with automated follow-up reminders". Direct overlap in purpose, different kind of software |
| `-pilot` suffix crowding | Crowded in this exact niche: `RigorPilot-Skills` (481 stars), `ResearchPilot-Skills` (312), `skillPilot` (27), `skill-pilot` (20), `pilot-skills` (8), `MoviePilot-Skills` (7) |
| Incumbent in the task space | **`vaibhavarora14/job-application-agent`** — 156 stars, MIT, homepage `jobappagent.com`, 11 topics, pushed the same day as this audit. **This is the skill installed on this machine**, which is why its description reaches so far |
| Other task-space listings | JobGPT (mcpmarket.com), `track-application` (awesomeskill.ai), Career-Ops (aiskill.market) |

Metadata gaps, all of them: no remote, so no description, homepage, topics, release, or social preview. The repo does have `LICENSE` (MIT) and an install line in the README.

**Reading it:** absence here is an index gap, not a quality verdict. The one real problem is that the name is not empty space.

## 1. Target queries

Two blocked searches were not run; treat these as the list to validate, not results.

| Capability | Query a stranger would type |
|---|---|
| Tracker | "job application tracker", "how to keep track of job applications spreadsheet" |
| Follow-ups | "follow up after no response on a job application", "job application follow-up email template" |
| Briefing | "prepare for an interview with AI", "interview briefing company research" |
| Shortlist | "find jobs matching my resume automatically", "job shortlist by fit" |
| Funnel | "job search tracker with response rates" |
| Whole search | "AI agent to manage my job search", "Claude Code skill for job applications" |

## 2. Name decision

**Recommendation: rename before the remote exists.** This is the cheapest moment it will ever have: zero stars, zero installs, no inbound links, no marketplace entry pushed.

Evidence against `application-pilot`:

1. The phrase is a job title in aviation, so it cannot be won. Searching it returns crop-duster listings rather than anything related.
2. `Obada-barakat/ApplicationPilot` already does job-application tracking with follow-up reminders under this name.
3. `-pilot` is the most crowded suffix in the agent-skill namespace, and it also reads as "pilot program".
4. It sits one letter away from `job-application-agent`, a 156-star project with its own domain. A near-synonym of an incumbent's name means permanently living in its shadow: searchers find it, read a similar name, and assume it is the thing.

If the name is kept instead, the cost is qualification everywhere: a disambiguation line in the README and site page, a topic mix that leans on `job-search` rather than the name, and accepting that name searches never resolve to it.

Candidate alternatives, grouped. All checked against GitHub name search only, not against trademark or directory rules.

Plain task names, strongest for search:

- `application-tracker` — exactly what people type; the `application-tracker` topic page already has 86 repos. Generic, so it will never be a brand
- `job-application-tracker` — same, longer, near-identical to several existing repos
- `job-search-tracker`

Family names, strongest for cross-linking with recruiter-lens and job-lens:

- `search-lens` — keeps the `-lens` pattern; "search" collides with web search
- `job-lens-desk`, `career-lens` — the pattern stretched thin; reads as a derivative

Desk and logbook names, relatable and mostly empty space:

- `job-desk` — 93 repos on GitHub, none in this niche; "desk" is already recruiting language for a recruiter's queue of roles
- `application-desk` — same idea, names the artifact
- `search-desk` — short, a little vague
- `job-logbook` — the tracker is literally a log; "logbook" is unclaimed here
- `application-ledger` — precise about append-only rows, slightly accounting-flavoured

Queue and pipeline names:

- `job-queue` — collides with literal job queues in computing
- `application-queue`
- `job-pipeline` — reads as CI/CD to any developer, including this audience

**My pick, in order:** `job-desk`, then `application-tracker`, then `job-logbook`. `job-desk` is short, unclaimed in this space, says "the place your search is run from", and does not rhyme with the incumbent. `application-tracker` wins if the priority is being found by the exact phrase people type rather than owning a name.

Whatever is chosen, `npx skills add arm-pz/<name> --skill <name>`, the marketplace entry, the flat install directory, and every cross-reference in job-lens and recruiter-lens change together.

## 3. GitHub listing

**About (description, 350 character limit):**

```
Agent skill that runs the job search around the applications: shortlist with honest posting dates, evidence-based fit scoring, a Markdown or CSV application tracker, follow-up drafts for roles gone quiet, interview briefings and a funnel review. Never submits, never invents experience or metrics. Works with Claude Code, Cursor, Codex and Qoder.
```

**Topics:** `job-search`, `job-application`, `application-tracker`, `interview-prep`, `resume`, `agent-skills`, `claude-code-skill`, `cursor`, `codex`, `qoder`, `markdown`, `follow-up`

Topic counts checked today: `agent-skills` 31,934 repos, `job-search` 5,196, `interview-prep` 1,583, `application-tracker` 86. `job-application`, `follow-up`, `markdown` and `resume` were not counted; `cursor`, `codex` and `qoder` are platform topics.

**Homepage:** no page exists yet. Slot for `https://skills.caffeinity.com/<name>` once the site page is published; leave empty until then rather than pointing at the domain root.

## 4. README opening

Replace the current opening, which leads with the family story rather than the task.

```markdown
# <name>

A job-search agent skill that keeps the search itself in order: shortlist roles
against your criteria with real posting dates, score each one for fit from your
own resume, track every application in one Markdown or CSV file, draft the
follow-ups for roles that went quiet, brief you before an interview, and read
the funnel weekly. It never submits an application and never invents experience,
dates or recruiter names.

Install: `npx skills add arm-pz/<name> --skill <name>`

Ask it things like:

- "Find senior backend roles posted this week that match my resume."
- "Turn my list of applications into a tracker with follow-up dates."
- "Which ones went quiet past seven days? Write the follow-ups."
- "Brief me before Thursday's interview at Acme."

Unrelated to **job-application-agent** (vaibhavarora14), which automates form
filling and submission, and to **ApplicationPilot** (Obada-barakat): this skill
prepares and tracks, and you send everything yourself.

Siblings: [recruiter-lens](https://github.com/arm-pz/recruiter-lens) judges your
material, [job-lens](https://github.com/arm-pz/job-lens) writes it, <name> runs
the search around both.
```

The disambiguation line is required as long as the aviation-results and same-name projects exist, and useful regardless of the name choice.

## 5. Release notes (shipped as v1.0.0, 2026-10-19)

Shipped text differs from the draft below in three ways: the version is 1.0.0
to match `SKILL.md` and `.claude-plugin/plugin.json`, `<name>` is filled in as
`application-pilot`, and the sibling named in the hand-off bullet is
`applicant-kit`, not job-lens. Release body was verified against
`releases/latest` (only a trailing newline differs).

```markdown
## <name> v0.1.0

Coordinates a job search in plain files the user can audit.

- Eight modes: search brief, role discovery, fit scoring, application packet,
  tracker, follow-up queue, interview briefing, funnel review
- Tracker schema with a fixed status machine, dedupe key and aging rules
  (`references/tracker.md`)
- Posting-date honesty rules and per-source access notes (`references/sources.md`)
- Hand-off table for the job-lens and recruiter-lens siblings, and a precedence
  rule against automated application tools (`references/siblings.md`)
- Discovery and per-mode tests in `tests/`

It does not submit applications, and it has no CLI, network calls or telemetry.

Install: `npx skills add arm-pz/<name> --skill <name>`
```

## 6. Site page

Not drafted. No `skills.caffeinity.com` page can be written honestly until the repo is public, and the sibling pages already follow a shape to match. Slot: `docs/site/<name>.md`, title `<name> — job search tracker, shortlist and follow-ups`, description under 155 characters, install line, the four example prompts from section 4, and the same disambiguation paragraph.

**Superseded 2026-10-19:** the repo is public, so a page was authored against the sibling template instead of this slot. It is live at `https://skills.caffeinity.com/application-pilot/` with the tarball `agent-skills/application-pilot.tar.gz` (`sha256:354c6f3c…`), listed in both discovery indexes, the sitemap and the hub. The page says "applicant-kit produces" where `SKILL.md` still says job-lens; fix the repo, not the page.

## 7. Distribution

Candidate listings that the audit found carrying this category. **Submission rules for each were not checked**; verify before preparing entries, and do not submit to more than one place in a day.

- `skills.sh` (Vercel's skill index, the target of `npx skills add`) — check whether arm-pz skills are already resolvable there
- `mcpmarket.com/tools/skills` — lists JobGPT in this category
- `awesomeskill.ai` — lists `track-application` in this category
- `aiskill.market` — lists Career-Ops
- `agenticskills.io` — general skill index
- GitHub `agent-skills` and `job-search` topic pages, which the chosen topics feed automatically

One honest constraint for every entry text: this skill does not apply for you. Several listings in this category are populated by tools that do, so the entry needs to say what it is, not just what it helps with.

## 8. Apply commands

Applied as of 2026-10-19: remote and pushes exist, description (315 chars) and
15 topics are set, homepage is `https://skills.caffeinity.com/application-pilot`,
licence reads MIT, and `v1.0.0` is released. The commands below are the original
draft and are kept for the record; do not re-run them.

```bash
# after the remote exists and the first push is done
git push -u origin master
gh release create v1.0.0 --title "application-pilot v1.0.0" --notes-file <release-notes.md>
gh repo edit arm-pz/<name> \
  --description "<About text from section 3>" \
  --add-topic job-search,job-application,application-tracker,interview-prep,resume,agent-skills,claude-code-skill,cursor,codex,qoder,markdown,follow-up
```

Rename now, before any of that, and the change is three places: repo folder and clone, `SKILL.md` `name`, `plugin.json`, marketplace entry, plus the cross-references in job-lens and recruiter-lens. Rename later and it is those places plus the live URL, stars, installs and directory entries.

## 9. Re-check plan

Baseline recorded above (nothing indexed). Re-run the same checks on **2026-11-03**, two weeks after the push:

- name alone, name + "github", name + "agent skill"
- the six task queries in section 1
- `gh repo view` metadata: description, homepage, topics, release
- which of the section 7 directories list it, and which list competitors and not this

Compare against this file rather than against memory, and expect indexing to lag the push.
