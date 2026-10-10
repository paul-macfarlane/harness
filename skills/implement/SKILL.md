---
name: implement
description: Plan, build, test and review features, a refactor or a bug fix in one pass, ending in a PR per work package. Use after /grill (and /design-ui for UI), or directly for refactors and bugs.
---

Input: feature names from the features table in `docs/requirements.md`, a feature doc area (all the rows it covers), or a description of a refactor or bug. With no input, list the ready features and ask which to build.

## Ready
If the features table has no Status column, propose adding it and stop. Check each feature is ready. If one isn't, say which step to go back to (`/grill` or `/design-ui`) and skip it:
- its row has a use case and Status `todo`, and no open PR covers it
- no open question in its feature doc or `docs/requirements.md` affects it
- if it has UI, its feature doc links approved screens

For a bug or refactor, only check that any change visible in the UI has approved screens.

Group features that share a feature doc into one work package, each on its own branch. Build what a feature depends on first, branching from that work if it isn't merged yet. Run work packages in parallel worktrees only when none is large or risky (the red-team list in the standards) and they share no feature docs or code areas. Otherwise run them one after another.

## Plan
1. Read `docs/requirements.md`, the feature docs the work touches, `docs/architecture.md`, the project `CLAUDE.md` and the relevant code.
2. If the work needs a new or changed architecture or tech stack decision, get Paul's decision as the standards describe and record it in `docs/architecture.md` before planning further.
3. Write the plan to `docs/work/<slug>.md`: the approach, the tests (per the engineering practice in the standards), and any implementation choice that affects a requirement.
4. If the work is large or risky, red-team the plan as the standards describe, revise it, then show Paul the behavior change and any requirement-affecting choices and wait for his go-ahead.

## Build
Build it with its tests. Run the fast tests and the e2e tests for the core journeys it touches until they pass. For UI, screenshot each changed screen at phone and desktop widths.

## Review
Review in a fresh-context subagent on two axes. Fix what it finds and review again until nothing fixable is left; if a finding survives three rounds, hold the work for Paul.
- **Spec:** does the change do what the requirements, feature docs, approved screens (compare the screenshots) and work package say, and nothing more? Flag any unrequested feature or scope creep.
- **Standards:** check against `docs/architecture.md` (no unapproved stack or structural changes) and the goals and engineering practice in the standards. Doc or feature changes this reveals (repeated text, overlapping features) are proposals for Paul, not fixes.

## Finish
Set the Status of each row the work completes to `done`, delete the work package, and open a PR with the screenshots, the decisions from the work package and the summary from the standards. If Paul approves requirement changes from the summary, put them in the docs on the branch before he merges.

When something needs Paul (a large plan's go-ahead, ambiguity in the docs, or anything the standards say comes back to him), hold that work package with the question in it and carry on with the rest. Decide anything else yourself and note it in the work package. End the run with the PRs opened and anything held for Paul.
