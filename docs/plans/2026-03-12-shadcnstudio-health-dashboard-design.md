## Shadcnstudio Health Dashboard Design

### Goal
Create a standalone HTML artifact that mimics the provided healthcare dashboard screenshot using a shadcnstudio-style composition approach instead of a custom freeform layout.

### Approach
Use a dashboard-shell composition: sidebar rail, compact top header, center widget stack, and right utility rail. Internal sections should read like assembled shadcnstudio blocks such as application shell, dashboard sidebar, dashboard header, statistics cards, widgets, and assistant/chat panels.

### Layout
- Left sidebar with brand, grouped nav items, and promo card
- Top header with greeting, search, and compact action icons
- Center column with diagnosis hero card, health overview stats, and prescriptions list
- Right column with appointment schedule card and AI care feed card

### Visual Direction
- Neutral shadcn-style surfaces with rounded cards and light shadows
- Screenshot-inspired healthcare palette with cool indigo accents
- Consistent semantic tokens so the file can be swapped to another primitive token pack later

### Interaction
- Active nav state
- Day pill selection in appointments
- Health metric tab selection
- Focus and hover states on inputs, cards, pills, and actions
- Lightweight AI composer interaction

### Constraints
- Keep the result as one standalone HTML artifact in `artifacts/`
- Do not rely on runtime imports from `shadcnstudio.com`
- Preserve enough block structure that the page still reads as a shadcnstudio-style dashboard composition
