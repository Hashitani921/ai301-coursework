---
name: pr-precheck
description: Decide whether one candidate pull request is ready to submit by comparing its diff, claims, and tests with its accepted plan, issue, and repository requirements.
---

# pr-precheck: evidence-based PR readiness

## The question

Answer one question about one PR package: **is this ready to submit?** The package comprises an issue and thread, accepted plan and reproduction, candidate title and description, commits, branch diff, and test evidence. Compare the actual change and proof with the plan, issue, and stated repository rules. Do not grade issue selection, rewrite the implementation, or silently add checks.

## Inputs and modes

In **live mode**, first identify the target issue and PR or draft. Read the student's `plan.md` including `## Deviations`, the branch's committed `git diff main...HEAD` (three dots) from the fork checkout, the draft PR title and description in `pr_draft.md` or the PR page, and recorded command/output in `test_evidence.md`. Read the issue body and relevant thread, the repository PR template, `docs/CONTRIBUTING.md` or equivalent, and any stated policy. When a house-chain assignment replaces the student's own change, read its house issue, repro pack, plan, diff, draft, and test evidence under the same checks. Report inaccessible inputs; never substitute an uncommitted working-tree edit for the branch diff.

In **eval mode**, the named bundle is the whole world. Read its Repo facts, Issue, Thread highlights, Plan context including repro and deviations, and Candidate PR title, description, commits, diff, and test evidence. Fetch nothing and read no other files. Run every rubric check and the complete verdict rule for that one bundle.

## The scope seam (live mode only)

Read `scope.md` before any live grading. If its `Repo:` entry remains a placeholder, stop without a verdict and tell the student to fill it with the section's Path Review repo. Refuse to grade a PR outside the named repo. Apply the house rules in scope, including fork-to-upstream targeting. Ignore `scope.md` entirely in eval mode.

## The voice seam (live mode only)

Read `voice-guide.md` in live mode and compare the outgoing PR title and description with its rules. Quote any broken rule in the readable summary. Voice alone does not change the verdict unless a named rubric check also fails. Ignore `voice-guide.md` entirely in eval mode.

## Component reads

Read `rubric.md` for the exact checks, weights, and verdict rule; `references/evidence-guide.md` for the location and meaning of each evidence family; and `procedure.md` for the read, gathering, grading, and output sequence. Execute the procedure as written. If a needed step is absent, report that gap instead of inventing it. If the rubric contains no authored checks/verdict rule or the procedure has no authored steps, refuse to grade and identify the empty component.

## Verdict and output

The only verdicts are `accept` (ready to submit) and `reject` (hold). Give a concise per-check summary if useful. End with one valid fenced JSON block matching this schema exactly, in this key order, with nothing after it:

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

Name a concrete fact or quote for every grade. Judge the implementation and observable evidence, not length, formatting, or polish: a terse complete PR can pass and a polished drifting one must fail. Apply the rubric's written pass conditions even if intuition disagrees; revise the rubric later, not a single run. Follow the procedure rather than improvising hidden steps. If a necessary claim cannot be verified from the allowed package, grade it `unclear`; under the rubric's verdict rule a required `unclear` holds the PR. Do not turn an honestly documented, plan-recorded shortfall into silent drift, and do not treat a full test-suite command as proof of the issue's specific behavior without an observable result.
