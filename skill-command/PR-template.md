## Summary
[What changed and why. 1-2 sentences. Include context if fixing a bug or addressing user feedback.]

## Changes
- [File/component 1: what changed]
- [File/component 2: what changed]
- [Key behavior change or decision]

## Review Focus
- [ ] [Specific thing reviewers should validate]
- [ ] [Edge case or potential issue]
- [ ] [If UI: keyboard nav and accessibility tested?]

## Artifacts
**Code:** [Link to main file(s) changed](https://github.com/tini-works/coredesign/blob/BRANCH-NAME/calo-tracker/src/path/to/FileName.tsx)

**Related docs:** *(Only include if applicable)*
- [CR Spec](https://github.com/tini-works/coredesign/blob/BRANCH-NAME/calo-tracker/docs/change-requests/##-category/CR##-##-slug/CR##-##-slug.md) *(if CR-driven)*
- [Design artifacts](https://github.com/tini-works/coredesign/blob/BRANCH-NAME/calo-tracker/docs/change-requests/##-category/CR##-##-slug/WIREYYMMDD-CR##-##-slug.md) *(if created)*

## Testing
- [What was tested and result]
- [Any untested areas]
- [If UI: keyboard nav, screen reader, mobile tested]

---

## AI Agent Instructions

**Use this template for ANY PR.** Guidelines:

1. **Always include:** Summary, Changes, Review Focus, Artifacts (code links), Testing
2. **Summary:** Include rationale. If fixing CR##-##, reference it here. If hotfix, explain context.
3. **Review Focus:** 2-3 specific checklist items. Examples:
   - "Verify button is keyboard-focusable (Tab key)"
   - "Check ActionSheet dismisses on Escape"
   - "Ensure no console errors on load"
4. **Artifacts:** REQUIRED - Always include direct GitHub links to changed files
5. **Testing:** Be specific. Examples:
   - ✅ "Manual test: clicked button 5x, works every time"
   - ❌ "Tested" (too vague)
6. **Delete:** "Related docs" section if no CR or design artifacts
7. **Keep it lean:** Target <2 min read time

**Before creating PR:**
- [ ] Title is descriptive (`fix:` / `feat:` / `docs:`)
- [ ] Branch name follows pattern (`fix/slug` or `feat/slug`)
- [ ] All code links point to correct files
- [ ] Review Focus items are testable/specific
- [ ] Testing section documents what was actually tested
