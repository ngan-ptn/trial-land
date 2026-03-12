## Tini Health Dashboard Design

### Goal
Create a Tini-token-swapped version of the shadcnstudio-style health dashboard base file.

### Approach
Duplicate the base dashboard and replace its local visual token definitions with values sourced from the Tini token library. The swap should cover color semantics, radius behavior, and shadow/elevation so the result is a true token-pack variant rather than a color-only skin.

### Token Model
- Load external primitive values from `DATA260312-tini-preview-primitives.css`
- Map page-local semantic tokens from the Tini values
- Align page radii to the Tini `--radius` model and computed steps
- Align shadow tokens to Tini elevation levels

### Constraints
- Keep the file standalone in `artifacts/`
- Preserve the existing layout and interactions from the base dashboard
- Make the visual change driven by tokens rather than layout edits
