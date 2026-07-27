---
name: commit
description: Inspect, validate, and commit changes using Conventional Commits. Use whenever the user asks to commit, create a commit, prepare a commit, or choose a commit message.
---

# Commit

Create focused, validated commits that follow the [Conventional Commits](https://www.conventionalcommits.org/) specification.

## Process

1. Inspect `git status`, staged and unstaged diffs, and recent commit style.
2. Identify the intended change and detect unrelated modifications.
3. Follow repository guidance such as `AGENTS.md` or `CLAUDE.md`.
4. Run the repository's required formatting, linting, type-checking, and tests when practical.
5. Stage only files belonging to the intended change. Do not include unrelated changes without user approval.
6. Commit with a concise Conventional Commit message.
7. Report the commit hash, subject, and validation result.

If there is nothing to commit, say so. Do not amend an existing commit, bypass hooks, force operations, or push unless explicitly requested.

## Message Format

```text
type(scope): imperative summary
```

Omit the scope when it adds no clarity:

```text
type: imperative summary
```

Use a lowercase type and a concise imperative summary without a trailing period.

Common types:

- `feat`: add user-visible behavior
- `fix`: correct faulty behavior
- `refactor`: restructure code without changing behavior
- `perf`: improve performance
- `test`: add or revise tests
- `docs`: documentation only
- `build`: build system or dependencies
- `ci`: continuous integration configuration
- `chore`: maintenance not covered above
- `revert`: revert an earlier commit

Use `!` before the colon and add a `BREAKING CHANGE:` footer for breaking changes:

```text
feat(api)!: rename decode error type

BREAKING CHANGE: `decode::Error` is now `decode::DecodeError`.
```

## Choosing the Message

Describe the purpose of the complete diff, not the editing action or file names. Prefer specific subjects such as:

```text
fix(parser): preserve nested error paths
refactor(decode): rename Error to DecodeError
docs: document nullable decoder behavior
```

Avoid vague subjects such as `update files`, `fix stuff`, or `changes`.

For a change with multiple independent concerns, propose separate commits rather than forcing them into one message.
