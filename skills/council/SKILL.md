---
name: council
description: Have other models score a finished change from 1 to 10 and keep fixing until every score clears a bar, with a hard cap on rounds. Use when the user says "council 9" (or any number), before calling risky work done, or when a change must match someone's taste ("would Sean like this").
---

# Council

From Theo's video "Stop Searching For the Perfect Model"
(https://www.youtube.com/watch?v=TWoS5Nmyoc8). The idea is his; the caps are ours, because the uncapped version
burns a week of tokens in two days.

## The idea

A model that wrote the code is in "make the change" mode: fast, confident, done. Put a model in "review this"
mode and it behaves differently, even if it is the same model
([13:59](https://www.youtube.com/watch?v=TWoS5Nmyoc8&t=839s)). A model from a different company is different
again: models from one family review like the same person at different times of day
([06:01](https://www.youtube.com/watch?v=TWoS5Nmyoc8&t=361s)).

Theo's numbers ([12:01](https://www.youtube.com/watch?v=TWoS5Nmyoc8&t=721s)): Opus scored its own first draft
7.4 and the last round 8.9. Reviewers from other families went from about 7.7 to 9.1. So even with only Claude,
a separate review step pays off; with another family available, it pays off more.

## How to run it

`council N` means: the work is not done until every reviewer scores it N or higher.

1. Finish the change and verify it yourself first (run it, look at it).
2. Start the reviewers, **in parallel, at most two**:
   - Prefer one model from a different family if the harness offers one (Codex/GPT, Gemini, another).
   - With only Claude: one fresh reviewer that did not write the code. Opus for checkable code, Fable when the
     question is taste.
   - Effort **high, not xhigh**. Higher effort finds more nits and the loop never ends
     ([23:00](https://www.youtube.com/watch?v=TWoS5Nmyoc8&t=1380s)).
3. Give each reviewer the same brief: what changed, why, how to run it, and the scoring question. Reviewers may
   run the code, test it and ask you questions. That is the point; a diff alone is a weaker review
   ([16:00](https://www.youtube.com/watch?v=TWoS5Nmyoc8&t=960s)).
4. Each returns a score from 1 (throw it away) to 10 (can't see why you wouldn't merge) and the issues behind
   any lost points.
5. Fix what is real, then re-score.

## Hard caps

- **Three rounds at most.** If scores are not rising, stop and tell the user where it stands.
- **Do not let reviews grow the scope.** Fix the issues that matter to this change; list the rest for the user.
  Theo saw a 1,000-line PR grow to 20,000+ lines and 600 subagents chasing every edge case
  ([21:00](https://www.youtube.com/watch?v=TWoS5Nmyoc8&t=1260s)).
- **Before the first round, say the cost in one line** (reviewers, model, effort) when on a tight plan.
- Skip council for small or easily undone changes. It is for risky code, security, and work that must match
  someone's taste.

## Taste scoring

The score question can be anything a model can judge
([17:02](https://www.youtube.com/watch?v=TWoS5Nmyoc8&t=1022s)):

- "How likely is Sean to be happy with this?" (point reviewers at his written rules and taste notes)
- "Would a design studio put this in a portfolio?"
- Several axes at once: how bad is the problem it fixes, how likely is it to cause trouble later, how likely is
  it to annoy the user.

If one reviewer flags something the user hates and the others missed it, block on it anyway.

## Report

At the end, list each reviewer, its model, and its scores per round, e.g.
`Opus high: 7 → 9 · Fable medium: 8 → 9.5`. Put the same lines at the bottom of the PR if there is one.

## Also from the video

- Give the agent permission to throw work away. Agents are scared to delete code; say "nothing here is
  essential, this can be scrapped" when a direction is wrong
  ([20:00](https://www.youtube.com/watch?v=TWoS5Nmyoc8&t=1200s)).
- The goal is that the agent comes back only when the work is ready, verified, and scored, so the user is not
  watching threads ([24:01](https://www.youtube.com/watch?v=TWoS5Nmyoc8&t=1441s)).
- Not worth it on pay-per-token API pricing. It is a subscription-stacker's tool
  ([23:00](https://www.youtube.com/watch?v=TWoS5Nmyoc8&t=1380s)).
