# Behavioral & Design System Diagrams

This document consolidates all conceptual diagrams for Layers **B, C, D, E** in the product-to-design-system pipeline.

---

## B — Layer 2: Interaction Contract
**Purpose:** Behavioral truth — what must happen.

```mermaid
flowchart TD
    U[User Intent] --> A[User Action]
    A --> S[System Decision]
    S --> V[Visible Outcome]

    S -->|rule violated| E[Error / Recovery Path]
    E --> V

    subgraph Contract["Interaction Contract"]
        A
        S
        V
        E
    end
```
**Interpretation:**  
“When the user does X, the system decides Y, and the user sees Z.”

---

## C — Layer 2.5: State Machine
**Purpose:** Behavioral enforcement — what is allowed or impossible.

```mermaid
stateDiagram-v2
    [*] --> idle

    idle --> loading: submit
    loading --> success: success
    loading --> error: failure
    loading --> timeout: timeout

    error --> idle: retry
    timeout --> idle: restart

    success --> [*]
```
**Interpretation:**  
“These are the only valid states. Anything else is a bug.”

---

## D — Layer 3: UI Intent
**Purpose:** Experience translation — how behavior is felt.

```mermaid
flowchart TD
    S[System State Change] --> I[User Interpretation]
    I --> F[User Feeling]
    F --> C[User Confidence / Clarity]

    subgraph UIIntent["UI Intent"]
        I
        F
        C
    end
```
**Interpretation:**  
“When the system changes state, the UI ensures understanding, emotional safety, and orientation.”

---

## E — Design System Rules & Patterns
**Purpose:** Crystallized reuse — organization-level truths.

```mermaid
flowchart TD
    I1[UI Intent from Flow A]
    I2[UI Intent from Flow B]
    I3[UI Intent from Flow C]

    I1 --> R[Reusable Rule / Pattern]
    I2 --> R
    I3 --> R

    R --> U[Used Across Features]
```
**Interpretation:**  
“When the same UI intent appears repeatedly, it becomes a system rule or pattern.”

---

## End-to-End Relationship (B → C → D → E)

```mermaid
flowchart LR
    B[Interaction Contract<br/>(What happens)]
    C[State Machine<br/>(What is allowed)]
    D[UI Intent<br/>(How it feels)]
    E[Design System<br/>(What we reuse)]

    B --> C
    C --> D
    D --> E
```
