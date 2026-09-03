# Weekly status agent — rules

A rules file for an agent that writes your weekly status report. Point it at whatever tracker and
chat you already use, run it before the report is due, read the draft, send it.

It is deliberately tool-agnostic. Every place this file says *the tracker* or *the team channel*,
substitute your own — the rules are about what to look for, not about which product you bought.

---

## 0. Setup — the only part you must edit

Fill this in once. If a line does not apply to you, delete it rather than leaving it blank; an
empty instruction reads as "find nothing" and the agent will obey.

```yaml
report_due:        Friday 16:00 <your timezone>
draft_me_at:       one hour before report_due
window:            the 7 days ending at report_due

tracker:
  where:           <how to reach your tracker — MCP server, CLI, exported JSON, a URL>
  scope:           <the board / project / label that IS this team's work>
  done_means:      <the exact column or status name that counts as shipped>

chat:
  where:           <how to reach your team channel>
  channels:        <the 1-3 channels where decisions actually land>

numbers:
  - name:          <metric 1 — the one leadership asks about first>
    where:         <dashboard, query, or file>
  - name:          <metric 2>
    where:         <...>
  # Two or three. A weekly report with nine numbers is a dashboard, and nobody reads it.

audience:          <who reads this and what they decide with it>
```

---

## 1. What to read

Read these four sources, in this order. Stop at the window boundary — last week's report already
covered last week.

1. **The tracker, for what moved.** Every item whose status changed inside the window. Record the
   item, what it moved from, what it moved to, and the day it moved.
2. **The tracker, for what did not move.** Every item still open that has had no status change and
   no comment for **7 days or more**. Record how many days. This list is the whole reason the
   report is worth writing — see §4.
3. **What shipped.** Whatever your team treats as the record of delivery: merged changes, released
   versions, closed deploy tickets. If two sources disagree, prefer the one your audience would
   check.
4. **The team channel, for decisions and blockers.** Messages in the window that (a) settle a
   question, (b) name something as blocked, or (c) change a plan. Ignore everything else. Chat is
   mostly not signal and treating it as signal is how the report gets long.

Then pull the numbers named in §0. Report each as **current value, and the change since last
week's report**. A number with no direction is decoration.

---

## 2. What to write

Use `weekly-status-template.md`. Five blocks, in this order, never more:

**Done** · **In progress** · **Blocked** · **Numbers** · **One risk worth naming**

Rules that apply to all five:

- One line per item. If a line needs a second sentence, it is two items or it is not important.
- Name the thing, not the ticket ID alone. "Vendor migration, sixty percent" beats "#4471 in
  progress". Put the ID at the end if your audience uses them.
- Lead with the noun, not with "we". The reader is scanning.
- No adjectives of effort. *Hard, complex, tricky, heavy lift* describe your week, and the report
  is not about your week.

---

## 3. What NOT to write

These are the failure modes this agent exists to prevent. They are not style preferences.

- **Do not soften Blocked.** An item that is blocked is *blocked*. It is not "almost done", "in
  final review", "wrapping up", or "just needs a look". If it has not moved, the report says it
  has not moved, and says for how long.
- **Do not promote In progress to Done.** Done means the thing your `done_means` column says, and
  nothing else. Not "code complete". Not "merged, deploy Monday" — that is In progress.
- **Do not invent causes.** If something slipped and no source says why, write that it slipped and
  that no reason was recorded. "Blocked on vendor" is a claim; only make it if someone made it.
- **Do not fill a block to be even.** If nothing is blocked, the Blocked block says `Nothing
  blocked this week.` Padding it teaches the reader to skip it, and then the week something IS
  blocked, they skip that too.
- **Do not smooth the numbers.** Report the value you found. If it is worse than last week, the
  arrow points down.

---

## 4. The stale-item rule

Any open item with no movement for **7 days or more** goes in **Blocked**, with the day count,
even if nobody has called it blocked.

This is the rule that makes the report honest, and it is the one people will ask you to relax.
The argument for keeping it: a human writing their own status has an interest in the untouched
task not being mentioned, and that interest is exactly why the reader stopped trusting status
reports. The agent has no such interest. Write:

    Infra ticket — untouched since the 22nd (9 days). No blocker recorded.

Not:

    Infra ticket — in progress.

If an item is legitimately parked, say so and say until when. "Parked until the vendor call on the
14th" is information. "In progress" is not.

---

## 5. One risk worth naming

Exactly one. Pick the thing most likely to make next week worse that the reader can still do
something about. Two sentences: what could happen, and what would prevent it.

If the honest answer is that nothing is at risk, write `No risk worth naming this week.` — and
mean it. A fabricated risk every week is the same lie as a softened blocker, pointed the other
way.

---

## 6. Honest limits — state these in the report when they apply

The agent reports what the tools show. Where the tools are blind, the report says so rather than
guessing:

- **Decisions made out of band.** If your team settles things in calls or hallways and never
  writes them down, those decisions are invisible here. When the channel shows a question with no
  recorded answer, list it under Blocked as `decision not recorded`. The fix is not a better
  agent; it is writing decisions down.
- **Work outside the scope.** Anything not in the `scope` from §0 does not exist to this report.
- **Numbers you did not name.** The agent pulls the metrics in §0 and no others.

---

## 7. Deliver

Produce the draft at `draft_me_at` and send it to the author, not to the audience. It is a draft.

**Keep the human review.** Read it before it goes. Fixing a detail or two is the normal case and
takes about ten minutes. Roughly once a quarter something needs framing that raw status cannot
give — a reorganisation, a missed quarter, a decision that needs context. That is the week you
write the top of the report yourself and let the agent fill the five blocks underneath.

Never let it send to the audience unread. The value of the report is that a person stands behind
it; an unread automated report is a feed, and feeds do not get trusted, they get filtered.
