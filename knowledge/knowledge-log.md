# Workspace Knowledge Log

**Purpose:** Track how collective understanding evolved across versions.

**Scope:** Document assumption → reality shifts that impact workspace-wide practices.

**Order:** Reverse chronological (newest first)

---

<!-- New knowledge entries go here (above this comment) -->

## KL-W002: Bird-Eye Boards Need Explicit Inference Markers [Reusable]

**Date:** 2026-03-13
**Context:** Translating wide role-based bird-eye images into markdown flow artifacts
**Source Version:** N/A

**Initial Assumption:**
The exported bird-eye images would be legible enough to transcribe directly into structured user flows.

**Reality Discovered:**
The section headers remain readable, but many lower-level notes become illegible once exported at very large canvas widths. The safest artifact is a flow document that separates directly readable labels from inferred flow steps.

**Evidence:**
- Both source images were 32768 pixels wide, which made the full-board preview unreadable.
- Cropped views exposed section titles clearly but not every subordinate note, especially on the MFA board.
- The doctor board still yielded enough readable labels to confirm the main structure and a subset of detailed tasks.

**Impact on Approach:**
- Translate wide boards by using the visible lane structure first.
- Mark any reconstructed detail as inferred instead of presenting it as exact source text.

**Lesson Learned:**
For large journey maps, preserve confidence levels in the artifact: direct transcription where visible, explicit inference where not.

**Tags:** [Reusable]

## KL-W001: Token Bridge CSS For Static HTML Previews [Experiment]

**Date:** 2026-03-12
**Context:** Static artifact previews for the SynthCare dashboard and purchase-order modal
**Source Version:** v1

**Initial Assumption:**
Artifact HTML previews would need their own separate palette and typography rules to match screenshot styling.

**Reality Discovered:**
A shared bridge stylesheet can expose the exact Tini semantic token values and map them onto preview-specific aliases, letting static HTML mocks reuse the same color, radius, shadow, motion, and typography primitives without rebuilding the app.

**Evidence:**
- Existing artifacts already had stable HTML structure and light interaction scripts.
- The main gap was the token layer, not layout composition.
- Tini token semantics covered both previews once a small alias layer was added for screenshot-specific accents.

**Impact on Approach:**
- Keep preview HTML files thin and mostly unchanged.
- Centralize token sourcing in one artifact stylesheet for reuse across future mockups.

**Lesson Learned:**
For static UI validation, treat the token layer as the reusable asset and the HTML file as a disposable skin.

**Tags:** [Experiment]

---

## Adding New Knowledge Log Entries

**Template:**

```markdown
## KL-W###: [Topic] [Status Tag]

**Date:** YYYY-MM-DD
**Context:** [What were you working on]
**Source Version:** [Origin version or N/A]

**Initial Assumption:**
[What we thought was true]

**Reality Discovered:**
[What actually turned out to be true]

**Evidence:**
- [Data points]
- [Observations]
- [User feedback]

**Impact on Approach:**
- [How this changed what we do]
- [New practices adopted]

**Lesson Learned:**
[The takeaway for future work]

**Tags:** [Version-specific/Pending Review/Adopted]
```

**When to Create Entry:**
- Assumption invalidated during implementation
- User research contradicts design decisions
- Technical exploration reveals better approach
- Cross-version pattern emerges
