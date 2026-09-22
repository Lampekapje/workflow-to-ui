---
name: ui-wireframe
description: Use when turning a UI spec, workflow, or app concept into a low-fidelity clickable HTML wireframe (greyscale, real content, reachable states, primary loop) to evaluate layout and interaction flow before writing production code or visual styling.
---

# UI Wireframe

*Part of [FlowyourI](https://github.com/lampekapje/workflow-to-ui) by [Ivar Limpens Richaards](https://sixtyoneeighty.dev)*

A wireframe's job is to make a structural mistake obvious in thirty seconds. It does that by being *deliberately unfinished* — greyscale, plain, no brand — so that everyone looking at it discusses the layout and the flow instead of the shade of blue.

This is the step between the spec and the build. It is cheap, and it is where the expensive mistakes get caught.

## Before you start

You need a work model — archetype, volume, primary loop. If you don't have one, use the `workflow-to-ui` skill first; wireframing without it just renders a guess at higher fidelity and makes the guess harder to argue with.

## Rules that make a wireframe useful

**Greyscale only.** Whites, greys, near-black. One accent grey for the primary action, used once per screen. The moment real color appears, feedback shifts to aesthetics and the structural review is over. This is the most important rule here and it is worth defending.

**Real content, never lorem ipsum.** Use plausible names, realistic lengths, actual domain vocabulary. Lorem ipsum hides the two most common layout failures: content that's far longer than the box, and content that's far shorter and leaves the layout looking empty. Include at least one deliberately long value and one empty one per list.

**Realistic volume.** If the real thing has 200 rows, show enough to make density real — 30+ rows, not 5. A wireframe with three tidy rows makes every layout look fine. The loaded state is the one people live in.

**Every state reachable.** Add controls to switch between empty, loading, error, and loaded. These are the states the build will get wrong, and they're free to demonstrate here. A small state-switcher bar at the top of the page is fine — it's a review tool, not part of the design.

**Clickable through the primary loop.** The whole loop should be walkable, even if the rest is dead. Include the keyboard shortcuts if the spec has them — wire up the actual keys, because a keyboard-driven design cannot be evaluated with a mouse.

**Annotations, not guesses.** Where behavior can't be shown, label it. Numbered margin notes explaining "sorts by age, sticky", "autosaves every 3s", "this is 400 rows in production" carry more review value than the pixels do.

## Build

Use `assets/wireframe-kit.html` as the starting point. It's a single self-contained file with the greyscale token set, the common shell structures, a state switcher, and an annotation layer. Copy it and fill in the real screens.

Structure the output as **one HTML file containing every screen**, switched by a simple screen selector at the top rather than separate files. Reviewers flip between screens constantly, and separate files break that.

Technical notes:
- Single self-contained file. Inline CSS and JS. No build step, no external requests — it needs to survive being emailed around.
- Plain HTML and vanilla JS. No framework. This is a sketch, and its code should be disposable without regret.
- Keep it under a few hundred lines per screen. If a screen needs more, the screen is too complicated.
- Responsive if the spec calls for mobile: include a viewport toggle so the collapse behavior can be reviewed too.

Read `references/wireframe-conventions.md` for the visual shorthand — how to indicate images, charts, avatars, truncation, loading, and interactive affordances without drawing them properly.

## Presenting it

Lead with what you want them to look at, not a tour of the features. Something like: "the triage loop is the thing to judge here — press `j` to move down the queue and `a` to accept. I'm assuming 200 items a day, which is why the rows are this tight."

Name your uncertainties explicitly. "I wasn't sure whether the evidence panel needs the full history or just the last three events — it's showing the full history and it's crowding the decision buttons." Reviewers engage far better with a specific doubt than with "let me know what you think".

Then offer the two forks: adjust the structure, or move to `frontend-design` for the visual layer.

## What not to do

Don't add color "just to make it nicer". Don't choose a typeface. Don't polish it toward looking finished — a wireframe that looks done gets approved rather than critiqued, which defeats its only purpose. If someone says "it looks unfinished", that's the wireframe working; say so, and point out that changing the structure now costs minutes.
