# One post → twelve pieces

The file from the video. The twelve pieces the agent produced overnight from one blog post, each
with the rule it follows, the failure mode worth checking, and the piece itself.

The source post is **"The Ultimate 2026 Guide to ChatGPT/AI Cold Emails"**,
<https://reply.io/blog/chatgpt-ai-cold-emails/> — mapped in [`example-post.md`](example-post.md).
Every piece below comes from that one article.

## The instruction the agent runs on

Verbatim, the prompt from the video:

> Watch the blog. When a new post goes live, rewrite it overnight into 12 pieces — 4 LinkedIn, 5 X,
> 1 newsletter, 2 threads. Match each platform's tone, queue for review by 7 AM.

That mix is the part to edit. **4 + 5 + 1 + 2** is what this channel publishes into; yours will be a
different four numbers. Everything else in this file — the rules, the reject-ifs, the shape of each
piece — transfers unchanged.

The run, as the video shows it:

```
Watch    reply.io/blog · new posts
         1 new post · Sep 21 · Cold email
Read     chatgpt-ai-cold-emails.md
         2,480 words · 3 strongest lines
Rewrite  12 pieces → content-calendar
         4 LinkedIn · 5 X · 1 newsletter · 2 threads

Twelve pieces queued for review — 7:00 AM
```

## How to read the rules

Each piece has three lines it is held to:

- **Shaped for** — where it will live, which decides length and register.
- **Rule** — the transformation. This is what stops twelve pieces from being one piece pasted twelve
  times.
- **Reject if** — the failure mode specific to this piece. The review queue checks this.

Of the twelve below, **four came back edited** in the video's review pass — pieces 2, 5, 10 and 11.
That ratio is the honest one: about a third needs a human hand, and roughly one in ten misses
platform tone in a way only a person catches.

---

# LinkedIn — four pieces

Long-form, professional, slower. The reader will give you six paragraphs if the first one earns it.

## 1 · "The first line does more work than the subject line"

**Shaped for** the feed, read by people who will stop for an argument if it starts with a claim.
**Rule** open with the counter-intuitive half of the article's finding, then earn it.
**Reject if** it opens by announcing the topic ("A few thoughts on cold email subject lines…").

> Everyone optimises the subject line. We spent a quarter on it.
>
> Then we looked at what actually moved reply rates, and it wasn't the subject line. It was the line
> underneath it.
>
> The subject gets you opened. The first line decides whether they keep reading — and the only thing
> that works there is proof the email was written for this person, not at them.
>
> One specific detail. Something you could not have written to anybody else.
>
> That is the whole test. If the first line survives a find-and-replace on the company name, it isn't
> a first line. It's a greeting.

## 2 · "We stopped sending 'Re:' subject lines. Here is what replaced them." · *edited*

**Shaped for** the reader who has used the trick and half-knows it is a trick.
**Rule** name the tactic, concede why it worked, then give the replacement. Do not moralise.
**Reject if** it scolds. The people doing this are the audience, not the villain.

> We looked at what actually moved reply rates this year.
>
> It wasn't the tool. It was the first line — proof the email was written for this person, not at
> them.
>
> Three habits we kept:
>
> 1. Subject line: two to four words, no clickbait.
> 2. First line: one specific detail about them.
> 3. One ask, one link, then stop.
>
> We stopped sending "Re:" subject lines. Here's what we send instead: the actual subject. Two to
> four words describing the thing. It gets opened less often and answered more often, and the second
> number is the one that pays.

## 3 · "Write for them, not at them."

**Shaped for** a short post built around one line from the article.
**Rule** lead with the quote, then one concrete example of the difference. No more than five lines.
**Reject if** the example is abstract — "be more personal" is the thing this is replacing.

> "Write for them, not at them."
>
> At them: "I wanted to reach out because we help companies like yours improve outbound efficiency."
>
> For them: "You're hiring three SDRs this quarter — that's usually when the sequence tooling starts
> to hurt."
>
> Same offer. The second one could not have been sent to anyone else, and that is the entire
> difference.

## 4 · "What actually moved reply rates this year"

**Shaped for** the reader who wants the finding and the method behind it, not the anecdote.
**Rule** lead with the result, then the evidence, then what it costs to copy.
**Reject if** it reads as a case study with the numbers removed.

> What actually moved reply rates this year, in order:
>
> **The first line.** One specific, checkable detail about the recipient. Bigger effect than anything
> else on this list.
>
> **Subject length.** Short wins — the guide has 1–5 words outperforming, and 1–3 word subjects ahead
> of longer ones.
>
> **One ask.** One question or one suggestion. Two asks halve the reply rate because the reader now
> has to decide which one they are answering.
>
> **Total length.** Under 70 words. Two or three short paragraphs. Fifteen seconds to read.
>
> What did *not* move it: the tool, the send-time tweaking, the signature design. The first line is
> where the work is.

---

# X — five pieces

Short, fast, competing with everything else on the screen. One idea per post.

## 5 · "Subject line: 1–5 words. That's it." · *edited*

**Shaped for** the scroll. One claim, no preamble.
**Rule** state the number, stop. The whole post is the rule.
**Reject if** it explains itself. Explanation is what the LinkedIn version is for.

> Subject line: 1–5 words. That's it.
>
> 1–3 gets replied to more than anything longer.
>
> You are not writing a headline. You are writing a label.

## 6 · "1–5 words. That's a subject line."

**Shaped for** the same claim, reframed as a correction rather than advice.
**Rule** show the before and after. No commentary between them.
**Reject if** the bad example is a strawman nobody would actually send.

> "Quick question about your Q4 outbound strategy and whether we might be a fit"
>
> That's not a subject line. That's the email.
>
> "Q4 outbound" — 1–5 words. That's a subject line.

## 7 · "Personalize the first line, not the signature"

**Shaped for** the reader who has already personalised the wrong thing.
**Rule** name the common misplacement, then point at the right place.
**Reject if** it says "personalise more". The point is *where*, not *how much*.

> Personalize the first line, not the signature.
>
> Nobody has ever replied because your footer had their company logo in it.
>
> They reply because line one proved you knew something about them before you hit send.

## 8 · "AI assists the human touch — it doesn't replace it."

**Shaped for** a quote post that closes an argument rather than opening one.
**Rule** the quote, then the one-sentence cost of getting it wrong.
**Reject if** it is the quote alone — a quote with no consequence is a poster, not a post.

> "AI assists the human touch — it doesn't replace it."
>
> The failure mode isn't bad AI output. It's good AI output that nobody read before sending.

## 9 · "Two to four words in the subject → higher open rate"

**Shaped for** the feed, as a finding rather than an opinion.
**Rule** one arrow, one claim, one caveat. The caveat is not optional — it is what makes it credible.
**Reject if** it presents a tendency as a law.

> Two to four words in the subject → higher open rate.
>
> Caveat worth stating: opens are not replies. Short subjects get opened; the first line is what gets
> answered. Optimise the subject for the open and the first line for the reply, and stop grading them
> on the same number.

---

# Newsletter — one piece

## 10 · "This week: the subject-line rule we keep breaking" · *edited*

**Shaped for** a section inside a longer letter, read by people who already subscribed.
**Rule** **a fresh opening line.** The newsletter never reuses the article's first sentence — a
subscriber who read the post should still find something new in the first three seconds. Enter
through a different door: an aside, a cost, a confession.
**Reject if** the first line is the article's first line, reworded.

> **This week: the subject-line rule we keep breaking**
>
> Open rate slipped last quarter? Start with the subject: two to four words, no clickbait.
>
> We know the rule. We published the rule. And going back through what we actually sent last quarter,
> several sequences opened with something over eight words — and a couple of those were
> fake-familiar: the "Re:" trick, on a thread that never existed.
>
> Here is the rest of the checklist we now run before every send:
>
> - Subject line — 3–5 words, clean and personal. No "Re:", no "following up".
> - First line — one specific detail about them, not about us.
> - Reason for outreach — why now, in one sentence.
> - Value — what's in it for them, with proof.
> - CTA — one question or one suggestion. Not two.
> - Signature — plain.
>
> Under 70 words total. Two or three short paragraphs. Fifteen seconds to read.
>
> The uncomfortable part: every one of those is in the guide we published, and we still had to build
> a checklist to make ourselves do it.

---

# Threads — two pieces

A thread is not a long post with line breaks. Each post has to survive being read alone, because
some of them will be.

## 11 · "How to write a cold email in 2026" — five posts · *edited*

**Shaped for** a reader who saves threads and comes back to them.
**Rule** one claim per post, five posts, no padding. Post one states the problem; posts two to four
are the method; post five is the transferable rule.
**Reject if** any post needs the previous one to make sense.

> **1/5** Most cold emails fail before the first line. Not because the offer is wrong — because the
> subject was written to be clever instead of clear.
>
> **2/5** Subject: 1–5 words. Describe the thing. "Q4 outbound", not "a quick question about your
> outbound strategy". You are labelling, not selling.
>
> **3/5** First line: one specific detail about them. This is where you show the email was written
> for them, not at them. If it survives find-and-replace on the company name, rewrite it.
>
> **4/5** Value: 1–2 short sentences. What's in it for them, with proof. Then one ask — one question
> or one suggestion. Two asks and they answer neither.
>
> **5/5** Whole thing under 70 words, fifteen seconds to read. Then the test that catches everything
> the rules miss: would you reply to this yourself?

## 12 · "Five subject lines we would actually send" — four posts

**Shaped for** the reader who wants examples, not principles.
**Rule** show the lines. Commentary is one line per example, maximum. The last post is the pattern.
**Reject if** the examples are generic enough to belong to any company.

> **1/4** Five subject lines we would actually send, and why each one works. All 1–5 words, none of
> them clever.
>
> **2/4** "Q4 outbound" — names the topic, nothing else.
> "Your SDR job post" — proves we looked.
> "Sequence tooling" — two words, zero pitch.
>
> **3/4** "Reply rates, honestly" — signals the register before they open it.
> "3 SDRs, 1 question" — the only one with a number, and the number is theirs.
>
> **4/4** The pattern: every one of them is a label for something real on their side. None of them
> promises a benefit, and none of them pretends to be a reply to a thread that never existed.

---

## The review step, and why it stays

Twelve pieces landed in the queue at 7:00 AM. Four came back edited — pieces 2, 5, 10 and 11 above.
The rest went out as written.

That is the ratio to plan for. The agent is good at structure and reliable about the rules; what it
misses is platform tone, and it misses it in ways that read fine in isolation and wrong in the feed.
Ten minutes of review per batch is what keeps the system honest, and it is the step worth protecting
when someone suggests automating the last mile.

Two limits worth stating plainly:

- **The agent multiplies what you give it.** A weak original becomes twelve weak pieces. This system
  rewards writing fewer, better posts — that pressure is a feature.
- **Derivation is not judgement.** The agent can check that a piece came from the source. It cannot
  tell you whether the piece is worth publishing.

## Running this yourself

The agent reads the source post once and produces all twelve in a single pass, then writes them into
the review queue rather than publishing. The three things to change before you run it:

1. **The mix.** `4 LinkedIn, 5 X, 1 newsletter, 2 threads` → wherever you actually publish.
2. **The tone notes.** One short paragraph per platform, in your voice, describing how that platform
   sounds when you get it right.
3. **The queue.** Anything that holds drafts and lets a person mark them read or edited. The point is
   that nothing reaches an audience without someone having looked at it.
