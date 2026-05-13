---
name: deduplicate-and-unify-utility-functions
description: Workflow command scaffold for deduplicate-and-unify-utility-functions in ManGaAI.
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /deduplicate-and-unify-utility-functions

Use this workflow when working on **deduplicate-and-unify-utility-functions** in `ManGaAI`.

## Goal

Removes duplicate utility functions from feature or service files and consolidates them into shared/utils, updating all call sites to use the shared version.

## Common Files

- `src/shared/utils/index.ts`
- `src/core/services/*.ts`
- `src/features/*/components/*.tsx`
- `src/features/*/services/*.ts`
- `src/components/business/*.tsx`
- `src/pages/*.tsx`

## Suggested Sequence

1. Understand the current state and failure mode before editing.
2. Make the smallest coherent change that satisfies the workflow goal.
3. Run the most relevant verification for touched files.
4. Summarize what changed and what still needs review.

## Typical Commit Signals

- Identify duplicate utility functions in feature/service/component files.
- Move or implement the unified version in src/shared/utils/index.ts.
- Remove local duplicates from all affected files.
- Update all call sites to use the shared utility.
- Clean up imports and remove dead code.

## Notes

- Treat this as a scaffold, not a hard-coded script.
- Update the command if the workflow evolves materially.