# Claude Instructions for docliQ-land

## Repository Overview

This is a versioned collection of docliQ applications with shared resources.

```
docliQ-land/
├── fixtures/         # Shared fixture data
├── guidelines/       # Visual & compliance guidelines
├── knowledge/        # Iterative knowledge system
├── versions/         # Independent app versions (v1, v2, ...)
└── .claude/skills/   # Claude-specific skills
```

## Available Skills (Slash Commands)

| Command | When to Use |
|---------|-------------|
| `/commit` | Commit changes with auto-generated message (max 100 chars) |
| `/resolve-conflict` | Safely resolve git merge/rebase conflicts |
| `/knowledge:during` | During development - capture a learning immediately |
| `/knowledge:weekly` | Weekly - sync progress, review experiments |
| `/knowledge:after` | After iteration - comprehensive review |
| `/ooux-dot-map` | Generate Entity Relationship diagram using OOUX technique |
| `/info-map` | Generate Information Architecture (IA) Map |
| `/user-flows` | Generate User Flow documentation with JTBD |

Skills are defined in `.claude/skills/` folder.

## Knowledge System

The `/knowledge/` folder tracks learnings across versions:

| File | Purpose |
|------|---------|
| `decision-log.md` | Why we chose X over Y |
| `pattern-library.md` | Reusable patterns |
| `knowledge-log.md` | Assumption → reality shifts |
| `lessons-learned.md` | Strategic insights |
| `sum-changed.md` | Progress tracker |

### Tagging

| Tag | Meaning |
|-----|---------|
| `[Experiment]` | New, unvalidated |
| `[Reusable]` | Ready for 2nd validation |
| `[Adopted]` | Validated in 2+ versions |
| `[Deprecated]` | No longer use |
| `[Source: vX]` | Origin version |

## Working with Versions

Each version in `/versions/` is fully independent. When working on a version:

1. Navigate to the version folder
2. Run `bun install` and `bun run dev`
3. Database: `bun run db:push` then `bun run db:seed`

## Shared Resources

- **Fixtures** (`/fixtures/`): Shared test data for all versions
- **Guidelines** (`/guidelines/`): Design and compliance docs
- **Knowledge** (`/knowledge/`): Cross-version learnings

## Naming Conventions

**All new artifact/document files MUST follow `/guidelines/naming-conventions.md`.**

Pattern: `[CODE][YYMMDD]-[slug](-[increment]).ext`

Example: `COMP260206-market-leaders.md`, `JTBD260206-onboarding-flow.md`

Artifacts save to `artifacts/`. See the full reference for codes and rules.

## AI Behavior Rules

When working in this repo:
- Check which version you're working in before making changes
- Follow naming conventions in `/guidelines/naming-conventions.md` for all new files
- Document learnings using `/knowledge:during`
- Don't share code between versions (only fixtures/guidelines/knowledge)
- Read `/knowledge/` before making architectural decisions
- Apply proper tags when documenting patterns
