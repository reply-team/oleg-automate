# The Invoices in My Inbox

A small agent in Claude that reads my new email once a week, finds the bills, and writes them
into one list in Google Drive. It is one page of instructions plus two connections and a timer,
no coding required.

This folder: https://github.com/reply-team/oleg-automate/tree/main/The%20Invoices%20in%20My%20Inbox

| file | what it is |
|---|---|
| `instructions-page.md` | the page from step two of the video, word for word. Paste it into a scheduled task in Claude Cowork and change the lines marked `[change:]` — your day and time, and your folder name |

How to set it up, the same six steps as in the video:

1. Make one folder in Google Drive, for example `Bills`.
2. Take `instructions-page.md` and change the `[change:]` lines.
3. In Claude, connect Gmail (the connector is made by Google): Connect, sign in with Google, Allow.
4. Connect Google Drive the same way.
5. In the Claude desktop app, open the Cowork tab, make a scheduled task, paste the page into its
   prompt and pick the day and time.
6. The two rules are already on the page: it never pays, replies or deletes, and every bill it
   logs gets the Gmail tag `Logged`, so nothing lands on the list twice.

One limit to know: the Gmail connector sees that a PDF is attached but cannot open it. Bills whose
amount is only inside a PDF go on a second list, "Open these yourself".

## The files

- [`instructions-page.md`](https://github.com/reply-team/oleg-automate/tree/main/2026-10-02-video12-v3-new-factory/instructions-page.md)
