# Plan: Revamp Appointments Page → Calendar-Based "Dates" Page

## Context

The current Appointments page is a list-based view with swipeable card stacks and status filters. The user wants to transform it into a **calendar-centric "Dates" page** inspired by Amie, where a week strip with color-coded dots is the default view, a bottom sheet provides the full month grid for navigation, and tapping a day reveals a compact agenda below. This also absorbs the Past Appointments screen, adds a person filter for family members, and fixes a status display bug.

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
- **[+ Book]**: Opens existing bookig flow
- **Card tap**: Opens existing `AppointmentDetailScreen`
- **Person chips (bottom bar)**: Filter dots + agenda by All / Myself / Family member (only shown when family members exist)

---

## Implementation Plan

### Phase 1: Data Layer — `calendarUtils.ts`

**Create** `apps/src/lib/calendarUtils.ts`

Pure utility functions (no React deps, easy to test):
- `STATUS_DOT_COLOR` map — status → hex color
- `getDateKey(date)` → `'YYYY-MM-DD'` string
- `getMonthDays(year, month)` → 6-week grid of Date objects (with leading/trailing days)
- `getWeekForDate(date)` → the 7-day row (Mon–Sun) containing the given date
- `groupAppointmentsByDay(appointments)` → `Map<DateKey, Appointment[]>`
- `getDotsForDay(appointments)` → unique statuses sorted by priority (teal → green → amber → red)
- `isToday(date)`, `isSameDay(a, b)`, `isSameMonth(date, year, month)`
- `formatDayLabel(date, locale)` → "Wednesday, Feb 25" via `Intl.DateTimeFormat`
- `formatMonthYear(date, locale)` → "February 2026"
- `getDateRange(centerDate, radius)` → array of dates for the scrollable date strip

### Phase 2: New Components

All in `apps/src/components/calendar/`:

| Component | Description |
|-----------|-------------|
| `WeekStrip.tsx` | Amie-style static week strip: row 1 = year + weekday abbreviations (M T W T F S S), row 2 = month name + date numbers + dots. Month name is tappable (opens bottom sheet in month view). |
| `DateStrip.tsx` | Horizontal scrollable date strip for Day view. Shows ~7 dates with day names + dots, swipeable to browse continuously. |
| `MonthGridSheet.tsx` | **Bottom sheet** containing full month grid with `<` `>` arrows for month nav. Opens when tapping month name in WeekStrip. Has day cells with dots, tap to select + close sheet. |
| `CompactAppointmentCard.tsx` | **Top**: time range label (e.g. "09:00–10:00") spanning full width. **Body**: two-column — **Left** = doctor avatar circle (top-left, aligned with first text row), **Right** = for-who label, doctor name, specialty + location, status badge (top to bottom). 3px left border + status text badge. Completed appointments show "Rate visit" action. Reuses `DoctorAvatar`/`getAvatarInitials` from existing `AppointmentListCard.tsx`. |
| `BottomBar.tsx` | Sticky bottom bar with conditional person filter chips (only when family members exist) + `[+ Book]` button on right |
| `TodayPill.tsx` | Conditional floating "Today" button, positioned inside the calendar area (bottom-right of WeekStrip/DateStrip). Visible when selected date is not today. Works in both views. |
| `ViewToggle.tsx` | Two small icons in header (grid icon / list icon) to switch Month ↔ Day view |
| `index.ts` | Barrel export |

### Phase 3: Main Screen — `DatesScreen.tsx`

**Create** `apps/src/screens/DatesScreen.tsx`

State:
- `viewMode` — `'month' | 'day'` (toggle via header icons)
- `selectedDate` — which day is selected (defaults to today)
- `personFilter` — `'all' | '__self__' | familyMemberName`
- `isSheetOpen` — whether the month grid bottom sheet is open (month view only)

Derived state:
- `currentWeek` — computed from `selectedDate` via `getWeekForDate(selectedDate)`
- `sheetMonth`/`sheetYear` — which month the bottom sheet is showing (can navigate independently)

Data flow:
1. Filter appointments by `personFilter` (skip filter when no family members)
2. `groupAppointmentsByDay(filtered)` → Map
3. Pass Map to WeekStrip/DateStrip for dot rendering
4. For selected day, get sorted agenda list

Layout (both views): Header with ViewToggle → WeekStrip or DateStrip + TodayPill → Day label + agenda list → BottomBar

### Phase 4: Navigation & Routing

**Modify** `apps/src/App.tsx`:
- Replace `AppointmentsScreen` → `DatesScreen`
- Remove `PastAppointmentsScreen` import and routing case
- `'past-appointments'` ViewState → redirect to appointments tab (backward compat)
- Remove archive button from header

**Modify** `apps/src/hooks/useNavigation.ts`:
- `openPastAppointments()` → redirect to appointments tab
- Keep `'past-appointments'` valid in `isValidViewState` for browser history compat

**Key decision**: TabKey stays `'appointments'` internally — only the display label changes. This avoids cascading refactors.

### Phase 5: i18n

**Modify** `apps/src/i18n/locales/{en,de}/`:

Add:
- `appointment.calendar.today` → "Today" / "Heute"
- `appointment.calendar.noAppointments` → "No appointments on this day." / "Keine Termine an diesem Tag."
- `appointment.calendar.subtitle` → "Your appointments at a glance" / "Deine Termine auf einen Blick"
- `appointment.personFilter.all` → "All" / "Alle"
- `appointment.personFilter.myself` → "Myself" / "Ich"

Change:
- `nav.appointments` → "Dates" (EN) / keep "Termine" (DE)

Remove obsolete keys:
- `appointment.othersSection`, `groupThisMonth`, `groupOlder`
- `appointment.filter.*` (status filter keys)
- `appointment.upcomingAll`, `upcomingMyself`, `upcomingFamily`
- `actions.pastAppointment`

### Phase 6: Cleanup

- **Delete** `apps/src/screens/PastAppointmentsScreen.tsx`
- **Keep** `AppointmentListCard.tsx` (used by HomeScreen)
- **Keep** `CardStackWithPager.tsx` (may be used elsewhere)
- **Keep** `AppointmentDetailScreen.tsx` (unchanged)

### Phase 7: Status Bug Fix

Bug: "status changes from rejected to pending when clicked"

Root cause investigation needed. The status comes from `migrated-domain.ts` mock data via `mapStatus(seed.targetStatus)` — it's static. Likely a rendering race in `AppointmentDetailScreen` where the appointment lookup briefly resolves to wrong data during navigation transition. Will instrument with console.log during implementation to pinpoint.

---

## Files Summary

| Action | File |
|--------|------|
| CREATE | `apps/src/lib/calendarUtils.ts` |
| CREATE | `apps/src/components/calendar/WeekStrip.tsx` |
| CREATE | `apps/src/components/calendar/DateStrip.tsx` |
| CREATE | `apps/src/components/calendar/MonthGridSheet.tsx` |
| CREATE | `apps/src/components/calendar/CompactAppointmentCard.tsx` |
| CREATE | `apps/src/components/calendar/BottomBar.tsx` |
| CREATE | `apps/src/components/calendar/TodayPill.tsx` |
| CREATE | `apps/src/components/calendar/ViewToggle.tsx` |
| CREATE | `apps/src/components/calendar/index.ts` |
| CREATE | `apps/src/screens/DatesScreen.tsx` |
| MODIFY | `apps/src/data/types.ts` — add `PersonFilter`, `ViewMode` types |
| MODIFY | `apps/src/hooks/useNavigation.ts` — redirect past-appointments |
| MODIFY | `apps/src/App.tsx` — swap screens, update routing + header |
| MODIFY | `apps/src/i18n/locales/en/nav.json` |
| MODIFY | `apps/src/i18n/locales/en/appointment.json` |
| MODIFY | `apps/src/i18n/locales/de/appointment.json` |
| MODIFY | `apps/src/i18n/locales/en/actions.json` |
| MODIFY | `apps/src/i18n/locales/de/actions.json` |
| DELETE | `apps/src/screens/PastAppointmentsScreen.tsx` |

## Verification

1. `pnpm build:packages` — ensure tokens + UI build
2. `pnpm dev` — verify:
   - Bottom tab shows "Dates" label
   - **Month view**: Amie-style week strip with year, weekdays, month name, dates, and dots
   - **Month view**: Tap month name → bottom sheet with full month grid and `<` `>` arrows
   - **Month view**: Select day in bottom sheet → updates week strip + agenda
   - **Day view**: Horizontal scrollable date strip works smoothly
   - **View toggle**: Header icons switch between Month ↔ Day views
   - **Today pill**: Floating button appears in both views when not on today
   - **Bottom bar**: Person chips only appear when family members exist
   - **Bottom bar**: `[+ Book]` opens existing booking flow
   - Card tap opens AppointmentDetailScreen with correct status
   - Navigate to past months/days to see completed/cancelled appointments
   - Status does not change when tapping an appointment card (bug fix)
3. `pnpm test` — run existing + any new tests
4. Check EN and DE translations are complete
