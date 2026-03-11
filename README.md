# docliQ-land

A versioned collection of independent web applications built with [Better T Stack](https://github.com/AmanVarshney01/create-better-t-stack) + Tailwind CSS v3.

## Stack

Each version is a fully independent application with:

- **Frontend:** React + TanStack Router
- **Backend:** Hono
- **Database:** SQLite + Drizzle ORM
- **API:** tRPC
- **Styling:** Tailwind CSS v3

## Project Structure

```
docliQ-land/
├── artifacts/        # Generated design artifacts (OOUX maps, IA maps, etc.)
├── common-language/  # Shared terminology & implementation patterns
├── docs/             # Project documentation, plans, changelogs
├── fixtures/         # Shared fixture data (JSON) for all versions
├── guidelines/       # Design system, copy, testing, deployment guides
├── knowledge/        # Iterative knowledge accumulation
├── scripts/          # Knowledge automation scripts
├── workflows/        # Design workflow templates (brainstorming, flows, ethics)
└── versions/
    └── v1/           # Current active version
```

## Running a Version

```bash
# Navigate to the version
cd versions/v1

# Install dependencies
bun install

# Start development servers
bun run dev
```

The app will be available at:
- Frontend: http://localhost:3001
- Backend API: http://localhost:3000

## Database Commands

Run from within a version folder (e.g., `versions/v1`):

```bash
# Apply schema changes
bun run db:push

# Seed the database
bun run db:seed

# Open database UI
bun run db:studio
```

## Knowledge Commands

Run from the repo root:

```bash
# During development - when you learn something
bun run knowledge:during

# Weekly - track progress and review experiments
bun run knowledge:weekly

# After iteration - comprehensive review and extraction
bun run knowledge:after
```

## Shared Resources

- **Fixtures** (`fixtures/`): JSON test data shared across all versions (users, doctors, appointments, etc.)
- **Guidelines** (`guidelines/`): Visual design system, copy guidelines, decision trees, deployment & testing guides
- **Common Language** (`common-language/`): Shared terminology, state machines, and implementation patterns
- **Workflows** (`workflows/`): Design process templates (brainstorming, hypothesis formation, solution tradeoffs, ethics gates)
- **Knowledge** (`knowledge/`): Cross-version learnings, decision log, pattern library, lessons learned

## Versioning Philosophy

Each version is **fully independent** - no shared code between versions. This allows:

- Clean experimentation without breaking existing versions
- Easy comparison between different implementations
- Simple rollback by switching to a previous version folder
- Consistent test data across all versions via shared fixtures
