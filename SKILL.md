---
name: kn-git-standard-commit
description: "Unified git commit workflow: plan commit boundaries, stage intentionally, generate Conventional Commit messages, enforce git safety rules, and run minimum verification before commit. Use when the user asks to commit, split commits, stage changes, craft commit messages, or mentions '/commit'."
license: MIT
allowed-tools: Bash
---

# KN Git Standard Commit (v2)

## Goal

Create commits that are:
- logically scoped
- safe to ship
- easy to review
- semantically consistent (Conventional Commits)

## Required Inputs (ask if missing)

- Single commit or multiple commits?
- Any commit style constraints? (scope rules, subject length, footer requirements)
- Any issue references required? (`Closes #`, `Refs #`)

Default behavior if unclear:
- Split into multiple commits when changes are unrelated.
- Use Conventional Commits.
- Keep subject <= 72 chars.

## Conventional Commits 1.0.0 (Required)

```text
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

### Specification-aligned rules

- Header MUST be `<type>[optional scope][optional !]: <description>`.
- `feat` MUST be used for new features.
- `fix` MUST be used for bug fixes.
- `scope` MAY be used and MUST be a noun in parentheses, e.g. `feat(parser): ...`.
- Description MUST immediately follow `: ` and be a short summary.
- Body MAY be added after one blank line and can be multi-paragraph.
- Footer(s) MAY be added after one blank line, following git trailer style (e.g. `Refs: #123`, `Reviewed-by: Name`).
- Footer tokens use `-` instead of spaces, except `BREAKING CHANGE`.
- Breaking changes MUST be indicated by either:
  - `!` before `:`, e.g. `feat(api)!: ...`, or
  - footer `BREAKING CHANGE: <description>`.
- `BREAKING-CHANGE` is accepted as synonymous footer token.
- Types are case-insensitive for tooling, but this skill enforces lowercase for consistency.

### SemVer mapping (intent)

- `fix` -> PATCH
- `feat` -> MINOR
- Any commit with breaking change (`!` or `BREAKING CHANGE`) -> MAJOR

### Supported types in this skill

- `feat`: new feature
- `fix`: bug fix
- `docs`: docs only
- `style`: formatting/style (no behavior change)
- `refactor`: internal code restructure (no feature/fix)
- `perf`: performance improvement
- `test`: test changes
- `build`: build/dependency changes
- `ci`: CI/config automation changes
- `chore`: maintenance/misc
- `revert`: revert a previous commit

### Valid examples

```text
feat(lang): add Polish language
fix: prevent racing of requests
chore!: drop support for Node 6

BREAKING CHANGE: use JavaScript features not available in Node 6.
```

## Unified Workflow (must follow in order)

### 1. Inspect working tree

```bash
git status
git diff
git diff --stat
git diff --staged
```

### 2. Define commit boundaries

Split by logical intent:
- feature vs refactor
- behavior vs formatting
- tests vs production code
- dependency/build changes vs app logic
- backend vs frontend vs docs

If mixed within the same file, use patch staging.

### 3. Stage intentionally

```bash
git add <paths...>
git add -p
git restore --staged <path>
git restore --staged -p
```

### 4. Review staged content only

```bash
git diff --cached
```

Sanity checks:
- no secrets/tokens
- no accidental debug logs
- no unrelated churn

### 5. Summarize intent before writing message

Write 1-2 lines internally:
- What changed?
- Why?

If unclear, split commit further.

### 6. Generate commit message

Rules:
- imperative mood (`add`, `fix`, `refactor`)
- present tense
- clear scope when useful
- concise subject, optional body for why/tradeoffs
- footer for issue references / breaking changes

### 7. Run minimum relevant verification

Run the fastest meaningful check for staged scope:
- lint / unit tests / targeted build
- do not skip hooks unless user explicitly asks

### 8. Commit and repeat

```bash
git commit -m "<type>[scope]: <description>"
```

For multi-line messages:

```bash
git commit -m "$(cat <<'EOM'
<type>[scope]: <description>

<why and key context>

Refs #123
EOM
)"
```

Repeat until working tree is clean.

## Git Safety Protocol (hard rules)

- NEVER modify git config automatically
- NEVER run destructive git commands (`reset --hard`, force operations) unless explicitly requested
- NEVER use `--no-verify` unless explicitly requested
- NEVER force push protected branches
- If hooks fail: fix the issue and create a new commit flow

## Deliverable

Always provide:
- final commit message(s)
- short summary per commit (what/why)
- verification command(s) run
- staged-scope evidence command used (`git diff --cached`)
