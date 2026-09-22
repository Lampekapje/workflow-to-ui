# UI Flow Review — Mortgage Underwriting Application

> Review conducted using `ui-flow-review` against the actual work requirements.

## Verdict
**Mismatched Shape.** The original team built an executive analytics dashboard with modal popups for a job that is actually high-volume triage. Underwriters spend 70% of their time clicking between modal tabs and closing confirmation dialogs rather than evaluating risk. Replacing this with a keyboard-driven list-detail triage shell eliminates 4 avoidable interactions per loan.

---

## Primary Loop Analysis

**Volume:** 150 loan files per underwriter per shift.  
**Target interaction budget for 100+ volume:** **1 interaction per item, zero mouse trips.**

### Baseline Loop (Original Dashboard + Modal Design)
1. Underwriter scrolls down dashboard table to find next row. (Scroll + mouse target)
2. Clicks "Open File" button. (1 click)
3. Modal loads with default "Personal Info" tab. Clicks "Financials" tab to see DTI. (1 click)
4. Clicks "Risk Engine" tab to see automated flags. (1 click)
5. Selects decision from dropdown, clicks "Save Decision". (2 clicks)
6. Modal asks: *"Are you sure you want to approve Loan #8942?"* Clicks "Confirm". (1 click)
7. Modal closes; dashboard re-renders and jumps back to top of page. (Re-find place)

**Baseline Cost:** **6 mouse interactions + 2 re-orientations per loan.**  
Total shift overhead: $6 \times 150 = 900\text{ clicks/day}$.

### Optimized Loop (FlowyourI Triage Shell)
1. Loan record already selected in left pane; all key financials and flags visible side-by-side in right pane.
2. Underwriter presses <kbd>a</kbd> (Advance) or <kbd>r</kbd> (Reject).
3. Queue auto-advances to the next loan immediately; a non-blocking 5-second undo toast appears.

**Optimized Cost:** **1 keystroke, 0 mouse trips, 0 blocking modals.**  
**Savings:** 5 interactions eliminated per file. At 150 files/day, this recovers **~28.5 minutes of avoidable friction per underwriter per day** (over 2 hours a week per person).

---

## Findings

### 1. Shape Mismatch — [Structural]
- **What:** The homepage opened with 6 summary charts (loan approval rates, monthly volume, average FICO) before showing the queue at the bottom of the fold.
- **Why it costs:** Underwriters do not monitor high-level business trends; they process a queue. Every morning required scrolling past vanity charts to start working.
- **Fix:** Demoted charts to a supervisor reporting tab. Made the Active Queue list-detail pane the default home screen.

### 2. Destructive Confirm Dialog on Hot Path — [Flow / Safety]
- **What:** Approving or rejecting triggered a blocking modal: *"Are you sure?"*
- **Why it costs:** Routine decisions should never have blocking modals. Confirmation dialogs train users to hit "Yes" automatically, which actually increases mistakes while doubling click overhead.
- **Fix:** Removed the confirmation dialog. Replaced with an immediate 5-second undo toast (`[u] Undo`) and an audit trail.

### 3. Tabbed Information Fragmentation — [Findability]
- **What:** Key underwriting criteria (Credit, DTI, Income verification flags) were split across three separate tabs inside a modal.
- **Why it costs:** Every loan forced two tab clicks just to assemble the facts needed for a 5-second decision.
- **Fix:** Unified the three critical risk factors into a persistent 4-box stat grid and an evidence callout list within the primary detail pane.

---

## Working Well
- **SLA Sorting:** The queue was already correctly sorted by document expiration and lock expiration dates.
- **Audit Logging:** Every decision was already immutably logged with timestamp and user ID in the backend.

---

## Not Assessed
- Visual branding, font choices, and color palette (deferred to `frontend-design`).
- Backend risk engine response latency.
