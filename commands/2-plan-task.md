---
description:
globs: *
alwaysApply: true
---

META-INSTRUCTION: RULE LOADING (START OF TASK)

Before writing any plan:
1. Read task file to identify target files/extensions
2. Match extensions against `globs` in `<agent_requestable_workspace_rules>`
3. Load ALL matching rules using Read tool
4. Output (file names only, no paths):
   ## Rules Loaded
   - [rule.mdc] - matched [glob] for [target files]

---

"do pla; Create a concise implementation plan for [TASK_ID] as specified in task-[N].md from story [STORY_ID].

INTENTION: Generate a focused, actionable plan that can be immediately executed without extensive refinement.

Create task-[N]-plan.md with this structure:

## 1. Issue

- Clear statement of what needs to be implemented

## 2. Solution

- High-level approach and technical rationale

## 3. Implementation Steps

1. [Specific action with file paths and function names]
2. [Continue with numbered steps...]

## 4. Verification

- Key requirements to validate implementation
- **Test Gate**: If this task includes code changes, all existing unit tests MUST pass before execution is complete

Keep the plan concise and actionable. Each step should be specific enough that no creative decisions are needed during execution."

---

META-INSTRUCTION: RULES SUMMARY (END OF TASK)

After completing the plan, output:

## Rules Applied
**Rules Loaded & Used:**
- [rule] - [how it influenced the plan]

**Rules NOT Loaded:**
- [rule] - [why not relevant to this task]