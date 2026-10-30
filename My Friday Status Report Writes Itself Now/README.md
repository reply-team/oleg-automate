# My Friday Status Report Writes Itself Now

One prompt in the Claude desktop app. On Friday, Claude reads this week's project emails in Gmail, the meetings in
Google Calendar and the project plan in Google Drive, then writes the weekly status report as a new Google Doc under
four headings — done, moved, at risk, next — with a link to the email or document behind every line. It tells you in
the chat which lines it is not sure about. You read it, fix a line or two, and send it yourself.

| file | what it is |
|---|---|
| `prompt.md` | the four sentences from the video, plus the two sentences added after the first run |

What it needs: the Gmail, Google Calendar and Google Drive connectors in Claude (made by Google). No code.

Two things to know:

- Claude only sees what was written down. A decision made in a hallway or on a call is not in the report — add it by hand.
- A misleading email subject can put a line under the wrong heading. Every line has its link: open it when a line looks odd.

## The files

- [`prompt.md`](https://github.com/reply-team/oleg-automate/tree/main/the-weekly-project-status-report-written/prompt.md)
