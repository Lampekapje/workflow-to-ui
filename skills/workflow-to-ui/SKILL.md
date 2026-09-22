---
name: workflow-to-ui
description: Use when someone describes work they want software to support ("a tool to review submissions", "track our pipeline", "log workouts", "design UI for X"), when receiving a UI request without a screen-by-screen spec, before writing frontend code to derive screens, layout shells, interaction loops, navigation, and state coverage from user workflows. Do not use for aesthetic styling (colors, fonts, brand).
---

# Workflow → UI

*Part of [FlowyourI](https://github.com/lampekapje/workflow-to-ui) by [Ivar Limpens Richaards](https://sixtyoneeighty.dev)*

Most bad interfaces are not ugly. They are the wrong *shape* for the work: a dashboard built for a job that is actually triage, a 40-field form for something people do on their phone in eight seconds, a wizard for a task done nine times a day.

This skill converts a description of work into a structural spec: what screens exist, what shell each one uses, what the user's repeated loop is, and what happens in every state. It deliberately says nothing about color, type, or framework.

## The procedure

Work through these five steps in order. Do not skip to step 4 — the layout is *derived*, and picking it first is how you end up with a dashboard nobody looks at.

### 1. Build the work model

You need seven facts. Infer as many as you can from what they already said, and only ask about the ones that would actually change the design. See `references/intake.md` for how to infer each one and how to ask without running an interview.

| Fact | Why it changes the design |
|---|---|
| **The verb** — what the user *does*, in their words | Selects the archetype |
| **Volume** — items per session: 1, 10, 500? | Decides density and whether per-item cost matters |
| **Frequency** — hourly, daily, monthly, once | Decides whether to optimize for learnability or speed |
| **Stakes** — reversible, annoying, catastrophic | Decides confirmation, undo, and guardrails |
| **Expertise** — will they use this 1000 times or twice? | Decides keyboard vs discoverability, labels vs icons |
| **Context** — desk, phone, warehouse floor, interrupted? | Decides input method and session resumption |
| **Session length** — 10 seconds or 3 hours? | Decides chrome, autosave, and focus mode |

Write this out explicitly. It is the thing you will check every later decision against.

### 2. Name the archetype

Read `references/work-archetypes.md` and match the work to one of the fourteen archetypes. The file opens with a quick-match table keyed on the phrases people actually use.

Almost every real app is **two or three archetypes**, not one. When that happens:

- Identify the **primary loop** — the thing done most often, by count, not by importance. A tool where managers approve 5 things a week and staff submit 300 is a capture tool with an approval annex, not an approval tool.
- Everything else becomes subordinate: a secondary screen, a mode, or a panel. It does not get equal billing in the navigation.
- If two archetypes are genuinely co-equal and conflict (e.g. dense triage and focused authoring), that is two apps, or two modes with a hard switch between them. Say so rather than averaging them into mush.

### 3. Design the loop before the screens

The primary loop is the 3–7 step cycle the user repeats. Write it as numbered steps and **count the interactions per item** (clicks, keystrokes, page loads, scroll-to-finds).

Then budget it, because per-item cost multiplies by volume:

| Volume per session | Target interactions per item |
|---|---|
| 100+ | 1 — one keystroke, auto-advance |
| 20–100 | 1–3, no mouse trip required |
| 5–20 | 3–8, mouse fine |
| 1–5 | Whatever it takes; optimize for confidence, not speed |

If the loop is over budget, fix it *here* — by removing steps, adding keyboard shortcuts, batching, defaulting, or deferring — not by making the buttons bigger later.

### 4. Pick the shell per screen

Read `references/layout-shells.md`. Each archetype names its default shell; the file gives the anatomy, the mobile collapse behavior, and how each shell fails. Only depart from the archetype's default shell if you can name why the work is unusual — and then say so in the spec.

Pick the navigation model at this point too (rules in `references/flow-and-states.md`): no nav, tabs, sidebar, or nested-with-search. The count of top-level destinations decides it, and if you have more than about 12, the information architecture is wrong rather than the nav.

### 5. Cover the states, then write the spec

Every screen owes an answer for: first-run, empty, loading, partial/slow, error, no-permission, too-much-data, and stale/offline. Most generated UIs specify only the happy path, which is the single most common structural failure. `references/flow-and-states.md` has the matrix and what each state should say.

Then produce the spec using `assets/ui-spec-template.md`. Before you hand it over, run the checklist in `references/anti-patterns.md` — it catches the recurring tells of an interface designed by pattern-match rather than from the work.

## Output

Default to the filled-in spec template as the deliverable — it is short, structural, and reviewable in a few minutes. Include the ASCII wireframes; they make wrong layouts obvious in a way prose does not.

**Handoffs:**

- To make it visible and clickable before anyone builds it → the `ui-wireframe` skill.
- For palette, typography, and visual identity once structure is settled → the `frontend-design` skill. Do not do its job here; mixing the two means the aesthetics get discussed and the structure does not.
- To critique an existing or proposed design against the work → the `ui-flow-review` skill.

## Working style

Propose, don't interrogate. State your assumptions as a compact work model and let them correct it — "I'm assuming this is triage: ~80 items a day, one decision each, at a desk. Correcting that changes the layout, so tell me if it's off." That is faster and better than five rounds of questions, and people are much better at rejecting a wrong guess than at answering an open question about their own work.

Be willing to say the shape is wrong. If someone asks for a dashboard and describes triage, build the triage tool and explain the substitution in one line. The dashboard they asked for would have been opened twice.

Design for the second week, not the demo. Empty states look great in a demo and are a rounding error in real use; the loaded, cluttered, 400-items-and-three-are-urgent state is what people actually live in. Spec that one first.

## Reference files

- `references/intake.md` — the seven facts: how to infer each, how to ask, what to do with no answer
- `references/work-archetypes.md` — the fourteen archetypes, their loops, shells, and failure modes (start with the quick-match table)
- `references/layout-shells.md` — twelve shells with anatomy, responsive behavior, density, and misuse
- `references/flow-and-states.md` — loop budgeting, navigation rules, the state matrix, modals, destructive actions, keyboard contract
- `references/anti-patterns.md` — the pre-handoff checklist and the recurring structural tells
- `assets/ui-spec-template.md` — the output format
