---
name: rca
description: Perform a root cause analysis of a bug fix — a branch, PR, commit range, or diff — using a structured template (context, one section per distinct root cause with file/why/fix, causal chain, verification). Use when the user invokes /rca, asks to "perform an RCA", "root cause analysis", "why did this bug happen", or wants to understand what broke and why a fix closes the gap.
---

# RCA: Root Cause Analysis

Produce a report explaining what was broken, why, and how the fix closes the gap. This is analysis, not implementation — do not propose or make code changes as part of this skill unless the user separately asks for that.

## Process

1. **Scope it.** Default to the current branch vs its base (`git log <base>..HEAD`, `git diff <base>...HEAD --stat`). If the user names a ticket, PR, or specific commits instead, use those. Ask only if genuinely ambiguous.
2. **Read the diff and commit messages**, not just file names — the causal "why" lives in the actual code change, not the stat summary.
3. **Read the tests that were added or changed.** A regression test's description and comments are often the most reliable source of root-cause wording — frequently written by whoever fixed the bug, sometimes with the bug tracker link.
4. **Separate distinct causal mechanisms.** A branch/PR can bundle more than one real fix. Don't force unrelated fixes into one root cause just because they landed in the same commit — give each its own section, and label a fix that's related-but-not-causally-the-same as "Related fix", not "Root cause".
5. **Write the report** using the template below (as a file if the user wants one kept, inline otherwise).

## Template

```markdown
# RCA: <ticket/bug id> — <one-line symptom>

## Context
<what was reported, what prompted the investigation, expected outcome>

## Root cause #N — <short label>
`<commit hash>` — *<commit subject>*

**File:** `<path>` — `<function/area>`

<what the code actually did, what assumption it made, and where/why that
assumption broke — the causal chain from code to bug, not just a restatement
of the diff>

**Fix:** <what changed and why that specifically closes the gap>

## Related fix — <label>
(only for a bundled but causally distinct fix — same shape as above, minus forcing it into the root-cause narrative)

## Causal chain
(only when there are 2+ root causes and the relationship between them isn't obvious from listing them — an arrow chain from trigger to user-visible symptom)

## Verification
<tests that pin down each fix; if none exist, say so plainly instead of skipping the section>
```

## Rules

- Every root cause needs the causal **why**, not just the what. "It logged a warning and moved on" describes a symptom; say what state that left broken and why nothing ever corrected it.
- One root cause per distinct causal mechanism — resist merging two bugs that happen to share a commit.
- Omit the causal-chain section entirely when there's only one root cause; don't force a diagram for its own sake.
- State plainly whether this report accompanies real code changes or is analysis-only — never blur the two.
