# Evidence guide: where evidence lives in a PR package

Use only the named eval bundle in eval mode. In live mode use the issue/thread and repo's stated policy plus the student's `plan.md`, committed branch diff, `pr_draft.md`, and `test_evidence.md`. Treat statements in a PR description as claims to verify, not as proof that the diff or test did them.

## Plan fidelity (harness category: silent-drift)

- **Eval location:** Plan context's scope, file list, exclusions, test plan, and any deviation note; Candidate PR's entire unified diff, commits, title, and description; Issue and Thread highlights for requested behavior.
- **Live location:** `plan.md` including `## Deviations`, the issue and maintainer thread, `git diff main...HEAD` and its file list, and the outgoing PR title/description.
- **Good:** Each changed behavior is necessary for the plan or specifically justified as a deviation, and each promised part is implemented or explicitly deferred in the plan and description. Tests and docs directly supporting the fix are within scope. Silent addition of a new flag/config option or silent omission of promised docs is drift even if the description sounds confident. A documented narrower outcome is judged on that stated scope.

## Test evidence (harness category: not-tested)

- **Eval location:** Plan context's repro input, wrong output, expected result, controls, and test plan; Candidate PR's Test evidence and added test hunks; Repo facts' stated checks.
- **Live location:** Posted repro/plan, `test_evidence.md` with actual commands and stdout/stderr, test hunks in the branch diff, `pr_draft.md` Testing, and repo `Makefile` / contribution instructions.
- **Good:** The exact changed path is exercised, with an observable before/after or equivalent target assertion and relevant controls. Each claimed fixed failure mode has evidence; a plan-recorded deferral narrows the claim. The result of relevant repo checks is visible, and a failed/skipped check is explained truthfully. `tests pass` with no named behavior, an unrelated control test, or an unrun required check does not establish readiness.

## Diff quality (harness category: unreviewable)

- **Eval location:** Every unified-diff hunk and the Candidate PR commit list, compared with the Plan context's file boundary.
- **Live location:** `git diff main...HEAD --stat` and the full three-dot diff from the fork's branch; commit history and `plan.md`.
- **Good:** The fix and directly related tests are easy to isolate. Debug prints, commented-out attempts, dead helpers, unrelated import rewrites, or broad reformatting are removed before submission. A terse or imperfect commit message does not by itself make a focused diff unreviewable.

## Standards and comms (harness category: standards-wall)

- **Eval location:** Repo facts' PR template, contribution/AI policies, and Thread highlights; Candidate PR title, description, changed files, and test evidence.
- **Live location:** The target repo's `.github/PULL_REQUEST_TEMPLATE.md`, `docs/CONTRIBUTING.md` or equivalent and linked policies, maintainer issue comments, `pr_draft.md`, branch diff, and `scope.md`. Compare the title/description to `voice-guide.md` only in live mode.
- **Good:** Each applicable, explicit request is met with substantive content: the issue link, required checklist or sections, any required docs/tests, and an AI-use disclosure with tool and extent if policy or course instructions require one. When an eval repo requires disclosure of **all** AI use, treat the candidate as AI-assisted for that policy. Do not infer a disclosure policy merely from a human-authorship guideline or from the presence of a generic AI policy. Do not let perfect template prose override a contrary diff.
