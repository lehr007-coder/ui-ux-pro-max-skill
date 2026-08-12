---
name: task-observer
description: Observe multi-step work to identify repeatable skill candidates and improvements to existing skills. Runs in proposal-only mode: never directly rewrites production skills, agent rules, hooks, MCP config, workflows, or runtime configuration.
---

# Task Observer — Safe PR Mode

## Purpose
Use the upstream Task Observer methodology from `tools/task-observer/` to notice recurring workflows, user corrections, successful techniques, gaps, and skill-improvement opportunities.

## Mandatory safety gate
This repository uses proposal-only operation.

1. Never directly modify an existing production skill, agent rule, hook, MCP configuration, runtime setting, workflow, or tool integration based solely on an observation.
2. Never self-modify this Task Observer skill in place.
3. Record observations first. Separate evidence from interpretation.
4. Any proposed skill change must be placed on a new Git branch and surfaced as a pull request against `main`.
5. The pull request must explain: evidence observed, affected skill(s), exact proposed change, expected benefit, conflict/overlap risks, tests or validation performed, and rollback path.
6. Do not merge a Task Observer-generated change automatically unless the user explicitly requests the merge after the proposal exists.
7. Do not commit secrets, credentials, cookies, private tokens, personal data, or sensitive session content to observation logs or PRs. Redact or summarize sensitive evidence.
8. Prefer improving an existing skill over creating a duplicate skill when their scopes substantially overlap.
9. Check for conflicts with gstack, ECC, Ruflo, Claude-Mem, Video Editor Agent, Video Shotcraft, Taste, UI UX Pro Max, Agent Reach, LiteLLM, MarkItDown, Code Review Graph, and other installed components before proposing changes.

## Upstream reference
The pinned upstream implementation is available at `tools/task-observer/`. Read its `SKILL.md` and files under `tools/task-observer/references/` when needed. Preserve upstream attribution and licensing when adapting material.

## Observation workflow
During substantive multi-step tasks, watch for:
- repeated user corrections or preferences;
- repeated sequences of tools/actions;
- recurring failures or omissions;
- techniques that consistently improve results;
- instructions repeatedly supplied manually;
- missing QA, safety, or handoff steps;
- tasks that recur often enough to justify a reusable skill.

For each useful observation, capture: date/task context, evidence, affected skill or new-skill candidate, confidence, proposed improvement, and any risk/conflict notes.

## Change workflow
When an improvement is ready to implement:

```text
OBSERVE
  ↓
LOG EVIDENCE
  ↓
DRAFT CHANGE
  ↓
CREATE BRANCH
  ↓
IMPLEMENT + TEST
  ↓
OPEN PR
  ↓
USER/MAINTAINER REVIEW
  ↓
MERGE ONLY AFTER APPROVAL
```

If repository write tools are unavailable, produce a structured handoff document instead of pretending the change was made.

## Review standard
Do not propose changes merely because something happened once. Prefer patterns supported by repeated evidence or a high-impact correction. Keep recommendations specific, reversible, testable, and narrowly scoped.
