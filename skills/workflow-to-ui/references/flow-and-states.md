# Flow and states

The layout is half the design. The other half is what happens over time: where people land, what they repeat, how they get out, and what the screen shows when things aren't ideal.

## Entry: three arrivals, not one

Every app has three arriving users, and designing only for the first is why so many tools feel empty and then feel overwhelming.

1. **Never used it.** Needs orientation and a first success. Wants: one obvious action, sample or seeded data, and no configuration before value.
2. **Returning with work to do.** This is the overwhelming majority of all sessions, and the state to optimize. Wants: straight into the primary loop, with what's changed since last time visible.
3. **Returning with nothing pending.** Everything's handled. Wants: acknowledgement that it's done, and a useful secondary suggestion — not a false-alarm empty state that looks broken.

Specify the home screen for state 2 first. Then check it degrades gracefully to 1 and 3.

## The primary loop

Write the repeated cycle as numbered steps, then count interactions per item and compare against the budget:

| Items per session | Budget per item | Implication |
|---|---|---|
| 100+ | **1** | Single keystroke, auto-advance, no confirms |
| 20–100 | **1–3** | Keyboard path required, no mouse trip |
| 5–20 | **3–8** | Mouse fine, but no page reloads mid-loop |
| 1–5 | unbounded | Optimize confidence, not speed |

Ways to get back under budget, roughly in order of value:

- **Remove a step.** Usually a confirmation, a navigation, or a field with a knowable default.
- **Default it.** Last value, current time, their team, the only option.
- **Batch it.** One decision covering 20 items beats 20 decisions.
- **Keyboard it.** Single keys for the hot outcomes, shown in the interface.
- **Auto-advance.** Never make the user re-find their place.
- **Replace confirm with undo.** One interaction saved per item, and a better safety story.

A loop that reads fine in prose can still be terrible — the count is what catches it. "Click the row, click Edit, change the status dropdown, click Save, click Back" is five interactions and a page transition for something that should be one key.

## Navigation model

Choose on the count of top-level destinations:

| Destinations | Model |
|---|---|
| 1 | **No nav.** Hero tool. Don't add a nav bar to justify the header. |
| 2–5 | **Tabs** — bottom bar on mobile, top bar on desktop. All visible at once. |
| 6–12 | **Sidebar**, grouped, collapsible, with the current location marked. |
| 13+ | **Nested + search.** But first: is this actually several apps, or one app with a bloated IA? |

Rules that hold across all of them:

- Name destinations after **what the user does or seeks**, not the data model. "Approvals", not "Workflow Entity Manager".
- The primary loop gets the home slot and the best keyboard access. Rank by frequency, not by org chart.
- Current location always visible. Deep hierarchies need breadcrumbs.
- Never nest more than two levels deep in a sidebar.
- The nav should *disappear* when someone enters a focus surface (canvas, wizard, full-screen triage). Chrome that's useful for finding work is noise while doing it.

## The state matrix

Specify these for every screen. Most generated UIs cover only the happy path, and this is the single most common structural failure — the states below are where real users spend a surprising share of their time.

| State | What it must do |
|---|---|
| **First run** | Explain the value in one line and offer one action. Seeded/sample data beats an empty grid. |
| **Empty (by choice)** | "Nothing to review" is *success* — say so. Don't dress a finished queue as a failure. |
| **Empty (after filtering)** | Say which filter caused it and offer to remove it. |
| **Loading — first** | Skeleton matching the real layout, so nothing jumps when it lands. |
| **Loading — subsequent** | Keep the old content visible and dim it. Never blank a screen the user was reading. |
| **Slow (>3s)** | Progress, an estimate if you have one, and a cancel. Partial results beat a spinner. |
| **Error — recoverable** | Plain language, what happened, what to do, retry button, and the entered data preserved. |
| **Error — unrecoverable** | What failed, whether data was lost, who to contact, a reference code. |
| **No permission** | Why, and how to request access. Not a 403. Don't show an action and then deny it — hide or disable with a reason. |
| **Too much data** | Where volume can outgrow the layout, define the fallback: pagination, virtualization, a forced filter, or a switch to a denser shell. |
| **Stale / offline** | Say when data is from, whether actions will queue, and what happens on reconnect. |
| **Conflict** | Two people edited it — say so, show both, let a human choose. Never silent last-write-wins. |

## Modals

Budget: roughly **zero to one** modal in a primary loop.

A modal is right when: the decision is genuinely blocking, it's irreversible, it needs full attention, and it's rare. That's about it.

Use instead:
- Inline editing for a small change
- A side panel for detail that keeps context visible
- A new screen for anything with more than about three fields
- A toast with undo for confirmation of a reversible action

Never put a modal inside a modal. If you need to, the flow is wrong.

## Destructive actions

Match the friction to the consequence. The common failure is applying the same weight everywhere — which trains people to click through everything, including the one that mattered.

| Consequence | Treatment |
|---|---|
| Reversible, small | **Just do it** + undo toast (5–10s) |
| Reversible, large (bulk) | Do it + undo, stating the count: "Archived 47 items — Undo" |
| Irreversible, recoverable elsewhere | Confirm dialog naming the specific thing |
| Irreversible, permanent | Type-to-confirm, plus a cooling-off or delay where feasible |
| Affects other people | Show the blast radius before confirming: "This removes access for 12 people" |

Undo is nearly always better than confirm: it costs the user nothing on the happy path and protects against the slip that a dialog they've stopped reading doesn't.

## Keyboard contract

For any expert or high-volume tool, specify these explicitly — retrofitting keyboard support is much harder than designing for it.

- Focus visible at all times, and a logical tab order that follows the visual layout.
- `/` or `⌘K` for search/command from anywhere.
- `Esc` closes the topmost layer, consistently.
- `j`/`k` or arrows to move through lists without a mouse.
- Single keys for the primary outcomes in a triage loop, **displayed in the UI** — a shortcut nobody discovers doesn't exist.
- `⌘Enter` to submit from inside a text field.
- Nothing may be mouse-only. Every drag needs a keyboard equivalent.

## Responsive behavior

Decide per screen which of these applies, rather than assuming everything reflows:

- **Reflow** — multi-column collapses to one, in a priority order you have explicitly decided.
- **Reveal** — secondary panels become drawers or sheets behind a control.
- **Replace** — a different shell entirely for small screens (table → cards, month grid → agenda).
- **Refuse** — some surfaces genuinely don't belong on a phone. A good mobile *viewer* is more honest than a bad mobile editor. Say which you chose.

The question to answer per screen is "what is the phone user actually trying to do here?" — usually a subset, occasionally the whole job, sometimes nothing.
