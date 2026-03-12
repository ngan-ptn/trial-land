## Health Dashboard HTML Comparison

### Files Compared

- [`artifacts/DATA260312-shadcnstudio-health-dashboard.html`](/Users/nganpham/Documents/trial-land/artifacts/DATA260312-shadcnstudio-health-dashboard.html)
- [`artifacts/DATA260312-shadcn-health-base.html`](/Users/nganpham/Documents/trial-land/artifacts/DATA260312-shadcn-health-base.html)
- [`artifacts/DATA260312-tini-health-dashboard.html`](/Users/nganpham/Documents/trial-land/artifacts/DATA260312-tini-health-dashboard.html)
- [`artifacts/DATA260312-corepvs-health-dashboard.html`](/Users/nganpham/Documents/trial-land/artifacts/DATA260312-corepvs-health-dashboard.html)

### Overview

| File | Role | Token Source | Visual Character | Best Use |
|---|---|---|---|---|
| [`artifacts/DATA260312-shadcnstudio-health-dashboard.html`](/Users/nganpham/Documents/trial-land/artifacts/DATA260312-shadcnstudio-health-dashboard.html) | Original shadcnstudio-style composition | Local in-file semantic tokens | Screenshot-inspired, soft healthcare, more branded | Initial reference build |
| [`artifacts/DATA260312-shadcn-health-base.html`](/Users/nganpham/Documents/trial-land/artifacts/DATA260312-shadcn-health-base.html) | Clean pre-swap baseline | Same local in-file semantic tokens | Same as the shadcnstudio version | Before-state for token swap tests |
| [`artifacts/DATA260312-tini-health-dashboard.html`](/Users/nganpham/Documents/trial-land/artifacts/DATA260312-tini-health-dashboard.html) | Tini token variant | [`artifacts/DATA260312-tini-preview-primitives.css`](/Users/nganpham/Documents/trial-land/artifacts/DATA260312-tini-preview-primitives.css) | Crisp clinical, cooler, more systematic | Testing Tini semantic/radius/shadow model |
| [`artifacts/DATA260312-corepvs-health-dashboard.html`](/Users/nganpham/Documents/trial-land/artifacts/DATA260312-corepvs-health-dashboard.html) | CorePVS token variant | [`artifacts/DATA260312-corepvs-brand-primitives.css`](/Users/nganpham/Documents/trial-land/artifacts/DATA260312-corepvs-brand-primitives.css) | More enterprise, calmer, more operational | White-label stress test with CorePVS |

### Detailed Comparison

| Aspect | `shadcnstudio-health-dashboard` | `shadcn-health-base` | `tini-health-dashboard` | `corepvs-health-dashboard` |
|---|---|---|---|---|
| Layout structure | Dashboard shell | Dashboard shell | Same as base | Same as base |
| Content | Healthcare dashboard | Same | Same | Same |
| Interactions | Tabs, day pills, diagnosis selection | Same | Same | Same |
| External token file | No | No | Yes | Yes |
| Color swap | No | No | Yes | Yes |
| Radius swap | No | No | Yes | Yes |
| Shadow swap | No | No | Yes | Yes |
| White-label readiness | Medium | High as baseline | High | High |
| Screenshot fidelity | Highest | Highest | Medium | Medium |
| Brand neutrality | Lower | Lower | Higher | Higher |
| Best comparison role | Reference | Control | Token pack A | Token pack B |

### Recommendation

| Recommendation | File |
|---|---|
| Use as the visual reference | [`artifacts/DATA260312-shadcn-health-base.html`](/Users/nganpham/Documents/trial-land/artifacts/DATA260312-shadcn-health-base.html) |
| Use as the controlled before-state | [`artifacts/DATA260312-shadcn-health-base.html`](/Users/nganpham/Documents/trial-land/artifacts/DATA260312-shadcn-health-base.html) |
| Use to test Tini token behavior | [`artifacts/DATA260312-tini-health-dashboard.html`](/Users/nganpham/Documents/trial-land/artifacts/DATA260312-tini-health-dashboard.html) |
| Use to test CorePVS token behavior | [`artifacts/DATA260312-corepvs-health-dashboard.html`](/Users/nganpham/Documents/trial-land/artifacts/DATA260312-corepvs-health-dashboard.html) |

### Note

[`artifacts/DATA260312-shadcnstudio-health-dashboard.html`](/Users/nganpham/Documents/trial-land/artifacts/DATA260312-shadcnstudio-health-dashboard.html) and [`artifacts/DATA260312-shadcn-health-base.html`](/Users/nganpham/Documents/trial-land/artifacts/DATA260312-shadcn-health-base.html) are effectively the same visual version right now. The second exists mainly to provide a clearly named baseline for token swap comparisons.
