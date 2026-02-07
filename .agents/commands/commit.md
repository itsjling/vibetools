# Commit

Commit your changes using git, following Commitizen/Conventional Commits format.

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
- Component or feature names

### Subject
- Use imperative mood ("add" not "added" or "adds")
- Lowercase, no period at the end
- Be concise and descriptive

### Examples
- `feat(ui): add dark mode toggle`
- `fix(convex): resolve interview plan validation error [MMV-456]`
- `docs: update AGENTS.md with commit standards`
- `refactor(api): simplify authentication flow`

## Process

### Step 1: Analyze Changes

Run these commands in parallel to understand what you're committing:
1. `git status` - See all untracked and modified files
2. `git diff` - See unstaged changes
3. `git diff --staged` - See staged changes
4. `git log -5 --oneline` - See recent commit history for style reference

### Step 2: Determine Commit Details

Based on the analysis:

1. **Identify the type**: What kind of change is this? (feat, fix, refactor, etc.)
2. **Identify the scope**: What area is affected? (ui, api, convex, etc.) - optional
3. **Write the subject**: Concise description in imperative mood
4. **Extract task ID**: Look for task IDs in branch name or user messages (e.g., "MMV-123")

### Step 3: Generate Commit Message

Format: `<type>(<scope>): <subject>` or `<type>: <subject>`

Add `[TASK-ID]` at end if available:
```
feat(ui): add candidate filtering [MMV-123]
```

**Commit Message Rules:**
- Must follow conventional commit format
- Include task ID in square brackets at the end if available
- Keep subject concise (under 50 characters ideally)
- Use imperative mood, lowercase
- No period at the end

### Step 4: Stage and Commit

1. **Stage relevant files**: Use `git add` for files that should be committed
   - **Always quote file paths** to avoid issues with special characters: `git add "path/to/file.ts"`
   - Do NOT commit files that likely contain secrets (.env, credentials.json, etc.)
   - Warn the user if they specifically request to commit those files
   - **Only stage files that are relevant to the current commit**
   - **Do NOT delete or revert changes** in files that are unrelated to the current commit
   - **Ignore unrecognized or irrelevant files** - leave them unchanged rather than modifying them
2. **Create the commit**: `git commit -m "<commit message>"`
3. **Verify success**: Run `git status` to confirm the commit was created

## Important Notes

- **NEVER** commit secrets or sensitive files (.env, credentials.json, etc.)
- **NEVER** skip hooks (--no-verify) unless explicitly requested
- **NEVER** force push to main/master without warning
- **NEVER** delete or revert changes in files unrelated to the current commit
- **DO NOT** use `git commit --amend` unless explicitly requested
- **DO NOT** commit changes to main/master without user confirmation
- **DO NOT** modify, delete, or revert unrecognized or irrelevant files - ignore them instead
- If there are no changes to commit, inform the user

## Error Handling

### No Changes to Commit
If there are no staged changes and no untracked files, inform the user.

### Commit Hook Failures
If pre-commit hooks fail:
1. Show the error to the user
2. Fix the issue if possible
3. Create a NEW commit (don't amend unless explicitly requested)

## Examples

### Example 1: Simple Feature Commit

User: "Commit my dark mode changes"

**Analysis:**
- Changed files: `DarkModeToggle.tsx`, `ThemeProvider.tsx`
- Change type: New feature
- Scope: UI

**Commit Message:**
```
feat(ui): add dark mode toggle
```

**Commands:**
```bash
git add "src/components/DarkModeToggle.tsx" "src/providers/ThemeProvider.tsx"
git commit -m "feat(ui): add dark mode toggle"
```

### Example 2: Bug Fix with Task ID

User: "Commit the race condition fix for MMV-456"

**Analysis:**
- Changed files: `convex/interviews.ts`
- Change type: Bug fix
- Scope: Convex
- Task ID: MMV-456

**Commit Message:**
```
fix(convex): resolve race condition in interview creation [MMV-456]
```

**Commands:**
```bash
git add "convex/interviews.ts"
git commit -m "fix(convex): resolve race condition in interview creation [MMV-456]"
```

### Example 3: Multiple File Refactor

User: "Commit these auth changes"

**Analysis:**
- Changed files: Multiple auth-related files
- Change type: Refactor
- Scope: Auth

**Commit Message:**
```
refactor(auth): simplify authentication flow
```

**Commands:**
```bash
git add "src/hooks/useAuth.ts" "src/providers/AuthProvider.tsx" "src/components/Login.tsx"
git commit -m "refactor(auth): simplify authentication flow"
```

## Task ID Extraction

Look for task IDs in:
1. Branch name (e.g., `feature/MMV-123-add-filtering`)
2. User's request (e.g., "commit changes for MMV-123")
3. Recent commits in the same branch

Common patterns:
- `MMV-123`
- `JIRA-456`
- `TICKET-789`
- `#123` (GitHub issue)

If no task ID is found, that's okay! Just create the commit without it.

## Validation Checklist

Before committing, verify:
- [ ] Commit message follows conventional commit format
- [ ] Task ID is included if available
- [ ] No secrets or sensitive files are being committed
- [ ] All relevant files are staged
- [ ] File paths are quoted in git add commands
- [ ] Only files relevant to the current commit are being staged
- [ ] No unrelated changes are being deleted or reverted
- [ ] Commit type accurately reflects the changes
- [ ] Subject is in imperative mood and lowercase

## Notes

- Follow the project's conventions defined in `AGENTS.md`
- Always run `git status` after commit to verify success
- Check recent commit history to match the project's style
