# Claude Did the Paperwork for Our New Hire

One prompt in the Claude desktop app. When a signed offer comes in, Claude reads the email thread, copies the
four first-week files in Google Drive and fills in the name and start date, books the first-week meetings in
Google Calendar, and writes the welcome email as a Gmail draft. It asks before it shares anything, and it sends
no email: the draft waits for a person.

| file | what it is |
|---|---|
| `prompt.md` | the four sentences from the video, plus the two lines added after the first run |

What it needs: the Gmail, Google Drive and Google Calendar connectors in Claude (made by Google). No code.

Two things to know:

- Claude copies whatever is in your files. Keep the four templates current (ours still had last year's office address).
- Claude shares with the address it finds in the emails. Read the address in the approval request before you say yes.

## The files

- [`prompt.md`](https://github.com/reply-team/oleg-automate/tree/main/employee-onboarding-paperwork-for-a-new/prompt.md)
