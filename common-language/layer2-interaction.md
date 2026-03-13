# LAYER 2 - INTERACTION: [Prototype Name]

---

## Template Usage Instructions

1. **Copy this file** and rename using the naming convention
2. **Replace all `[placeholder]` values** with specifics from your prototype analysis
3. **Add or remove steps** in Happy Path as needed for the flow length
4. **Add or remove states** in System States to match the FSM / state management
5. **Add alternate paths** for each edge case or recovery scenario discovered
6. **Fill the Evidence Index** with line references to source code for traceability
7. **Remove this instruction section** before finalizing

---

## Feature Overview

- **Problem**: [What the user needs to accomplish through this flow]
- **When this flow starts and ends**: [Trigger to start, condition that marks completion]

## Entry Points

- **Where user can enter this flow**: [Screen name, route, or component]
- **From which screens / actions**: [List all entry triggers - buttons, deep links, redirects, etc.]

## Happy Path (Primary Flow)

Step-by-step narrative of the ideal flow.

**Step 1:**
- **User intent**: [What the user wants to do]
- **User action**: [What the user physically does - tap, type, select, etc.]
- **System response**: [What the system does in response]
- **Visible UI change**: [What the user sees change on screen]

**Step 2:**
- **User intent**: [What the user wants to do]
- **User action**: [What the user physically does]
- **System response**: [What the system does in response]
- **Visible UI change**: [What the user sees change on screen]

**Step 3:**
- **User intent**: [What the user wants to do]
- **User action**: [What the user physically does]
- **System response**: [What the system does in response]
- **Visible UI change**: [What the user sees change on screen]

**Step 4:**
- **User intent**: [What the user wants to do]
- **User action**: [What the user physically does]
- **System response**: [What the system does in response]
- **Visible UI change**: [What the user sees change on screen]

## System States (Behind the scenes)

> These are system-relevant conditions that affect behavior.

| State name | What it means (plain language) | User-visible? |
|------------|-------------------------------|---------------|
| **[state_1]** | [Plain language description] | [Yes/No] |
| **[state_2]** | [Plain language description] | [Yes/No] |
| **[state_3]** | [Plain language description] | [Yes/No] |
| **[state_4]** | [Plain language description] | [Yes/No] |
| **[state_5]** | [Plain language description] | [Yes/No] |

## Decision Points & Rules

> Moments where the system must decide something.

| Decision | Rule (plain language) | If violated | Notes |
|----------|-----------------------|-------------|-------|
| [Decision 1] | [What the system checks / enforces] | [What happens on violation] | [Code reference] |
| [Decision 2] | [What the system checks / enforces] | [What happens on violation] | [Code reference] |
| [Decision 3] | [What the system checks / enforces] | [What happens on violation] | [Code reference] |

## Alternate Paths (Edge & Recovery)

Describe deviations from happy path:

**[Scenario 1 - e.g., No data / empty state]:**
- **Trigger**: [What causes this path]
- **System behavior**: [How the system responds]
- **User experience**: [What the user sees and can do]

**[Scenario 2 - e.g., Timeout]:**
- **Trigger**: [What causes this path]
- **System behavior**: [How the system responds]
- **User experience**: [What the user sees and can do]

**[Scenario 3 - e.g., User cancels]:**
- **Trigger**: [What causes this path]
- **System behavior**: [How the system responds]
- **User experience**: [What the user sees and can do]

**[Scenario 4 - e.g., System failure]:**
- **Trigger**: [What causes this path]
- **System behavior**: [How the system responds]
- **User experience**: [What the user sees and can do]

## Completion Criteria

- **What defines "done"**: [The condition that marks this flow as complete]
- **What is persisted**: [Data saved after completion]
- **Where user lands next**: [Screen / route after completion]

## Open Questions / Assumptions

- **Unknown**: [Gaps in evidence that need clarification]
- **INFERRED**: [Behavior deduced but not explicitly defined in code]
- **ASSUMPTION**: [Beliefs about external systems or future behavior]

---

## Evidence Index

**Key Evidence Sources:**
- **[Source Category 1]**: [File/location reference] ([what it contains])
- **[Source Category 2]**: [File/location reference] ([what it contains])
- **[Source Category 3]**: [File/location reference] ([what it contains])
- **[Source Category 4]**: [File/location reference] ([what it contains])
- **[Source Category 5]**: [File/location reference] ([what it contains])

