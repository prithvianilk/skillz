---
name: auto-pr
description: Take current repository changes through pull request creation, CodeRabbit and CI monitoring, final review audit, and merge when every gate is clear. Use when the user asks for an automatic PR workflow, says auto PR, or explicitly requests raise, babysit, and merge as one operation.
---

# Auto PR

Orchestrate the plugin's existing PR skills without duplicating their workflows.

## Required skills

Use these skills as the source of truth for their stages:

- `$raise-pr`
- `$babysit-pr`
- `$merge-pr`

Load and follow each skill when its stage begins. If one is unavailable, report the missing skill and stop instead of recreating its behavior here.

## Workflow

1. Use `$raise-pr` for the current changes. Preserve the resulting PR number, URL, base branch, head branch, and reported check state for the remaining stages.
2. Use `$babysit-pr` on that PR. Continue its monitoring stage while CI or reviews are actively progressing, using bounded waits and concise updates.
3. Preserve `$babysit-pr`'s permission boundary. If feedback requires code, tests, commits, pushes, replies, or conversation resolution, pause the automatic flow and request the permission that skill requires. After an approved change, return to its monitoring stage.
4. When `$babysit-pr` reports no failing or pending gates and recommends merging, use `$merge-pr` on the same PR.
5. Return the final PR and merge status. If any stage stops, report its blocker and do not skip ahead.

## Authorization

Invoking `$auto-pr` authorizes the raise and merge stages for the PR it creates or identifies, subject to the safeguards in their skills. It does not override `$babysit-pr`'s approval requirements and does not authorize deployment or unrelated repository changes.
