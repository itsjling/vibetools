---
name: fix
description: Fix the issues identified in a prior code review. Parses review output and applies fixes in severity order.
---

# fix

Fix the issues identified in a prior code review.

INPUT: The output from `/review` or equivalent structured review of code issues.

STEPS:
1. Parse each itemized issue from the review
2. Address issues in severity order: critical first, then major, then minor
3. For each issue:
   - Locate the specified file and line/range
   - Apply the suggested fix or an equivalent correct solution
   - Verify the change resolves the stated problem without introducing regressions

CONSTRAINTS:
- If an issue is unclear, the fix would conflict with project patterns, or the location cannot be found: stop and ask for clarification
- Do not modify unrelated code, even if you notice other opportunities
- Preserve existing formatting, naming conventions, and architectural decisions unless the issue specifically requires change
- Add or update tests when the issue is in the Testing category or when the fix involves logic changes

OUTPUT FORMAT:
1. SUMMARY: Brief description of what was fixed (2-3 sentences)
2. CHANGES (omit if no changes made):
   - [severity] file:line-range — what was changed and why
3. FOLLOW-UP: Any items that require human review or could not be auto-resolved
