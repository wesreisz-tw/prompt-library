---
description: Run test review for acceptance criteria coverage and edge case gaps against a story.
globs: "*"
alwaysApply: false
---

## Test Review

### Objective

Perform the full test review workflow for the given story. Output is written to `specifications/{story-folder}/test-review.md` and a summary is provided in the response.

### Story context

- If the user has a file open under `specifications/**` (e.g. `specifications/DBP-345-save-users/story.md`), derive the story folder from that path.
- Otherwise, ask the user for the story ID or folder (e.g. `DBP-345` or `specifications/DBP-345-save-users`).

### Rules to apply

- Read and follow the workflow in **rules/test-review.mdc** from Step 0 through Step 5.
- When the rule refers to edge case heuristics, use **rules/edge-case-heuristics.mdc**.

### Workspace

Test discovery and spec/story files live in the **project workspace** where the user is working, not necessarily the prompt-library repo. Run discovery and read specs in the project that contains the code and `specifications/`. Use the discovery steps in **rules/test-review.mdc** Step 0, adapting patterns to the project’s language and test framework (e.g. `.test.ts`, `.spec.ts`, `*_test.py`, `.Tests.cs`, or whatever the codebase uses).

### Output

- Write the review to `specifications/{story-folder}/test-review.md` per Step 5 of the test-review rule.
- Provide the summary in the response: coverage score, critical gaps, edge case gaps, pyramid balance, prioritized recommendations.

### When a previous review exists

Before writing the new review, check if `specifications/{story-folder}/test-review.md` already exists.

- **If it exists:**
  - Read the existing file and retain its key outcomes (e.g. AC coverage count, critical/high recommendations, pyramid percentages, date).
  - After producing the new review, add a **Comparison with previous review** section in the written file and in the response. Summarize: improvements (gaps closed, recommendations addressed), regressions (new gaps or worsened metrics), and unchanged items. Use the previous review’s date/header so the comparison is unambiguous.
- **If it does not exist:** Omit the comparison section.
