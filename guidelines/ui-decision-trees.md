# Component Decision Trees

Use these trees to select the right component for each use case.

---

## Actions Group

**Choosing between Button, IconButton, Link**

- If action navigates to a different page/URL → use **Link**
  • `variant="default"` for inline text links
  • `variant="nav"` for navigation menu items
  • Set `external={true}` for links opening new tabs
- If action is in a menu/dropdown context → use **MenuItem** (future component)
  
- If action is in a constrained space (toolbar, table row, icon-only context) → use **IconButton**
  • Always provide `aria-label` for accessibility
  • Consider `badge` prop for notification count
- If action is the primary CTA on the page/section → use **Button (variant="primary")**
- If action is a supporting/secondary action → use **Button (variant="secondary")**
- If action is a low-emphasis/tertiary action → use **Button (variant="ghost")**
- If action is a destructive action (delete, remove, clear) → use **Button (variant="danger")**
  • Consider adding confirmation dialog for destructive actions

---

## Selection Group

**Choosing between Checkbox, Radio, RadioGroup, Select, Combobox**

- If toggling a single ON/OFF setting → use **Checkbox**
  • Consider using `indeterminate={true}` for "select all" pattern
  • Use with label text: "Enable notifications"
- If selecting MULTIPLE options from ≤ 6 items → use **Checkbox Group**
  • Stack checkboxes vertically for clarity
- If selecting exactly ONE option from ≤ 4 visible choices → use **RadioGroup**
  • `direction="vertical"` for forms, `"horizontal"` for compact layouts
  • Use meaningful labels for each radio option
- If selecting exactly ONE option from 5-10 items → use **Select**
  • Include empty placeholder: "Select an option"
  • Consider searchable options with many items
- If selecting exactly ONE option from > 10 items or needs search → use **Combobox** (future component)
  • For now, use Select with filtered options

---

## Feedback Group

**Choosing between Toast, Modal, InlineAlert, Progress, Spinner, Skeleton**

- If feedback is non-blocking and auto-dismisses → use **Toast**
  • `duration={5000}` for 5 second display
  • `duration={0}` for persistent toasts
  • Use `action` prop for undo/retry
  • Position consistently (top-right, top-center, bottom-right)
- If feedback requires user acknowledgment/decision → use **Modal**
  • Blocks interaction until dismissed
  • Use for critical confirmations, destructive actions
  • Provide clear title, message, and action buttons
  • Consider `closeOnEscape={true}` for better UX
- If feedback is contextual to specific content → use **InlineAlert**
  • Place near related content
  • Use dismissible alerts (non-blocking)
  • Does NOT block interaction
  • Use `variant` to indicate severity (success, warning, error, info)
- If showing progress of a known-duration task → use **Progress**
  • `value={0-100}` - percentage complete
  • `showLabel={true}` - "X% complete"
  • Use indeterminate state for unknown duration
- If showing progress of an unknown-duration task → use **Spinner**
  • `size="sm"` for inline, `"md"` for sections, `"lg"` for pages
- • Use consistent placement (centered or top-right)
- If content is loading and you want to preserve layout → use **Skeleton**
  • Matches the structure of loaded content
  • Use for cards, lists, inputs
  • Show 2-3 skeleton pulses before content loads
  • Consider adding shimmer effect for polished feel

---

## Display Group

**Choosing between Card, Badge, Avatar, Tooltip, DataTable**

- If displaying a grouped piece of content with optional action → use **Card**
  • Use `variant="elevated"` for emphasis
  • Use `badge` prop for status indicators (NEW, LIVE, etc.)
  • Use `hoverable={true}` for clickable cards
  • If displaying a single entity with image → use **Avatar**
  • Provide `name` or `initials` for fallback
  • Use `size` prop (xs, sm, md, lg, xl)
  • Consider `onClick` for profile navigation
- If showing small status indicator or count → use **Badge**
  • Use `variant` to indicate status (success, info, warning, error)
  • Can be displayed standalone or on cards/avatars
  • Position consistently (top-right or top-left)
- If showing supplementary information on hover → use **Tooltip**
  • Wrap the element you want to explain
  • Use `position` prop: `"top"`, `"right"`, `"bottom"`, `"left"`
  • Consider delay (show after X ms of hover)
  • Provide helpful, concise descriptions
- If displaying structured tabular data with sorting/filtering → use **DataTable** (future component)
  • Define columns with `accessor` functions
  • Support `selectable` rows
  • Consider `sortable` columns
  • Include pagination component for large datasets

---

## Navigation Group

**Choosing between Tabs, Breadcrumbs, Sidebar, Pagination**

- If switching between views in the same context (no URL change) → use **Tabs**
  • Keep tab count low (2-5 for clarity)
  • Use clear, short labels
  • Position based on content (top or bottom)
  • If many views or complex navigation → use **Sidebar**
  • Provide nested navigation with **NavGroup** for grouped items
  • Use `defaultOpen={true}` for expanded sections by default
  • Consider `collapsible` sections for large nav
- If showing user's location in deep navigation → use **Breadcrumbs**
  • Last item is current page (no link)
  • Include ellipsis for long paths: "/Products / Categories / Subcategory"
  • Use chevron separators between items
- If navigating through paginated data → use **Pagination**
  • `currentPage={state}` - current page number
  • `totalPages={count}` - total pages
  • Show page range for context: "Page 5 of 12"
  • Consider `showFirstLast={false}` for minimal UI
  • Use `boundaryCount={2}` to show 2 pages around current

---

## Layout Group

**Choosing between Stack, Grid, Container, Divider, Spacer**

- If arranging items in a single direction with consistent spacing → use **Stack**
  • `direction="vertical"` for vertical stacking
  • `direction="horizontal"` for horizontal layouts
  • Use `gap` prop: `"xs"`, `"sm"`, `"md"`, `"lg"`, `"xl"`, `"2xl"`
  • Use `align` prop: `"start"`, `"center"`, `"end"`, `"stretch"`
  • Align items consistently for visual rhythm
- If arranging items in a 2D grid with responsive columns → use **Grid**
  • `columns={{ sm: 1, md: 2, lg: 3 }}` for responsive breakpoints
  • `columns={{ default: 1 }}` for single column default
  • Use `gap` prop: `"md"`, `"lg"`, `"xl"`
  • Consider `rows="auto"` for auto height based on content
- If centering content with max-width → use **Container**
  • Use `maxWidth` prop: `"sm"`, `"md"`, `"lg"`, `"full"`
  • Apply consistent padding
- If adding visual separation between sections → use **Divider**
  • `orientation="horizontal"` (default) or `"vertical"` for sections
  • `thickness="1"` (1px separator)
  • Consider adding label or icon to divider
- If creating flexible space between items → use **Spacer**
  • `size="sm"` (8px), `"md"` (16px), `"lg"` (32px)
  • Use `flex={true}` to expand to fill space
  • Consider `size="xl"` (48px) for page-level spacing
  • Never use `Spacer` for simple margin/padding adjustments

---

## Quick Reference

| If you need... | Use |
|----------------|------|------|
| Navigate to new page | Link (external={true}) |
| Trigger an action (primary) | Button variant="primary" |
| Trigger an action (secondary) | Button variant="secondary" |
| Trigger low-emphasis action | Button variant="ghost" |
| Trigger destructive action | Button variant="danger" |
| Toggle a setting | Checkbox |
| Select from many options | Select |
| Show status (non-blocking) | Toast |
| Show blocking feedback | Modal |
| Show inline feedback | InlineAlert variant |
| Show progress | Progress |
| Show loading state | Spinner |
| Preserve layout while loading | Skeleton |
| Grouped content with action | Card (hoverable) |
| Status indicator | Badge |
| User profile image | Avatar |
| Explain element on hover | Tooltip |
| Switch views in same context | Tabs |
| Nested navigation | Sidebar with NavGroup |
| Deep nav with context | Breadcrumbs |
| Paginate data | Pagination |
| Stack items vertically/horizontally | Stack (direction + align) |
| Grid layout | Grid (columns) |
| Center content | Container (maxWidth) |
| Separate sections | Divider |
| Add space | Spacer |
| Single direction layout | Stack |

---

**Decision Tree Version:** 1.0
**Created:** 2026-01-11
**Based on:** Component Specifications (Step 4)
**Design System:** Clean Systematic Confidence
**Reference:** docs/design-tokens.json, docs/design-guideline.md
