# Design Brief: Revamp “Appointments” → Calendar-Based “Dates” Page

## Context

The current Appointments experience is list-based. This revamp introduces a **calendar-centric “Dates” page** inspired by Amie:
- A week strip with small color dots is the default way to navigate.
- A bottom sheet month grid helps jump across weeks/months.
- Selecting a day reveals a compact agenda list below.

This also absorbs the “Past Appointments” experience into the same calendar flow, adds a person filter for family members, and fixes a status display bug where a status appears to change after tapping.

## Goals

- Make it faster to answer: “What do I have on this day/week?”
- Reduce switching between “upcoming” vs “past” screens by making time navigation the primary control.
- Keep the UI mobile-native-feeling: quick taps, swipes, and a lightweight agenda.
- Support households: filter by “All / Myself / Family member”.

## Design Summary

### Two Views: Month (default) and Day

**MONTH VIEW** (default):
```
┌──────────────────────────────────┐
│  Dates               [📅] [📋]  │  ← Header with Month/Day toggle
├──────────────────────────────────┤
│  2026    M   T   W   T   F  S  S│  ← Amie-style week strip header
│  Feb    23  24 [25] 26  27 28  1│    (static, shows current week)
│              ●   ●●      ● [Today]│  ← dots + conditional Today pill
├──────────────────────────────────┤
│  Wednesday, Feb 25               │  ← Selected day label
│  ┌── 09:00–10:00 ──────────────┐│  ← CompactAppointmentCard
│  ┃ [AS]  For Myself            ││    Time range as top label
│  ┃       Dr. Anna Schmidt      ││    3px left color bar (status)
│  ┃       Arzttermin · Praxis   ││    + status text badge
│  ┃       [AWAITING CONFIRM]    ││    Avatar top-left, aligned
│  └─────────────────────────────┘│    with for-who row
│  ┌── 14:30–15:30 ──────────────┐│
│  ┃ [HW]  For Emma (Child)      ││    Completed cards keep
│  ┃       Dr. Hans Weber         ││    "Rate visit" action
│  ┃       Cardiology · Herzkl.  ││
│  ┃       [CONFIRMED]           ││
│  └─────────────────────────────┘│
├──────────────────────────────────┤
│  [All][Myself][Emma]    [+ Book] │  ← Bottom bar (chips conditional)
└──────────────────────────────────┘

Note: [Today] floating pill sits inside the calendar area
(overlays bottom-right of the WeekStrip), like Amie.

Tap "Feb" month name → opens bottom sheet:
┌──────────────────────────────────┐
│  ─────  (drag handle)            │
│  March 2026 >          < >      │  ← Month title + nav arrows
│  MON TUE WED THU FRI SAT SUN   │
│                            1     │
│   2   3   4  (5)  6   7   8     │  ← Full month grid with dots
│   9  10  11  12  13  14  15     │    Today = filled circle
│  16  17  18  19  20  21  22     │    Selected = ring outline
│  23  24  25  26  27  28  29     │
│  30  31                          │
└──────────────────────────────────┘
```

**DAY VIEW** (toggle via header icon):
```
┌──────────────────────────────────┐
│  Dates               [📅] [📋]  │  ← Header with Month/Day toggle
├──────────────────────────────────┤
│ ← 23  24 [25] 26  27  28  1  → │  ← Horizontal scrollable date strip
│   Mon Tue Wed Thu Fri Sat Sun   │    (Amie-style, swipe to scroll)
│        ●   ●●      ● [Today]   │    dots + conditional Today pill
├──────────────────────────────────┤
│  Wednesday, Feb 25               │  ← Selected day label
│  ┌── 09:00–10:00 ──────────────┐│  ← Same CompactAppointmentCard
│  ┃ [AS]  For Myself            ││    as Month view (identical)
│  ┃       Dr. Anna Schmidt      ││
│  ┃       Arzttermin · Praxis   ││
│  ┃       [CONFIRMED]           ││
│  └─────────────────────────────┘│
├──────────────────────────────────┤
│  [All][Myself][Emma]    [+ Book] │  ← Same bottom bar
└──────────────────────────────────┘

Note: [Today] pill also inside calendar area for Day view.

```

### Key Differences: Month vs Day View

| Aspect | Month View | Day View |
|--------|-----------|----------|
| **Header strip** | Static week strip (current week of selected date) | Horizontally scrollable date strip (swipe to browse days) |
| **Month nav** | Tap month name → bottom sheet with full month grid | Scroll date strip continuously across month boundaries |
| **Week context** | Shows one week at a time, changes when selecting a day in different week via bottom sheet | Scrolls fluidly day-by-day |

### Bottom Bar

- **Conditional person chips**: Only show `[All] [Myself] [Family...]` chips when user has family members. Solo users see only the `[+ Book]` button.
- `[+ Book]` button always present on the right side
- Sticky at bottom, above the tab bar

### Color-Coded Dot System

| Dot Color | Statuses | Hex |
|-----------|----------|-----|
| Teal | `matching`, `await_confirm` | `#13A3B5` |
| Green | `confirmed` | `#22C55E` |
| Amber | `completed` | `#F59E0B` |
| Red | `cancelled_*`, `modified_by_practice` | `#EF4444` |

- Multiple dots side by side (max 3, then +N)
- Today: filled teal circle behind number
- Selected day: teal ring outline

### Key Interactions
- **Month/Day toggle**: Header icons switch between static week strip and scrollable date strip
- **Tap month name (month view)**: Opens bottom sheet with full month grid + `<` `>` arrows for month navigation
- **Select day in bottom sheet**: Updates selected date, closes sheet, week strip updates to show that week
- **Date nav (day view)**: Swipe date strip horizontally to browse days continuously
- **"Today" pill**: Conditional floating button, appears in BOTH views when not viewing today
- **[+ Book]**: Opens existing booking flow
- **Card tap**: Opens existing `AppointmentDetailScreen`
- **Person chips (bottom bar)**: Filter dots + agenda by All / Myself / Family member (only shown when family members exist)

---

## UX Notes

- Empty state: if no appointments for a selected day, show a friendly “no appointments” message.
- Past and future are navigated the same way; no separate “past appointments” destination is needed.
- Ensure status display is stable: tapping must not visually “flip” a status.

## Localization

- English-first, with German parity.
- Labels needed: “Dates”, “Today”, “All”, “Myself”, and an empty-state message.
