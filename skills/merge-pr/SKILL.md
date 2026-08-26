---
name: merge-pr
description: Merge an existing GitHub pull request only after required CI passes and no review is pending or blocking.
---

# Merge PR

Merge the target PR only when its merge gates are clearly satisfied.

## Workflow

1. Identify the PR from the current branch or an explicit PR number. Inspect its state, base/head, mergeability, draft status, required checks, review decisions, unresolved conversations, and branch protection requirements with `gh pr view --json ...` and check runs.
2. Treat any failing, pending, required, or unknown CI check as a stop condition. Treat requested changes, pending required reviews, unresolved blocking conversations, conflicts, and draft status as stop conditions.
3. If any gate is unclear or the PR is not cleanly mergeable, report exactly what blocks merging and stop. Do not dismiss reviews, resolve threads, rerun checks, or change branch protection to make it mergeable.
4. When all gates are satisfied, merge using the repository's normal method (prefer the configured squash/merge/rebase policy). Do not delete the branch unless the user explicitly asks.
5. Verify the resulting PR state and report the merge commit or final status.

## Safety

Invoking this skill authorizes merging the identified PR once the gates above are verified. It does not authorize unrelated cleanup, review dismissal, force-pushes, or branch-protection changes.
