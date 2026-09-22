# FlowyourI

> **You're doing UI wrong. Start with the flow.**

Most bad interfaces are not ugly. They are the **wrong shape for the work**:
- A dashboard built for a job that is actually triage.
- A 40-field form for something people do on their phone in eight seconds.
- A wizard for a task done nine times a day.
- A multi-tab modal with "Are you sure?" confirmation dialogs for a high-volume queue.

AI agents are notorious for jumping straight from a fuzzy idea (*"build me an app to review submissions"*) into 500 lines of generic React and Tailwind code with twenty vanity metric cards. 

**FlowyourI** enforces structural interaction engineering before a single line of production code or CSS is written. It models the human work, matches the correct layout shell, budgets every click and keystroke, and tests the non-happy-path states.

*Created by **Ivar Limpens Richaards** ([@lampekapje](https://github.com/lampekapje)) &middot; [sixtyoneeighty.dev](https://sixtyoneeighty.dev)*

---

## The Niche: Structural Interaction vs. Aesthetic Styling

AI tooling has plenty of aesthetic engines, but zero structural ones:

| Focus | What It Does | Who Does It |
|---|---|---|
| **Aesthetic Direction** | Color palettes, typography, vibe, anti-AI slop styling | Anthropic's official `frontend-design` |
| **Component Libraries** | UI token databases, glassmorphism, Tailwind / shadcn snippets | `ui-ux-pro-max` |
| **Structural Work Modeling** | **Verbs & volume $\to$ Archetypes $\to$ Interaction budgeting $\to$ Layout shells $\to$ State coverage** | **FlowyourI** (`workflow-to-ui`) |

FlowyourI deliberately says **nothing about color, fonts, or frameworks**. It locks down the structural geometry and interaction physics of the application first. Once the structure is agreed, you can hand it off to `frontend-design` for styling.

---

## The 3 Skills

FlowyourI comes packed as a modular suite of three composable agent skills:

```
                  ┌────────────────────────────────────────────────────────┐
                  │ 1. workflow-to-ui                                      │
                  │ Seven intake facts → Archetype → Interaction Budget   │
                  │ → Layout Shell → 8 Non-Happy-Path States → Spec Matrix │
                  └───────────────────────────┬────────────────────────────┘
                                              │
                                              ▼
                  ┌────────────────────────────────────────────────────────┐
                  │ 2. ui-wireframe                                        │
                  │ Low-fi clickable greyscale HTML wireframe              │
                  │ Real content, keyboard shortcuts, live state switcher   │
                  └───────────────────────────┬────────────────────────────┘
                                              │
                                              ▼
                  ┌────────────────────────────────────────────────────────┐
                  │ 3. ui-flow-review                                      │
                  │ 7-dimension critique, quantified interaction waste     │
                  │ ("5 clicks × 200 items = 25 mins lost per day")       │
                  └────────────────────────────────────────────────────────┘
```

### 1. `workflow-to-ui`
Translates any fuzzy work description into a concrete structural spec.
- **The Seven Intake Facts:** Verb, Volume, Frequency, Stakes, Expertise, Context, Session Length.
- **14 Work Archetypes:** Triage, Monitor, Author, Capture, Explore, Decide, Track, Coordinate, Retrieve, Configure, Onboard, Converse, Compare, Collaborate.
- **Interaction Budgeting:** Enforces strict physical budgets ($100+\text{ items/session} \to 1\text{ key, auto-advance}$; $20\text{--}100 \to 1\text{--}3\text{ interactions}$; $5\text{--}20 \to 3\text{--}8$).
- **12 Layout Shells:** Matches work to proven architectural shells with collapse behaviors and explicit failure modes.
- **The 8-State Matrix:** First-run, empty, loading, slow, error, no-permission, overflow, and offline.

### 2. `ui-wireframe`
Turns the spec into a **disposable, clickable single-file HTML wireframe**:
- **Greyscale only:** Eliminates distracting debates over shades of blue so teams focus on layout and flow.
- **Realistic data density:** No `lorem ipsum`. 30+ rows, long names, edge-case numbers.
- **Embedded Review Chrome:** Built-in switcher bar to test Loaded, Empty, Loading, and Error states live.
- **Zero build step:** Pure HTML and vanilla JS that runs anywhere and can be emailed or shared instantly.

### 3. `ui-flow-review`
Critiques existing or proposed interfaces against the real work:
- Measures the primary loop and **counts every click and keystroke**.
- Calculates the cost of friction multiplied by daily volume.
- Identifies anti-patterns (e.g. destructive confirm dialogs on hot paths, kanban boards at 400 items, information split across modal tabs).

---

## Live Example

Check out the complete end-to-end walkthrough in [`examples/loan-triage-walkthrough/`](examples/loan-triage-walkthrough/):
1. [`1-intake-and-spec.md`](examples/loan-triage-walkthrough/1-intake-and-spec.md): Real mortgage underwriting intake turned into a 1-keystroke list-detail spec.
2. [`2-wireframe.html`](examples/loan-triage-walkthrough/2-wireframe.html): **Interactive, working wireframe** with live `j`/`k` navigation, `a` (advance) and `r` (reject) shortcuts, 5-second undo toast, and a live state switcher. Open it directly in any browser!
3. [`3-flow-review.md`](examples/loan-triage-walkthrough/3-flow-review.md): Quantified review demonstrating how eliminating modal tabs saved **28.5 minutes per underwriter per shift**.

---

## Installation & Platform Support

FlowyourI uses standard markdown skill definitions with YAML frontmatters, making it natively compatible across modern agent environments.

### Claude Code
Install as a plugin directly:
```bash
claude plugin add lampekapje/workflow-to-ui
```
Or copy the skills into your personal skills directory:
```bash
cp -r skills/* ~/.claude/skills/
```

### Google Antigravity
Drop into your global or project skills directory:
```bash
mkdir -p ~/.gemini/antigravity/skills
cp -r skills/* ~/.gemini/antigravity/skills/
```

### OpenAI Codex
Copy to your Codex skills folder:
```bash
mkdir -p ~/.codex/skills
cp -r skills/* ~/.codex/skills/
```

### Cursor & Windsurf
Add to your project rules (e.g. `.cursor/rules/workflow-to-ui.mdc` or `.windsurfrules`):
```markdown
# Workflow to UI Rules
Always follow the work-modeling and interaction-budgeting rules defined in:
https://github.com/lampekapje/workflow-to-ui
```

---

## Repository Structure

```
workflow-to-ui/
├── .claude-plugin/
│   └── plugin.json                     # Claude Code plugin manifest
├── skills/
│   ├── workflow-to-ui/                 # Primary work-to-spec skill
│   │   ├── SKILL.md
│   │   ├── assets/ui-spec-template.md  # Output spec template
│   │   └── references/                 # Intake, archetypes, shells, states, anti-patterns
│   ├── ui-wireframe/                   # Clickable greyscale wireframe skill
│   │   ├── SKILL.md
│   │   ├── assets/wireframe-kit.html   # Reusable single-file wireframe kit
│   │   └── references/                 # Shorthand & conventions
│   └── ui-flow-review/                 # Structural review skill
│       ├── SKILL.md
│       └── references/rubric.md        # 7-dimension critique rubric
├── examples/
│   └── loan-triage-walkthrough/        # Full working end-to-end example
├── .gitignore
├── LICENSE                             # MIT License (c) 2026 Ivar Limpens Richaards
└── README.md
```

---

## License

[MIT](LICENSE) &copy; 2026 **Ivar Limpens Richaards** ([https://sixtyoneeighty.dev](https://sixtyoneeighty.dev))
