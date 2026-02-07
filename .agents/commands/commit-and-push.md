# Commit and Push

Commit and push your changes using git, following Commitizen/Conventional Commits format.

## Commit Instructions

For commit instructions, conventions, and process, see `/commit`. This command follows the same commit standards and process, then additionally pushes to the remote repository.

## Process

### Steps 1-4: Commit

Follow the commit process defined in `/commit`:
1. Analyze changes
2. Determine commit details
3. Generate commit message
4. Stage and commit

### Step 5: Push to Remote

After successfully committing:

1. **Check remote tracking**: Run `git status` to see if branch tracks a remote
2. **Push changes**:
   - If branch tracks remote: `git push`
   - If new branch: `git push -u origin <branch-name>`
3. **Confirm success**: Verify push completed successfully

## Important Notes

- **NEVER** commit secrets or sensitive files (.env, credentials.json, etc.)
- **NEVER** skip hooks (--no-verify) unless explicitly requested
- **NEVER** force push to main/master without warning
- **DO NOT** use `git commit --amend` unless explicitly requested
- **DO NOT** commit changes to main/master without user confirmation
- If there are no changes to commit, inform the user

## Error Handling

### No Changes to Commit
If there are no staged changes and no untracked files, inform the user.

### Commit Hook Failures
If pre-commit hooks fail:
1. Show the error to the user
2. Fix the issue if possible
3. Create a NEW commit (don't amend unless explicitly requested)

### Push Failures
If push fails (e.g., remote has changes):
1. Show the error to the user
2. Ask if they want to pull first or force push (if safe)

## Examples

### Example 1: Simple Feature Commit

User: "Commit and push my dark mode changes"

**Process:**
1. Follow `/commit` process to commit changes with message: `feat(ui): add dark mode toggle`
2. Push to remote: `git push`

### Example 2: Bug Fix with Task ID

User: "Commit and push the race condition fix for MMV-456"

**Process:**
1. Follow `/commit` process to commit changes with message: `fix(convex): resolve race condition in interview creation [MMV-456]`
2. Push to remote: `git push`

### Example 3: Multiple File Refactor

User: "Commit and push these auth changes"

**Process:**
1. Follow `/commit` process to commit changes with message: `refactor(auth): simplify authentication flow`
2. Push to remote: `git push`

## Notes

- Follow the project's conventions defined in `AGENTS.md`
- Default to not pushing if unclear about remote state
- Always run `git status` after commit to verify success
- Check recent commit history to match the project's style
