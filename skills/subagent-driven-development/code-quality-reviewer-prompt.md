# Code Quality Reviewer Prompt Template

Use this template when dispatching the batched code quality reviewer.

**Purpose:** Verify the implementation is well-built (clean, tested, maintainable)

**Dispatch once, at the end of the plan** — after every task has committed and its
per-task spec review has passed. This is a single review over the *entire*
implementation, not a per-task review. Use a capable model (`opus`).

```
Task tool (general-purpose):
  Use template at requesting-code-review/code-reviewer.md

  DESCRIPTION: [one-paragraph summary of the whole implementation]
  PLAN_OR_REQUIREMENTS: [plan-file]
  BASE_SHA: [commit where the branch started]
  HEAD_SHA: [final commit]
```

**Scope — code quality only.** This review focuses on *how the code is built*, not on
whether the whole plan was delivered. Whole-plan completeness and cross-task
integration are the separate final whole-implementation review's job — don't duplicate
that here. Concentrate on:
- Code quality: clean separation of concerns, error handling, type safety, DRY without
  premature abstraction, edge cases.
- Testing: tests verify real behavior (not mocks), edge cases covered, all tests passing.
- File organization:
  - Does each file have one clear responsibility with a well-defined interface?
  - Are units decomposed so they can be understood and tested independently?
  - Does the implementation follow the file structure from the plan?
  - Did this work create new files that are already large, or significantly grow existing
    files? (Don't flag pre-existing file sizes — focus on what this change contributed.)

**Code reviewer returns:** Strengths, Issues (Critical/Important/Minor), Assessment
