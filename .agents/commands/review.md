# review

Review the code changes for best practices, implementation quality, and optionally conformance to plan.

SCOPE:
- If files or git commits are specified: review those specifically
- If none specified: review all current uncommitted changes (git diff) in context of the whole project

PLAN REFERENCE (optional):
- Include only if you want conformance checking: path, URL, or commit to the plan document
- If omitted: skip dimension (a) and focus solely on implementation quality

DIMENSIONS:
a) CONFORMANCE TO PLAN — If plan reference provided, verify changes match stated intent, requirements, or design. Flag deviations, missing pieces, or scope creep.

b) BEST PRACTICES & IMPLEMENTATION QUALITY — Always assess:
   - Code readability and maintainability
   - Error handling and edge cases
   - Testing coverage and approach
   - Security considerations
   - Performance implications
   - Consistency with project conventions

ADDITIONAL NOTES:
- Keep items actionable and specific.
- Do not list nitpicks unless they materially impact quality.
- Do not include code snippets unless absolutely necessary for context.

OUTPUT FORMAT:
1. SUMMARY: Brief overview of findings (2-4 sentences). State clearly if no issues found.

2. ITEMIZED ISSUES (omit section entirely if no issues):

   Separate each issue with a blank line for readability:

   - severity: [critical | major | minor]
   - category: [Plan | Style | Logic | Security | Performance | Testing | Documentation]
   - location: file path and line/range (e.g., `src/auth.ts:42-58` or `src/auth.ts:42`)
   - current: brief description of what exists (1 line)
   - problem: why this is an issue
   - fix: concrete suggestion or required change

   [blank line before next issue]

3. INSTRUCTIONS (if issues found): 1-2 sentence guidance on prioritization or approach
