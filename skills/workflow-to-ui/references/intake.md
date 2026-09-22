# Intake

The goal is a work model in one pass. People are bad at answering open questions about their own work and very good at correcting a wrong guess, so the technique is: **infer, state your assumptions compactly, invite correction.**

## Infer first

Most of the seven facts are already implied by how someone describes what they want.

| Fact | Inference signals |
|---|---|
| **Verb** | The verb they used. "Review", "track", "log", "find", "approve". Trust their word over your reframing of it. |
| **Volume** | Plural + adjective: "all the submissions", "a few clients", "every ticket". "All" usually means hundreds; "manage my X" usually means dozens. |
| **Frequency** | "Every morning", "at month end", "when someone applies". Also: if they're asking for software at all, the task probably recurs. |
| **Stakes** | Money, people, permanence, external visibility, regulation. "Send to the client" and "delete" are high; "add a note" is low. |
| **Expertise** | Who they say uses it. "My team" = trained, repeat, wants speed. "Customers" or "the public" = untrained, one-shot, wants obviousness. |
| **Context** | Named devices, locations, or conditions. "On site", "in the van", "while on a call". Silence usually means desk, but check if the domain is physical. |
| **Session** | Falls out of volume × per-item time. 200 items at 5 seconds is a 20-minute grind; 3 items at 20 minutes is deep work. |

## Ask only what changes the design

Ask when the answer would flip the archetype, the shell, or the density. Don't ask for completeness.

Worth asking:

- **"Roughly how many of these in a typical session — five, fifty, five hundred?"** Flips density and the interaction budget.
- **"What happens after they [do the thing]? Where does it go?"** Reveals the real flow and usually a second archetype nobody mentioned.
- **"What does someone do most often — like, what's 80% of the clicks?"** Finds the primary loop when several archetypes are competing.
- **"What's the worst thing someone could do by accident?"** Sets the guardrails and the destructive-action ladder.
- **"Phone, desk, or both — and if both, what do they do on the phone?"** The second half of that question is the one that matters.

Rarely worth asking: preferred framework (they said tech stack doesn't matter), color preferences (that's frontend-design's territory, later), "what features do you want" (produces a list of screens, not a model of work).

## Stating assumptions

Compact, specific, correctable. Something like:

> Here's what I'm assuming: this is **triage** — one person going through ~80 applications a morning, deciding advance/reject/hold on each, at a desk, doing it daily. That points at a keyboard-driven list-detail layout rather than a dashboard. If the volume is more like 8 than 80, or if these decisions need a second opinion, tell me — either one changes the shape.

Two properties make this work: the numbers are concrete enough to be obviously wrong if they're wrong, and the last line names exactly which facts would change the answer.

## When you get no answer

Proceed anyway with stated defaults. A concrete wrong spec gets corrected in one round; a request for more information gets abandoned.

Sensible defaults when unstated:

- **Volume**: moderate (10–50), but design the layout so density can go up without restructuring.
- **Frequency**: daily. Optimizes for the repeat user, which is the right bet for internal tools.
- **Stakes**: reversible with undo. Add hard confirmation only where you can see real consequence.
- **Expertise**: mixed — label everything, but add keyboard shortcuts for the primary loop.
- **Context**: desktop primary, mobile read-and-light-action.
- **Session**: 5–15 minutes.

## Red flags in the brief

Signals that the stated request doesn't match the described work. Name these early — they're the highest-value thing this step produces.

| They asked for | But described | Probably want |
|---|---|---|
| "A dashboard" | Going through items and deciding | Triage, list-detail |
| "A dashboard" | Looking up specific records | Retrieve, search-first |
| "An AI chatbot" | Four known parameters and a result | Hero tool with a form |
| "A kanban board" | 400 items | Table with status grouping |
| "A mobile app" | Multi-column data comparison | Responsive web, desktop-primary |
| "A form" | Something done 50 times a day | Capture optimized hard, or bulk entry |
| "A wizard" | A daily task | One dense screen |
| "Reports" | Recurring "why did this happen" questions | Explore, not static reports |

When you spot one, build the right thing and explain the substitution in a sentence. Don't build the wrong thing because it was asked for by name, and don't refuse to build — just say what you changed and why, and let them push back.
