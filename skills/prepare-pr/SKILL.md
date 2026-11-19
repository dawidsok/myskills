---
name: prepare-pr
description: Draft a pull request description for the current branch from its commits and diff, using the repository's PR template when available. Show the draft for review, then copy the approved text to the clipboard. Use when the user invokes /prepare-pr or asks to prepare, draft, or write a PR description.
---

# Prepare PR

Draft a PR description from the current branch, get explicit approval, then copy the approved text to the clipboard.

## Process

1. **Find the base branch.** Prefer the remote's default branch; otherwise check `main` and `master`. Confirm with `git merge-base` when needed.
2. **Find the repository's PR template.** Check the standard locations:
   - `.github/pull_request_template.md`
   - `.github/PULL_REQUEST_TEMPLATE.md`
   - `.github/PULL_REQUEST_TEMPLATE/`
   - `docs/pull_request_template.md`

   If several templates apply and the repository does not identify a default, ask the user which one to use. If none exists, use: Summary, Changes, How to test, and Additional notes.
3. **Read the branch changes:**
   - `git log <base>..HEAD --format='%h %s%n%b'`
   - `git diff <base>...HEAD --stat`
   - The actual diffs of non-trivial changed files, not only the stat. Skip generated files, lockfiles, and snapshots unless they contain relevant behavior.
   - Extract a ticket ID from the branch name when it follows a clear convention such as `ABC-123`.
4. **Draft the description:**
   - Add the ticket ID to the title when one exists.
   - Group changes by feature or root cause, not by commit.
   - Give concrete, runnable test steps supported by the diff.
   - Include additional notes only for relevant configuration, environment variables, migrations, rollout constraints, or reviewer context.
   - Preserve the repository template's structure and checklist state. Mark an item complete only when the evidence verifies it.
5. **Show the full draft** and stop.
6. **Wait for explicit approval.** Apply requested edits and show the revised draft again.
7. **Copy the approved draft.** Use the first available clipboard command: `pbcopy`, `wl-copy`, `xclip -selection clipboard`, or `Set-Clipboard`. If none exists, save it to a temporary Markdown file and report the path.

## Rules

- Copy only after explicit approval of the current draft.
- Never silently copy a revised draft.
- Never fabricate tests, configuration, or migration details.
- Keep claims traceable to the commits, diff, tests, or user-provided context.
