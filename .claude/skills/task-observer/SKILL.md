---
name: task-observer
description: Observe multi-step work to identify repeatable skill candidates and improvements to existing skills. Proposal-only mode: all changes to production skills/configuration must go through a separate Git branch and pull request; never silently self-modify.
---

# Task Observer — Safe PR Mode

Use the pinned upstream implementation at `tools/task-observer/` as the reference methodology. Observe recurring work, corrections, preferences, failures, and successful patterns, but do not directly rewrite production skills or configuration.

## Non-negotiable controls
- Never directly modify production skills, rules, hooks, MCP configuration, runtime configuration, workflows, or this observer based only on an observation.
- Never expose or commit secrets, credentials, cookies, tokens, personal data, or sensitive session content.
- For every proposed change: create a branch, implement narrowly, validate, and open a PR against `main`.
- PR body must state evidence, affected components, exact change, benefit, overlap/conflict risks, validation, and rollback.
- Do not auto-merge observer-generated PRs. Merge only after explicit user/maintainer approval.
- Prefer improving an existing skill over duplicating it.
- Check overlap with gstack, ECC, Ruflo, Claude-Mem, Video Editor Agent, Video Shotcraft, Taste, UI UX Pro Max, Agent Reach, LiteLLM, MarkItDown, Code Review Graph, and other installed components.

## Workflow
Observe → log evidence → draft improvement → create branch → implement/test → open PR → review → merge only after approval.

Read `tools/task-observer/SKILL.md` and its `references/` files for the upstream methodology when needed. If GitHub write access is unavailable, output a structured handoff rather than claiming a change was made.
