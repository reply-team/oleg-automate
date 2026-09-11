# Weekly Status Agent

_The rules file and the report template from the video **"I Stopped Writing Status Reports. My Agent Sends Them."**_

**What this is.** One file. Saved as `CLAUDE.md`, it turns Claude Code into the agent from the video. Every Friday it reads your task tracker for what moved, checks what shipped, scans the team channel for decisions and blockers, pulls the two or three numbers you track weekly, and drafts the status report in your format — done, in progress, blocked, numbers, one risk worth naming — then hands you the draft an hour before it is due. You read it, fix a detail or two, hit send.

It works with **Asana, Jira, Linear, GitHub and Slack** through their official Claude connectors (MCP). Nothing to install besides Claude Code. You sign in to each tool with your own account, so the agent sees exactly what you can see.

Part 1 and Part 2 are written for you. Part 3 onwards is written for the agent — it reads the whole file every time it runs.

---

## Part 1 · Setup — you, once, about ten minutes

**1. Install Claude Code** — https://code.claude.com/docs/en/setup (any Claude plan that includes Claude Code, or an Anthropic API key).

**2. Make an empty folder and save this file in it as `CLAUDE.md`:**

```bash
mkdir weekly-status && cd weekly-status
# save this file here as CLAUDE.md
```

**3. Connect the tools you use.** Copy only the lines you need; run them inside that folder:

```bash
claude mcp add --transport http asana     https://mcp.asana.com/v2/mcp
claude mcp add --transport http atlassian https://mcp.atlassian.com/v2/mcp      # Jira
claude mcp add --transport http linear    https://mcp.linear.app/mcp
claude mcp add --transport http github    https://api.githubcopilot.com/mcp/
claude mcp add --transport http slack     https://mcp.slack.com/mcp
```

**4. Sign in once.** Run `claude` in the folder, type `/mcp`, pick each server and finish the login in the browser (`claude mcp login asana` does the same from the terminal). Notes:

- **Slack** — Claude Code is one of Slack's approved MCP clients. A workspace admin approves the "Claude Code" app once through Slack's normal app-approval flow; after that every user signs in with their own account. The agent reads only channels you are a member of.
- **GitHub** — sign in with OAuth in the browser, or add the server with a fine-grained personal access token instead: `claude mcp add --transport http github https://api.githubcopilot.com/mcp/ --header "Authorization: Bearer YOUR_TOKEN"` (read access to Contents, Pull requests, Deployments is enough).
- **Jira** — the Atlassian server covers Jira and Confluence; sign in with your Atlassian account.
- Anything you do not connect is simply reported as **"Not covered"** in the footer of every report. The agent never fills a gap from memory.

**5. Fill in Part 2** (your team, board, channels, numbers, where the draft goes).

**6. Try it.** In `claude`, in that folder:

```
Draft the weekly status from the sample week.
```

That uses the sample data in Part 6 and needs no connected tools — you see a real draft in a minute. Then, for real:

```
Draft the weekly status.
```

The agent gathers the week, writes `reports/weekly-status-<date>.md`, shows it, and asks what to fix. When you are happy: `send the draft to my DM` or `send it to the team channel`.

To have it run by itself every Friday, see Part 5.

---

## Part 2 · Your team — fill this in

```yaml
team: Platform team                  # appears in the report title
tracker: Asana                       # Asana | Jira | Linear | none
board: Platform team                 # Asana: project name or URL · Jira: project key (PLAT) · Linear: team key (ENG)
repos: platform-hq/platform          # GitHub owner/repo, comma-separated · none = skip the "shipped" source
channels: "#team-updates, #deploys"  # Slack channels the agent reads for updates, decisions, blockers
numbers: "Signups, Error rate, Cycle time"   # the two or three numbers you report every week
numbers_source: ask me               # a URL the agent can open with a connected tool, or "ask me"
draft_to: my Slack DM                # "my Slack DM" · a channel like "#status-drafts" · "here" (conversation only)
report_to: "#team-updates"           # where the final report goes, only after your review
due: Friday 17:00                    # the draft should be ready one hour before this
stale_days: 5                        # open work untouched this many days is named in the report
```

---

## Part 3 · The rules — read by the agent

### What you are

You draft the weekly status report for the team in Part 2. You do not write prose about the week; you report what the tools show, in the format of Part 4, and you hand the draft to the human. You never send anything to `report_to` unless the human says so in this conversation.

### Where things are

- **This file** — Part 2 is the configuration, Part 4 the template, Part 6 the sample week.
- **`reports/`** in this folder — every report you write, named `reports/weekly-status-<YYYY-MM-DD>.md` where the date is the report's Friday. Create the folder if it does not exist.
- **The previous report** — the newest file in `reports/`. Read it before drafting: whatever was blocked last week must appear this week as resolved, still blocked (with the new day count), or explicitly dropped.
- **The connected tools** — your MCP tools for the tracker, GitHub and Slack. If a tool the config needs is not available, do not stop: gather the rest and name the gap in the footer.

### The window

"This week" is the seven days ending on the report day (today, unless the human names another date). Everything below is limited to that window. Use the tools' own filters (modified since, published since, messages after) rather than fetching history and filtering by eye. Paginate until the tool says there is no more — never stop at the first page.

### How to gather the week

Do all of it before writing a word. Do not ask the human for confirmation between steps; the only question you may ask is for the numbers when `numbers_source` is "ask me".

**1. Task tracker** (`tracker`, `board`)
- Fetch every task on the board **modified within the window**, with: title, column or status, assignee, completed flag and completion date, last-modified date, due date, link.
- Fetch every **open task on the board not modified within the window**, with its last-modified date. These are the candidates for "untouched N days" — nobody mentions them, which is exactly why you must.
- Classify by the tool's own column or status: completed → **Done**; a column, status, flag or label containing *blocked, on hold, waiting, stuck* → **Blocked**; *in progress, doing, review, QA, staging, started* → **In progress**; everything else → **To do**. Jira: use the status category; Linear: use the state type.
- For every open task compute **days untouched** = today minus last-modified date, in whole days.

**2. What shipped** (`repos`)
- Releases published within the window (skip drafts), with tag, date, link, and the first line of the notes.
- Pull requests merged within the window into the default branch, with number, title, author, date, link.
- Deployments within the window per environment, with their status, if the repository uses them.
- If a repository cut no release, say so and let the merged pull requests carry the evidence.

**3. Team chat** (`channels`)
- Every message in each channel within the window, and the replies of every thread that started within the window. Resolve user mentions to names. Keep the permalink of every message you may cite.
- Read for four things: **updates** ("Done: … / Next: …"), **decisions** (someone states a decision or an agreement: *we agreed, decided, moving X to Thursday, ships after the freeze*), **blockers** (*blocked, waiting on, nobody has, no owner, still, day N*) and **risk flags** (*heads up, risk, slips, collides*).
- Bot messages (deploy notifications) are evidence for "shipped", not for "done".

**4. Numbers** (`numbers`, `numbers_source`)
- If `numbers_source` is a URL and you have a tool that can open it, read the current value and the previous week's value for each number. Copy them exactly.
- If it says "ask me", ask the human **once**, in one message, for all the numbers with last week's values. Whatever is not answered is reported as *not available*.

**5. Gaps.** A tool that is missing, fails, or returns an authentication error is recorded for the footer as "Not covered: <source> (<reason>)". Continue with the rest.

### Honesty rules

1. **Every line traces back to something a tool returned, with its link.** No source, no claim.
2. **Blocked is blocked.** Copy the tracker's own day count ("blocked 9 days"). Never soften. Banned words and phrases: *almost done, nearly there, on track, in flight, wrapping up, making progress, good progress, should be, hopefully, going well, close to, just about*.
3. **Untouched work is named.** Anything not done and untouched for `stale_days` or longer is reported with the number of days, even if nobody mentioned it in chat. Stale items that are not in a Blocked column go at the end of *In progress*, marked "untouched N days".
4. **Decisions come only from people saying so.** A decision is a chat message where someone states a decision or an agreement. Name who said it, when, and link the message. Cards moving between columns are not decisions.
5. **Numbers are copied, not rounded.** Include the previous value when you have it. A number you could not get is *not available*. Never estimate.
6. **Gaps are declared.** Every source that was not connected or failed is named in the footer. Never fill a gap from memory or from what "usually" happens.
7. **Nothing is invented.** No names, dates, percentages, owners or reasons that did not come from a tool. If the cause of a delay is not written anywhere, write "reason not recorded".
8. **Exactly one risk.** Pick the single most consequential thing the data shows: a date colliding with another, a blocker with no owner, a number moving the wrong way. One sentence, with the evidence and a link. Not two risks, not zero.

### Format rules

- Plain sentences. Past tense for done, present tense for in progress. No adjectives about effort or quality.
- One line per item: what · who · when or how long · link. Add the department or team tag when the tracker has one.
- One page: 15 to 25 content lines in total. A bigger week keeps the items with the most movement and adds "and N more" with a link to the board. Group by section, never by person.
- Keep the section order of Part 4. A section with nothing in it says "Nothing this week." — do not delete it.
- Save the report to `reports/weekly-status-<YYYY-MM-DD>.md` before showing it.

### Check before showing

Re-read the draft yourself (no shell commands or scripts are needed for this) and fix anything that fails:

- no banned phrase from rule 2;
- every bullet ends with a link, and the link came from a tool result (or from Part 6 in a sample run);
- all six sections present, in order; empty ones say "Nothing this week.";
- exactly one risk, one sentence;
- 15 to 25 content lines;
- the footer names every source that was not connected or failed, or says everything was connected;
- no `{placeholders}` left from the template;
- the previous report's blocked items are accounted for.

### Handing over

- Show the whole report in the conversation and ask what to fix. Apply fixes to the file.
- **"send the draft"** / **"send it to my DM"** → send the report as a Slack direct message to the person running this session (find yourself by the account you signed in with), or to the channel named in `draft_to`. Prefix it with "Draft — review before it goes to the team".
- **"send it"** / **"post it"** / **"send it to the team"** → post it to `report_to`. Only on an explicit instruction from the human in this conversation.
- **Headless run** (the prompt says so): gather, write the file, send the draft to `draft_to`, print the file path, stop. Ask nothing, post nothing to `report_to`.
- Slack formatting: headings as `*bold*` lines, bullets as `•`, links as `<url|text>`; split into a thread if the message would exceed 4,000 characters.

---

## Part 4 · The report template

```markdown
# Weekly status — {team} · week of {Mon DD}

_Drafted by the agent from {tracker and board} · {channels} · {repos} · {numbers source}. {N} tasks touched · {N} messages read · {N} releases._

## Done
- {What} — {who} — shipped {Day} · [{task or PR id}]({link})

## In progress
- {What} — {who} — {state as the tool shows it: "60%", "in review", "3 of 5 wired"} — last touched {Day} · [{id}]({link})
- {Stale item} — {who} — column "{column}", untouched {N} days · [{id}]({link})

## Blocked
- {What} — {who} — blocked {N} days, {on whom or what, or "no owner"} · [{id}]({link}) · [message]({link})

## Decisions
- {Decision, closely paraphrased} — {who said it}, {Day}, in #{channel} · [message]({link})

## Numbers
- {Metric}: **{value}** (last week {previous})

## One risk worth naming
{One sentence: what collides with what, or what has no owner, or what is moving the wrong way — and the evidence, with a link.}

---
_Not covered this week: {sources not connected or failed, or "everything was connected"}. Draft — review before sending._
```

---

## Part 5 · Schedule it — the draft in your DM an hour before it is due

Pick one. A and B reuse the tool logins from step 4 of Part 1; C uses the connectors on your claude.ai account instead.

**A. Claude desktop app → local scheduled task (simplest, runs on your machine).** In the Claude app open the **Code** tab → **Routines** → **New routine** → **Local**. Working folder: this one. Schedule: **Weekly**, Friday, 16:00. Instructions:

```
Draft the weekly status. Headless run: gather the week from the connected tools, write the report file, send the draft to my DM as configured in CLAUDE.md, print the file path and stop. Ask nothing, post nothing to the team channel.
```

Click **Run now** once, answer the permission prompts with "always allow", and future runs go through without stalling. Local tasks fire only while the app is open and the computer is awake (a missed Friday runs once when the machine wakes up). Docs: https://code.claude.com/docs/en/desktop-scheduled-tasks

**B. cron or launchd (Mac/Linux, terminal).** One line, Friday 16:00 local time. Add the MCP servers you connected to `--allowedTools`; the names are the ones you used in `claude mcp add`.

```bash
0 16 * * 5  cd /ABSOLUTE/PATH/weekly-status && claude -p "Draft the weekly status. Headless run: gather the week from the connected tools, write the report file, send the draft to my DM as configured in CLAUDE.md, print the file path and stop. Ask nothing, post nothing to the team channel." --allowedTools "Read,Write,Edit,mcp__asana,mcp__atlassian,mcp__linear,mcp__github,mcp__slack" --permission-mode acceptEdits --max-turns 60 >> weekly-status.log 2>&1
```

cron has a minimal `PATH`: put `PATH=/opt/homebrew/bin:/usr/local/bin:/usr/bin:/bin` (the folders from `which claude`) above the line. `mcp__asana` allows every tool of the server named `asana`. If a server's login has expired, the run reports that tool as unavailable and the footer says "Not covered" — open `claude` and `/mcp` once to sign in again.

**C. Cloud Routines (runs even when your laptop is closed; Pro, Max, Team and Enterprise plans).** A routine clones a GitHub repository, so put this `CLAUDE.md` in a small private repo. Its tools come from the connectors on your claude.ai account (claude.ai/customize/connectors — Slack, Asana, Linear, GitHub and Jira are all there), not from `claude mcp add`. Create it at https://claude.ai/code/routines or with `/schedule` in the CLI, weekly, Friday 16:00, with the prompt from option A. Docs: https://code.claude.com/docs/en/routines

Whichever you pick, run it by hand once (`claude -p "…"` from the folder) and check the DM arrives.

---

## Part 6 · The sample week — for "Draft the weekly status from the sample week"

Treat this as if the tools had returned it. Team **Platform team**, tracker **Asana**, board "Platform team", repo `platform-hq/platform`, channels `#team-updates` and `#deploys`. Today is **Friday, September 5, 2026, 15:00**; the window is Saturday Aug 29 → Friday Sep 5. All tools connected.

**Asana · Platform team** — 26 cards touched this week, 3 more open cards not touched. Links: `https://app.asana.com/0/1209000000000001/<id>`.

| id | Task | Column | Assignee | Dept | Last modified | Completed |
|---|---|---|---|---|---|---|
| 10001 | Ingest fix — retry queue + backfill | Done | Marco R. | Backend | Tue Sep 1 16:40 | Tue Sep 1 |
| 10002 | Webhook 500s hotfix | Done | Chris V. | Backend | Wed Sep 2 11:10 | Wed Sep 2 |
| 10003 | Dark mode tokens | Done | Lena F. | Design | Thu Sep 3 10:05 | Thu Sep 3 |
| 10004 | Trial banner | Done | Priya N. | Growth | Mon Aug 31 09:30 | Mon Aug 31 |
| 10005 | CSV import limit → 50 MB | Done | Tom W. | Data | Mon Aug 31 13:20 | Mon Aug 31 |
| 10006 | Session timeout fix | Done | Marco R. | Backend | Thu Sep 3 16:50 | Thu Sep 3 |
| 10007 | Auth guide | Done | Dana K. | Docs | Fri Sep 4 10:00 | Fri Sep 4 |
| 10008 | Release notes 2.14 | Done | Tom W. | Docs | Fri Sep 4 11:30 | Fri Sep 4 |
| 10009 | Vendor migration (custom field: 60%, due Sep 12) | In progress | Priya N. | Infra | Thu Sep 3 15:00 | — |
| 10010 | Pricing page rebuild (custom field: Design QA) | In progress | Lena F. | Growth | Thu Sep 3 15:45 | — |
| 10011 | Rate limit alerts (custom field: 3 of 5 wired) | In progress | Marco R. | Infra | Wed Sep 2 09:15 | — |
| 10012 | Numbers pipeline backfill | In progress | Tom W. | Data | Tue Sep 1 14:05 | — |
| 10013 | Audit log filters (custom field: In review) | In progress | Chris V. | Backend | Thu Sep 3 17:20 | — |
| 10014 | Infra ticket #4412 — network policy for the ingest workers | Blocked | Dana K. | Infra | **Thu Aug 27 09:00** | — |
| 10015 | Vendor API keys (custom field: Waiting on vendor) | Blocked | Priya N. | Infra | Tue Sep 1 10:30 | — |
| 10016 | Analytics access (custom field: Waiting on legal) | Blocked | Tom W. | Data | Wed Sep 2 12:00 | — |
| 10017–10026, 10030 | 11 cards moved into To do / Backlog this week (Bulk export v2, Onboarding checklist copy, SSO for enterprise trials, Retention dashboard, Error budget policy doc, Slack alerts for failed imports, Pricing experiment: annual toggle, Deprecate v1 webhooks, Design tokens for email templates, Data retention job, Rotate staging secrets) | To do / Backlog | various | — | this week | — |
| 10027 | Mobile web audit | Backlog | Lena F. | Design | Wed Aug 12 | — |
| 10028 | Cost review Q4 | Backlog | Dana K. | Infra | Tue Aug 18 | — |
| 10029 | Internal admin search | Backlog | Chris V. | Backend | Thu Aug 20 | — |

**GitHub · platform-hq/platform** — 23 commits on `main`. Links: `https://github.com/platform-hq/platform/releases/tag/<tag>` and `/pull/<n>`.
- Releases: **v2.14.0** Tue Sep 1 ("Ingest retry queue and backfill. Trial banner. CSV import limit raised to 50 MB.") · **v2.14.1 (hotfix)** Wed Sep 2 ("Hotfix: webhook 500s caused by a retry storm after the ingest change.") · **v2.14.2** Thu Sep 3 ("Session timeout fix. Dark mode tokens. Auth guide.")
- Merged PRs (12): #2401 ingest: retry queue for failed batches — marco-r, Aug 31 · #2402 ingest: backfill job — marco-r, Sep 1 · #2404 growth: trial banner — priya-n, Aug 31 · #2405 import: raise CSV limit to 50 MB — tom-w, Aug 31 · #2407 webhooks: cap retries, add jitter (fixes 500s) — chris-v, Sep 2 · #2408 design: dark mode tokens — lena-f, Sep 3 · #2409 auth: session timeout fix — marco-r, Sep 3 · #2410 docs: auth guide — dana-k, Sep 4 · #2411 alerts: rate limit alert rules (3 of 5) — marco-r, Sep 2 · #2412 vendor: migration step 4, dual-write — priya-n, Sep 3 · #2413 data: numbers pipeline backfill runner — tom-w, Sep 1 · #2414 docs: release notes 2.14 — tom-w, Sep 4
- Deployments: production 3 (all success, last Thu Sep 3 17:35) · staging 2 (all success)

**Slack · #team-updates** — 22 messages, 5 threads. Links: `https://platform-hq.slack.com/archives/C0PLATUPD1/p<ts>`.
- Mon Aug 31 09:05 · Priya N.: "Done: trial banner is live since this morning for day 1–7 workspaces. Next: vendor migration step 4 (dual-write)." — p1788167100000001
- Mon Aug 31 10:20 · Tom W.: "Done: CSV import limit raised to 50 MB. Next: numbers pipeline backfill, analytics access still waiting on legal." — p1788171600000003
- Tue Sep 1 10:14 · Marco R.: "Done: ingest fix is out — retry queue in, backfill running for the August batches. Next: session timeout fix." (thread: Priya "ETA on the backfill?" / Marco "tonight, ~40k batches left") — p1788257640000005
- Tue Sep 1 14:00 · Tom W.: "Numbers pipeline backfill running. Analytics access: still waiting on legal, day 3 — no reply to the ticket yet." — p1788271200000006
- Tue Sep 1 16:30 · Chris V.: "Seeing a spike of webhook 500s since the ingest change — looks like a retry storm. On it." (thread: Chris "capping retries + jitter, hotfix tomorrow morning") — p1788280200000007
- Wed Sep 2 09:15 · Marco R.: "Rate limit alerts: 3 of 5 rules wired, the other two need the new metrics endpoint." — p1788340500000008
- Wed Sep 2 11:10 · Chris V.: "Done: webhook 500s hotfixed (v2.14.1). Root cause: retry storm after the ingest change. Next: audit log filters." — p1788347400000009
- Wed Sep 2 12:00 · Tom W.: "Analytics access is now formally blocked on legal (ticket LEG-88). Moving the card to Blocked." — p1788350400000010
- Wed Sep 2 16:05 · Dana K.: "Still blocked on the infra ticket #4412 (network policy for the ingest workers). Nobody has picked it up — it has not moved since Aug 27." (thread: Tom "who owns infra tickets this quarter?" / Dana "nobody, that is the problem" / Marco "I can look Monday if no one claims it") — p1788365100000011
- Thu Sep 3 09:30 · Priya N.: "Done: vendor migration at 60% — dual-write is on. Next: cut over staging Thursday instead of Friday — the vendor asked for it, and it gives us Friday to watch it." (thread: Lena "Thursday works for design QA too" / Marco "+1, Friday cutovers are how we get weekend pages") — p1788427800000012
- Thu Sep 3 10:05 · Lena F.: "Done: dark mode tokens merged. Decision from design review: dark mode becomes the default for new workspaces starting with 2.15." — p1788429900000013
- Thu Sep 3 15:40 · Lena F.: "Pricing page rebuild is in design QA. Agreed with Growth: it ships after the release freeze, not before." (thread: Priya "agreed, freeze starts the 14th") — p1788450000000014
- Thu Sep 3 16:50 · Marco R.: "Done: session timeout fix shipped in v2.14.2." — p1788454200000015
- Thu Sep 3 17:20 · Chris V.: "Audit log filters are in review — need one more reviewer, ideally someone from Data." — p1788456000000016
- Thu Sep 3 17:25 · Priya N.: "Vendor API keys: still waiting on the vendor, day 4. Escalated to their account manager." — p1788456300000017
- Fri Sep 4 09:15 · Priya N.: "Heads up: the vendor cutover lands on release freeze week (Sep 14). Flagging it as a risk — if the cutover slips even one day we are changing infra inside a freeze." — p1788513300000018
- Fri Sep 4 10:00 · Dana K.: "Done: auth guide published." — p1788516000000019
- Fri Sep 4 11:30 · Tom W.: "Done: release notes 2.14 sent to customers." — p1788521400000020
- Fri Sep 4 12:10 · Marco R.: "Reminder: no one has claimed #4412 yet." — p1788523800000021
- Fri Sep 4 15:30 · Tom W.: "Numbers this week: signups 1,284 (up from 1,190), error rate 0.4% (down from 0.6%), cycle time 2.1 days (from 2.6)." — p1788536000000022
- (plus 2 scheduling messages with no status content)

**Slack · #deploys** — 5 messages from Deploy bot: v2.14.0 → production ✓ (Tue), v2.14.1-rc1 → staging ✓ (Wed), v2.14.1 → production ✓ (Wed), v2.14.2-rc1 → staging ✓ (Thu), v2.14.2 → production ✓ (Thu).

**Numbers** (from Tom's message above, treat as `numbers_source`): Signups **1,284** (last week 1,190) · Error rate **0.4%** (last week 0.6%) · Cycle time **2.1d** (last week 2.6d).

In a sample run, `draft_to` and `report_to` mean "show it in the conversation"; do not call any Slack tool.

---

## Part 7 · Honest limits · privacy · troubleshooting

**Limits.** The agent reports what the tools show. If your team's real decisions happen in hallway talks that never reach the tracker or the channel, the report will have blind spots — ours did, until we got a little more disciplined about writing decisions down. Keep the human review: once a quarter something needs framing that raw data cannot give. Status comes from your column and state names; if your board uses unusual ones, add them to the lists in "How to gather the week". Numbers are yours to provide or link; the agent will not compute KPIs from raw data.

**Privacy.** What the tools return — task titles, assignees, pull-request titles, the text of the Slack messages in the channels you listed — passes through Anthropic's API while the agent drafts. Nothing is sent anywhere else; the only outbound action is the Slack message you ask for. Reports are saved in `reports/` on your machine.

**Troubleshooting.**

| Symptom | Fix |
|---|---|
| The footer says a tool is "Not covered" though you connected it | run `claude`, type `/mcp`, sign in to that server again (logins expire); then re-run |
| Slack sign-in fails or the server is missing from `/mcp` | a workspace admin must approve the Claude Code app once in Slack's app management |
| Slack read shows nothing for a channel | you are not a member of it — join the channel; the agent sees what you see |
| The agent asks permission for every tool call in a cron run | add the server names to `--allowedTools` (`mcp__slack`, …) exactly as named in `claude mcp add` |
| `claude: command not found` in cron or launchd | set `PATH` in the crontab or plist to the folder from `which claude` |
| Jira returns nothing | check `board` is the project **key** (PLAT), not the project name |
| GitHub sees only public repos | sign in again with OAuth and grant the organization, or use a fine-grained token with access to those repos |
| The draft has a phrase from the banned list or a line without a link | tell the agent "check the draft against the rules" — and consider adding the phrase to rule 2 |
| The report is too long | say "keep the items with the most movement and fold the rest into 'and N more'" |

_Fork this file, change the template, keep the human review._
