# Support Tickets Are Docs Bugs

*fieldnotes.example/support-tickets-are-docs-bugs · 6 min read · by the Field Notes team*

We read six months of support tickets in one sitting. Two thousand three hundred of them, printed
out, on a Tuesday, with three people and a lot of coffee.

We went in looking for the product's weak spots. We expected a ranked list of broken things —
the feature that confuses everyone, the button in the wrong place, the workflow with a dead end
in the middle. We got something else.

## Half of them weren't bugs in the product

They were bugs in the docs.

Not "the docs are thin here". The answer was written, published, and live. The person who filed
the ticket had simply not found it — and in most cases had been looking in the right place while
they were failing to find it.

That reframe is the whole article, so it is worth being exact about what it means. A support
ticket about a documented behaviour is a report that a specific page failed to answer a specific
question at a specific moment. It has a reproduction case. It has a severity. It has a person
attached to it who will tell you what they were trying to do. **Every ticket is a docs bug
report** — it just arrives in a queue nobody treats as a bug tracker.

We had a docs backlog before this. It was a list of pages we felt bad about. What we had never
had was a list of pages that had demonstrably failed, ranked by how often, with the failing query
attached.

## People don't read documentation. They search it, mid-panic, with the wrong words.

This is the second half of the finding and it is the half that changed how we write.

Our mental model of a reader was someone sitting down with the documentation the way you sit down
with a manual — beginning, middle, end, forming a picture. Almost nobody does this. The person
opening our docs is nine minutes into something not working, in a hurry, and often slightly
embarrassed. They type three or four words into a search box. They scan whatever comes back for
about six seconds. If the first paragraph does not contain their answer, they leave and open a
ticket.

And the words they type are not our words. We had a page titled *Configuring inbound routing
rules*. The tickets it should have answered said "emails going to the wrong inbox". Nobody
searching in a panic types "configuring". They type what is happening to them.

So the page was correct, complete, well organised, and invisible.

## What we did about it

Five things, in the order we did them, because the order mattered more than we expected.

1. **We tagged tickets against pages, not features.** Every ticket got the URL of the page that
   should have answered it. This took two weeks and it is the only expensive step. It is also the
   one that makes the other four possible — without it you are guessing which docs are failing,
   and everyone guesses their favourites.

2. **We ranked pages by tickets, not by traffic.** Traffic tells you what people found. Tickets
   tell you what they needed and didn't get. Our most-read page generated almost no tickets. Our
   fourth-most-read page generated more than the next six combined, and no dashboard we owned had
   ever pointed at it.

3. **We rewrote titles in the reader's words.** *Configuring inbound routing rules* became *Mail
   is going to the wrong inbox*. We kept the old title as a subheading, because the people who
   already knew our vocabulary should not be punished for it. Search traffic to that page went up
   by a factor we did not believe until we checked it twice.

4. **We moved the answer up.** For every page in the top twenty, we found the two questions its
   tickets actually asked and put both answers in the first paragraph. Not in a summary box, not
   after the prerequisites, not below the conceptual overview — in the first paragraph, in the
   first six seconds. **Two asks? First paragraph.** That is the whole rule and it is the one we
   still repeat to each other. *We moved three answers up* on the first afternoon and the ticket
   volume on those three pages fell inside a week.

5. **We closed the loop.** Support now files docs bugs directly, on the page, with the customer's
   own wording pasted in. Not a summary of the wording. The wording. That sentence is the search
   query we failed to match, and paraphrasing it destroys the only evidence in the ticket.

## What actually changed

Ticket volume on the top twenty pages fell by a bit over a third in the first quarter. **Same
docs. Fewer tickets.** We did not add a single new page during that period, which is the detail
we keep having to repeat, because the instinct when documentation fails is always to write more
documentation.

The second change was slower and matters more. Support stopped being a place where the same
question gets answered two hundred times and started being an instrument. A queue you read as
data behaves differently from a queue you read as work.

The third change was to the writing itself. Knowing that a reader arrives mid-panic, through a
search box, with the wrong words, is a constraint — and constraints are the only thing that has
ever made our documentation shorter.

## The part that generalises

None of this is really about documentation.

It is about a feedback channel that was already open, already full, already staffed, and pointed
at the wrong department. The tickets had been arriving the entire time. What was missing was
somebody willing to read them as reports about our writing rather than reports about our product.

If you have a support queue and a docs site and no path between them, the audit is one afternoon
and three questions. Which page should have answered this. What did the person actually type. Is
the answer in the first paragraph.

We ran the same exercise on our in-app help text a month later. Same result, smaller numbers, and
this time it took an afternoon instead of two weeks, because we already knew what we were reading.
