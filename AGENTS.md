# Repository Guidelines

## Project Structure & Module Organization
This repository currently contains one primary artifact: `SKILL.md`, which defines the `kn-git-standar-commit` workflow and safety rules.

- `SKILL.md`: Source of truth for commit workflow, allowed commit types, and git safety protocol.
- `.git/`: Local repository metadata.

Keep future additions small and explicit. If you add examples or references, place them in clearly named folders (for example, `examples/` or `references/`) and link them from `SKILL.md`.

## Build, Test, and Development Commands
There is no build system or runtime application in this repository today. Use lightweight validation commands:

- `rg --files`: quick inventory of tracked files.
- `git status`: verify working tree before and after edits.
- `git diff` and `git diff --cached`: review unstaged vs staged changes.

If you introduce tooling later, document exact commands here (for example, lint or docs checks).

## Coding Style & Naming Conventions
Use concise, instructional Markdown.

- Headings: sentence case, clear and action-oriented.
- Lists: short bullets with one idea per line.
- Code fences: include language hints like `bash` or `text`.
- Filenames: use descriptive lowercase names; keep `SKILL.md` as the canonical skill definition file.

Keep examples copy-pastable and avoid ambiguous placeholders.

## Testing Guidelines
Current validation is manual review.

- Confirm content accuracy against `SKILL.md`.
- Run `git diff` to verify no accidental churn.
- Prefer small, focused changes that are easy to inspect.

When automated checks are added, include command names and expected pass criteria in this section.

## Commit & Pull Request Guidelines
This project follows Conventional Commits as defined in `SKILL.md`.

- Format: `<type>[scope]: <description>`
- Example: `docs(skill): clarify staged diff review step`
- Keep subject lines imperative and <= 72 characters.

Before committing, review staged content and run minimum relevant verification. PRs should include: purpose, summary of changes, and any rationale for workflow or safety-rule updates.

## Security & Configuration Tips
Do not commit secrets, tokens, or machine-specific credentials. Never use destructive git operations (for example, `git reset --hard`) unless explicitly requested and approved.
