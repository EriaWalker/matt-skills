---
name: triage
description: Triage Terra GitHub issues and move them through the Terra delivery lifecycle.
disable-model-invocation: true
---

# Triage

Triage GitHub issues for Terra. Do not use external pull requests as a triage surface.

Read these project rules before changing an issue:

- `Docs/project/issue-tracker.md`
- `Docs/project/triage-labels.md`
- `Docs/project/agent-domain.md`
- [AGENT-BRIEF.md](AGENT-BRIEF.md)

Use concise, factual comments. Do not add a fixed AI disclaimer. Do not create or write `.out-of-scope/`.

## Labels and lifecycle

Every triaged issue has exactly one category label: `bug` or `enhancement`. Category labels coexist with one lifecycle label and supplemental labels.

Use the Terra lifecycle:

```text
needs-triage or needs-info
  -> ready-for-agent
  -> agent-in-progress
  -> implemented-unverified
  -> behavior-verified + code-reviewed
  -> verified
```

- `needs-triage` — initial evaluation is needed.
- `needs-info` — required information is missing. Move it back to `needs-triage` after a useful reply.
- `ready-for-agent` — fully specified and safe for an AFK agent.
- `agent-in-progress` — an agent has claimed the work.
- `implemented-unverified` — implementation exists but needs verification.
- `behavior-verified` and `code-reviewed` — both are required before `verified`.
- `ready-for-human` — an inbound or manual exit for work that requires a person.
- `wontfix` — record the reason, add the label, and close the issue.

Remove obsolete lifecycle labels when applying the next state. Ask before an unusual transition or when the issue has conflicting lifecycle labels.

## Wayfinding

A `wayfinder:map` issue is a planning map. Keep it out of the delivery lifecycle.

Create executable AFK decision tickets as GitHub sub-issues. Give each child one `wayfinder:<type>` label (`research`, `prototype`, `grilling`, or `task`) plus its required category label.

- Only executable AFK tickets enter `ready-for-agent` and the normal Terra lifecycle.
- `grilling` and `prototype` tickets that require human input close as `decision resolved`; do not force them through implementation and verification.
- You may create `wayfinder:*` labels, sub-issue relationships, and documented blocking relationships when the Wayfinder workflow requires them.

## Process

### 1. Show attention

Query GitHub Issues and show these buckets, oldest first:

1. Unlabeled issues.
2. `needs-triage` issues.
3. `needs-info` issues with new reporter activity.
4. Issues that block a ready item.

Show the category, lifecycle state, and a one-line summary. Let the maintainer choose an item.

### 2. Gather evidence

Read the issue body, comments, labels, author, and dates. Read prior triage notes before asking again. Explore the codebase using the domain docs and relevant ADRs.

Check whether the requested behavior already exists. Report the code locations and evidence. For a bug, reproduce the reported steps when possible. Report confirmed, disproved, or insufficient detail.

### 3. Recommend and decide

Recommend one category and one lifecycle outcome. Explain the relevant codebase context and evidence. Wait for maintainer direction before applying a non-trivial outcome.

Use `/grilling` and `/domain-modeling` one question at a time when the issue needs decisions. Preserve resolved decisions in the issue brief and appropriate domain docs.

### 4. Apply the outcome

- `ready-for-agent` — post an agent brief and apply the label.
- `ready-for-human` — post the same structure, state why human work is required, and apply the label.
- `needs-info` — post specific, actionable unanswered questions.
- `wontfix` — state the reason, apply the label, and close the issue.
- `implemented-unverified` — record the implementation commit and verification still required.
- `verified` — require behavior evidence and `code-reviewed` before applying it.

When implementation completes, retain Terra Commit Report rules. Record a `Feat Commit Report — <commit SHA>` or `Correction Commit Report — <commit SHA>` with scope, verification results, and remaining debt or follow-up.

## Quick overrides

When the maintainer gives an explicit state change, confirm the labels, comment, and close action, then apply it. Do not start a grilling session unless they ask for one.

## Needs-info template

```markdown
## Triage Notes

**What we established:**

- point 1

**What we still need from you (@reporter):**

- specific question
```

When resuming, read existing triage notes, identify newly answered questions, and do not re-ask resolved questions.
