# Create Pull Request

Create well-formatted GitHub pull requests that follow Commitizen/Conventional Commits standards.

## When to Use This Command

Use this command when:
- User explicitly asks to create a PR or pull request
- User asks to "open a PR" or "submit for review"
- Changes are committed and ready to be pushed for review
- User mentions a task ID (e.g., "MMV-123") that should be included in the PR

## Commit Convention Standards

This project follows Commitizen/Conventional Commits:

### Format
```
<type>(<scope>): <subject>
```

Or without scope:
```
<type>: <subject>
```

Optionally with task ID:
```
<type>(<scope>): <subject> [TASK-ID]
```

### Types
- `feat` - New feature
- `fix` - Bug fix
- `docs` - Documentation changes
- `style` - Code style changes (formatting, etc.)
- `refactor` - Code refactoring
- `test` - Adding or updating tests
- `chore` - Maintenance tasks
- `perf` - Performance improvements
- `ci` - CI/CD changes
- `build` - Build system changes
- `revert` - Revert previous changes

### Scope (optional)
Area affected, such as:
- `ui` - User interface changes
- `api` - API changes
- `convex` - Convex backend changes
- `auth` - Authentication
- `agents` - Agent skills and AI capabilities
- Component or feature names

### Subject
- Use imperative mood ("add" not "added" or "adds")
- Lowercase, no period at the end
- Be concise and descriptive

### Examples
- `feat(ui): add dark mode toggle`
- `fix(convex): resolve interview plan validation error`
- `docs: update AGENTS.md with commit standards`
- `refactor(api): simplify authentication flow`

## PR Creation Process

### Step 1: Analyze Changes

Run these commands in parallel to understand the current state:

1. `git status` - See all untracked and modified files
2. `git diff` - See unstaged changes (if any need to be committed)
3. `git diff --staged` - See staged changes (if any need to be committed)
4. `git log <base-branch>...HEAD --oneline` - See all commits in the branch
5. `git diff <base-branch>...HEAD` - See all changes compared to base branch
6. Check if branch tracks remote and needs pushing

### Step 2: Handle Uncommitted Changes

If `git status` shows uncommitted changes:
1. Review the changes with the user if needed
2. Commit the changes following the Commitizen format (this is acceptable when user asks to create a PR per AGENTS.md)
3. Then proceed with PR creation

### Step 3: Determine PR Details

Based on the analysis of ALL commits and changes in the branch:

1. **Identify the type**: What kind of change is this? (feat, fix, refactor, etc.)
2. **Identify the scope**: What area is affected? (ui, api, convex, etc.)
3. **Write the subject**: Concise description in imperative mood
4. **Extract task ID**: Look for task IDs in branch name, commits, or user messages (e.g., "MMV-123", "JIRA-456")

**Important**: Analyze ALL commits in the branch, not just the latest one!

### Step 4: Generate PR Title

Format: `<type>(<scope>): <subject>` or `<type>: <subject>`

Add `[TASK-ID]` at end if available:
```
feat(ui): add candidate filtering [MMV-123]
```

**Title Rules:**
- Must follow conventional commit format
- Include task ID in square brackets at the end if available
- Keep subject concise (under 50 characters ideally)
- Total PR title including type, scope, and task ID should be under 72 characters
- Use imperative mood, lowercase

### Step 5: Generate PR Description

Create a comprehensive PR description with these sections:

```markdown
## Summary
- Brief overview of what changed and why
- Use bullet points for multiple changes
- Focus on the "what" and "why", not the "how"

## Changes
- **Component/Area 1**: Description of specific changes
- **Component/Area 2**: Description of specific changes
- Use bold for component names
- Be specific about what was modified, added, or removed

## Task
[Task ID if available, e.g., MMV-123]

## Notes (optional)
- Any important context for reviewers
- Breaking changes
- Migration steps if needed
- Screenshots if UI changes
```

**Description Guidelines:**
- Be clear and comprehensive
- Help reviewers understand the context
- Highlight important changes
- Include any relevant technical details
- Add screenshots for visual changes
- Mention breaking changes prominently

### Step 6: Push Branch (if needed)

If the branch hasn't been pushed or is behind remote:
```bash
git push -u origin <branch-name>
```

### Step 7: Create the PR

**Determine PR status**: Ask user if unclear whether work is complete or in progress

**For complete work:**
```bash
gh pr create --title "<PR title>" --body "$(cat <<'EOF'
<PR description>
EOF
)" --base <base-branch>
```

**For work-in-progress (draft PR):**
```bash
gh pr create --draft --title "<PR title>" --body "$(cat <<'EOF'
<PR description>
EOF
)" --base <base-branch>
```

**Important:**
- Default base branch is usually `next` (check with user if unsure)
- Use `--draft` flag if user mentions "WIP", "draft", "work in progress", or if work is incomplete
- If unclear whether work is complete, confirm with user before creating
- Use HEREDOC syntax for multi-line PR descriptions
- Ensure proper escaping of special characters

### Step 8: Return PR URL

After creating the PR, provide:
- The PR URL (returned by `gh pr create`)
- A brief confirmation of what was created

## Common Patterns

### Multiple Commits

If the PR contains multiple commits, analyze ALL commits to understand the full scope:

```bash
git log <base-branch>...HEAD --oneline
```

Then create a PR title and description that encompasses all changes.

### Task ID Extraction

Look for task IDs in:
1. Branch name (e.g., `feature/MMV-123-add-filtering`)
2. Commit messages
3. User's request (e.g., "create PR for MMV-123")

Common patterns:
- `MMV-123`
- `JIRA-456`
- `TICKET-789`
- `#123` (GitHub issue)

### No Task ID

If no task ID is found, that's okay! Just create the PR without it:

```
feat(ui): improve candidate page layout
```

## Error Handling

### Uncommitted Changes
If `git status` shows uncommitted changes:
1. Review the changes with the user if needed
2. Commit the changes following the Commitizen format (this is acceptable when user asks to create a PR per AGENTS.md)
3. Then proceed with PR creation

### Branch Not Pushed
If the branch hasn't been pushed to remote:
```bash
git push -u origin <branch-name>
```

### Not on a Feature Branch
If the user is on `main` or `next`, warn them and ask if they want to create a new branch first.

### No Changes
If there are no commits or changes, inform the user and ask them to make changes first.

### gh Not Authenticated
If `gh auth status` fails, guide the user to authenticate:
```bash
gh auth login
```

### Merge Conflicts
If the branch has merge conflicts with the base branch, inform the user and ask them to resolve conflicts before creating the PR.

### Outdated Branch
If the base branch has moved ahead significantly, inform the user and ask if they want to update/rebase their branch first.

### Existing PR
If a PR already exists for this branch, inform the user and provide the existing PR URL instead of creating a duplicate.

## Examples

### Example 1: Simple Feature PR

User: "Create a PR for my dark mode feature"

**Analysis:**
- Branch: `feature/dark-mode-toggle`
- Changes: Added dark mode toggle component, updated theme provider
- Commits: 2 commits related to dark mode

**PR Title:**
```
feat(ui): add dark mode toggle
```

**PR Description:**
```markdown
## Summary
- Adds dark mode toggle to user settings
- Persists user preference across sessions

## Changes
- **DarkModeToggle component**: New toggle component in settings
- **Theme provider**: Updated to support dark mode state
- **Local storage**: Added persistence for user preference

## Notes
- Default is light mode for existing users
```

**Commands:**
```bash
git push -u origin feature/dark-mode-toggle
gh pr create --title "feat(ui): add dark mode toggle" --body "$(cat <<'EOF'
## Summary
- Adds dark mode toggle to user settings
- Persists user preference across sessions

## Changes
- **DarkModeToggle component**: New toggle component in settings
- **Theme provider**: Updated to support dark mode state
- **Local storage**: Added persistence for user preference

## Notes
- Default is light mode for existing users
EOF
)" --base next
```

### Example 2: Bug Fix with Task ID

User: "Open PR for MMV-456, I fixed the race condition"

**Analysis:**
- Branch: `fix/MMV-456-race-condition`
- Changes: Modified interview creation mutation
- Task ID: MMV-456

**PR Title:**
```
fix(convex): resolve race condition in interview creation [MMV-456]
```

**PR Description:**
```markdown
## Summary
- Fixes race condition when creating multiple interviews simultaneously
- Ensures atomic operations for interview plan updates

## Changes
- **Interview mutation**: Added transaction wrapper for atomic updates
- **Error handling**: Improved error messages for concurrent creation attempts
- **Tests**: Added test case for concurrent interview creation

## Task
MMV-456

## Notes
- No breaking changes
- Existing interviews are not affected
```

**Commands:**
```bash
git push
gh pr create --title "fix(convex): resolve race condition in interview creation [MMV-456]" --body "$(cat <<'EOF'
## Summary
- Fixes race condition when creating multiple interviews simultaneously
- Ensures atomic operations for interview plan updates

## Changes
- **Interview mutation**: Added transaction wrapper for atomic updates
- **Error handling**: Improved error messages for concurrent creation attempts
- **Tests**: Added test case for concurrent interview creation

## Task
MMV-456

## Notes
- No breaking changes
- Existing interviews are not affected
EOF
)" --base next
```

### Example 3: Refactor PR

User: "Create PR to refactor the authentication flow"

**Analysis:**
- Branch: `refactor/auth-simplification`
- Changes: Simplified auth hooks, removed duplicate code
- Multiple files affected

**PR Title:**
```
refactor(auth): simplify authentication flow
```

**PR Description:**
```markdown
## Summary
- Simplifies authentication flow by consolidating duplicate logic
- Improves code maintainability and reduces bundle size

## Changes
- **useAuth hook**: Consolidated authentication logic into single hook
- **Auth provider**: Removed redundant state management
- **Login/Logout**: Simplified to use centralized auth hook
- **Tests**: Updated tests to reflect new structure

## Notes
- No functional changes to user experience
- All existing auth flows continue to work as expected
- Reduced bundle size by ~2KB
```

**Commands:**
```bash
git push
gh pr create --title "refactor(auth): simplify authentication flow" --body "$(cat <<'EOF'
## Summary
- Simplifies authentication flow by consolidating duplicate logic
- Improves code maintainability and reduces bundle size

## Changes
- **useAuth hook**: Consolidated authentication logic into single hook
- **Auth provider**: Removed redundant state management
- **Login/Logout**: Simplified to use centralized auth hook
- **Tests**: Updated tests to reflect new structure

## Notes
- No functional changes to user experience
- All existing auth flows continue to work as expected
- Reduced bundle size by ~2KB
EOF
)" --base next
```

### Example 4: Draft PR

User: "Create a draft PR for my WIP feature"

**Commands:**
```bash
git push -u origin feature/new-feature
gh pr create --draft --title "feat(ui): add new feature" --body "$(cat <<'EOF'
## Summary
- Work in progress for new feature
- Still testing and refining

## Changes
- **Feature component**: Initial implementation (WIP)

## Notes
- Not ready for review yet
- Will mark as ready when testing is complete
EOF
)" --base next
```

## Best Practices

1. **Always analyze before creating**: Run git commands to understand what you're submitting
2. **Be thorough**: Include all relevant details in the PR description
3. **Use proper conventions**: Follow the Commitizen format exactly
4. **Include task IDs**: Always include task IDs when available
5. **Think about reviewers**: Write descriptions that help reviewers understand context
6. **Highlight breaking changes**: Make them obvious in the description
7. **Add screenshots**: For UI changes, include before/after screenshots when possible

## Validation Checklist

Before creating the PR, verify:
- [ ] PR title follows conventional commit format: `type(scope): subject` or `type: subject`, with optional `[TASK-ID]`
- [ ] Task ID is included (if available)
- [ ] PR description has Summary and Changes sections
- [ ] All important changes are documented
- [ ] Base branch is correct (usually `next`)
- [ ] Branch has been pushed to remote
- [ ] Commit history has been reviewed
- [ ] ALL commits in the branch have been analyzed (not just the latest)

## Notes

- This command requires `gh` (GitHub CLI) to be installed and authenticated
- Default base branch is `next` unless otherwise specified
- Always verify the base branch with the user if unsure
- The command follows the project's conventions defined in `AGENTS.md`
- When user asks to create a PR, committing uncommitted changes is acceptable per AGENTS.md
