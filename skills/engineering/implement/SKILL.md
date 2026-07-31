---
name: implement
description: "Implement a piece of work based on a spec or set of tickets."
disable-model-invocation: true
---

# Implement

Implement the work described by the supplied spec or tickets on the current branch.

## 1. Pin the scope and review base

Read the full spec or every supplied ticket, including any linked blocking tickets. Identify the acceptance criteria, pre-agreed public seams, and the capability each blocker supplies. Inspect the current code at those seams. Inherit blocker-supplied seams by reusing or extending them; create a seam only when no fitting one exists.

Capture the current commit with `git rev-parse HEAD`; keep that exact SHA as the review base. Also inspect `git status --short` so pre-existing work remains distinguishable from this implementation.

Start implementation when every acceptance criterion has an identified public seam, every inherited capability is present on the current branch, and the review-base SHA resolves.

## 2. Build through the seams

Run `$tdd` and implement one vertical red-green slice at a time through the pre-agreed seams. After each slice, run its narrow test and any directly affected typecheck.

This step is complete when every acceptance criterion works through its agreed public seam and the targeted tests are green.

## 3. Validate and create the review commit

Run the repository's full required validation suite.

Stage only the in-scope files and commit them to the current branch. This review commit must exist because `$code-review` compares committed `HEAD` with a fixed point.

This step is complete when the required checks pass, the review-base-to-`HEAD` diff is non-empty, and every in-scope change is committed.

## 4. Review the committed range

Run `$code-review` with the exact review-base SHA and the originating spec or tickets. Resolve every actionable finding, rerun the affected checks, stage only the review fixes, and amend the review commit. Repeat the review after any amendment.

Implementation is complete when both review axes have no actionable findings, the required checks pass on the reviewed `HEAD`, and every in-scope change is committed.
