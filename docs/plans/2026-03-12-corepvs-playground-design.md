## CorePVS Playground Design

### Goal
Create a single standalone HTML playground that demonstrates four reusable UI blocks under the CorePVS brand token pack: datatable, form, statistics, and sidebar navigation.

### Approach
Use one artifact HTML file with top-level tabs. Each tab reveals one focused block instead of stacking all blocks on the page. This keeps the visual review isolated while proving that one token pack can drive multiple component families.

### Structure
- Header with title and short token-pack note
- Tab list for `Datatable`, `Form`, `Statistics`, and `Sidebar`
- One content panel visible at a time
- Shared semantic token mapping inside the file
- Primitive values loaded from the external CorePVS stylesheet

### Block Content
- Datatable: toolbar, search, filters, status badges, rows, pagination
- Form: grouped fields, segmented controls, textarea, checkboxes, actions
- Statistics: KPI cards, trend chips, progress strips, compact breakdown panel
- Sidebar: navigation rail, grouped links, active state, support/account area

### Interaction
- Client-side tab switching
- Hover and focus states on controls
- Lightweight row selection and filter-pill toggles
- No persistence or backend behavior

### Constraints
- Keep the file standalone in `artifacts/`
- Consume CorePVS tokens directly
- Preserve shadcn-style semantic token usage so future token swaps remain simple
