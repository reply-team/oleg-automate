# I Built a Support Agent in One Evening. It Asks Me Before It Sends

A small agent in Claude that reads new support emails every hour, finds the order, and writes the reply
as a draft in Gmail. It never sends anything: a person reads each draft and presses send. It is one page
of instructions plus two connections and a timer, no code at all.

| file | what it is |
|---|---|
| `instructions-page.md` | the page of instructions from step two of the video. Paste it into a scheduled task in Claude Cowork and change the lines marked `[change:]` |
| `answers-page.md` | an example page of answers: the questions people ask most, each with the answer. Swap the answers for your own replies |

How to set it up, the same six steps as in the video:

1. Make one Google Drive folder with two files: your order sheet and your page of answers
   (start from `answers-page.md` and copy in the replies you already send).
2. Take `instructions-page.md` and change the `[change:]` lines.
3. In Claude, connect Gmail (the connector is made by Google): Connect, sign in with Google, Allow.
4. Connect Google Drive the same way, so the agent can read the order sheet and the page of answers.
5. In the Claude desktop app, open the Cowork tab, make a scheduled task, paste the page into its prompt
   and set it to run every hour.
6. The two rules are already on the page: it never sends anything, and refunds, angry customers and
   questions that are not on the page get the `For me` tag and no draft.

Two things to know from the first week:

- A customer who writes from a different email address has no exact match in the order sheet. The page
  says: no exact match means no draft, and the email gets the `For me` tag.
- When something changes (a shipping time, for example), change the page of answers the same day.
  Until you do, the drafts will say the old thing, and only the fact that every draft waits for you
  catches it.

## The files

- [`answers-page.md`](https://github.com/reply-team/oleg-automate/tree/main/I%20Built%20a%20Support%20Agent%20in%20One%20Evening.%20It%20Asks%20Me%20Before%20It%20Sends/answers-page.md)
- [`instructions-page.md`](https://github.com/reply-team/oleg-automate/tree/main/I%20Built%20a%20Support%20Agent%20in%20One%20Evening.%20It%20Asks%20Me%20Before%20It%20Sends/instructions-page.md)
