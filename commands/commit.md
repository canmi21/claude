---
argument-hint: [commit-message]
description: Analyze changes, group semantically, commit.
---

# Command: /commit

**Role:** Git Orchestrator. Transform working tree into clean, semantic commit history.
**Output:** Commit hashes only. No markdown/explanations.

## CORE LOGIC & CONSTRAINTS

1. **Pre-conditions:** Ensure git repo, dirty tree, writable branch. Else abort.
2. **Style:** Mimic `git log -5 --oneline` (Conventional Commits, language, verbosity).
3. **Diff Strategy:** Read full diff for small changes; skim structure/intent for large diffs.

## EXECUTION WORKFLOW

### Phase 1: Context & Intent Analysis

Check `git status --porcelain`.

- **IF Staged Changes Exist:**
  - **MODE:** EXPLICIT INTENT.
  - **Action:** Treat staged files as a *single final commit*. DO NOT add/remove files.
- **IF No Staged Changes:**
  - **MODE:** AUTO-ORCHESTRATION.
  - **Filter:** KEEP Engineering-Relevant (Code, Config, Canonical Docs). DROP Noise (Scratch notes, temp files, unknown artifacts) even if not ignored.
  - **Grouping:** Bundle files by Semantic Theme (Feature/Fix/Refactor) + Directory.
    - *Rule:* 1 Commit = 1 Semantic Unit. NEVER 1 file/1 commit unless atomic.
    - *Rule:* Large refactors separate from logical fixes.

### Phase 2: Commit Generation

Iterate through defined groups:

1. `git add` group files.
2. **Message Logic:**
   - IF `[commit-message]` arg present AND single commit group: Use arg.
   - ELSE: Generate concise message based on intent (not implementation) following **Style**.
3. `git commit`.

### Phase 3: Finalize

1. Print generated Commit Hashes.
