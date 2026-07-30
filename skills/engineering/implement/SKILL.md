---
name: implement
description: "Implement a piece of work based on a spec or set of tickets."
disable-model-invocation: true
---

Implement the work described by the user in the spec or tickets.

At the start, rename the current thread to `🔄 #<issue-number> - <issue-title>`. Preserve the status emoji exactly. For multiple tickets, use the primary ticket.

Before scoping implementation, read the repository's agent instructions. Follow its domain-doc router when present: read the domain glossary for vocabulary, relevant accepted ADRs for target behavior, and linked module specifications for detail. Treat superseded and deprecated ADRs as history, proposed ADRs as non-authoritative, and explicitly open or deferred contracts as unresolved. When accepted target behavior differs from current code, record an implementation gap rather than preserving the old behavior. Never guess an unresolved contract.

Before writing tests or code, build a reuse map. For every requirement, record its target authority, inspect the repository's existing behavior, conventions, and architectural seams, classify its domain state as aligned, gap, or open, then classify the implementation seam as reuse, extend, or create. Reuse or extend a fitting seam; when none fits, create the smallest coherent seam for the codebase. The map is complete when every requirement has a target authority, domain state, implementation seam, regression seam, and every proposed new abstraction has a concrete reason. Share it in the first progress update, then continue unless it reveals a blocker.

Use $tdd where possible, at pre-agreed seams.

Run typechecking regularly, single test files regularly, and the full test suite once at the end.

Once done, use $code-review to review the work. Resolve every actionable finding, including duplicated behavior, bypassed existing seams, and unnecessary new abstractions, before committing.

Commit your work to the current branch.

After all required work, tests, code review, and the commit are complete, rename the same thread by replacing `🔄` with `✅`. If required user input or authority prevents useful progress, replace `🔄` with `❌`.
