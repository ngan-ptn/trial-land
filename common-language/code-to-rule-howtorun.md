# Code-to-Rule Patterns — Step-by-Step Guide

> How to follow `code-to-rule-pttrns.md` effectively.
> Each step has a prompt, a template, and a clear output to feed into the next step.

---

## Prerequisites

- Have the **source code** (or existing flow) for the feature you want to analyze
- Know which screens/routes are in scope

---

## Step 1 — Extract (Code → Layer 2: Interaction Contract)

**Goal:** Surface what the code *actually does* in human-readable form.

- Open the source code for your feature
- Use the **AI Prompt** from `code-to-rule-pttrns.md` (lines 93–108) — paste it + your code into Claude
- Fill the **Layer 2 template** from `code-to-rule-pttrns.md` (lines 111–159):
  - Feature name & purpose
  - Entry points
  - Happy path (step-by-step: user intent → user action → system decision → what user sees)
  - System states table
  - Decision rules
  - Alternate & failure paths
  - Completion criteria
  - Open questions (mark `INFERRED` / `UNKNOWN`)

**Reference example:** `layer2-interaction.md`

**Key rule:** This document is read by designers first, developers second. Use plain language.

**Output:** A complete Layer 2 doc → review with a designer to spot UX smells.

---

## Step 1.5 — Formalize (Layer 2 → Layer 2.5: State Machine)

**Goal:** Make the interaction contract deterministic and testable.

- Use the **State Machine prompt** from `code-to-rule-pttrns.md` (lines 38–87)
- Take your Layer 2 happy path + alternate paths and convert them into:
  - **A) Mermaid state diagram** — visual, for designers
  - **B) YAML state machine spec** — exact, for developers
- Fill the full **State Machine template** from `state-machine.md`:
  - Scope & intent (what it governs / doesn't)
  - Entry & exit states
  - States overview table
  - Events table
  - Transitions table (with certainty: `EXPLICIT` / `INFERRED` / `UNKNOWN`)
  - Rules & invariants
  - Error & recovery states
  - Timeouts & constraints
  - Cancellation & reversibility
  - Mapping to UI intent
  - Open questions

**Key rule:** Every happy path step must map to `(state) --event--> (state)`. If it doesn't, the Layer 2 doc is incomplete — go back.

**Output:** A state machine doc that defines all valid states. "Anything not listed is a bug."

---

## Step 2 — Reflect (Layer 2 → Layer 3: UI Intent)

**Goal:** Translate *what happens* into *how it should feel*.

- Use the **UI Intent Reflector prompt** from `code-to-rule-pttrns.md` (lines 172–186)
- Fill the **Layer 3 template** from `code-to-rule-pttrns.md` (lines 189–231):
  - Experience goal (what user should feel)
  - Core screens table (screen → purpose → emotional tone)
  - Information hierarchy per screen (primary / secondary / must-not-distract)
  - Action hierarchy (primary vs secondary actions per screen)
  - Feedback philosophy (loading / success / failure / pending)
  - Error handling intent (inline vs global, blocking vs non-blocking, tone)
  - Progress & control (orientation, back/cancel, irreversibility)
  - Accessibility & cognitive load
  - Experience anti-patterns observed

**Reference example:** `layer3-ui-intent.md`

**Bridge tool:** Use `layer2-3-bridge.md` if the jump from Layer 2 → Layer 3 feels too big. It provides an intermediate mapping: contract → intent translation table.

**Key rule:** Focus on experience principles, not components. This doc must be reusable across features.

**Output:** A Layer 3 doc → use it to align designers and compare intent across flows.

---

## Step 3 — Crystallize (Layer 3 → Design System Patterns)

**Goal:** Extract *reusable* rules from specific UI intents.

- Use the **Decision Tree** from `crystallize-decision-tree.md` to classify each Layer 3 intent:

```
For each UI Intent in Layer 3:
  ├─ Does this intent appear in 2+ screens/flows?
  │   ├─ YES → Does it solve the same user/system tension each time?
  │   │   ├─ YES → EXTRACT as Design System Pattern
  │   │   └─ NO  → Document as VARIANT (same surface, different rule)
  │   └─ NO  → Is it likely to recur in future flows?
  │       ├─ LIKELY    → Mark as CANDIDATE (extract later when confirmed)
  │       └─ UNLIKELY  → Keep as SCREEN-LOCAL rule (no pattern needed)
```

- For each "Extract" decision, fill the **Design System pattern template** from `code-to-rule-pttrns.md` (lines 260–289):
  - Pattern name (behavior-based, not component-based)
  - Problem it solves
  - When to use / when NOT to use
  - Core UX rules (must / must not)
  - Required user signals
  - System responsibilities
  - Related patterns
  - Origin (flow names + date)

**Key rule:** Only create patterns justified by *repeated* intent. If it only exists in one flow, it's not a pattern yet.

**Output:** Design System rules + a candidates watch list. The decision tree stays as a **separate artifact** — links to Design System but is not merged into it.

---

## File Map

| Step | Action | Template file | Example output |
|------|--------|---------------|----------------|
| 1 | Extract | `code-to-rule-pttrns.md` (L111–159) | `layer2-interaction.md` |
| 1.5 | Formalize | `state-machine.md` | *(create per feature)* |
| 2 | Reflect | `code-to-rule-pttrns.md` (L189–231) | `layer3-ui-intent.md` |
| 2→3 | Bridge | `layer2-3-bridge.md` | *(optional, when gap feels large)* |
| 3 | Crystallize | `crystallize-decision-tree.md` + `code-to-rule-pttrns.md` (L260–289) | *(Design System patterns)* |

---

## Supporting Files

| File | Role |
|------|------|
| `layer-2-3-state-dls.md` | Visual cheat sheet — Mermaid diagrams showing what each layer represents and how they connect end-to-end |
| `layer2-3-bridge.md` | Optional intermediate step between Layer 2 and Layer 3 when the jump feels too big |
| `implementation-template.md` | Full prototype template — translates Design System output into a buildable dev spec |
| `implementation-template (lighter-ver).md` | Fast experiment version — for quick validation before committing to full implementation |

---

## Where the Output Goes

```
Step 1 output  → Review with designer → feeds Step 1.5
Step 1.5 output → Validates Layer 2 completeness → feeds Step 2
Step 2 output  → Align team on experience intent → feeds Step 3
Step 3 output  → Design System patterns → feeds implementation templates
                                        → feeds dev tool specs (forDevTool/)
```
