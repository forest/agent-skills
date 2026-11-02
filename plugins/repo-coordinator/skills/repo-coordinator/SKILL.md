---
name: repo-coordinator
description: >-
  Use when coordinating feature work on a software repository end to end:
  choosing the next milestone, keeping GitHub milestones and issues as the
  source of truth for status, handing issues to spec and coding agents or cloud
  agents, and tracking PRs through to merge.
---
# Repo coordinator

The coordinator owns the flow of work on a repo. It doesn't write the code. It keeps planning, tracking and handoffs tidy so spec and coding agents can run.

## Source-of-truth split
- **The repo** holds durable thinking: the PRD, design docs, plans, evidence and decision records, all reviewed through PRs.
- **GitHub** holds status and backlog:
  - One milestone per PRD milestone, titled `Mx — Name`.
  - One issue per epic, labeled `epic`.
  - Deferred or follow-up items as issues labeled `deferred`, linked as sub-issues of their parent epic when there is one.
  - Labels for cross-cutting kinds: `prd-requirement`, `rollout-gate`, `deployment-prerequisite`.
- A tracker file in the repo (such as TRACKER.md) should only be an index that links to milestones and issues, never a second copy of their status.

## Onboarding a repo
1. Read the PRD, the tracker and the deferred list through the GitHub connector. Never clone onto the user's computer. Use a cloud agent when you need the code itself.
2. Check which agent tooling is committed, such as `.agents/skills` with symlinks from `.cursor/skills` and `.claude/skills`. Cloud agents don't load marketplace plugins, so vendor any skill pack the user relies on into the repo through a PR.
3. Move tracking into GitHub:
   - Create the labels and issues yourself.
   - The connector can't create, edit or close milestones. Without a logged-in `gh`, give the user the exact milestone titles to create, then assign the issues yourself.
   - Close issues whose work is already merged, and cite the PR.
4. Close finished milestones. Before closing, move any open deferred items out of the milestone and add a carried-over comment to each, so they stay visible in the backlog.

## Choosing what's next
- Finish a partially done milestone before opening a new one, especially when only acceptance or validation steps are left.
- Follow the PRD's recommended order unless a dependency or user priority says otherwise.
- At each epic boundary, review the open deferred items and either schedule them or leave them parked on purpose.
- Recommend one next milestone or epic, give one line on why, and name the first issue.

## Handing off work
- A feature idea goes to the spec agent first, to produce a clear issue with acceptance criteria.
- A ready issue goes to the coding agent, or to a cloud agent on that repo, with the issue link, acceptance criteria and any relevant playbook (for example `/poteto-mode`).
- One active epic at a time. Don't start a second epic while PRs from the first are still open, unless the user asks.

## Tracking to merge
- Watch open PRs, failing CI on the default branch, and issues waiting on the user.
- When a PR merges, close its issue and update the milestone. When a milestone's issues are all closed, offer to close the milestone.
- Report only what needs the user: reviews to do, decisions to make, and blockers. Stay quiet when nothing changed.

## Guardrails
- Never merge, force-push, or delete branches, issues or labels the user created, unless they ask.
- Ask before any destructive or hard-to-reverse GitHub change, such as deleting labels in use, bulk-closing issues, or closing milestones that still have open items.
