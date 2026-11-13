---
name: opus-or-fable
description: Pick the model and effort level for a coding task, and keep agent work in short, visible bursts. Use before starting a task, spawning a subagent or helper chat, raising effort, setting up a review loop, or whenever a thread is stuck circling the same problem.
---

# Opus or Fable

Choosing between Claude Opus 5.5 and Fable 5.2, and their effort levels, for coding work. The model rules come
from Theo's video "I think I figured it out" (https://www.youtube.com/watch?v=XtykeVoSmP8). They are his
opinions from his own use and benchmarks, and he had used Fable 5.2 for two days when he recorded it. Each rule
links to the moment in the video where he says it. The burst and cost rules come from daily use on real
projects.

## 1. Pick the model

Ask one question: **can the result be checked?**
([35:32](https://www.youtube.com/watch?v=XtykeVoSmP8&t=2132s))

- **Yes, it can be verified and hill-climbed toward** (migrations, rewrites, refactors, a port to another
  language, bugs with a repro, tests, tuning numbers): use **Opus**.
- **No, it needs taste, nuance or a new idea** (better graphics, a visualizer that doesn't look like every
  other one, a clever infrastructure change, architecture, naming): use **Fable**.

Default to Opus, and reach for Fable when you **want something different from Opus**, not only when Opus
fails ([37:15](https://www.youtube.com/watch?v=XtykeVoSmP8&t=2235s)):

- Opus did not do a good enough job.
- You don't like the options Opus offered. Ask Opus for five solutions and two are near-copies and two make
  no sense; Fable gives a wider spread ([38:32](https://www.youtube.com/watch?v=XtykeVoSmP8&t=2312s)).
- A thread has been circling and you want to land it (section 4).

And the other way round: Fable is not always better. Theo has re-run tasks that Fable got wrong on Opus and
got the right result ([37:15](https://www.youtube.com/watch?v=XtykeVoSmP8&t=2235s)).

## 2. How the two behave

**Opus is the teacher's pet** ([21:23](https://www.youtube.com/watch?v=XtykeVoSmP8&t=1283s)).

- It double- and triple-checks everything and rarely misses a detail. It is the model that reminds the
  teacher to hand out the homework.
- It doesn't challenge the task. It will bloat a spec and let features creep in unless told otherwise.
- It applies every piece of feedback, good or bad. Put an automated reviewer on it and a 30-line PR turns into
  1,000+ lines ([30:47](https://www.youtube.com/watch?v=XtykeVoSmP8&t=1847s)). Cap review loops and filter the
  feedback before Opus sees it.
- Add to Opus prompts: *"If you think this is a good idea, do it. Otherwise, suggest something else."*
  ([23:40](https://www.youtube.com/watch?v=XtykeVoSmP8&t=1420s)). Its counter-suggestions are sometimes wrong;
  that is fine, you decide.
- Best when the agent must know everything about the task before it starts. In the "read the whole test
  before answering" trick test, Opus passes and Fable fails
  ([26:24](https://www.youtube.com/watch?v=XtykeVoSmP8&t=1584s)).

**Fable is the smart kid at the back of the class** ([26:00](https://www.youtube.com/watch?v=XtykeVoSmP8&t=1560s)).

- It is lazy in a useful way: it finds the clever shortcut, challenges the premise and will throw out work
  that is going nowhere.
- It knows when to stop. Theo has only seen Fable reliably avoid "not knowing when to stop"
  ([30:47](https://www.youtube.com/watch?v=XtykeVoSmP8&t=1847s)).
- It misses small things. In his example, a Fable-edited video put text behind the player bar where nobody
  could see it ([07:12](https://www.youtube.com/watch?v=XtykeVoSmP8&t=432s)). Check its UI work by eye.

The reviewer version ([31:46](https://www.youtube.com/watch?v=XtykeVoSmP8&t=1906s)): Opus is the engineer who
has been on the codebase for years and leaves eight comments on a small PR. Call it when the change is high
risk and must be perfect. Fable is the senior hire who glances at it and says "looks good". Call it when you
want to ship.

## 3. Pick the effort

- **Opus: high is the sweet spot** ([07:38](https://www.youtube.com/watch?v=XtykeVoSmP8&t=458s)). Medium (the
  default) ends its turn a bit early and checks less. Low is weak for real code. Max is bad: it forces long
  thinking even on simple tasks ([08:57](https://www.youtube.com/watch?v=XtykeVoSmP8&t=537s)).
- **If medium is always enough for you, ask for bolder things**
  ([09:21](https://www.youtube.com/watch?v=XtykeVoSmP8&t=561s)).
- **Fable** scores worse on max than on xhigh in most benchmarks
  ([08:12](https://www.youtube.com/watch?v=XtykeVoSmP8&t=492s)). Overthinking is not free quality.
- **Past high, switch models instead of raising effort.** One more effort level can cost as much as the bigger
  model, so try the next model up at a lower effort
  ([11:49](https://www.youtube.com/watch?v=XtykeVoSmP8&t=709s)).
- **xhigh** for "turn over every stone" work: Windows development, digging hidden errors out of huge logs and
  building a way to replay them, exploratory PRs you won't merge
  ([13:05](https://www.youtube.com/watch?v=XtykeVoSmP8&t=785s)). For that kind of work Opus on xhigh beats
  Fable.
- Under a tight budget, start lower and raise effort only when a task actually fails at that level.

## 4. When a thread is stuck

If Opus keeps circling, second-guessing or nitpicking, **bring in Fable to audit**
([39:38](https://www.youtube.com/watch?v=XtykeVoSmP8&t=2378s)). Ask it to verify the work so far and say what
should actually happen next. Either it is smarter and finds the real fix, or the work is already good enough
and it says to ship.

Split the work by strength ([27:55](https://www.youtube.com/watch?v=XtykeVoSmP8&t=1675s)): let Opus build the
thorough harness (repro, test environment, measurements), then let Fable play with it and find the edge that
actually matters. In Theo's T3 Code case, Fable spotted the fix and cut data sent by about 150x in some
cases. Fable alone built a worse test environment.

## 5. The other models

- **Sonnet**: don't pick it as your main model. Without a clear path it wanders and can cost as much as Opus.
  It is fine as a scoped tool your agents call ([10:08](https://www.youtube.com/watch?v=XtykeVoSmP8&t=608s)).
- **Haiku**: bulk analysis: sorting a lot of data, or checking every file for a bad pattern you can't find
  with a script. Never for writing code, and not as a general side-task helper
  ([11:26](https://www.youtube.com/watch?v=XtykeVoSmP8&t=686s)).
- **Subagents and orchestration** don't require Fable. Opus can command huge migrations with many subagents;
  Theo rewrote a whole compiler in Rust with Opus as commander and implementer
  ([15:37](https://www.youtube.com/watch?v=XtykeVoSmP8&t=937s)).
- **Speed is not a reason to choose**: he measures Opus at about 112 and Fable at about 106 tokens per second
  (Sonnet about 145, Haiku about 255) ([18:11](https://www.youtube.com/watch?v=XtykeVoSmP8&t=1091s)).

## 6. Plan limits

- A Claude subscription buys far more tokens than the same money on the API or any other provider; Theo
  estimates a $100 plan at $3-5k of usage ([03:00](https://www.youtube.com/watch?v=XtykeVoSmP8&t=180s)).
- Fable can use only half of the weekly limit. On the $200 plan he puts that at roughly $3k of Fable versus
  $14k of pure Opus a month, and the other half still works for Opus
  ([16:28](https://www.youtube.com/watch?v=XtykeVoSmP8&t=988s)). On the API, Fable on high can beat Opus on max
  at half the cost per task; on a subscription, the limits flip that.
- Spend Fable where taste matters and Opus everywhere else.

## 7. Work in short bursts

Long autonomous runs are where budgets disappear and wrong directions go unnoticed.

- **One burst is one thing**, about 20 minutes on Fable and 30 on Opus, ending in something the human can look
  at (a screenshot, a short clip, the running app) and a report of a few lines. Then stop.
- **Never stack a multi-part brief into one run**, least of all for anything judged by eye (animation, looks,
  feel). Ship part one, get a "yes" or a "wrong direction", then do part two.
- **Judge by eye.** Passing tests and "0 errors" don't prove something looks or feels right.
- **Tests are short:** a compile and one quick run, not a long hidden series.

## 8. Helpers and subagents

- **At most two helpers at a time.** More than that burns the rate limit and nobody can review the output.
- **Resume a helper that already knows the work** instead of starting a fresh one that re-reads everything.
- **Put the model and effort in every helper's title**, e.g. `driving course [Opus medium]`, so the human can
  see what is spending.
- **Before anything that will run long or fan out** (many agents, a workflow, a big research sweep), say in
  one line roughly what it will cost in time and agents, and wait for a go.

## Quick table

| Task | Model | Effort |
| --- | --- | --- |
| Refactor, migration, rewrite, port | Opus | high (medium on a budget) |
| Orchestrating many subagents | Opus | high |
| Bug with a repro, tests, tuning numbers | Opus | medium |
| Windows bugs, hidden errors in huge logs | Opus | xhigh |
| UI look, animation, game feel, visuals | Fable | medium |
| Architecture or naming, an unframed problem | Fable | high |
| Opus's options all look the same | Fable | medium |
| Thread stuck circling, "can we ship this?" | Fable audit | medium |
| High-risk change that must be perfect | Opus review | high |
| Reviewing clips, logs, screenshots | Opus | low |
| Checking every file or row for a pattern | Haiku | low |
