# State Machine — <Feature / Flow Name>

> Purpose: Define all valid states and transitions for this flow.  
> Audience: Designers (behavior clarity) + Developers (deterministic implementation)

---

## 1. Scope & Intent
- What this state machine governs:
- What it explicitly does NOT cover:
- Related Layer 2 doc:
- Related Layer 3 intents:

---

## 2. Entry & Exit

### Entry States
- <state_name> — when/where the flow starts

### Exit States
- <state_name> — successful completion
- <state_name> — user-aborted
- <state_name> — terminal failure (if any)

---

## 3. States Overview (Human-Readable)

| State | Description (plain language) | User-visible? | Notes |
|------|------------------------------|---------------|-------|
| idle | Waiting for user action      | Yes           |       |
|      |                              |               |       |

---

## 4. Events (What can happen)

| Event | Triggered by | Description |
|------|--------------|-------------|
| submit_form | User | User confirms input |
| api_success | System | Backend responds OK |
| api_error | System | Backend returns error |

---

## 5. State Transitions (Authoritative)

> Every row = one allowed transition.  
> Anything not listed here is invalid by default.

| From State | Event | To State | Conditions (if any) | Side Effects | Certainty |
|-----------|-------|----------|---------------------|--------------|-----------|
| idle | submit_form | loading | form_valid | call API | EXPLICIT |
| loading | api_success | success | — | persist data | EXPLICIT |
| loading | api_error | error | — | show error | EXPLICIT |

Certainty values:
- **EXPLICIT** – clearly defined
- **INFERRED** – derived, not stated
- **UNKNOWN** – placeholder, needs decision

---

## 6. Rules & Invariants (Must Always Hold)

- The user can never reach `<state>` without `<event>`
- `<state>` must always show visible feedback
- Only one transition may be active at a time
- Time-bound states must communicate progress

---

## 7. Error & Recovery States

| Error State | Trigger | User Experience | Recovery Path |
|------------|--------|-----------------|---------------|
| error | api_error | Inline message | Retry → loading |
|        |          |                 | Back → idle |

---

## 8. Timeouts & System Constraints

| State | Constraint | Behavior |
|------|------------|----------|
| loading | > 10s | Show timeout message |
| pending | 120s | Auto-release, go to idle |

---

## 9. Cancellation & Reversibility

- States user can exit manually:
  - <state>
- States that are irreversible:
  - <state> (reason)

---

## 10. Mapping to UI Intent (Layer 3)

| State | Expected UI Signals |
|------|---------------------|
| loading | Spinner, disabled CTA |
| error | Inline message, retry |
| success | Confirmation + next step |

---

## 11. Open Questions / Risks

- What happens if <event> occurs in <state>?
- Is <state> truly terminal?
- Should <transition> be reversible?

---

## 12. Change Log

| Date | Change | Reason |
|-----|-------|--------|
|     |       |        |
