---
name: opus-or-fable
description: Pick the model and effort level for a coding task, and keep agent work in short, visible bursts. Use before starting a task, spawning a subagent or helper chat, or raising effort, and whenever a thread is stuck circling the same problem.
---

# Opus or Fable

Choosing between Claude Opus 5.5 and Fable 5.2 (and their effort levels) for coding work. The model rules come
from Theo's video "I think I figured it out" (https://www.youtube.com/watch?v=XtykeVoSmP8). They are his
opinions, from his own use and benchmarks. The burst and cost rules come from daily use on real projects.

## 1. Pick the model

Ask one question: **can the result be checked?**

- **Yes, it can be verified and iterated toward** (migrations, rewrites, refactors, plain features, bug fixes
  with a repro, tests, tuning numbers): use **Opus**.
- **No, it needs taste or a new idea** (visuals, animation, UI feel, game feel, architecture, naming, a problem
  nobody has framed yet): use **Fable**.

Default to Opus. Move to Fable when you want something *different*, not only when Opus has failed.

How they behave:

- **Opus is the teacher's pet.** It double-checks everything and rarely drops a detail. It does not push back,
  so it applies every piece of feedback, good or bad, and lets specs grow. When you brief it, add: *"If you think
  this is a good idea, do it. Otherwise, suggest something else."*
- **Fable is the smart kid at the back of the class.** It is more creative, questions the premise and knows when
  to stop. It is also lazier and misses small things, so pair it with a check (a screenshot, a test, an Opus
  pass) on anything detail-heavy.

Other models:

- **Sonnet**: not a main coding model. When it wanders it can cost as much as Opus.
- **Haiku**: bulk classification and pattern-finding over many items. Never for writing code.

## 2. Pick the effort

- **Opus: high** is the sweet spot. Medium can end its turn early. Low is weak for real code. Max overthinks.
- **Fable**: in Theo's benchmarks it scored worse on max than on xhigh.
- **Above high**, don't raise effort again. Try the bigger or different model at a lower effort instead.
- **xhigh** only for "turn over every stone" work: Windows-specific bugs, digging through huge logs.
- Under a tight budget, start lower (low or medium) and raise effort only when a task actually fails at that
  level.

## 3. When a thread is stuck

If Opus keeps circling, nitpicking or re-fixing the same thing, **bring in Fable to audit** the thread. It will
either find the real fix or tell you it is fine to ship. The reverse works too: let Opus build the thorough
harness (repro, test environment, measurements), then let Fable look at the evidence. In Theo's T3 Code
example, Opus built the performance test bed and Fable spotted a fix that cut data sent by about 150x in some
cases.

Code review: Opus and Sonnet catch more small issues than Fable. Use Fable for "is this the right design",
Opus for "is every line right".

## 4. Work in short bursts

Long autonomous runs are where budgets disappear and wrong directions go unnoticed.

- **One burst is one thing**, about 20 minutes on Fable and 30 on Opus, ending in something the human can look
  at (a screenshot, a short clip, the running app) and a report of a few lines. Then stop.
- **Never stack a multi-part brief into one run**, least of all for anything judged by eye (animation, looks,
  feel). Ship part one, get a "yes" or a "wrong direction", then do part two.
- **Judge by eye.** Passing tests and "0 errors" don't prove something looks or feels right.
- **Tests are short:** a compile and one quick run, not a long hidden series.

## 5. Helpers and subagents

- **At most two helpers at a time.** More than that burns the rate limit and nobody can review the output.
- **Resume a helper that already knows the work** instead of starting a fresh one that re-reads everything.
- **Put the model and effort in every helper's title**, e.g. `driving course [Opus medium]`, so the human can
  see what is spending.
- **Before anything that will run long or fan out** (many agents, a workflow, a big research sweep), say in
  one line roughly what it will cost in time and agents, and wait for a go.

## 6. Plan limits

On Claude subscription plans, Fable can use only part of the weekly limit (Theo puts it at roughly half), so
Opus stretches much further for the same money. Spend Fable where taste matters and Opus everywhere else.

## Quick table

| Task | Model | Effort |
| --- | --- | --- |
| Refactor, migration, rewrite | Opus | high (medium on a budget) |
| Bug with a repro, tests, tuning numbers | Opus | medium |
| UI look, animation, game feel, visuals | Fable | medium |
| Architecture or naming, an unframed problem | Fable | high |
| Thread stuck circling | Fable audit | medium |
| Line-by-line code review | Opus | medium |
| Reviewing clips, logs, screenshots | Opus | low |
| Classifying or tagging many items | Haiku | low |
