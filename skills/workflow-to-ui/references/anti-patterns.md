# Anti-patterns and pre-handoff checklist

Run this before delivering a spec. Each item catches a failure that is cheap to fix on paper and expensive to fix in code.

## Checklist

**Work model**
- [ ] The archetype is named, and it matches the verb they actually used
- [ ] Volume, frequency, stakes, expertise, context and session length are all stated (assumed values marked as assumptions)
- [ ] If multiple archetypes, one is explicitly primary and the others are subordinate in the navigation

**Loop**
- [ ] The primary loop is written as numbered steps
- [ ] Interactions per item are counted and within budget for the stated volume
- [ ] There is a keyboard path through the whole primary loop
- [ ] No page transition inside the loop
- [ ] No confirmation dialog on the hot path (undo instead)

**Screens**
- [ ] Every screen names its shell and why
- [ ] Every screen has exactly one primary action, visually dominant
- [ ] Density is stated per screen and matches the volume
- [ ] The home screen is designed for the returning-with-work user, not the empty demo

**States**
- [ ] Empty, loading, error, no-permission, and too-much-data specified for each screen
- [ ] "Empty because everything's done" reads as success, not failure
- [ ] Errors preserve entered data
- [ ] Back preserves filter state, scroll position, and selection

**Navigation**
- [ ] Destination count matches the chosen nav model
- [ ] Destinations named for user goals, not data entities
- [ ] Nav recedes on focus surfaces

**Safety**
- [ ] Destructive actions have friction proportional to consequence
- [ ] Bulk actions state their blast radius before firing
- [ ] Undo exists wherever it reasonably can

**Responsive**
- [ ] Each screen states reflow / reveal / replace / refuse
- [ ] Mobile priority order is explicit where columns collapse

---

## The recurring structural tells

These are the patterns that show up when an interface is assembled from familiar shapes rather than derived from the work. They are structural — they survive any amount of good visual design on top.

**Everything-is-a-dashboard.** The home screen is a grid of metric tiles regardless of what people do in the app. Tell: nobody can name a decision that changes based on any tile. Fix: make the home screen the primary loop; metrics go on a secondary screen if anyone genuinely wants them.

**Card soup.** Every piece of content chopped into equal rounded cards with equal shadow, so nothing is more important than anything else. Tell: you can't identify the primary action within two seconds. Fix: hierarchy — different weights for different importance, and lists for list-shaped things.

**Feature-parity navigation.** Every capability gets a top-level nav item, ranked by how it was discussed rather than how often it's used. Tell: the most-used screen is third in the sidebar. Fix: rank by frequency.

**Happy-path-only.** Empty, error, and overflow states are unspecified, so they get invented under deadline. Tell: the spec has no word for what 5,000 rows looks like. Fix: the state matrix.

**Wizard for a daily task.** A stepper for something done repeatedly, optimizing the first use at the cost of every subsequent one. Fix: one dense screen with defaults.

**Chat-as-interface for a bounded problem.** A conversational UI wrapping what is really four fields and a button. Tell: you could enumerate every useful input. Fix: a form. Add chat only for genuinely unbounded input.

**Modal stacking.** Modals opening modals, each blocking context the user needs. Tell: two overlays at once. Fix: side panels and dedicated screens.

**Confirmation theatre.** A dialog on every action, including harmless ones, which trains people to dismiss without reading — so the dangerous one gets dismissed too. Fix: undo for the reversible, real friction only for the irreversible.

**The infinite Done column.** A track view where completed items accumulate forever, so the board gets slower and less readable every week. Fix: define archival at the terminal stage.

**Data-model navigation.** Screens named after tables. "Entities", "Records", "Items". Tell: you'd have to explain a nav label to a new user. Fix: name things after what the user is trying to do.

**Density mismatch.** Generous spacing and big cards in a tool where someone processes 300 items a day, so they scroll past whitespace for a living. Or the reverse: a 6pt table for something used twice a month on a phone. Fix: derive density from volume.

**Uninterpretable numbers.** Metrics with no baseline, target, or comparison. "1,247" — is that good? Fix: every number gets a comparison or it doesn't earn its place.

**The lost place.** Acting on an item returns the user to the top of a re-sorted list. Tell: the user's position is not treated as state. Fix: preserve selection, scroll, filters; auto-advance in queues.

**Invisible filter state.** A filter is active somewhere off-screen, so the user draws a confident conclusion from a subset of the data. Fix: active filters always visible as removable chips.

**Mystery configuration.** Settings labelled in implementation terms with no statement of effect. Fix: plain language, say what happens when it's off, and show the blast radius.
