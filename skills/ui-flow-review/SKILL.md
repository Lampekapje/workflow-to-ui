---
name: ui-flow-review
description: Use when critiquing an existing or proposed interface, when someone asks what's wrong with an app or why it feels clunky, slow, or annoying, when reviewing wireframes or component trees, or before shipping frontend layouts to verify structural fit, interaction budgets, and state coverage.
---

# UI Flow Review

*Part of [FlowyourI](https://github.com/lampekapje/workflow-to-ui) by [Ivar Limpens Richaards](https://sixtyoneeighty.dev)*

Most complaints about interfaces — "it's clunky", "people don't use it", "it takes forever" — are structural, not aesthetic. The layout is the wrong shape for the work, or the repeated loop costs three times what it should. This skill finds that, in a form the person can act on.

## Start with the work, not the screen

Before critiquing anything, establish what the interface is *for*. Without that, you can only produce generic advice about contrast ratios and whitespace.

Determine: what the user does, how many times per session, how often, and what happens if they get it wrong. If you can't tell from what's been shared, ask one question — "what does someone do in here most often, and roughly how many times a day?" — because nearly every judgment below depends on the answer.

Then name the archetype using `../workflow-to-ui/references/work-archetypes.md`, and compare it to the shell actually being used. A mismatch here is the finding; everything else is detail.

## Measure the loop

Walk the primary loop and **count**. Clicks, keystrokes, page transitions, scroll-to-finds, and any moment the user has to re-find their place.

Compare against the budget for the stated volume (1 interaction per item at 100+/session, 1–3 at 20–100, 3–8 at 5–20). A loop 3× over budget is usually the single most valuable finding in the whole review, and it's a number rather than an opinion, which makes it hard to argue with and easy to act on.

## Run the rubric

`references/rubric.md` has the full checklist across seven dimensions, with the specific questions to ask and what a failure looks like. Work through it rather than reacting to whatever you noticed first — the reason a review is useful is that it catches the things nobody noticed, and the missing error state is never what catches your eye.

## Report

Order by cost to the user, not by how easy the fix is, and not in the order you found them. Use this shape:

```
## Verdict
[One or two sentences. Does the shape fit the work? If not, what should it be?]

## Primary loop
[The counted steps, the number, the budget, and where the excess is.]

## Findings
### 1. [Finding] — [structural / flow / state / safety]
What: [what the interface does now]
Why it costs: [the concrete consequence, quantified where possible]
Fix: [the specific change]

## Working well
[Genuinely, 2-3 things. Not filler — a review that finds nothing right is usually wrong,
and people discount an all-negative review entirely.]

## Not assessed
[Visual design, performance, content, accessibility beyond structure — whatever you
couldn't see or didn't cover.]
```

Quantify wherever possible. "Five interactions per item at 200 items a day is roughly 25 minutes of avoidable clicking per person per day" lands; "the flow feels inefficient" does not.

## Judgment

Separate what's **wrong** from what's **different from how you'd do it**. Plenty of unusual choices are correct for work you don't fully understand. If you can't articulate the cost to the user, it's a preference, and it should be labelled as one or dropped.

Be specific about uncertainty. "If this is used by trained staff daily, the missing labels are fine and the missing shortcuts aren't — if it's public-facing, reverse that" is more useful than hedged advice that assumes neither.

Don't drift into visual critique. Color, type, and spacing are `frontend-design`'s domain, and mixing them in reliably dilutes the structural findings — people fix the easy visual notes and skip the layout change that mattered.

## Reference

- `references/rubric.md` — the seven-dimension checklist with failure signatures
- Uses `../workflow-to-ui/references/` for archetypes, shells, states, and anti-patterns
