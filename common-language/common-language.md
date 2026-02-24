# Common Language

## Flow to Build Design System

```
Code / Flow reality
    ↓ extract
Layer 2 – Interaction Contract
    ↓ reflect
Layer 3 – UI Intent
    ↓ crystallize ——(decision-tree)
Design System rules & patterns
```

**Layer 3 = Backbone to build & evolve Design System**

* Design System starts with rules, not with buttons

**Layer 2 = Input to validate & stress-test Design System**

* Expose pattern pressure
* Validate Design System
* Prioritize Design System roadmap (how mature teams build DLS)

**Design System – Patterns**: Defines principles & rules

**Decision Trees / Usage Guide** (your file):
* If situation X → choose Y
* For designers + devs when building for real

👉 Can link back and forth, but **should not be merged**.

———

## AI Prompt

You are not designing new experiences.
You are extracting, reflecting, and crystallizing patterns from existing behavior.
Do not invent.
Do not optimize.
Surface uncertainty explicitly.

**——**

You are a software analyst and product interaction mapper.

Goal: From the provided code file, extract ONLY:
1. Layer 2: Interaction Contract (state machine + transitions + rules)
2. Layer 3: UI Intent (layout principles, primary actions, feedback/errors, accessibility intent)

Strict rules:
* Do NOT invent flows not evidenced in the code.
* If something is implied but not explicit, mark it as INFERRED and cite the code evidence (file line numbers or function/component names).
* If unknown, mark as UNKNOWN.
* Keep naming consistent with code (state names, event names, routes).
* Output must follow the provided templates exactly.
* Provide a short "Evidence Index" referencing where each extracted item came from in the code (component/function names; line numbers if available).

Now analyze the code. Save the output with the following structure:

——------

## PRODUCT INTENT

### Feature Name
Short, unambiguous

### Context
Describe user situation and emotional state

### JTBD
When <situation>
I want to <motivation>
So that <outcome>

### Success Criteria
* Measurable user outcome
* System outcome

### Constraints (Hard)
* Legal / Compliance
* Performance
* Privacy

### Non-goals
Explicit exclusions to prevent scope creep

———

## LAYER 2 - INTERACTION: Content Structure Template

```yaml
states:
  - state_name

initial_state: state_name

transitions:
  - from: state_a
    to: state_b
    trigger: user_action / system_event
    conditions:
      - condition
    side_effects:
      - system_action

timeouts:
  state_name: duration_in_seconds

error_states:
  - state_name
```

---

### Feature Overview
* What problem this interaction solves
* When this flow starts and ends

### Entry Points
* Where user can enter this flow
* From which screens / actions

### Happy Path (Primary Flow)
Step-by-step narrative of the ideal flow.

Step 1:
* User intent:
* User action:
* System response:
* Visible UI change:

Step 2:
...

### System States (Behind the scenes)
> These are system-relevant conditions that affect behavior.

| State name | What it means (plain language) | User-visible? |
|------------|-------------------------------|---------------|
|            |                               | Yes / No     |

### Decision Points & Rules
> Moments where the system must decide something.

| Decision | Rule (plain language) | If violated | Notes |
|----------|-----------------------|-------------|-------|

### Alternate Paths (Edge & Recovery)
Describe deviations from happy path:
* No data
* Timeout
* User cancels
* System fails

For each:
* Trigger
* System behavior
* User experience

### Completion Criteria
* What defines "done"
* What is persisted
* Where user lands next

### Open Questions / Assumptions
* Anything unclear from code

——

## LAYER 3 - UI INTENT: Content Structure Template

### Layout Principles
* Screen hierarchy rules
* Interaction density

### Primary Actions
* One primary action per screen
* Placement rules

### Feedback & Error Handling
* Inline vs modal
* Tone and urgency

### Accessibility
* Touch target
* Contrast
* Keyboard / screen reader notes

**–**

### Experience Goal
What the user should feel during this flow
(e.g. fast, reassuring, low cognitive load)

### Core Screens

| Screen | Purpose | Emotional tone |
|--------|---------|----------------|

### Information Hierarchy
For each screen:
* Primary focus:
* Secondary info:
* What must not distract:

### Primary & Secondary Actions

| Screen | Primary Action | Secondary Actions | Notes |
|--------|----------------|-------------------|-------|

### Feedback Philosophy
How the system communicates with the user:
* Loading:
* Success:
* Failure:
* Empty states:

### Error Handling Style
* Inline vs global
* Blocking vs non-blocking
* Tone (neutral / empathetic / urgent)

### Progress & Orientation
* Does user always know:
  * Where they are?
  * What's next?
  * Can they go back?

### Accessibility & Reachability (Intent-level)
* One-hand usage assumptions
* Minimum touch target intent
* Reading / comprehension level

### Explicitly Not Defined
* Visual style
* Brand elements
* Color / typography

——

## DESIGN SYSTEM — CONTENT STRUCTURE TEMPLATE

You are a design system architect.
Using the provided UI Intent (Layer 3), extract reusable Design System rules and patterns.

Rules:
* Only create patterns that can apply to multiple flows.
* Each pattern must be justified by repeated intent.
* Write rules in human language, not component specs.
* Clearly state when the pattern should and should not be used.
* Output must follow the provided Design System template exactly.

### Design System – Interaction Pattern

#### Pattern Name
Human-readable, behavior-based.

#### Problem This Pattern Solves
What user/system tension it addresses.

#### When to Use
Situations where this pattern applies.

#### When NOT to Use
Clear exclusions.

#### Core UX Rules
Non-negotiable rules (must / must not).

#### Required User Signals
What user must always see or be able to do.

#### System Responsibilities
What the system must guarantee.

#### Related Patterns
Dependencies or alternatives.

#### Origin
Derived from:
* Feature / Flow name(s)
* Date
