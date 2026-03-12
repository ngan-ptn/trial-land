---
## Evidence Index

**Key Evidence Sources:**
- **FSM State Management**: Lines 129-187 (StateMachineContext, states array, transitions object)
- **Component Navigation**: Lines 193-821 (5 main screens with navigation patterns)
- **User Actions**: Multiple onClick handlers throughout (lines 233, 243, 328, 491, 667, etc.)
- **Progress Indicators**: Lines 210-216, 308-319 (step tracking)
- **Error Handling**: Lines 823-846 (FailedState component)
- **Timeout Logic**: Lines 161-169 (120s confirmation timeout)

---

LAYER 2 - INTERACTION: Content Structure Template
## Feature Overview
- **Problem**: Users need to book medical appointments through a guided multi-step wizard
- **When this flow starts and ends**: Starts when user opens appointment booking, ends when appointment is confirmed or booking fails

## Entry Points
- **Where user can enter this flow**: SpecialtySelection screen (route "/")
- **From which screens / actions**: App launch, deep link, or "Book New Appointment" button (line 814)

## Happy Path (Primary Flow)
Step-by-step narrative of the ideal flow.

**Step 1:**
- **User intent**: Select medical specialty
- **User action**: Search specialty, select from recent searches, or choose common specialty
- **System response**: Transition to 'searching' state, navigate to location screen
- **Visible UI change**: Progress bar advances to 25%, new screen loads

**Step 2:**
- **User intent**: Specify appointment location and search radius
- **User action**: Use current location, enter address, or select saved location; adjust radius slider
- **System response**: Collect location parameters, prepare for search
- **Visible UI change**: Map preview, radius selection, location options

**Step 3:**
- **User intent**: Review and select from available appointments
- **User action**: Browse doctor results, select time slot
- **System response**: Transition to 'item_selected' state, navigate to confirmation
- **Visible UI change**: Doctor cards with availability, time slot selection

**Step 4:**
- **User intent**: Confirm appointment details
- **User action**: Verify patient, add optional reason, confirm appointment
- **System response**: Process booking, navigate to appointments management
- **Visible UI change**: Confirmation modal with details, success state

## System States (Behind the scenes)
> These are system-relevant conditions that affect behavior.
| State name | What it means (plain language) | User-visible? |
|----------|-------------------------------|---------------|
| **idle** | Initial state, ready to start booking | No |
| **searching** | Processing specialty search | Yes (loading implicit) |
| **result_listed** | Search results available for selection | Yes |
| **item_selected** | Specific appointment time chosen | No |
| **confirmation_pending** | Awaiting user confirmation with 120s timeout | Yes |
| **confirmed** | Appointment successfully booked | Yes |
| **failed** | Booking process failed | Yes |

## Decision Points & Rules
> Moments where the system must decide something.
| Decision | Rule (plain language) | If violated | Notes |
|--------|-----------------------|-------------|-------|
| State transition validity | Only allowed transitions as defined in FSM | Console warning, no state change | Lines 139-153 |
| Confirmation timeout | Auto-fail after 120s in confirmation_pending | Transition to 'failed' state | Lines 161-169 |
| Navigation flow | Sequential progression through screens | Route guards prevent skipping | Route structure |

## Alternate Paths (Edge & Recovery)
Describe deviations from happy path:

**No data (search results empty):**
- **Trigger**: No appointments found for criteria
- **System behavior**: INFERRED - Would show empty state with option to modify search
- **User experience**: Clear messaging, ability to adjust filters

**Timeout (120s):**
- **Trigger**: User stays in confirmation_pending > 120s
- **System behavior**: Auto-transition to 'failed' state
- **User experience**: Error screen with retry option

**User cancels:**
- **Trigger**: Back button usage at any step
- **System behavior**: Navigate to previous screen, reset related state
- **User experience**: Smooth backward navigation, partial data preserved

**System fails:**
- **Trigger**: Network error, server failure during booking
- **System behavior**: Transition to 'failed' state
- **User experience**: Error message with retry button (lines 832-842)

## Completion Criteria
- **What defines "done"**: User reaches ManageAppointments screen with new appointment visible
- **What is persisted**: Appointment details, patient info, location, time
- **Where user lands next**: /appointments route showing new appointment in "Upcoming" tab

## Open Questions / Assumptions
- **Unknown**: Data persistence mechanism between sessions
- **INFERRED**: Real-time availability checking during search (not explicitly shown)
- **ASSUMPTION**: Integration with external booking systems for actual appointment creation