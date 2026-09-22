# Layout shells

Twelve structural containers. The archetype picks the shell; this file tells you what goes in it, how it behaves when the screen shrinks, and how it breaks.

Read the ASCII diagrams as proportion, not pixels.

**Contents:** [List-detail](#list-detail) · [Dashboard grid](#dashboard-grid) · [Canvas + inspector](#canvas--inspector) · [Single-column form](#single-column-form) · [Filter rail + results](#filter-rail--results) · [Board](#board) · [Table-first](#table-first) · [Calendar/timeline](#calendartimeline) · [Search-first](#search-first) · [Settings tree](#settings-tree) · [Wizard](#wizard) · [Hero tool](#hero-tool) · [Thread](#thread) · [Document + margin](#document--margin)

---

## List-detail

```
┌──────────┬──────────────────────────────┐
│ ▸ item   │  Item title                  │
│ ▸ item   │  meta · meta · meta          │
│ ▸ ITEM ◀ │                              │
│ ▸ item   │  Full content of the         │
│ ▸ item   │  selected item.              │
│ ▸ item   │                              │
│ ▸ item   │  ┌──────┐ ┌──────┐ ┌──────┐  │
│ ▸ item   │  │ A(1) │ │ B(2) │ │ C(3) │  │
│  42 left │  └──────┘ └──────┘ └──────┘  │
└──────────┴──────────────────────────────┘
   ~30%                ~70%
```

**For:** Triage, Decide, Retrieve results, Collaborate.
**Ratio:** 25–35% list. Wider than that and the detail pane gets cramped; narrower and list rows can't carry enough to recognize an item.
**Selection is state:** keep the selected row visibly marked, keep list scroll position independent of detail scroll, and keep selection through a refresh.
**Keyboard:** `j`/`k` or arrows move selection; the detail pane follows without a click. This is the shell's whole advantage — without it you have two panes and no speed.
**Mobile:** collapses to list → push detail as a full screen → back returns to the *same scroll position*. Losing scroll position on back is the defining mobile failure of this shell.
**Fails when:** list rows are too sparse to identify an item without clicking; the detail pane reloads the whole page; actions live only in the list row so the user must aim at a 20px target.

---

## Dashboard grid

```
┌─────────────────────────────────────────┐
│  ┌───────────────────────────────────┐  │
│  │   THE ONE NUMBER      ↑ 12% vs LW │  │  ← hero answers "is it fine?"
│  └───────────────────────────────────┘  │
│  ┌─────────┐ ┌─────────┐ ┌───────────┐  │
│  │  tile   │ │  tile   │ │   tile    │  │  ← 3-6 supporting, clickable
│  └─────────┘ └─────────┘ └───────────┘  │
│  ┌───────────────────────────────────┐  │
│  │  needs attention (3)              │  │  ← the exceptions list
│  └───────────────────────────────────┘  │
│  updated 30s ago                        │
└─────────────────────────────────────────┘
```

**For:** Monitor.
**Hierarchy is mandatory:** one hero, then supporting, then an exceptions list. A uniform grid of identical tiles carries no information about what matters.
**Every tile links** to the records behind it.
**Mobile:** single column in priority order — and the priority order is the real design decision. If you can't order them, you have too many.
**Fails when:** every tile is the same size (nothing is important); no comparison values; no timestamp; built by asking stakeholders what they want to see instead of what decision it drives.

---

## Canvas + inspector

```
┌───┬────────────────────────────┬────────┐
│ ▤ │                            │ ▾ Type │
│ ▤ │      T H E   W O R K       │ ▾ Size │
│ ▤ │                            │ ▾ Fill │
│ ▤ │                            │        │
│ ▤ │                            │  [ ▸ ] │  ← collapsible
└───┴────────────────────────────┴────────┘
 48px           70%+                 ~20%
```

**For:** Author.
**Canvas dominates.** Tools are contextual to the selection; panels collapse and remember it.
**Save state visible, always saving.** No exit dialogs.
**Mobile:** usually a viewer, not an editor. Be honest about this rather than shipping an unusable phone editor — a good read-and-comment mobile view beats a bad mobile editor.
**Fails when:** persistent toolbars eat vertical space; modal formatting dialogs; state lost on refresh; a separate preview mode where live rendering was possible.

---

## Single-column form

```
┌─────────────────────────┐
│  Log a workout          │
│                         │
│  Exercise               │
│  [ Squat            ▾]  │  ← defaulted from last time
│                         │
│  Weight        Reps     │
│  [ 100 ] kg    [ 5  ]   │  ← related fields may share a row
│                         │
│  [    Save entry     ]  │  ← full-width primary
│  Saved: Squat 100×5  ✎  │
└─────────────────────────┘
```

**For:** Capture, and the steps inside a Wizard.
**One column.** Two-column forms measurably slow completion and cause skipped fields; only pair fields that are genuinely one unit (first/last, amount/currency).
**Labels above inputs**, always visible. Placeholder-as-label disappears exactly when it's needed.
**Validate on blur**, not on submit, and never clear the form on error.
**Mobile:** this shell is already mobile-shaped; just check input types and tap targets.
**Fails when:** it's long enough to need a scrollbar for a 10-second task; required fields the user can't answer; no partial save.

---

## Filter rail + results

```
┌───────────┬─────────────────────────────┐
│ Date      │ [status: open ×] [q3 ×]     │  ← active filters, removable
│ ○ 7d      │ 247 results  [▦ table ▾]    │
│ ● 30d     │ ┌─────────────────────────┐ │
│ Status    │ │                         │ │
│ ☑ Open 42 │ │   result view           │ │  ← switchable representation
│ ☐ Done 205│ │                         │ │
│ ☐ Void  0 │ └─────────────────────────┘ │
└───────────┴─────────────────────────────┘
   ~220px
```

**For:** Explore.
**Counts next to every facet**, including zeros, so dead ends are visible before clicking.
**Live application**, no apply button. **Filter state in the URL.**
**Mobile:** filters become a bottom sheet with a badge showing the active count; keep the active-filter chips on the main screen so state is never hidden.
**Fails when:** filter state is invisible or lost on back; facets without counts; a single fixed result representation.

---

## Board

```
┌──────────┬──────────┬──────────┬────────┐
│ New   12 │ Active 8 │ Review 3 │ Done   │
│ £42k     │ £210k    │ £88k     │        │  ← stage totals
├──────────┼──────────┼──────────┼────────┤
│ ┌──────┐ │ ┌──────┐ │ ┌──────┐ │        │
│ │ card │ │ │ card │ │ │ card │ │        │
│ │ 3d   │ │ │ 14d ⚠│ │ │ 1d   │ │        │  ← age in stage
│ └──────┘ │ └──────┘ │ └──────┘ │        │
└──────────┴──────────┴──────────┴────────┘
```

**For:** Track, under ~50 items and ~7 stages.
**Cards carry 3 fields max** plus age-in-stage. More than that and it's a table in disguise.
**Drag is never the only path** — keyboard and menu moves are required for accessibility and touch.
**Mobile:** horizontal snap-scroll between columns, or a grouped list. Do not shrink four columns onto a phone.
**Fails when:** item count outgrows it and nobody switches to a table; no age or totals; an infinite Done column.

---

## Table-first

```
┌─────────────────────────────────────────┐
│ [search        ] [filter ▾]  [ ⬚ 3 sel ]│
├──┬────────┬────────┬────────┬───────────┤
│☐ │ Name  ↑│ Status │ Owner  │ Updated   │
├──┼────────┼────────┼────────┼───────────┤
│☐ │ …      │ ●Open  │ …      │ 2h ago    │
│☑ │ …      │ ●Done  │ …      │ 1d ago    │
└──┴────────┴────────┴────────┴───────────┘
```

**For:** Track at volume, admin lists, anything where comparing rows matters.
**Sticky header**, sortable columns, sort state visible, and sort persisted.
**Bulk selection with a contextual action bar** that appears on selection.
**Row click opens detail; never make the whole row a single ambiguous target with buttons inside it** — nest actions in an explicit menu.
**Mobile:** cards, or horizontal scroll with a frozen first column. Pick deliberately; a squeezed table is unusable.
**Fails when:** 14 columns because the data has 14 fields; pagination where infinite scroll suits, or vice versa; no bulk actions on a list clearly used in bulk.

---

## Calendar/timeline

```
┌────────────────────────────────────────┐
│ ‹ March 2026 ›      [day|week|month]   │
├─────┬─────┬─────┬─────┬─────┬─────┬────┤
│ Mon │ Tue │ Wed │ Thu │ Fri │ Sat │ Sun│
│ ▓▓▓ │     │ ▓▓▓ │ ░░░ │     │     │    │
│     │ ▓▓▓ │ ▓▓▓ │     │ ▓▓  │     │    │  ← overlap must be visible
└─────┴─────┴─────┴─────┴─────┴─────┴────┘
```

**For:** Coordinate.
**Overlaps and conflicts render visibly** — that's the shell's entire justification over a form.
**Time zone stated** wherever two parties exist.
**Mobile:** day or agenda view by default. A month grid on a phone is decoration.
**Fails when:** conflicts only surface on save; recurrence edits the series silently; no agenda alternative.

---

## Search-first

```
┌─────────────────────────────────────────┐
│                                         │
│      [ 🔎 Search…                    ]  │  ← focused on load
│                                         │
│  Recent                                 │
│  ▸ Acme Corp · #4821 · last week        │  ← disambiguating metadata
│  ▸ J. Smith · Billing · London          │
└─────────────────────────────────────────┘
```

**For:** Retrieve.
**Focused on load**, `/` or `⌘K` from anywhere, recents before any query.
**Result rows disambiguate** — enough detail to pick the right J. Smith without opening three.
**Mobile:** same, with the keyboard raised on load only if search is genuinely the sole purpose of the screen.
**Fails when:** exact-match only; title-only results; back clears the query.

---

## Settings tree

```
┌─────────────┬───────────────────────────┐
│ [search   ] │  Notifications            │
│ General     │                           │
│ ▾ Account   │  ☑ Email on mention       │
│   Profile   │     Sends to you@co.com   │  ← plain-language effect
│   Security  │                           │
│ ▾ Team    ◀ │  Inherited from org ⓘ     │
│   Members   │                           │
│   Roles     │  [ Save ]  [ Reset ]      │  ← explicit save
└─────────────┴───────────────────────────┘
```

**For:** Configure.
**Search across all settings** is the primary finding mechanism past ~30 settings.
**Explicit save with a dirty indicator.** Show inheritance and overrides.
**Mobile:** drill-down list, back to the category.
**Fails when:** flat lists of toggles; jargon labels; autosaved permissions; no reset.

---

## Wizard

```
┌─────────────────────────────────────────┐
│  ●───●───○───○     Step 2 of 4          │  ← honest progress
│                                         │
│  Where should we send invoices?         │
│  [ field                             ]  │
│                                         │
│  [ ‹ Back ]        [ Continue ]  Skip   │
└─────────────────────────────────────────┘
```

**For:** Onboard only. One decision per step, back preserves input, save-and-resume if long.
**Fails when:** used for a repeated task; hidden extra steps; back destroys entered data.

---

## Hero tool

```
┌─────────────────────────────────────────┐
│                                         │
│   ┌─────────────────────────────────┐   │
│   │  paste or drop something here   │   │
│   └─────────────────────────────────┘   │
│            [   Convert   ]              │
│                                         │
│   ───────── result appears here ──────  │
└─────────────────────────────────────────┘
```

**For:** single-purpose utilities and very high-frequency Capture. One input, one action, one output, no navigation at all.
**Resist adding a nav bar.** If a second function appears, question whether it belongs in the same tool.
**Fails when:** it grows a sidebar and becomes an app nobody asked for.

---

## Thread

```
┌─────────────────────────────────────────┐
│  ▸ you: …                               │
│  ▸ it: …                                │
│    [ ⟳ retry ]  [ ⧉ copy ]              │
│  ┌─────────────────────────────────┐    │
│  │ Ask something…            [ ↑ ] │    │
│  └─────────────────────────────────┘    │
│  try: "summarize this"  "find X"        │  ← starters, never a blank box
└─────────────────────────────────────────┘
```

**For:** Converse. Starters present, stop/retry/edit always available, structured output rendered structurally.
**Fails when:** it's the shell for something that was really a form.

---

## Document + margin

```
┌────────────────────────────┬────────────┐
│  Heading                   │ ┌────────┐ │
│  Body text with a ░░░░░░   │ │ AB: ▸  │ │  ← anchored to highlight
│  highlighted span here.    │ │ 2 open │ │
│  More body text.           │ └────────┘ │
└────────────────────────────┴────────────┘
```

**For:** Collaborate. Anchored comments, unread tracking, explicit resolution.
**Mobile:** comment count badges inline, tap to open a sheet.
**Fails when:** comments detach from content on edit; no "what's new"; resolution deletes rather than archives.

---

## Choosing density

Density is a deliberate choice driven by volume and session length, not a style preference.

| Signal | Density |
|---|---|
| 100+ items per session, expert users, daily use | **High** — compact rows, small type, minimal padding |
| Mixed use, moderate volume | **Medium** |
| Mobile, occasional use, high stakes, or one item at a time | **Low** — generous spacing, large targets |

High density is not a compromise and doesn't mean careless: expert tools *should* be dense, because scrolling past whitespace all day is a real cost. Low density is not "clean" if it forces people to page through six screens of what could have been one table.
