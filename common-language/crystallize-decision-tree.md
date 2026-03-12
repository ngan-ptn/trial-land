# Crystallize — Decision Tree Template

> Bridge between **Layer 3 (UI Intent)** and **Design System rules & patterns**.
> This is a separate artifact — can link to Design System but **should not be merged** into it.

---

## Source

- **Layer 3 from:** [Feature / Flow name]
- **Date:** [YYMMDD]
- **Screens analyzed:** [list screens]

---

## Decision Logic

```text
For each UI Intent in Layer 3:
  ├─ Does this intent appear in 2+ screens/flows?
  │   ├─ YES → Does it solve the same user/system tension each time?
  │   │   ├─ YES → EXTRACT as Design System Pattern
  │   │   └─ NO  → Document as VARIANT (same surface, different rule)
  │   └─ NO  → Is it likely to recur in future flows?
  │       ├─ LIKELY    → Mark as CANDIDATE (extract later when confirmed)
  │       └─ UNLIKELY  → Keep as SCREEN-LOCAL rule (no pattern needed)
```

---

## Intent → Pattern Mapping

| # | UI Intent (from Layer 3) | In 2+ flows? | Shared tension | Decision | Output |
|---|--------------------------|:------------:|----------------|----------|--------|
| 1 | | Yes / No | | Extract / Variant / Candidate / Screen-local | |
| 2 | | | | | |
| 3 | | | | | |

---

## Extracted Patterns

> For each "Extract" row above, produce a full Design System pattern using the template in `common-language.md` (Design System — Interaction Pattern section).

### Pattern: [Name]

- **Problem this solves:** [user/system tension]
- **When to use:** [situations]
- **When NOT to use:** [exclusions]
- **Core UX rules:** [non-negotiable rules]
- **Origin:** Derived from [flow/screen names], [date]

*(Repeat for each extracted pattern)*

---

## Variants

> Same visual surface, different underlying rule. Document the differences.

| UI Intent | Flow A behavior | Flow B behavior | Why they differ |
|-----------|----------------|-----------------|-----------------|
| | | | |

---

## Candidates (Watch List)

> Not yet a pattern — revisit when a second use appears.

| UI Intent | Why it might recur | Revisit when |
|-----------|--------------------|--------------|
| | | |

---

## Screen-Local Rules

> Too specific for a pattern. Keep in the feature doc.

| Screen | Rule | Why not a pattern |
|--------|------|-------------------|
| | | |
