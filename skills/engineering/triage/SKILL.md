---
name: triage
description: Manage GitHub Issues through the Countries development lifecycle from ready-for-agent to verified. Use when selecting agent-ready work, claiming an issue, recording implementation, coordinating behavior verification and human code review, requesting revisions, completing verification, or auditing lifecycle-label consistency. Also maintain non-lifecycle descriptive labels such as bug or enhancement without treating them as workflow states.
---

# Countries Issue Lifecycle

Manage Issues in the repository named by `Docs/project/issue-tracker.md`. Read `Docs/project/triage-labels.md` before changing labels.

## Lifecycle labels

Use these labels as controlled workflow state:

1. `ready-for-agent` — fully specified and available for an AFK agent.
2. `agent-in-progress` — an AI agent is executing the PRD; implementation is incomplete.
3. `implemented-unverified` — implementation is complete and awaits verification.
4. `behavior-verified` — black-box behavior matches expectations.
5. `code-reviewed` — a human reviewed the code; final verification is pending.
6. `needs-revision` — implementation requires changes before acceptance.
7. `verified` — verification is complete and the work is accepted.

Treat `behavior-verified` and `code-reviewed` as parallel gates that may coexist. Treat every other lifecycle label as mutually exclusive with them and with each other.

## Descriptive labels

Treat all other labels as supplemental metadata, never as lifecycle state. They may describe issue type, impact, scope, difficulty, ownership, or collaboration needs. The set changes over time, so query the tracker instead of hard-coding a closed vocabulary.

Known examples include `bug`, `duplicate`, `enhancement`, `good first issue`, `help wanted`, `invalid`, `question`, and `wontfix`.

Do not remove descriptive labels during a lifecycle transition unless the user explicitly requests it or a label is demonstrably contradictory. In particular, `wontfix` is descriptive in this system and is not one of the development-cycle states.

## Workflow

1. Read the Issue body, comments, current labels, and linked PRD or evidence.
2. Identify its current lifecycle state and preserve relevant descriptive labels.
3. Check that the requested transition is supported by evidence.
4. State the proposed label removals, additions, comments, and close/reopen action before mutating GitHub.
5. Apply the transition with the issue-tracker workflow.
6. Re-read the Issue and report the resulting labels as verification.

Never infer that implementation, verification, review, or acceptance occurred merely from code or label age. Require explicit evidence from the current task, test results, reviewer statement, or maintainer instruction.

## Transitions

- Claim work: `ready-for-agent` -> `agent-in-progress`.
- Finish implementation: `agent-in-progress` -> `implemented-unverified`.
- Record black-box verification: `implemented-unverified` -> `behavior-verified`.
- Record human code review: `implemented-unverified` -> `code-reviewed`.
- When one verification gate already exists, add the other without removing the first.
- Accept only after both `behavior-verified` and `code-reviewed` exist: remove both and add `verified`.
- Request changes from `implemented-unverified`, `behavior-verified`, or `code-reviewed`: remove active verification labels and add `needs-revision`.
- Resume revision work: `needs-revision` -> `agent-in-progress`.
- Return a prematurely claimed Issue: `agent-in-progress` -> `ready-for-agent` only on explicit instruction.

Do not skip intermediate evidence gates unless the maintainer explicitly overrides the workflow. Flag unexpected or conflicting lifecycle labels before changing anything.

## Common operations

### Show available work

List open Issues labeled `ready-for-agent`, oldest first. Summarize the PRD, dependencies, and relevant descriptive labels. Do not claim one until instructed.

### Claim an Issue

Confirm it is `ready-for-agent`, add `agent-in-progress`, and remove `ready-for-agent`. Comment only when requested or when the repository workflow requires an execution note.

### Record implementation

Require implementation evidence and proportionate test results. Replace `agent-in-progress` with `implemented-unverified`. Do not claim behavior verification or human review.

### Record verification or review

For `behavior-verified`, cite black-box evidence. For `code-reviewed`, require an explicit human review outcome. Preserve the other gate when present. If both gates are present, report that the Issue is eligible for `verified`; do not mark it accepted without maintainer instruction.

### Mark verified

Require both verification gates or an explicit maintainer override. Replace active lifecycle labels with `verified`. Close the Issue only when explicitly requested or when its PRD states that verified Issues are closed.

### Audit lifecycle labels

List open Issues carrying lifecycle labels. Report invalid combinations, missing stages, stale `agent-in-progress` work, and evidence gaps. Do not repair them without instruction.

## Safety

- Treat GitHub label changes, comments, and closing as external mutations.
- Do not create, rename, or delete repository labels unless explicitly requested.
- Do not treat external pull requests as the request surface unless `Docs/project/issue-tracker.md` says otherwise.
- Keep Issue comments concise and factual; distinguish observed evidence from inference.
