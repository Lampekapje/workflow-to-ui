# Review rubric

Seven dimensions. Work through all of them — the point of a rubric is catching what you didn't notice, and missing states are never the thing that catches your eye.

---

## 1. Shape fit

*Does the layout match the archetype of the work?*

- Which archetype is the work? Which shell is in use? Do they correspond?
- Is the most frequent task on the home screen, or is the home screen a dashboard nobody asked for?
- If several archetypes are mixed, is one clearly primary — or do they have equal billing in the nav?
- Does the density match the volume? Compact rows for 300 items/day, generous spacing for occasional use.

**Failure signatures:** dashboard home for a triage job · kanban at 400 items · wizard for a daily task · chat for a bounded four-field problem · a form where a table with inline editing belongs · the most-used screen sitting third in the sidebar.

---

## 2. Loop cost

*How much does the repeated action cost, multiplied by how often it happens?*

- Count interactions per item. Compare with the budget for the volume.
- Is there a mouse trip in a high-volume loop? A page transition? A confirm dialog?
- Does the user lose their place after acting — scroll position, selection, filters?
- Is there a keyboard path through the whole loop, and is it discoverable from the interface?
- Are there bulk operations where the work is obviously done in bulk?

**Failure signatures:** click row → click Edit → change dropdown → Save → Back (5 interactions for a one-key job) · confirmation on a routine reversible action · list re-sorts after every change · shortcuts that exist but are documented nowhere · no multi-select on a list people obviously sweep through.

---

## 3. State coverage

*What happens when things aren't ideal?*

- Empty — and is "empty because you're done" distinguished from "empty because it's broken" and "empty because a filter killed it"?
- Loading — skeleton matching the layout, or a layout-shifting spinner? Does subsequent loading blank content the user was reading?
- Error — plain language, cause, next step, and is entered data preserved?
- No permission — explained with a route to access, or a bare 403? Are denied actions shown and then refused?
- Too much data — is there a defined behavior at 10× the expected volume, or does the layout simply degrade?
- Stale/offline — is data freshness visible?

**Failure signatures:** only the happy path designed · "Something went wrong" · form clears on validation error · finished queue rendered as a sad empty illustration · a table that becomes unusable past a few hundred rows with no pagination or virtualization.

---

## 4. Findability

*Can people locate what they need?*

- Nav model matched to destination count (no nav / tabs ≤5 / sidebar ≤12 / nested+search beyond)?
- Destinations named for user goals or for database tables?
- Is search present where the volume demands it, and is it forgiving of typos, partials, and informal names?
- Is current location always visible? Breadcrumbs where nesting is deep?
- Do result rows carry enough to disambiguate similar items?

**Failure signatures:** nav labelled "Entities" and "Records" · 18 sidebar items · search that only exact-matches · no recents in a lookup tool · three identically-titled results you must open to tell apart.

---

## 5. Safety

*Can people break things, and can they recover?*

- Does friction on destructive actions scale with consequence, or is it uniform?
- Is undo available where it could be? (Nearly always better than confirm for reversible actions.)
- Do bulk actions state their blast radius before firing?
- Can the user tell, before acting, what will be affected — especially with permissions and notifications?
- Is there an audit trail where decisions matter?

**Failure signatures:** same confirmation weight on "archive" and "delete forever" (trains dismissal, so the dangerous one gets dismissed too) · no undo anywhere · "Delete 47 items?" without saying which · autosaved permission changes · destructive action adjacent to a routine one.

---

## 6. Resilience to real data

*Does it survive contact with production?*

- What happens to layout with a 60-character name? A five-line note? A null?
- Are nulls rendered deliberately ("—", "Not set") or as blank cells that read as bugs?
- Are extreme numbers formatted and does the column accommodate them?
- Does the design still work at 10× the current record count?
- Are long lists virtualized or paginated?

**Failure signatures:** truncation with no tooltip or expansion · layouts that only look right with uniform tidy data · blank cells indistinguishable from load failures · unformatted large numbers · everything rendered at once.

---

## 7. Fit to context

*Does it work where it's actually used?*

- If it's used on mobile, is it designed for mobile — or is it a desktop layout squeezed down?
- For each collapsing screen, is there a deliberate priority order, or does it just reflow arbitrarily?
- Are tap targets adequate, and are the right native input types used?
- Does it survive interruption — a phone call mid-entry, a dropped connection?
- If it's used by trained staff daily, does it reward expertise (shortcuts, density, defaults) or treat everyone as a first-timer forever?

**Failure signatures:** month-grid calendar on a phone · 14-column table with horizontal scroll as the mobile story · no drafts on a form used in the field · permanent onboarding hints for daily users · tiny targets on a touch-primary tool.

---

## Scoring

If a number helps, rate each dimension 1–5 and weight by exposure — a loop-cost failure on a 300-items-a-day tool is worth many times a findability nit on a screen visited monthly.

The more honest summary is usually just: **what does this cost the user per day, and what's the one change that recovers most of it?** Lead with that.
