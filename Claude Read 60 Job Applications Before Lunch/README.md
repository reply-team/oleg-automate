# Claude Read 60 Job Applications Before Lunch

One prompt in the Claude desktop app. Claude reads the job post in Google Drive and lists the must-haves, reads every
resume in the applications folder one by one, writes two lines per person (what matches, what is missing), puts the
best matches on a short list in a new Google Doc, and writes invitation emails for them as Gmail drafts. It sends
nothing and rejects nobody: the decision is yours.

| file | what it is |
|---|---|
| `prompt.md` | the four sentences from the video, plus the two lines added after the first run |

What it needs: the Google Drive and Gmail connectors in Claude (made by Google). No code.

Two things to know:

- A strong person with an unusual resume (a scanned file, a career change) can land in "maybe". Read the "maybe" group every time.
- Do not let it write rejections. That decision, and those emails, stay with a person.

## The files

- [`prompt.md`](https://github.com/reply-team/oleg-automate/tree/main/reading-a-pile-of-job-applications-done/prompt.md)
