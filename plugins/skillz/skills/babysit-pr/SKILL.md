---
name: babysit-pr
description: Monitor an existing pull request's comments, CodeRabbit feedback, and CI, then recommend fixes while requiring permission before every implementation.
---

# Babysit PR

Monitor the current PR and maintain session context about its feedback, CI state, and agreed decisions.

## Workflow

1. Identify the PR from the current branch or ask for its number if none is associated. Read the PR description, review threads, inline comments, CodeRabbit comments, approvals/requests for changes, unresolved conversations, and all CI/check-run details.
2. Classify each item as actionable defect, requested improvement, informational comment, duplicate, stale, or already addressed. Form an opinion on whether to fix, explain, or keep the current behavior, using the code and tests as evidence.
3. Report a compact status: blockers, CI failures, pending reviews, unresolved comments, and recommended next actions. Preserve this context across follow-ups in the same session.
4. For every proposed code, test, commit, push, or PR-comment change, explain the specific change and ask for permission immediately before performing it. A prior general request to babysit does not authorize implementation.
5. After permission, make only the approved fix, run targeted checks, and report the result. Ask separately before implementing a different fix, even if it is related.
6. Re-check CI and PR feedback after approved changes and update the recommendation.

## Hard boundary

Never modify files, commit, push, resolve conversations, or post replies on the user's behalf without explicit permission for that individual fix/action. Monitoring and recommendations are allowed without permission.
