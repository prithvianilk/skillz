---
name: raise-pr
description: Create a GitHub pull request from the current changes and trigger a CodeRabbit review when the user asks to raise or open a PR.
---

# Raise PR

Raise a pull request for the current repository changes and start CodeRabbit review.

## Workflow

1. Inspect `git status`, the current branch, the diff, and repository guidance. Confirm the changes are coherent and identify the intended base branch; do not include unrelated user changes.
2. Run the repository's relevant formatter, linter, and tests when practical. Report failures and do not claim the PR is ready if required checks fail.
3. Ensure the current branch has a suitable name and commit the requested changes only if they are not already committed. Never create a commit if the user asked only for a draft or explicitly said not to commit.
4. Push the branch to its remote. Before doing so, verify the remote and branch target; do not force-push.
5. Create the PR with `gh pr create`, including a concise summary and testing notes. Preserve the user's requested draft/ready state.
6. Trigger CodeRabbit on the created PR, normally with `gh pr comment <number> --body "/coderabbit review"` when that repository uses the CodeRabbit command. If the command or integration is unavailable, report that clearly rather than pretending review started.
7. Return the PR URL, base/head branches, check status, and whether CodeRabbit was successfully triggered.

## Safety

- This skill authorizes the PR workflow, including pushing the branch and creating the PR, but never force-pushes or alters unrelated changes.
- Ask before changing repository settings, enabling integrations, changing branch protection, or using a different remote.
