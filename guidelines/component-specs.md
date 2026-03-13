---
name: component-specs
description: UI component behavior + visual polish rules. Invoke with a component name (e.g. /component-specs Button) or without args for visual foundations.
user-invocable: true
sources: Refactoring UI (Wathan/Schoger), Practical UI (Dannaway), ui-design-brain (carmahhawwari)
---

# Component Specs

When invoked without a component name, apply the Visual Foundations universally.
When invoked with a component name (e.g. `/component-specs Toast`), return that component's full spec and apply it.

---

## Visual Foundations

These rules apply to every component, always.

### Hierarchy
- De-emphasize the secondary element rather than over-emphasizing the primary one
- Use **size + weight + color together** to create hierarchy — never rely on just one dimension
- One primary action per section. One hero element per page.
- If everything is bold, nothing is bold

### Spacing
- Think in a consistent scale: `4 8 12 16 24 32 48 64 96 128` (px)
- When in doubt, add more whitespace. Then check if you can remove any.
- More padding inside an element → feels more premium. Less → feels dense/cheap.
- Between unrelated groups: use 2–3× more space than between related items

### Typography
- Limit to **2–3 font sizes** per screen. Use weight to create sub-levels within a size.
- Body text: 16px minimum. Never go below 14px for readable content.
- For de-emphasis: use lighter weight + slightly smaller size, **not a different color**
- Left-align body and labels. Center only short, isolated headings.
- Line height: 1.5 for body, 1.2–1.3 for headings

### Color
- **On white backgrounds**: grey text is fine for secondary content
- **On colored backgrounds**: never use grey text — use white at reduced opacity (e.g. `rgba(255,255,255,0.75)`) or a tinted white
- Reserve strong color for interactive elements (buttons, links, focus rings)
- Use no more than 3 tints per color: base, light (10% opacity), dark (shade)
- Danger = red. Success = green. Warning = amber. Info = blue. Stick to these.

### Shadows
- Smaller blur + visible offset = natural, grounded shadow
- Large diffuse blur = floating, detached look (use only for modals/overlays)
- Shadow scale: `xs` (1–2px blur), `sm` (4px), `md` (8px), `lg` (16px), `xl` (24px+)
- Don't add borders AND shadows to the same element — pick one

### Borders
- Borders add visual noise. Use spacing + background color change instead where possible.
- When you need separation: try `1px` border at `10–15% opacity` before trying full color
- Inside a form: borders on inputs are expected. Outside forms: often not needed.

### Empty States
- Design empty states intentionally — they're the first thing new users see
- Include: illustration or icon + brief explanation + a primary action ("Add your first…")
- Never leave a blank, white rectangle with no content

---

## Actions Group

### Button

**Visual rules**
- Size via padding, not fixed height: `px-4 py-2` (default), `px-3 py-1.5` (sm), `px-5 py-3` (lg)
- `primary` → solid fill, high contrast. Only one per section.
- `secondary` → outlined or low-opacity fill. Same color family as primary.
- `ghost` → no border, no fill. Text color only. Use for low-emphasis tertiary actions.
- `danger` → red fill or red border. Must feel "heavy enough" to signal consequence.
- Icon buttons: always square, always have `aria-label`. Icon centered, no text.
- Disabled: `opacity-50`, `cursor-not-allowed`. Don't hide disabled buttons — fade them.
- Loading state: replace label with spinner + keep button width stable (use `min-w`)

**Behavior & states**
- States: default → hover → active (pressed) → focus → disabled → loading
- Focus ring: `outline-2 outline-offset-2` in the button's brand color
- Loading: disable interaction, show spinner left of label or replace label entirely
- Never open a new tab from a `<button>` — use `<a>` with `target="_blank"` for that
- Keyboard: `Enter` and `Space` trigger click

**Accessibility**
- `<button type="button">` for actions, `<button type="submit">` for forms
- Destructive actions: confirm dialog before executing
- Color alone is not enough — use icon + label for danger actions

---

### IconButton

**Visual rules**
- Always square: same padding all sides
- Size should match surrounding text/icon scale
- Use `aria-label` — always. Screen readers get nothing otherwise.
- Optional `badge` prop: small red dot, top-right corner, max `99+`

**Behavior & states**
- Same states as Button
- Tooltip on hover showing the label text

---

### Link

**Visual rules**
- Underline on hover minimum. Underline always for inline body-text links.
- Color: brand primary. Don't use grey for links — they disappear.
- Visited state: slightly muted (optional, but helpful for navigation)
- External links: show `↗` icon or `target="_blank"` + `rel="noopener noreferrer"`

---

## Selection Group

### Checkbox

**Visual rules**
- Label always to the right of the checkbox
- Indeterminate state: dash icon, not a partial check
- Group: vertical stack with consistent gap (`gap-2`)

**Behavior & states**
- States: unchecked → checked → indeterminate → disabled
- Click on label should toggle the checkbox
- `aria-checked="mixed"` for indeterminate

---

### RadioGroup

**Visual rules**
- `direction="vertical"` default. `"horizontal"` only for 2–3 short options.
- Visually group with a label above the group, not beside each radio

**Behavior**
- Arrow keys navigate within group
- `role="radiogroup"` + `aria-labelledby` pointing to the group label

---

### Select

**Visual rules**
- Looks like an input — same height, same border, same padding
- Chevron icon right-aligned, always visible
- Placeholder: "Select an option" (neutral, not a real option)
- Width: match the expected content width, not full-width by default

**Behavior**
- Keyboard: `Space`/`Enter` opens, arrow keys navigate, `Escape` closes
- For > 10 options: strongly consider adding search/filter inside the dropdown

---

## Feedback Group

### Toast

**Visual rules**
- Max width: `360px`. Wider feels like a modal.
- Icon left of text to reinforce the variant (✓ success, ✕ error, ⚠ warning, ℹ info)
- Action button (if any): text only, right-aligned, same color as icon
- Stack multiple toasts — don't stack more than 3 at once (dismiss oldest)
- Position: top-right (desktop), bottom-center (mobile)

**Behavior & states**
- Default duration: `4000ms`. Errors: `6000ms`. Persistent: `duration={0}`
- Pause auto-dismiss on hover
- Swipe to dismiss on mobile
- `role="status"` for non-critical, `role="alert"` + `aria-live="assertive"` for errors

---

### Modal

**Visual rules**
- Max width: `560px` (default), `720px` (wide), `400px` (confirm dialogs)
- Padding: `24px` minimum inside
- Header: title + optional close `×` button top-right
- Footer: actions right-aligned. Primary action rightmost.
- Backdrop: `black/50` opacity. Click backdrop to close (unless critical confirmation).
- Mobile: full-screen sheet from bottom

**Behavior**
- Focus trap: Tab cycles only within modal
- `Escape` closes (unless `persistent`)
- Scroll: modal body scrolls, header and footer stay fixed
- Prevent body scroll when open
- `role="dialog"` + `aria-modal="true"` + `aria-labelledby` pointing to title

---

### InlineAlert

**Visual rules**
- Subtle background tint (10% opacity of the variant color) + left border (3px solid)
- Icon left, text beside it. Never full-color background (too loud in-context).
- Dismissible alerts: `×` top-right corner

**Behavior**
- `role="alert"` for errors/warnings. `role="status"` for info/success.
- Place immediately below the relevant field or section — not at the top of the page

---

### Progress

**Visual rules**
- Height: `6–8px` for default, `12px` for prominent
- Track: grey at `10–15%` opacity. Fill: brand primary.
- Label: show percentage or "X of Y steps" above or beside
- Indeterminate: animated gradient or shimmer

---

### Spinner

**Visual rules**
- Sizes: `sm` (16px), `md` (24px), `lg` (40px)
- Centered in the area it represents (button, card, full page)
- Color: brand primary for standalone, `currentColor` when inside buttons

**Accessibility**
- `role="status"` + `aria-label="Loading"`
- Don't show for < 300ms (flash is worse than no spinner)

---

### Skeleton

**Visual rules**
- Match the shape + approximate size of real content exactly
- Use `rounded` on text lines, `rounded-lg` on card placeholders
- Shimmer animation: left-to-right gradient sweep, `1.5s` duration
- Show 2–3 skeleton rows/cards (not a full-page skeleton)

---

## Display Group

### Card

**Visual rules**
- Padding: `16px` (compact), `24px` (default), `32px` (spacious)
- `elevated` variant: `shadow-md` + white background
- `outlined` variant: `border` + no shadow
- Hoverable cards: `hover:shadow-lg` + `hover:-translate-y-0.5` (subtle lift)
- Badge on card: top-right corner, absolute positioned

**Behavior**
- If the entire card is clickable: `role="link"` or wrap in `<a>`, not nested buttons inside
- Keyboard: `Enter` activates clickable cards

---

### Badge

**Visual rules**
- Sizes: `sm` (text-xs, px-1.5 py-0.5), `md` (text-sm, px-2 py-1)
- Pill shape (`rounded-full`) for status. Square-ish (`rounded`) for counts.
- Background: `10–15%` opacity of the variant color. Text: full variant color.
- Max content: `99+` for counts, 1–2 words for status

---

### Avatar

**Visual rules**
- Sizes: `xs` (24px), `sm` (32px), `md` (40px), `lg` (48px), `xl` (64px)
- Fallback order: image → initials (1–2 chars) → generic person icon
- Initials background: deterministic color from name hash (consistent per person)
- Group/stack: overlap by 25%, show `+N` for overflow

---

### Tooltip

**Visual rules**
- Max width: `240px`. Wrap text — don't expand beyond this.
- Background: near-black (`gray-900`), white text, `rounded-md`, `shadow-lg`
- Arrow: 6px triangle pointing at the trigger element
- Show delay: `300ms`. Hide delay: `0ms` (immediate).

**Behavior**
- `role="tooltip"` + `id` referenced by trigger's `aria-describedby`
- Never put interactive content (links, buttons) inside a tooltip
- Hide on `Escape` and on trigger blur

---

## Navigation Group

### Tabs

**Visual rules**
- Active indicator: `2–3px` border-bottom in brand primary (underline style) OR solid background pill (pill style). Pick one, use consistently.
- Inactive tabs: grey, no underline
- Don't use more than 5 tabs — use Sidebar for complex navigation
- Tabs full-width on mobile (each tab equal width)

**Behavior**
- `role="tablist"`, each tab: `role="tab"` + `aria-selected`, panel: `role="tabpanel"`
- Arrow keys navigate between tabs
- Active tab panel shown, others hidden (`hidden` or `display: none`)

---

### Breadcrumbs

**Visual rules**
- Separator: `/` or `›` (chevron). Same size as text. Muted color.
- Current page: no link, slightly darker/bolder
- Truncate long paths: show first + last, ellipsis in middle

**Behavior**
- `nav` + `aria-label="Breadcrumb"` wrapper
- `aria-current="page"` on the last item

---

### Sidebar

**Visual rules**
- Width: `240px` (default), `280px` (spacious), `64px` (icon-only collapsed)
- Active item: solid background pill (brand color at `10%`) + brand-colored text + icon
- Inactive: grey text + grey icon
- Section groups: small label above group in uppercase, `font-size: 11px`, `letter-spacing: wider`
- Hover: very subtle background (`gray-100`)

**Behavior**
- `role="navigation"` + `aria-label="Main navigation"`
- `aria-current="page"` on active item
- Collapsible sections: `aria-expanded` on the toggle button

---

### Pagination

**Visual rules**
- Active page: solid fill (brand primary). Adjacent pages: outlined or ghost.
- Show max 7 page buttons — use ellipsis beyond that
- `«` `‹` `›` `»` for first/prev/next/last
- Don't show pagination for < 2 pages

**Behavior**
- `role="navigation"` + `aria-label="Pagination"`
- Current page: `aria-current="page"`
- Disabled prev/next: `aria-disabled="true"`

---

## Layout Group

### Stack

**Visual rules**
- Use for single-direction layouts with consistent gap
- Prefer `Stack` over manual `flex` + `gap` to enforce the spacing scale
- `align="start"` for most content. `align="center"` for icon + label pairs.

---

### Grid

**Visual rules**
- Always define responsive breakpoints: `{ sm: 1, md: 2, lg: 3 }`
- Default to `gap-4` or `gap-6`. Never `gap-1` or `gap-2` for card grids — too tight.
- Prefer grid for equal-size card layouts. Use Stack + wrapping for tag lists.

---

### Divider

**Visual rules**
- Color: `border-gray-200` (light) or `border-gray-100` (very subtle)
- Never use dividers between every item — group related items and divide between groups
- Vertical dividers: use for toolbar separators, not for main layout sections

---

### Spacer / Container

**Visual rules**
- Container max-widths: `sm` (640px), `md` (768px), `lg` (1024px), `xl` (1280px), `full`
- Horizontal padding inside container: `16px` (mobile), `24px` (tablet), `32px` (desktop)
- Spacer: only for adding space between specific elements that gap/padding can't handle cleanly

---

## Quick Principles Checklist

Before calling a component "done", verify:

- [ ] All interactive states implemented: default, hover, active, focus, disabled
- [ ] Focus ring visible and in brand color
- [ ] Loading/empty state handled
- [ ] Mobile behavior specified (full-screen modal? stacked tabs? collapsed nav?)
- [ ] Color alone is not the only signal (add icon or label for status)
- [ ] Text has sufficient contrast (4.5:1 for normal text, 3:1 for large text)
- [ ] Spacing uses the scale (not arbitrary pixel values)
- [ ] One primary action per section — not two "primary" buttons
