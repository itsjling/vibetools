---
description: Commit using Conventional Commits (explicit permission required)
agent: build
---

Only commit and/or push when explicitly requested by the user.
Permission is per request and does NOT persist across the session.

Commit format:
<type>(<scope>): <subject> [TASK-ID]

Types:
feat | fix | docs | style | refactor | test | chore | perf | ci | build | revert

Subject rules:
- imperative, lowercase, no period

Process (only after explicit request):
1. git status, git diff, git diff --staged
2. Choose type/scope/subject, extract TASK-ID
3. git add <files>
4. git commit -m "<message>"

Push (only if explicitly requested in the same message):
- git push
- or git push -u origin <branch>

Rules:
- NEVER assume permission to commit or push
- NEVER commit secrets (.env, credentials)
- NEVER force-push main/master
- DO NOT amend unless explicitly requested
- If no changes, inform user
