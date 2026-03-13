# Claude Instructions for docliQ-land

## Repository Overview

This is a versioned collection of docliQ applications with shared resources.

```
trial-land/
├── artifacts/        # Design artifacts (named by convention)
├── common-language/  # Shared terminology & implementation patterns
├── fixtures/         # Shared fixture data (JSON)
├── non-analyzed/     # Artifacts pending review/analysis
├── guidelines/       # Visual & compliance guidelines
├── knowledge/        # Iterative knowledge system
├── product-context/  # Product roadmaps, use cases, screenshots
├── research/         # Raw research notes and findings
├── scripts/          # Knowledge automation scripts
├── skill-command/    # AI workflow prompts and slash command templates
├── templates/        # Document templates (ADR, retrospective, etc.)
├── versions/         # Independent app versions (v1, v2, ...)
└── .claude/skills/   # Claude-specific skills
```

## Available Skills (Claude Slash Commands)

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
These are Claude slash commands, not repo shell commands.

## Knowledge Commands From The Repo Root

Use the repo scripts when working from the terminal:

| Command | Purpose |
|---------|---------|
| `bun run knowledge:during` | During development - capture a learning immediately |
| `bun run knowledge:weekly` | Weekly - sync progress, review experiments |
| `bun run knowledge:after` | After iteration - comprehensive review |

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

**All new artifact files MUST follow `/guidelines/naming-conventions.md`.**

Pattern: `[CODE][YYMMDD]-[slug](-[increment]).ext`

Example: `COMP260206-market-leaders.md`, `JTBD260206-onboarding-flow.md`

### What the convention applies to

| Applies | Does NOT apply |
|---------|---------------|
| Files in `artifacts/` | Source code (`.ts`, `.tsx`, `.css`, etc.) |
| Files in `product-context/` that match an artifact code | Config files (`package.json`, `tsconfig.json`, etc.) |
| Any new design/research/planning document | System files (`README.md`, `CLAUDE.md`, `AGENTS.md`, `CHANGELOG.md`) |
| | `knowledge/`, `guidelines/`, `skill-command/`, `templates/` files (system reference files) |
| | `fixtures/` JSON data files |
| | `.claude/skills/` files (referenced by exact name) |

### Artifact codes quick reference

`COMP` `DATA` `FEAT` `FLOW` `IA` `INTV` `JMAP` `JTBD` `PERS` `PRD` `RSYN` `SCOP` `TASK` `TEST`

CR-tied only (include `CR##-##` in name): `FLOW` `WIRE`

## House Rules

### Before Starting
- Confirm which version (`versions/vX`) is in scope if the task touches code
- For new features or artifacts: read `product-context/` first to align on intent
- For design decisions: check `knowledge/decision-log.md` first — may already be answered
- For component choices: consult `guidelines/ui-decision-trees.md` (which to use) and `guidelines/component-specs.md` (how to implement + polish it)

### Key References (consult before acting)

| Question | Where to look |
|----------|--------------|
| Which component should I use? | `guidelines/ui-decision-trees.md` (fast picker) |
| How should this component behave and look? | `guidelines/component-specs.md` (behavior + visual polish) |
| What has been decided before? | `knowledge/decision-log.md` |
| What are the current design standards? | `guidelines/visual-guideline-v2.md`, `guidelines/copy-guideline.md` |
| What is in scope for this product? | `product-context/` |
| What folder does this belong in? | `REPO-BENEFITS.md` |

### Creating Artifacts (Documentation)

Default sequence for any new design output:
1. Pick the right template from `templates/` if one exists
2. Fill it in
3. Save to `artifacts/` using the naming convention: `[CODE][YYMMDD]-[slug].md`
4. After saving: run `bun run knowledge:during` to log what was decided and why

If no matching template exists: create the artifact directly in `artifacts/`, still named by convention.

### Folder Routing (apply automatically)

| Creating... | Save to... |
|-------------|-----------|
| Design artifact (OOUX, IA, flow, PRD, scope, etc.) | `artifacts/` |
| Imported/raw artifact not yet reviewed | `non-analyzed/` |
| Product roadmap or use-case doc | `product-context/` |
| New shared term, state machine, or pattern | `common-language/` |
| New design standard or visual rule | `guidelines/` |
| Never save design outputs inside `versions/` | — |

### Knowledge Capture (apply automatically)

- After creating an artifact or making a key decision: run `bun run knowledge:during`
- Log: what was decided, why, and what alternatives were considered
- Tag: `[Experiment]` (untested) → `[Reusable]` (worked once) → `[Adopted]` (validated 2+ times)

### Repeatable Workflows

These run automatically — no need to ask:
- **New artifact**: template → fill → `artifacts/[CODE][YYMMDD]-slug.md` → `bun run knowledge:during`
- **New design standard**: add to `guidelines/` → update `REPO-BENEFITS.md` if folder purpose changes
- **End of session**: if anything was decided or learned → `bun run knowledge:during` before closing

### UI Verification

When checking frontend output (runs at `http://localhost:3001`):
Use `agent-browser`: `open <url>` → `snapshot -i -c` (get @refs) → interact via `@ref` → `screenshot /Users/nganpham/Documents/trial-land/agent-browser/<name>.png` to confirm.
Use the repo-level `agent-browser/` folder for screenshots instead of `/tmp`.

### Core Principles

- **Automatic**: Apply naming, folder routing, and knowledge capture without being prompted
- **Reference-first**: Check `ui-decision-trees.md`, `component-specs.md`, and `knowledge/` before inventing a new pattern
- **Template-first**: Use existing templates before creating new structure
- **Consistent**: Follow `guidelines/` and `common-language/` — don't diverge without logging the reason
- **Minimal footprint**: Only create or modify what's needed for the task
