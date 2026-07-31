---
name: implement
description: "Implement a piece of work based on a spec or set of tickets."
disable-model-invocation: true
---

Implement the work described by the user in the spec or tickets.

Use /tdd where possible, at pre-agreed seams.

Run typechecking regularly, single test files regularly, and the full test suite once at the end.

Once done, use /code-review to review the work.

Commit your work to the current branch.

When the work has an associated issue-tracker item, post the implementation report after the commit succeeds. Start the report with one of these level-one Markdown headings so its purpose is visually distinct in the issue timeline:

- Use `# Feat Commit Report — <commit SHA>` when the commit substantially implements the Issue.
- Use `# Correction Commit Report — <commit SHA>` when the commit corrects findings from review or verification.

Include the implemented or corrected scope, verification results, and any remaining debt or follow-up work.
