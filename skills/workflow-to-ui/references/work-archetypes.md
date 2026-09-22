# Work archetypes

Fourteen shapes of work, each with the interface that fits it. Match on the **verb and the volume**, not the subject matter — "managing invoices" tells you nothing; "going through 200 invoices deciding which to flag" tells you everything.

## Quick match

| They say something like… | Archetype | Default shell |
|---|---|---|
| "go through", "clear the queue", "inbox zero", "process them" | [Triage](#1-triage) | List-detail |
| "keep an eye on", "see how we're doing", "is anything broken" | [Monitor](#2-monitor) | Dashboard grid |
| "write", "draft", "build the deck", "edit the thing" | [Author](#3-author) | Canvas + inspector |
| "log it", "submit", "record", "fill in", "clock in" | [Capture](#4-capture) | Single-column form |
| "dig into", "slice it", "figure out why", "explore" | [Explore](#5-explore) | Filter rail + result view |
| "approve", "sign off", "review and decide" | [Decide](#6-decide) | Queue + evidence panel |
| "where is each one", "what stage", "pipeline" | [Track](#7-track) | Board or status table |
| "book", "schedule", "who's free", "plan the week" | [Coordinate](#8-coordinate) | Calendar / timeline |
| "look up", "find that one thing", "pull up" | [Retrieve](#9-retrieve) | Search-first |
| "set up", "permissions", "settings", "configure" | [Configure](#10-configure) | Settings tree |
| "walk me through", "first time", "get started" | [Onboard](#11-onboard) | Wizard / stepper |
| "ask it", "talk to it", "it should answer" | [Converse](#12-converse) | Thread |
| "which one is better", "pick between" | [Compare](#13-compare) | Matrix / side-by-side |
| "comment on", "redline", "give feedback on" | [Collaborate](#14-collaborate) | Document + margin |

---

## 1. Triage

**Shape of the work:** High volume (dozens to hundreds per session), one decision per item from a small fixed set of outcomes, little deliberation each, repeated until the pile is gone.

**What governs it:** Cost per item × N. Anything adding half a second per item — a mouse trip, a confirm dialog, a re-sort, a page load — multiplies into the dominant cost. This is the archetype where interaction budgeting matters most.

**Shell:** List-detail. Queue on one side, the current item in full on the other.

**Primary loop:** land on item → read → one key → next item is already focused. Target: **1 interaction per item, zero mouse trips.**

**Non-negotiables:**
- Every outcome has a single-key shortcut, and the keys are visible in the UI, not buried in a help modal.
- Auto-advance after each decision. Never return the user to a list and make them find their place.
- **Undo, not confirm.** A confirmation dialog doubles the interaction count on the hot path. Show a 5-second undo toast instead.
- Stable sort during a session — items must not jump position when their state changes, or the user loses their place.
- Visible progress ("42 left"). A pile that never appears to shrink kills the will to continue.
- Bulk select for the obvious sweeps: everything from one sender, everything matching the current filter.

**Density:** High. Compact rows, 30–50 visible, small type, minimal padding. This is the one archetype where cramped is correct.

**Failure modes:** each item opens a modal; the decision needs a scroll; confirmation on every action; the list re-sorts after each decision; no keyboard path; loading spinner between items.

---

## 2. Monitor

**Shape of the work:** Glanceable and ambient. Someone checks in, wants "is everything okay" answered in under two seconds, and only digs deeper when it isn't. Often on a wall screen or a second monitor.

**What governs it:** Exception detection, not data display. The dashboard's job is to distinguish normal from abnormal at a glance — not to show every number that exists.

**Shell:** Dashboard grid, with a strict hierarchy: one hero indicator answering the main question, then 3–6 supporting tiles, then drill-down.

**Primary loop:** glance → normal, leave. Or: glance → something's off → drill into that one thing → act or escalate.

**Non-negotiables:**
- A single answer to "is this fine?" readable from across the room. If everything on the screen is equal weight, the answer is nowhere.
- Every metric shows a **comparison** — versus yesterday, versus target, versus normal range. A bare number is uninterpretable and therefore ignorable.
- Every tile is clickable through to the underlying records. A number you can't interrogate gets distrusted and then abandoned.
- Explicit "last updated" and a stale-data state. Stale dashboards cause worse decisions than no dashboard.
- Thresholds and alerting logic must be somewhere visible, or nobody trusts the colors.

**Density:** Medium-low. Large type on the numbers that matter. Whitespace is doing hierarchy work here.

**Failure modes:** 20 equal-weight charts (the "somebody asked for it" dashboard); no baseline so no number means anything; vanity metrics that never change; refresh rate faster than the decision cycle; red/amber/green with no stated thresholds; nothing clickable.

---

## 3. Author

**Shape of the work:** Long sessions on a single artifact — writing, designing, editing, composing. Flow state matters more than anything else. Low item count, very high time per item.

**What governs it:** Uninterrupted attention on the work surface. Every piece of chrome competes with the content.

**Shell:** Canvas + inspector. The artifact dominates; tools collapse away.

**Primary loop:** open → make a change → see it immediately → repeat for an hour → leave without thinking about saving.

**Non-negotiables:**
- The canvas gets 70%+ of the pixels. Inspector panels collapse and remember that they were collapsed.
- **Autosave, always**, with a visible save state. Never a modal asking "save changes?" on exit.
- Undo history that is deep and reliable, ideally with a version timeline for long work.
- Contextual tools — surface what applies to the current selection instead of showing every tool permanently.
- Zero blocking dialogs during the work. Anything modal breaks flow; use inline editing or a side panel.
- Resumption: reopen exactly where they left off, including scroll position and selection.

**Density:** Low chrome, whatever density the content itself wants.

**Failure modes:** permanent multi-row toolbars; modal dialogs for formatting; no autosave; losing state on refresh; panels that reopen every session; a "preview" mode separate from editing when live rendering was possible.

---

## 4. Capture

**Shape of the work:** Short, frequent, often mobile, often interrupted. Logging a workout, filing an expense, recording a reading, submitting a ticket. Seconds per entry, many entries over time.

**What governs it:** Time-to-submitted and the interruption rate. If capture takes more than about 20 seconds, people batch it up and do it badly later from memory — which is worse than not capturing it.

**Shell:** Single-column form. On mobile, consider one question per screen. For very high-frequency capture, consider a hero-input single-purpose tool instead.

**Primary loop:** open → the field they need is already focused → enter the one thing that changes → submit → confirmation → ready for the next one.

**Non-negotiables:**
- **Ruthless field triage.** Every field must justify itself against "would we notice if this were blank?" Most forms have 3 real fields and 12 aspirational ones.
- Default aggressively from last time, from context, from now, from their location. The best field is one already filled correctly.
- Never require information the user doesn't have at capture time — that is what forces fake data. Let them save partial.
- Native input types (date pickers, number pads, camera), and correct keyboard on mobile.
- Survive interruption: a half-finished entry must still be there after a phone call.
- Confirmation that shows *what was saved*, with an edit link — not just "Success!".

**Density:** Low. Big targets. Assume one thumb, in motion, in bad light.

**Failure modes:** a 30-field form for a 10-second job; required fields nobody can answer; validation that only fires on submit and clears the form; no drafts; desktop-shaped forms used mostly on phones.

---

## 5. Explore

**Shape of the work:** Open-ended, iterative narrowing. The user doesn't know what they're looking for until they see it. Analysis, investigation, browsing a catalogue.

**What governs it:** Speed of the narrow-and-widen cycle, and the ability to back out of a dead end without starting over.

**Shell:** Filter rail + result view that can switch representation (table / chart / cards / map) over the same result set.

**Primary loop:** broad view → apply a filter → see the result *immediately* → refine or back off → find something interesting → drill into a record → return to the same filtered set.

**Non-negotiables:**
- Filters apply live, with result counts shown **before** committing — a filter that returns zero should be visibly a dead end in advance.
- Active filters are always visible as removable chips, each individually removable. Hidden active filters are how people reach confidently wrong conclusions.
- The state is shareable and bookmarkable — put filter state in the URL. "Look at this" is the most common action after finding something.
- Back always returns to the prior filter state, never the unfiltered default.
- Every aggregate drills through to the underlying rows. "Where does this number come from" must be answerable in one click.
- Empty result states offer the loosening move: "no results — try removing [filter]".

**Density:** High in the result region; the rail is secondary.

**Failure modes:** apply-button filters; filter state lost on navigation; aggregates that don't drill through; no way to see what's currently filtered; one fixed chart type for questions that vary.

---

## 6. Decide

**Shape of the work:** Low volume, high stakes, needs context. Approvals, sign-offs, hiring decisions, clinical or financial calls. Few per day, consequential, often auditable.

**What governs it:** Confidence. The user must be able to see the evidence without leaving the decision, and must not be able to fire the irreversible action by accident.

**Shell:** Queue + evidence panel. The decision and everything needed to make it are on the same screen.

**Primary loop:** open item → read the summary → expand the evidence that matters → decide → record why → next.

**Non-negotiables:**
- **The evidence sits next to the button.** If the user has to open another tab or system to decide, they will rubber-stamp instead.
- Summarize first, detail on demand — a wall of raw data produces the same rubber-stamping as no data.
- Deliberate friction on the irreversible action, and *only* there: a typed confirmation, a two-step, or a delay with undo. This is the one archetype where a confirmation dialog earns its place.
- Capture the rationale at decision time. Retrofitted reasons are fiction, and this data is usually the point.
- Show the audit trail: who else touched this, what was decided on similar items.
- Support "not now" — defer, request more info, delegate. Forcing a binary produces bad decisions or a stuck queue.

**Density:** Medium. Summary dense, evidence expandable.

**Failure modes:** approve/reject buttons with no context attached; requiring a different system to see the evidence; the same confirmation weight on approve as on delete-forever; no partial or deferred outcome; rationale field that's optional and therefore empty.

---

## 7. Track

**Shape of the work:** Items moving through defined stages. Sales pipeline, support tickets, hiring, orders, manufacturing. The questions are "where is X" and "what's stuck".

**What governs it:** The item count and the stage count.

**Shell — choose on volume:**
- **≤ ~50 items, ≤ 7 stages, and people physically move items** → board (kanban). Drag is the right affordance when the move *is* the action.
- **50+ items, or many attributes matter** → status table with grouping, sorting, and filtering. A board with 400 cards is a wall of cards nobody reads.
- **Stages have hard dates** → timeline / Gantt instead.

**Primary loop:** scan for anomalies → open the one that's stuck → act or update → return to the same view.

**Non-negotiables:**
- **Surface the stuck.** The whole point is finding what isn't moving: show age-in-stage, flag items past a threshold. A board that shows only position and not time is a pretty picture with no information.
- Totals per stage — count and value. A pipeline without sums can't answer the actual business question.
- Whatever the shell, every state change must be possible without drag (keyboard, menu, bulk) — drag alone is inaccessible and terrible on touch.
- Define what happens at the ends: where do items go when done, and does the board stop growing forever?
- Make the card content configurable, or at minimum choose the 3 fields that drive decisions and show only those.

**Density:** Board medium; table high.

**Failure modes:** kanban chosen for aesthetics at 400 items; no age-in-stage; drag as the only move mechanism; no stage totals; a "Done" column that accretes forever.

---

## 8. Coordinate

**Shape of the work:** Time and constraints — booking, scheduling, rostering, planning. The answer depends on seeing conflicts and adjacency.

**What governs it:** Conflict visibility. The reason a calendar beats a form is that the shape of the free time is the information.

**Shell:** Calendar or timeline with a detail panel.

**Primary loop:** see the relevant span → spot a viable slot → place the thing → see conflicts immediately → adjust.

**Non-negotiables:**
- Conflicts appear at the moment of placement, not on submit.
- Time zones stated explicitly wherever two parties are involved. This is the single most common correctness bug in this archetype.
- Both directions of travel: pick a time and see who's free, or pick people and see when they're free.
- Recurrence needs an explicit answer to "this one, or all of them?" — every time.
- Show the surrounding context, not just the slot — a meeting is bad if it's sandwiched, and you can only see that in the grid.

**Density:** Medium; the grid sets it.

**Failure modes:** date entry via dropdowns instead of a grid; conflicts only revealed on save; implicit time zones; recurrence that silently edits the whole series; no view of the other party's constraints.

---

## 9. Retrieve

**Shape of the work:** Known-item lookup. The user knows what they want and wants it now — a customer record, a document, a part number.

**What governs it:** Time to the right result, and confidence that it *is* the right one.

**Shell:** Search-first. Search is the primary interface element, not a box in the corner.

**Primary loop:** land with search focused → type → results narrow as they type → recognize → open.

**Non-negotiables:**
- Search focused on load, and reachable by a single key from anywhere (`/` or `⌘K`).
- Results carry enough metadata to **disambiguate** — three people named J. Smith need distinguishing detail in the result row, or the user opens all three.
- Recent and pinned items before any search is typed. A large share of lookups are repeats.
- Forgiving matching: typos, partials, synonyms, IDs, and the informal names people actually use.
- A zero-results state that suggests a next move rather than a dead end.

**Density:** High.

**Failure modes:** browse hierarchies for known-item lookup; exact-match-only search; result rows with only a title; no recents; search that resets on back.

---

## 10. Configure

**Shape of the work:** Infrequent, consequential, hierarchical. Settings, permissions, integrations, rules. Done rarely, often by someone nervous about breaking something.

**What governs it:** Comprehension and reversibility. The user often doesn't know what a setting does or what will break.

**Shell:** Settings tree — grouped nav with search.

**Primary loop:** find the setting → understand what it affects → change it → verify the effect → leave confident.

**Non-negotiables:**
- **Search across all settings.** Past about 30 settings, nobody finds anything by browsing categories, because your categories aren't their categories.
- Explain the effect in plain language next to each control, including what happens if it's off. Not a tooltip — text.
- **Explicit save** with a dirty-state indicator, and never autosave anything destructive or system-wide.
- Show current effective state where it's inherited or overridden — "you're seeing this because of the org default".
- Preview or dry-run for anything that fans out (permissions, rules, notifications): "this will affect 47 people".
- Reset-to-default at both the individual and the section level, and an audit log of what changed and who changed it.

**Density:** Medium, grouped, generous spacing between groups.

**Failure modes:** 80 flat toggles; autosave on permission changes; jargon labels; no search; no indication of what inherits from where; no way back to default after experimenting.

---

## 11. Onboard

**Shape of the work:** One-shot, unfamiliar, sequential. Setup, first-run, applications, tax-return-style guided flows.

**What governs it:** Completion rate. Every step is a place to abandon.

**Shell:** Wizard / stepper.

**Primary loop:** see where you are in the whole → answer the current step → advance → arrive somewhere useful.

**Non-negotiables:**
- Honest progress — steps visible and numbered, with no surprise extra steps at the end.
- One coherent decision per step. Not one field; not eleven.
- Back preserves what was entered. Losing entered data on back is the classic abandonment cause.
- Save and resume for anything over about 5 minutes, especially if it needs information the user must go find.
- A skip or "do this later" path for everything non-essential, and a default for everything skipped.
- The last step lands them in real, working software with something already accomplished — never an empty app.

**Density:** Low. One thing at a time.

**⚠️ The key test:** a wizard is only right if the task is **done once or rarely**. Wizards for daily tasks are a serious anti-pattern — they optimize for the first use at the permanent expense of every use after. If it's daily, it's Capture, and it wants one dense screen.

---

## 12. Converse

**Shape of the work:** Open-ended dialogue where the user's need can't be predicted. Assistants, support, natural-language query.

**What governs it:** Whether the problem is genuinely open-ended. Chat is the most over-applied shell of the last few years.

**Shell:** Thread, with structured affordances embedded in it.

**Primary loop:** ask → response → refine → act on the result.

**Non-negotiables:**
- Suggested starting prompts. A blank input is the highest-abandonment element in interface design.
- Structured output where the answer is structured — render tables as tables, choices as buttons. Don't make people parse prose that was really a list.
- Stop generation, retry, and edit-and-resend, all always available.
- Visible scope: what it can see and do, stated up front, so users stop guessing.
- Preserve history, and make it searchable if sessions are long.

**⚠️ The key test:** if the set of things the user might want is small and knowable, chat is the **wrong** shell — a form or a set of buttons is faster and more reliable. Chat as a UI for a four-field form is a downgrade dressed as innovation. Use chat when the input space is genuinely unbounded, and add structured affordances wherever it isn't.

---

## 13. Compare

**Shape of the work:** Evaluating a small set of options against shared criteria. Plan selection, vendor evaluation, spec comparison.

**What governs it:** Working memory. If the user has to remember option A while looking at option B, the comparison fails.

**Shell:** Matrix — options as columns, criteria as aligned rows.

**Primary loop:** see all options at once → scan the criteria that matter → narrow to two → decide.

**Non-negotiables:**
- **Everything visible simultaneously**, aligned on a shared row grid. Carousels and separate cards defeat the purpose entirely.
- Highlight *differences*, and offer a "hide identical rows" control — the identical rows are noise.
- Criteria ordered by importance to the user, not by what's easy to tabulate.
- Handle "not applicable" honestly rather than padding rows to make the table look symmetrical.
- 2–4 options. Past about 5, filter first, then compare — people can't hold more than a handful.

**Density:** High and tight; alignment is everything.

**Failure modes:** comparison as separate cards requiring memory; rows in arbitrary order; differences not marked; every option padded to look equal; comparing 12 things at once.

---

## 14. Collaborate

**Shape of the work:** Multiple people acting on a shared artifact, often asynchronously — review, redlining, feedback, co-editing.

**What governs it:** Attribution and resolution. Who said what, about which part, and is it dealt with.

**Shell:** Document + margin threads.

**Primary loop:** open → see what's new since last time → read in context → respond or resolve → know it's handled.

**Non-negotiables:**
- Comments anchor to the specific content they're about, and survive edits to surrounding content.
- "What changed since I last looked" is a first-class feature, not a diff the user has to reconstruct.
- Resolution state is explicit and filterable — open vs resolved, with resolved recoverable.
- Attribution and timestamps on everything.
- Presence or at minimum a warning before conflicting edits.
- Notification granularity that doesn't force a choice between everything and nothing.

**Density:** Content-led; margin secondary.

**Failure modes:** comments detached from content; no unread tracking; resolved comments deleted; silent last-write-wins; all-or-nothing notifications.

---

## Composing archetypes

Real apps mix these. Some common compositions and how to resolve them:

| Composition | Resolution |
|---|---|
| Capture + Monitor (log data, see trends) | Capture is primary — it happens 100× more. Monitor is a second tab, not the home screen. |
| Track + Decide (pipeline with approvals) | Board is home; decisions open a focused panel with the evidence, not a route change. |
| Explore + Author (analyze, then write it up) | Two modes with an explicit switch. Don't cram an editor into a filter rail. |
| Triage + Decide (queue with high-stakes items) | Triage loop for the routine, with an escalation path that switches to full-evidence mode for the hard ones. |
| Retrieve + Author (find a doc, edit it) | Search-first entry, then the canvas takes the whole screen. Nav should disappear on entering the canvas. |
| Monitor + Explore (dashboard that drills down) | The natural pair. Every tile drills into a pre-filtered explore view. |

The recurring mistake is giving each archetype its own equal-weight top-level tab. Rank by frequency, give the primary loop the home screen and the best keyboard access, and let the others be reachable but subordinate.
