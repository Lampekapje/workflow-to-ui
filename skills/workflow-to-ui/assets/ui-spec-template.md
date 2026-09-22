# UI Spec — [Product name]

> Structural spec only. No color, typography, or framework decisions — those come after this is agreed.

## 1. Work model

| | |
|---|---|
| **Users do** | [verb, in their words] |
| **Archetype** | [primary] (+ [secondary] as a subordinate surface) |
| **Volume** | [N per session] |
| **Frequency** | [how often] |
| **Stakes** | [reversible / costly / irreversible] |
| **Expertise** | [one-shot / trained / expert daily] |
| **Context** | [device, environment, interruption] |
| **Session** | [typical length] |

*Assumed, not confirmed:* [list any fact you guessed — these are the ones worth correcting first]

## 2. Primary loop

The cycle repeated most often, by count:

1. [step]
2. [step]
3. [step]

**Interactions per item:** [N] — budget for this volume is [N]. [Met / how it was brought under budget.]

**Keyboard path:** [keys for each outcome]

## 3. Screen inventory

| Screen | Archetype | Shell | Density | Purpose |
|---|---|---|---|---|
| [Name] | [type] | [shell] | [H/M/L] | [one line] |

**Navigation:** [no nav / tabs / sidebar / nested] — [N] destinations: [list]
**Home screen:** [which, and why — should serve the returning-with-work user]

---

## 4. Screen: [Name]

**Purpose:** [one sentence — what the user accomplishes here]
**Shell:** [shell name] — [why this one for this work]
**Primary action:** [the one dominant action]

```
[ASCII wireframe — proportions, regions, and where the primary action sits]
```

**Regions**
- **[Region]:** [what's in it, how it behaves, what it's for]

**Interactions**
- [trigger → result]

**Keyboard:** [shortcuts specific to this screen]

**States**

| State | Behavior |
|---|---|
| First run | |
| Empty (nothing pending) | |
| Empty (filtered out) | |
| Loading, first | |
| Loading, subsequent | |
| Error | |
| No permission | |
| Too much data | |

**Responsive:** [reflow / reveal / replace / refuse] — [mobile priority order or the substitute shell]

*(Repeat section 4 per screen.)*

---

## 5. Flow

```
[entry] ──▶ [screen] ──▶ [screen] ──┐
              ▲                     │
              └─────────────────────┘
                   (primary loop)

  escape hatches: [undo / back / save draft / cancel]
```

## 6. Safety

| Action | Consequence | Treatment |
|---|---|---|
| [action] | [reversible?] | [undo / confirm / type-to-confirm] |

## 7. Non-goals

Deliberately not in this design, and why:
- [thing] — [reason]

## 8. Open questions

- [question] — [which part of the design it would change]
