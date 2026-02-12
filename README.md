# kn-git-standard-commit

Unified workflow for safe, intentional Git commits using Conventional Commits.

## What this skill does
`kn-git-standar-commit` guides commit creation from inspection to verification:

- Defines logical commit boundaries
- Stages changes intentionally (`git add`, `git add -p`)
- Generates Conventional Commit messages
- Enforces Git safety rules (no destructive shortcuts)
- Requires minimum relevant verification before commit

Source of truth: `SKILL.md`.

## Repository structure
- `SKILL.md`: Skill definition, workflow steps, commit format, and safety protocol
- `AGENTS.md`: Repository contributor guidelines
- `.gitignore`: Local environment ignore rules

## Quick usage
Use this skill when you need to create one or more clean, reviewable commits.

Typical flow:

```bash
git status
git diff
git add -p
git diff --cached
git commit -m "feat(scope): concise description"
```

Example commit messages:

- `feat(auth): add token refresh strategy`
- `fix(api): handle null user profile response`
- `docs(skill): clarify staged diff review step`

## Commit standard
Format:

```text
<type>[optional scope]: <description>
```

Supported types include `feat`, `fix`, `docs`, `refactor`, `test`, `ci`, and `chore`.

## Safety rules
This project does not allow unsafe Git shortcuts in normal flow:

- No destructive operations unless explicitly requested
- No `--no-verify` unless explicitly requested
- No force push to protected branches

## Contributing
1. Update `SKILL.md` or docs with focused changes.
2. Review staged diff only: `git diff --cached`.
3. Run the fastest relevant verification.
4. Commit using Conventional Commits.
