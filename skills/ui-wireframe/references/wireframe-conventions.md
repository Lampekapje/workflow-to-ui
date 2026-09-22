# Wireframe conventions

Shorthand that communicates intent without implying a finished design. The point of each convention is that it reads clearly as *a placeholder for X* rather than as *a bad version of X*.

## Placeholders

| Element | Convention |
|---|---|
| **Image / photo** | Grey box with a diagonal cross and the intended aspect ratio labelled. Never a stock photo — it imports a mood you haven't chosen. |
| **Avatar** | Grey circle with initials. |
| **Chart** | Flat grey bars or a single grey polyline with real axis labels. Never a styled chart library — it looks finished and invites color discussion. |
| **Icon** | A small grey square, or the icon's *name* in brackets: `[filter]`. Naming is better early, because it forces you to notice when an icon would be ambiguous without a label. |
| **Logo** | Box labelled "logo". |
| **Video / map** | Grey box, labelled, with the aspect ratio. |
| **Long text** | Real sentences at realistic length. Grey bars for body copy only where the text genuinely doesn't matter yet. |

## Interaction affordances

- **Primary action** — the single darkest element on the screen. Exactly one per screen. If you have two, the design has a hierarchy problem you can see immediately here.
- **Secondary action** — outlined, mid-grey.
- **Tertiary / destructive** — text only, no fill.
- **Disabled** — light grey with reduced opacity, plus a note saying *why* it's disabled. A disabled control with no stated reason is a support ticket.
- **Focus** — a visible 2px outline. Show it in the wireframe; it's the thing most likely to be dropped in the build.
- **Selected** — a left border bar plus a subtle background shift, not color.
- **Drag handle** — `⠿` and the keyboard equivalent noted beside it.

## Data realism

Include in every list or table:

- One **very long** value that threatens to break the layout (a 60-character company name, a five-line note)
- One **empty or null** value, rendered as you intend to render it — "—" or "Not set", never a blank cell that looks like a bug
- One **extreme number** (0, a negative, 1,847,293) to check formatting and column width
- **Realistic dates** including relative formats ("2 min ago", "last Tuesday") if that's the intent
- Enough rows to make density honest — 30+ for anything that will be long in practice

This is the highest-value part of a wireframe. Layouts that look good with tidy uniform data and fall apart on real data are the most common expensive mistake, and five minutes of realistic placeholder content catches it.

## State indication

Put a small switcher bar at the top of the page, visually separated from the design (a dashed border and a monospace label works) so nobody mistakes it for part of the product:

```
┌ review controls ─────────────────────────────────┐
│ screen: [triage ▾]  state: [loaded ▾]  □ mobile  │
└──────────────────────────────────────────────────┘
```

States worth wiring: `loaded` · `empty` · `first-run` · `loading` · `error` · `no-permission` · `overloaded`.

- **Loading** — skeleton blocks matching the real layout's geometry, so you can verify nothing shifts when content lands.
- **Error** — the real message text you intend to ship. Writing it now catches vagueness early; "Something went wrong" looks obviously inadequate sitting in a wireframe.
- **Overloaded** — the too-much-data case. Whatever your fallback is (pagination, virtualization, forced filter), show it.

## Annotations

Numbered markers in the margin, with a key beneath the screen. Use them for anything the static picture can't say:

```
  ① sorted by age in stage, descending; sticky header
  ② autosaves 3s after last keystroke; no save button
  ③ 400+ rows in production — virtualized, 50 rendered
  ④ j/k move selection, a/r/h decide, auto-advances
  ⑤ disabled until an owner is assigned
```

Behavior, volume, and timing are the three things a wireframe cannot show and reviewers most need to know.

## Greyscale palette

Nine steps is plenty. Anything you can't express with these, express with an annotation.

```
--w-0:  #ffffff   page
--w-1:  #f7f7f7   subtle fill, alternate rows
--w-2:  #ededed   placeholder blocks
--w-3:  #dcdcdc   borders, dividers
--w-4:  #b4b4b4   disabled text, muted icons
--w-5:  #8c8c8c   secondary text
--w-6:  #5c5c5c   body text
--w-7:  #2e2e2e   headings, primary action fill
--w-8:  #121212   maximum emphasis, use sparingly
```

One deliberate exception is allowed: a single muted signal color (a desaturated red-grey around `#9b6b6b`) for error and destructive states only, because greyscale genuinely cannot convey danger. Use it nowhere else — the moment it appears twice it stops meaning anything.
