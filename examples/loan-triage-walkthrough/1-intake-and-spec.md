# UI Spec — Mortgage Underwriting Triage

> Structural spec produced via `workflow-to-ui`. No color, typography, or framework decisions — those come after structure is agreed.

## 1. Work model

| Fact | Value |
|---|---|
| **Users do** | Triage: Review incoming mortgage loan files, verify debt-to-income and credit threshold flags, decide Advance / Reject / Hold |
| **Archetype** | Primary: **Triage** · Secondary: **Retrieve** (subordinate search for prior borrower files) |
| **Volume** | 120–160 loan files per underwriter per 6-hour shift |
| **Frequency** | Continuous daily queue processing |
| **Stakes** | Costly if wrong, but reversible with supervisor audit trail + 5-second undo toast |
| **Expertise** | Expert daily operators — want speed, dense data, strict keyboard controls |
| **Context** | Dual desktop monitors in underwriting operations center, occasional interruptions |
| **Session** | 45–90 minute continuous focus sprints |

*Assumed, not confirmed:* Assumed underwriters do not need to calculate interest rates inline; calculations are pre-computed by the risk engine.

---

## 2. Primary loop

The repeated cycle per loan application:
1. Underwriter inspects current loan record (flags, DTI, credit score, income verification).
2. Presses single key: `a` (Advance to closing), `r` (Reject with reason), or `h` (Place on documentation hold).
3. Queue automatically advances to next loan file instantly.
4. If a mistake is made, `u` or `Cmd+Z` triggers a 5-second non-blocking undo toast.

**Interactions per item:** **1 keystroke**, 0 mouse trips, 0 blocking confirmation modals.
- Budget for 120+ items/shift: **1 interaction per item**.
- Target met.

**Keyboard contract:**
- `j` / `k` or `↓` / `↑`: Next / Previous loan in queue
- `a`: Advance to Underwriting Stage 2
- `r`: Reject (opens inline quick-reason popover, `Enter` submits)
- `h`: Place on Hold (requests borrower document)
- `u`: Undo last action
- `/`: Focus search filter

---

## 3. Screen inventory

| Screen | Archetype | Shell | Density | Purpose |
|---|---|---|---|---|
| **Underwriting Queue** | Triage | List-Detail Split Pane | High | Process incoming loan pipeline at high velocity |
| **Audit & Held Queue** | Track | Status Table | Medium | Review loans flagged for secondary documentation |

**Navigation:** 2 top tabs: `Active Queue (142)` and `Held / Review (18)`.
**Home screen:** `Active Queue` (serves the returning underwriter immediately).

---

## 4. Screen: Active Underwriting Queue

**Purpose:** Rapid inspection and decisioning of pre-screened loan applications.  
**Shell:** List-Detail Split (`32%` queue column, `68%` evidence & decision pane).  
**Primary action:** Advance to Stage 2 (`a`).

```
┌─ Active Queue (142 remaining) ───────────────┬─ Loan #4892 — Marcus Vance ───────────────────────┐
│ [Search loans (/)] [Filter: Flagged ▾]        │ Risk Engine: PASS (Credit: 742 | DTI: 34.2%)      │
│                                              ├──────────────────────────────────────────────────┤
│ ▶ #4892 Marcus Vance       $420k  [HIGH RISK]│ Income Verification: W2 Verified ($145k/yr)       │
│   #4893 Elena Rostova      $310k  [CLEAN]    │ Assets: $88,200 (Bank sync verified 2h ago)      │
│   #4894 David Chen         $650k  [CLEAN]    │ Flagged Issue: Unexplained $12k deposit in June   │
│   #4895 Sarah Jenkins      $290k  [LOW DTI]  │ Notes: Self-employed co-signer attached.          │
│   #4896 Robert Thorne      $510k  [REVIEW]   ├──────────────────────────────────────────────────┤
│   #4897 Amanda Lee         $380k  [CLEAN]    │ [a] Advance    [r] Reject    [h] Request Docs     │
└──────────────────────────────────────────────┴──────────────────────────────────────────────────┘
```

**Regions:**
1. **Queue Rail (Left, 32%):** Compact list of pending files, sorted by SLA age. Active selection highlighted with solid indicator bar. Shows Loan ID, Borrower Name, Loan Amount, and Risk Badge.
2. **Evidence Pane (Right, 68%):** Pinned header with key metrics (Credit, DTI, Loan Amount). Summary of automated checks (Income, Assets, Identity). Risk flag callout box.
3. **Action Bar (Sticky Bottom of Detail Pane):** Decision shortcuts visible directly on buttons (`[a] Advance`, `[r] Reject`, `[h] Hold`).
4. **Undo Toast:** Non-blocking 5-second countdown bar in bottom-left.

---

## 5. State Coverage Matrix

| State | Behavior & Copy |
|---|---|
| **Loaded** | Queue populated (30+ visible rows), active loan loaded in detail pane with keyboard focus. |
| **Empty (All Done)** | *"Queue cleared. 142 loans processed today. Next batch syncs at 14:00."* with link to Held Queue. |
| **Empty (Filter Zero)** | *"No loans match filter 'High Risk'. [Clear filter (Esc)]"* |
| **Loading** | Skeleton rows in queue matching exact row height; skeleton blocks in evidence panel. No layout shift. |
| **Error** | Sticky warning bar: *"Unable to sync queue with risk engine. Last updated 4m ago. [Retry (r)]"* Entered notes preserved. |
| **No Permission** | Detail pane reads: *"Loan #4892 requires Senior Underwriter clearance (Amount > $1M). [Reassign file]"* |
| **Too-Much-Data** | Over 500 loans: Infinite virtual scroll with sticky column headers and SLA priority partition. |
| **Stale / Offline** | Warning indicator in review bar: *"Offline. Decisions queued locally (3 pending sync)."* |
