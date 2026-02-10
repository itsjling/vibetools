---
description: Commit and push using Conventional Commits
agent: build
---

Commit and push git changes.

Commit format:
<type>(<scope>): <subject> [TASK-ID]
(scope and TASK-ID optional)

Types:
feat | fix | docs | style | refactor | test | chore | perf | ci | build | revert

Subject rules:
- imperative, lowercase, no period, concise

Process:
1. git status, git diff, git diff --staged, git log -5 --oneline
2. Choose type, scope (optional), subject
3. Extract TASK-ID from branch, user message, or commits
4. git add <files>
5. git commit -m "<message>"
6. git push (or git push -u origin <branch>)

Rules:
- NEVER commit secrets (.env, credentials)
- NEVER skip hooks unless asked
- NEVER force-push to main/master
- DO NOT amend unless requested
- DO NOT commit to main/master without confirmation
- If no changes, inform user

On failure:
- Hook fails: show error, offer to fix
- Push fails: show error, ask to pull
