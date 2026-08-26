---
name: meeting-prep
description: Writes a five-bullet prep brief for every meeting on today's calendar and delivers them all in one morning message. Use when the user says "prep my day", "meeting brief", "what's on today", or when running on a morning schedule.
---

# Meeting Prep Agent

One file. It reads today's calendar, and for each meeting it writes a brief of **exactly five
bullets** — then sends every brief in a single morning message.

The point is not that the briefs are thorough. The point is that they are short enough that you
actually read them. An earlier version of this wrote beautiful one-page summaries; they stopped
getting read by Thursday. **Short enough to always read beats detailed enough to impress.**

---

## Setup

### 1. Put this file in place

```
your-repo/
└── .claude/
    └── skills/
        └── meeting-prep/
            └── SKILL.md      ← this file
```

The folder name must match `name:` in the frontmatter above (`meeting-prep`).

### 2. Connect a calendar and an email account

This skill does not talk to Google/Microsoft/anything directly. It uses whatever calendar and email
**MCP servers** you have connected, which is why it works with any provider. Connect them once:

```bash
claude mcp add --transport http google-calendar https://<your-connector-url>
claude mcp add --transport http gmail            https://<your-connector-url>
```

Check what actually connected before you trust it:

```bash
claude mcp list
```

If you use Outlook, Fastmail, CalDAV, or a self-hosted setup — connect those instead. Nothing below
names a provider.

### 3. Run it

```bash
claude "prep my day"
```

Once it produces something you'd actually read, put it on a schedule (7:30 works well — before the
first call, after the coffee):

```bash
# crontab -e   (Linux/macOS)
30 7 * * 1-5 cd /path/to/your-repo && claude -p "prep my day" >> prep.log 2>&1
```

On Windows use Task Scheduler with the same command.

Realistic setup time: **one evening**, and most of it is the OAuth consent screens.

---

## What the agent collects

For each meeting on today's calendar, gather exactly these four things about the other person:

1. **Our last emails** — the most recent thread with them, and what it was actually about.
2. **Notes from the previous call** — if you keep meeting notes, read the last one.
3. **The tasks we owe each other** — open commitments in both directions.
4. **What changed at their company** — one line. A funding round, a launch, a new office, a
   reorganisation.

If a source is unavailable — no previous call, no notes tool connected, nothing found — say
**"nothing found"** in the bullet. Do not fill the gap with a guess. A brief that quietly invents
context is worse than no brief, because you will repeat it out loud in the meeting.

---

## The brief: five bullets, never more

This is the whole design. Not a style preference — the constraint is the feature.

| # | Head | What goes in it |
|---|---|---|
| 1 | **Who I am meeting** | Name, role, company, and which call this is (first / third / etc.) |
| 2 | **Where we stopped** | The last unresolved point, in one sentence |
| 3 | **What they wait for** | What *you* promised and have not delivered |
| 4 | **What I want to get** | The one outcome that makes this meeting worth having |
| 5 | **One thing to ask** | Something human and specific — their new warehouse, their launch |

**Bullet 3 is the one that changes behaviour.** Promises you made and forgot get carried forward
into the next brief automatically, and they stare at you until you either do them or drop them on
purpose. Never omit bullet 3 because it is empty — write "nothing outstanding" so the absence is a
statement rather than a gap.

### Hard rules

- **Exactly five bullets. Never six.** If something important does not fit, it was not important
  enough for the ninety seconds before a call.
- **One or two sentences per bullet.** If a bullet needs a paragraph, it is the meeting's agenda,
  not its prep.
- **Never invent.** No inferred job titles, no guessed company news, no "probably". Unknown is a
  legitimate value and must be written as one.
- **No preamble.** Do not open with "Here is your brief". The reader has four minutes.

---

## Output format

All briefs in **one message**, in calendar order:

```
Good morning. Four meetings today — all four briefs are in this message.

─────────────────────────────────────────
9:00 — Marco Rossi — Northwind
morning brief · 5 bullets, never more

• Who I am meeting     Marco Rossi, founder at Northwind. Third call.
• Where we stopped     We stopped on the rollout date.
• What they wait for   Pilot pricing — I promised it last Friday.
• What I want to get   A date for the security review.
• One thing to ask     Their new Hamburg warehouse.
─────────────────────────────────────────

[... one block per meeting ...]

4 minutes for the whole day.
```

Deliver it wherever you already look at 7:30 — email to yourself, a Slack DM, a Telegram message, a
file in your notes vault. One message, not one per meeting: the whole point is that you read the day
in a single sitting.

**Skip** meetings with no external attendee (focus blocks, standups, lunch). Prep is for people you
have a history with.

---

## Before you connect anything — read this

The access **is** the trick, and it is also the whole risk. This agent reads your calendar and your
email. That is a real amount of your life.

- Decide deliberately what you connect. Read-only scopes if your provider offers them.
- Check what leaves your machine. `claude mcp list` shows the servers; know whether each one is
  local or remote, and what a remote one receives.
- Consider a dedicated account, or scoping to one label/folder, before pointing it at fifteen years
  of mail.
- If you schedule it, the run happens whether or not you are watching. Read `prep.log` for the first
  week.

None of this is a reason not to build it. It is a reason to decide once, on purpose, instead of
clicking through consent screens at 1am.

---

## Making it yours

The five heads are not sacred — the **count** is. If your work needs different bullets, change the
table above and leave the number at five. Some variants that work:

- Hiring: *who · what stage · what they asked last time · what I need to assess · one thing to ask*
- Support escalations: *who · what broke · what we promised · what I need from them · one thing to ask*
- Investor updates: *who · last conversation · what they are waiting for · what I want · one thing to ask*

If you find yourself wanting a sixth bullet, that is the signal your brief is turning back into the
one-page summary you stopped reading.
