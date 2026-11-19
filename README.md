# myskills

Five reusable [Agent Skills](https://agentskills.io/) for product thinking, concise output, pull requests, root-cause analysis, and Markdown notes.

## Skills

| Skill | Purpose |
| --- | --- |
| [`idea`](skills/idea/) | Refine and challenge a seed idea before writing a PRD. |
| [`minimal-output`](skills/minimal-output/) | Keep responses and implementations small, clear, and complete. |
| [`prepare-pr`](skills/prepare-pr/) | Draft a PR description from the current branch and repository template. |
| [`rca`](skills/rca/) | Explain a bug fix through distinct root causes and verification evidence. |
| [`scribe`](skills/scribe/) | Capture, search, and connect notes in a local Markdown note base. |

## Install

Install the repository with the Agent Skills CLI:

```bash
npx skills add dawidsok/myskills
```

Or copy an individual directory from `skills/` into the skills directory used by your agent.

## Configuration

- `scribe` uses `$NOTES_DIR` when set and falls back to `~/notes`.
- `prepare-pr` discovers standard GitHub PR template locations and uses the available system clipboard command.

## License

[MIT](LICENSE)
