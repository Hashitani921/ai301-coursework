# Procedure: how this tool grades a PR package

## Read order

1. Identify one PR URL or eval bundle id and the mode. Live: read `scope.md` first, confirm the target repo and fork branch, refuse an unfilled scope or an out-of-scope PR, then read `voice-guide.md`. Eval: ignore both files and never fetch outside the bundle.
2. Read this procedure, `rubric.md`, and `references/evidence-guide.md`; write down every named check, its weight, and the verdict rule. Stop if rubric or procedure is still an empty template.
3. Read the issue, relevant maintainer thread, and repo rules/template first. Record the requested behavior, constraints, and mandatory PR asks. Next read the accepted plan's repro, scope, exclusions, tests, and deviations. This fixes the comparison baseline before seeing the candidate's claims.
4. Read the **entire** committed diff (`git diff main...HEAD` in live mode) and commits. Record each changed file and behavior hunk. Then read title, description, and test evidence. Do not let a description substitute for a hunk or a test result.

## Evidence gathering

1. Make a small ledger with one row per rubric check and a source quote/fact. For plan fidelity, pair every changed file and behavior hunk with the plan's promised change or a recorded deviation; pair every promised deliverable with a hunk or an explicit deferral. Look both for extra work and for missing work.
2. For claim accuracy, list concrete assertions in title/description (`fixed`, `added`, `unchanged`, limits, test claims) and verify each against the diff, plan deviation, and test output. An honest limitation is recorded, not treated as hidden drift.
3. For decisive tests, extract the repro input/action and original wrong observation from the plan. Pair each claimed fixed path with the test-evidence input and actual after observation; check a control where the change could regress it. Verify that added regression tests assert the changed behavior. Separately record named repository check commands and outcomes, plus any stated explanation for skips or failures.
4. For diff quality, inspect every hunk and the commit list for debug statements, dead/commented-out attempts, unrelated files, mechanical churn, and hidden behavior beyond the issue. For standards, enumerate each *stated* template section, issue link, required test/doc/change-log item, disclosure policy, and maintainer request from repo facts; pair each with the candidate's response. Never create a rule from silence.
5. In live mode, gather issue-side evidence from the real repo and record URLs/date for anything not in local files. Compare the outgoing title and description with voice-guide rules. In eval mode, do not consult live issues, other bundles, or gold labels.

## Check execution

1. Execute the checks in rubric table order, including preferred checks and every check after a failure. For each, apply the written pass condition to its mapped evidence rather than intuition.
2. Grade `pass` only with an observed satisfying fact; `fail` for an observed contradiction, a required omitted artifact, or inadequate proof; `unclear` only when a necessary fact remains genuinely inaccessible after rechecking the mapped sections. Never fill a gap with an imagined test or unstated policy.
3. Put the deciding source fact or brief quote on one evidence line. For a negative grade, name the exact unplanned hunk, missing repro observation, leftover debris, or unmet repository ask. Review the ledger once for contradictions; adjust affected grades using the same written rule.

## Verdict assembly

1. Apply the rubric literally: `accept` iff all required checks pass; otherwise `reject`. A required `unclear` holds. Preferred grades neither veto nor rescue. Quote the first failing required check in rubric order in the readable summary; if several fail, name each briefly.
2. Verify each rubric check appears exactly once, in table order, with a valid grade and one-line evidence. Live: report any voice rule violation or source/procedure limitation before the JSON; voice alone cannot change the verdict.
3. Finish with the exact fenced JSON schema in `SKILL.md`, using the PR URL or bundle id as `item`. Nothing follows that block. This procedure reviews; it does not post, push, or edit the PR.
