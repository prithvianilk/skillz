---
name: babysit-pr
description: Request Codex and CodeRabbit reviews, monitor an existing pull request's feedback and CI, then recommend fixes while requiring permission before every implementation.
---

# Babysit PR

Monitor the current PR and maintain session context about its feedback, CI state, and agreed decisions.

## Workflow

1. Identify the PR from the current branch or ask for its number if none is associated.
2. For the current head commit, request both reviews unless each has already been requested: post `@codex review` to ask Codex and `/coderabbit review` to ask CodeRabbit. Invoking this skill authorizes only these two review-request comments; do not post any other comment without explicit permission.
3. Read the PR description, review threads, inline comments, Codex and CodeRabbit feedback, approvals/requests for changes, unresolved conversations, and all CI/check-run details.
4. Classify each item as actionable defect, requested improvement, informational comment, duplicate, stale, or already addressed. Form an opinion on whether to fix, explain, or keep the current behavior, using the code and tests as evidence.
5. Report a compact status: blockers, CI failures, pending reviews, unresolved comments, and recommended next actions. Preserve this context across follow-ups in the same session.
6. For every proposed code, test, commit, push, or other PR-comment change, explain the specific change and ask for permission immediately before performing it. A prior general request to babysit does not authorize implementation.
7. After permission, make only the approved fix, run targeted checks, and report the result. Ask separately before implementing a different fix, even if it is related.
8. Re-check CI and PR feedback after approved changes and update the recommendation.

## Hard boundary

Never modify files, commit, push, resolve conversations, or post replies on the user's behalf without explicit permission for that individual fix/action. The only pre-authorized PR comments are the `@codex review` and `/coderabbit review` requests described above. Monitoring and recommendations are allowed without permission.
