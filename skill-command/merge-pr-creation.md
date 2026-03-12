# Merge PR-Creation Skills

**Date:** 2026-02-12
**Author:** Claude
**Status:** Draft

## Context

Two PR-creation skill documents exist:
- **File A (current):** `~/.claude/skills/create-pull-request/SKILL.md` — procedural automation (template lookup, existing PR detection, draft logic, post-creation steps)
- **File B (downloaded):** `~/Downloads/SKILL-create-pull-request.md` — discipline-first (mandatory pre-PR gate, security audit, self-review, size evaluation)

Both analyses (mine + Codex) agree: use File B as policy core, graft File A's operational automation. Neither is complete alone.

## Design Decisions (confirmed)

| Decision | Choice | Rationale |
|----------|--------|-----------|
| Tone | Neutral directives | Strict but not preachy. Imperative voice. |
| Skill orchestration | Skill orchestrates | Discovers and invokes related skills before PR. Self-contained. |
| Hotfix section | Include | Same workflow compressed. Agent always sees it under time pressure. |
| Rationalization table | Convert to red flags list | 5-6 "stop if doing X" items. Actionable, fits neutral tone. |
| Base branch | Dynamic detection | `git remote show origin \| grep "HEAD branch"`, not hardcoded `origin/main`. |
| PR title generation | Trim | Brief guidance + conventional commit check. Drop 47-line heuristics section. |
| Template awareness | Keep | Check `.github/pull_request_template.md` > `~/.claude/templates/pull-request-template.md`. |

## Target Structure

```
---
name: create-pull-request
description: <current description, unchanged>
license: MIT
---

# Create Pull Request

## Overview                          ← NEW from B (2-3 lines, "communication artifact" framing)

## Prerequisites Check               ← FROM A (gh CLI, auth, related skills, clean dir)
  ### 1. gh CLI installed
  ### 2. GitHub authenticated
  ### 3. Related skills              ← Keep orchestration
  ### 4. Clean working directory

## Check for Existing PR             ← FROM A (detect, offer view/update/close)

## Pre-PR Gate (Mandatory)           ← FROM B (the core safety section)
  ### Step 1: Sync with Base Branch  ← Use dynamic base detection from A
  ### Step 2: Run Tests Locally      ← FROM B
  ### Step 3: Self-Review Full Diff  ← FROM B ("Iron Law" rewritten as neutral directive)
  ### Step 4: Security Audit         ← FROM B (secret grep, .gitignore check)
  ### Step 5: Evaluate PR Size       ← FROM B (size table, split guidance)

## Gather Context                    ← FROM A (branch, base, commits, diff stat)
  ### Information to Extract         ← FROM A (issue number, description, type, test procedure)

## Create the Pull Request           ← MERGED
  ### Commit Hygiene                 ← FROM B (brief, neutral)
  ### PR Title                       ← Trimmed from A (conventional commits + imperative mood)
  ### PR Body                        ← Template-first from A, minimum requirements from B
  ### Draft PR Decision              ← FROM A
  ### gh pr create Command           ← FROM A

## Emergency / Hotfix PRs            ← FROM B (compressed process, "never do" list)

## Post-Creation                     ← FROM A (browser verification, reviewers, labels, CI reminder)

## Error Handling                    ← FROM A (4 common issues)

## Red Flags                         ← CONVERTED from B's rationalization table
  5-6 items: "Stop if you catch yourself doing X"

## Summary Checklist                 ← FROM A + B additions (security, self-review, size)

## Integration                       ← FROM B (references to companion skills)
```

## Changes

### Step 1: Write merged SKILL.md

**File:** `~/.claude/skills/create-pull-request/SKILL.md`

Rewrite the entire file following the target structure above. Source content from both files. All rules from B's Pre-PR Gate preserved verbatim in substance, rewritten in neutral directive tone.

Key merges:
- B's "Iron Law" → "Self-review the full diff before creating any PR. `git diff` is required, not optional."
- B's rationalization table → Red Flags flat list (5-6 items)
- A's template lookup logic preserved exactly
- A's existing PR detection preserved exactly
- A's draft PR decision logic preserved exactly
- A's post-creation steps preserved exactly
- Dynamic base branch detection throughout (no hardcoded `origin/main`)

### Step 2: Verify merged skill

- Read final file, confirm all sections present
- Grep for key terms: "security", "self-review", "template", "existing PR", "draft", "hotfix", "red flag"
- Confirm frontmatter `name: create-pull-request` matches directory
- Confirm no hardcoded `origin/main` outside of example blocks (use variable `$BASE_BRANCH` or dynamic detection)

## Files Modified

- `~/.claude/skills/create-pull-request/SKILL.md` (full rewrite)

## Verification

1. Grep merged file for all required sections from target structure
2. Confirm template lookup references both `.github/pull_request_template.md` and `~/.claude/templates/pull-request-template.md`
3. Confirm Pre-PR Gate has all 5 steps (sync, test, self-review, security, size)
4. Confirm Red Flags section exists with 5-6 items
5. Confirm Emergency/Hotfix section exists
6. Confirm no orphaned content from either source was lost unintentionally

## Open Questions

None. All design decisions confirmed.
