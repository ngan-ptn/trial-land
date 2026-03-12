# Agent Instructions (docliQ-land)

## Naming Conventions (Required)

For any new artifact or document file, follow `guidelines/naming-conventions.md`.

Pattern: `[CODE][YYMMDD]-[slug](-[increment]).ext`

### Applies to

- All files in `artifacts/`
- Files in `product-context/` that match an artifact code (COMP, DATA, FEAT, FLOW, IA, INTV, JMAP, JTBD, PERS, PRD, RSYN, SCOP, TASK, TEST)
- Any new design, research, or planning document

### Does NOT apply to

- Source code files (`.ts`, `.tsx`, `.css`, etc.) — follow framework conventions
- Config files (`package.json`, `tsconfig.json`, etc.)
- System files: `README.md`, `CLAUDE.md`, `AGENTS.md`, `CHANGELOG.md`
- Reference files in `knowledge/`, `guidelines/`, `skill-command/`, `templates/`
- Fixture data files in `fixtures/`
- Skill files in `.claude/skills/` (must keep exact names for slash command resolution)

### Rule of thumb

Ask: does this file map to an artifact code above? Yes → use the convention. No → use a clear, descriptive kebab-case name.

---

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
4. After saving: log the decision and reasoning in `knowledge/knowledge-log.md`

If no matching template exists: create the artifact directly in `artifacts/`, still named by convention.

### Folder Routing (apply automatically)

| Creating... | Save to... |
|-------------|-----------|
| Design artifact (OOUX, IA, flow, PRD, scope, etc.) | `artifacts/` |
| Product roadmap or use-case doc | `product-context/` |
| New shared term, state machine, or pattern | `common-language/` |
| New design standard or visual rule | `guidelines/` |
| Never save design outputs inside `versions/` | — |

### Knowledge Capture (apply automatically)

- After creating an artifact or making a key decision: log it in `knowledge/knowledge-log.md`
- Log: what was decided, why, and what alternatives were considered
- Tag: `[Experiment]` (untested) → `[Reusable]` (worked once) → `[Adopted]` (validated 2+ times)
- At end of a completed version iteration: run `bun run knowledge:after` from repo root

### Repeatable Workflows

These run automatically — no need to ask:
- **New artifact**: template → fill → `artifacts/[CODE][YYMMDD]-slug.md` → log in `knowledge/knowledge-log.md`
- **New design standard**: add to `guidelines/` → update `REPO-BENEFITS.md` if folder purpose changes
- **End of session**: if anything was decided or learned → log in `knowledge/knowledge-log.md`

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
