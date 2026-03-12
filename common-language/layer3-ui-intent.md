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

LAYER 3 - UI INTENT: Content Structure Template
## Experience Goal
**What the user should feel during this flow**: Fast, reassuring, low cognitive load - Guided wizard with clear progress, minimal choices per screen, healthcare-appropriate professional tone

## Core Screens
| Screen | Purpose | Emotional tone |
|------|---------|----------------|
| **SpecialtySelection** | Guide users to select medical specialty | Supportive, helpful |
| **LocationSelection** | Define service area and preferences | Efficient, precise |
| **SearchResults** | Present available options clearly | Informative, trustworthy |
| **ConfirmAppointment** | Finalize booking with confidence | Reassuring, professional |
| **ManageAppointments** | Provide ongoing appointment control | Organized, empowering |

## Information Hierarchy
For each screen:

**SpecialtySelection:**
- **Primary focus**: Search bar and specialty selection
- **Secondary info**: Recent searches, common choices
- **What must not distract**: Navigation elements, complex options

**LocationSelection:**
- **Primary focus**: Location input method and radius
- **Secondary info**: Map preview, saved locations
- **What must not distract**: Advanced filtering options

**SearchResults:**
- **Primary focus**: Doctor availability and time slots
- **Secondary info**: Ratings, distance, insurance info
- **What must not distract**: Detailed medical histories

**ConfirmAppointment:**
- **Primary focus**: Appointment details and confirmation
- **Secondary info**: Patient selection, reason field
- **What must not distract**: Editing capabilities, complex options

## Primary & Secondary Actions
| Screen | Primary Action | Secondary Actions | Notes |
|------|----------------|------------------|-------|
| **SpecialtySelection** | Select specialty | Recent searches, browse common | Search bar doubles as action |
| **LocationSelection** | Continue with location | Use current location, saved locations | Back button for correction |
| **SearchResults** | Select time slot | Filter/sort, save doctor | More appointments link |
| **ConfirmAppointment** | Confirm appointment | Edit patient, add reason | Close to cancel |
| **ManageAppointments** | View appointments | Reschedule, cancel, book new | Tab switching |

## Feedback Philosophy
How the system communicates with the user:
- **Loading**: Implicit in navigation, no explicit loaders shown
- **Success**: Clear confirmation and navigation to appointment list
- **Failure**: Dedicated error screen with retry option
- **Empty states**: Not explicitly defined but implied helpful messaging

## Error Handling Style
- **Inline vs global**: Global error handling through FSM states
- **Blocking vs non-blocking**: Blocking for critical failures (timeout, system errors)
- **Tone (neutral / empathetic / urgent)**: Neutral to empathetic ("Something went wrong" - line 832)

## Progress & Orientation
- **Does user always know:**
  - **Where they are?** Yes - Step indicators (lines 210-216, 308-319)
  - **What's next?** Yes - Clear progression through wizard
  - **Can they go back?** Yes - Back buttons on every screen

## Accessibility & Reachability (Intent-level)
- **One-hand usage assumptions**: Mobile-first design, large touch targets
- **Minimum touch target intent**: 44px minimum (h-12 classes, buttons)
- **Reading / comprehension level**: Simple language, clear medical terms with context

## Explicitly Not Defined
- **Visual style**: Colors and typography defined but not interaction specifics
- **Brand elements**: Logo placement, brand voice
- **Color / typography**: While defined in config, semantic usage not fully specified
- **Animation**: Transition durations mentioned but interaction patterns not detailed