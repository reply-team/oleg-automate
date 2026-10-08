# My Meetings Write Their Own Notes Now

A small agent in Claude that reads the day's Google Meet transcripts every weekday evening and writes
one short page per meeting, plus a draft email for the people who were there. It is one page of
instructions plus three connections and a timer, no code at all.

| file | what it is |
|---|---|
| `instructions-page.md` | the page from step two of the video, word for word. Paste it into a scheduled task in Claude Cowork and change the lines marked `[change:]` — your time and your folder name |

How to set it up, the same six steps as in the video:

1. Turn on transcripts in Google Meet: in the calendar event, Video call options → Meeting records →
   Transcribe the meeting. Transcripts need Google Workspace Business Standard or higher. Each
   transcript lands in the meeting organizer's Drive, in a folder called `Google Meet`.
2. Take `instructions-page.md` and change the `[change:]` lines.
3. In Claude, connect Google Drive (the connector is made by Google): Connect, sign in with Google, Allow.
4. Connect Google Calendar and Gmail the same way. The calendar gives the agent the guest list; Gmail
   lets it write drafts.
5. In the Claude desktop app, open the Cowork tab, make a scheduled task, paste the page into its prompt
   and set it to run on weekdays at your time.
6. The two rules are already on the page: it never sends anything, and a task without a name and a
   date goes under `No owner yet`.

One limit to know: a call started from a link instead of the calendar event has no transcript turned
on, so there is nothing for the agent to read. Start meetings from the calendar.

## The files

- [`instructions-page.md`](https://github.com/reply-team/oleg-automate/tree/main/My%20Meetings%20Write%20Their%20Own%20Notes%20Now/instructions-page.md)
