## CorePVS Health Dashboard Design

### Goal
Create a CorePVS-token-swapped version of the shadcnstudio-style health dashboard base file.

### Approach
Duplicate the base dashboard and replace its local token definitions with mappings into the CorePVS primitive token pack. Keep layout, content, and interactions unchanged so the result remains directly comparable with the base and Tini variants.

### Token Model
- Load external primitives from `DATA260312-corepvs-brand-primitives.css`
- Map local semantic tokens to the CorePVS primitives
- Reuse the same page-level radius and shadow treatment already established in the other CorePVS artifacts

### Constraints
- Keep the file standalone in `artifacts/`
- Preserve the base dashboard structure and interactions
- Make the visual change token-driven rather than layout-driven
