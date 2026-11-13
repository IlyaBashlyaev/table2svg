---
name: git-commits
description: >
  Rules for writing git commit messages. Always load when creating, proposing or amending
  a commit message, even if the user does not explicitly ask for commit guidelines.
metadata:
  state: "2026-10-29"
---

# Git Commits

## Language

- This skill is written in English.
- Every commit message (subject and body) is written in English.

## Conventional Commits (mandatory)

Every commit message must follow the Conventional Commits format:

```
<type>(<scope>): <subject>

<body>
```

- Allowed types: `feat`, `fix`, `refactor`, `perf`, `docs`, `test`, `style`, `build`, `ci`, `chore`, `revert`.
- The scope is the affected domain or area in kebab-case, e.g. `billing`, `user-auth`.
- The subject uses the imperative mood ("Resolve", not "Resolved"), starts with a capital letter and has no trailing period.
- The body is optional, explains what and why (not how), and is separated from the subject by a blank line.

## Marking code in commit messages

Every reference to code must be wrapped in backticks (`` ` ``). This covers:

- Class, method, function, property and variable names, e.g. `OrderService`, `calculateTotal()`, `$items`
- Operators and language constructs, e.g. `??`, `?->`
- File paths, config keys, commands, job names and environment variables, e.g. `config/app.php`, `APP_ENV`, `composer install`

Examples:

```
fix(billing): Prevent a null error in `InvoiceService::calculateTotal()`

Replace `$invoice->customer?->discount ?? 0` with `$invoice->customer->discount ?? 0`,
since `??` already handles a missing value.
```

```
refactor(user-auth): Extract token validation into `TokenValidator`

Move the checks from `LoginController::store()` into a dedicated class
and cover them with tests in `TokenValidatorTest`.
```

```
ci: Run `phpstan` before `phpunit` in the `quality` stage
```

## Process

- Before writing a commit message, always run `git status --short` and `git diff HEAD` (staged and unstaged changes) and base the message only on what the diff shows now. Do not reuse the wording of an earlier message or of earlier conversation turns: the code may have changed since, and parts of it may already be committed or pushed. Describe only the changes that are still uncommitted.
- Never run `git commit` and `git push` unless the user explicitly asks for it. By default, only propose the message.
- Never co-author yourself, e.g., by `Co-Authored-By: Claude Sonnet 5.5 <noreply@anthropic.com>` for Claude Code.
- Follow the attribution lines given in the session context, if any.
