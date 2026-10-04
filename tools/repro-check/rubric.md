# Rubric: is this reproduction package ready to post?

Judge whether a maintainer can verify what was tried and what happened.
Grade the evidence against the issue, not the length, confidence, or
formatting of the comments. This rubric checks readiness to post; it
does not require a fix or a proven root cause.

## How to grade

Read the issue and thread context, repo facts, claim comment, and repro
report before assigning grades. In eval mode, use only the frozen
bundle; do not browse the live issue or assume missing artifacts exist.
In live mode, use the issue and repository documentation plus the
evidence contained in or quoted by the drafts, following `SKILL.md`.

For every check, record one grade and one deciding quote or fact:

- **P / `pass`:** the supplied evidence satisfies the whole pass condition.
- **F / `fail`:** the supplied evidence contradicts the condition or
  demonstrates a violation. Name the mismatch.
- **? / `unclear`:** evidence needed to decide is missing or genuinely
  ambiguous after reading the whole package. Name what is missing;
  do not fill the gap with assumptions.

Use facts across the package when their connection to the candidate's
run is explicit. The original reporter's environment or output is not
automatically evidence of the candidate's environment or run. A short
report can pass; headings, word counts, and a fixed number of steps are
not requirements.

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| claim-specific-and-respectful | Candidate claim comment, read against the issue's trigger or symptom and relevant thread context. | The claim identifies this issue through a concrete detail and states a relevant next action, such as reproducing, investigating, or independently testing a proposed fix. It distinguishes intended work from completed work and avoids blame, demands, unsupported certainty, or promises of a guaranteed fix. Another contributor's interest alone is not a reason to fail; apply any explicit coordination rule from the repo or live scope. | required |
| environment-identifiable | Repro report's environment record and version/build output, compared with the issue's target environment and the repo-facts template requests. | The tested project release or commit and operating system/platform are recorded, along with runtime, dependency, installation, or build details needed to interpret and repeat this particular run. For example, record the build profile when debug and release behavior differ. Material differences from the reporter's setup are acknowledged and the conclusion is limited accordingly. An identical environment is not required. | required |
| steps-rerunnable | Repro report's setup, commands or UI actions, input/configuration, and any explicitly identified repository instructions, compared with the issue's prerequisites. | A stranger can reconstruct the relevant starting state and follow the attempt through its final observation without inventing an input, command, flag, prerequisite, or UI action. Include the actual relevant input/configuration or an unambiguous included reference. Use the project's documented setup where supplied, or explain relevant deviations. A bare instruction such as "set up normally" or "run the test" is insufficient when essential details are otherwise absent. | required |
| proof-tests-the-issue | Candidate run's output excerpts, logs, test results, or concrete UI observations, read against the issue's input, trigger, expected behavior, and reported symptom, and the candidate's stated outcome and limitations. | Pass either of two evidenced outcomes. (1) Claimed reproduction: a materially faithful trigger produces the behavior the issue describes, not merely some failure. (2) Explicit cannot-reproduce attempt: followable steps exercise the relevant operation, artifacts show the actual result, and the report identifies material differences or trigger conditions it could not establish. The second outcome does not require proof that every original trigger was achieved; it must limit its conclusion to the unsuccessful attempt, without claiming the issue is absent or fixed. A setup failure, malformed substitute input, or unrelated error that prevents reaching the relevant operation does not establish either outcome. Exact stack traces or identical wording are unnecessary when the same behavior is demonstrably shown. | required |
| outcome-supported-and-honest | Repro report's expected/actual outcome and conclusions, plus factual claims of completed reproduction in the claim comment, compared with the candidate's supplied artifacts and environment record. | The package makes clear what should happen, what actually happened, and whether the issue was reproduced in the tested setup. Every claimed result is supported by the supplied evidence; hypotheses about causes are identified as hypotheses. It does not label an adjacent error as confirmation, declare a bug fixed because one attempt did not reproduce it, or generalize to untested versions/platforms. An evidenced and appropriately limited cannot-reproduce result passes. "Reproduced" or "same here" alone is not proof. | required |
| repo-conventions-followed | Repo-facts bug-report/template and contribution requirements, compared with the claim comment and repro report; in live mode, the corresponding repository docs and applicable scope rules. | The comments supply the information and follow the reporting/coordination rules explicitly requested for this kind of contribution. Equivalent wording or organization is acceptable unless the repository requires a particular format. Do not invent requirements or apply PR-only restrictions to issue comments. With no additional applicable convention stated, pass this check; missing information explicitly requested by the repo prevents a pass. AI-use requirements are graded separately below. | required |
| ai-policy-followed | Repo-facts AI-use policy, the package's account of whether AI was involved, and disclosures or review statements in the outgoing comments; in live mode, the corresponding contribution policy. | Pass when the package establishes compliance with AI requirements applicable to these comments. For an explicit policy requiring disclosure of all AI usage in any form and covering issues/comments, look for the tool and extent of assistance and any required human review, or an explicit account that no AI assistance was used. If neither use nor non-use is addressed under that policy, grade unclear: applicability and compliance remain unverified, so silence cannot earn a pass. This readiness rule does not assert that AI was used or that the repository itself requires a particular non-use declaration. Known AI use with a missing required disclosure fails. Do not infer AI use from writing style. Pass when no applicable AI requirement is stated; a PR-only disclosure policy does not govern an issue comment. | required |
| useful-isolation | Repro report's reduced input, control comparison, or repeat-run observations, read alongside the main evidence. | A smaller case, a relevant control, or a documented repeated observation helps distinguish the triggering condition from unrelated factors. Extra detail must contribute evidence; merely calling the reproduction "minimal" or "rigorous" does not satisfy this check. This strengthens a report but is not necessary for readiness. | preferred |

## Verdict rule

For a **full package**, return `accept` (**ready**) only when every
`required` check is `pass`. Return `reject` (**hold**) if any required
check is `fail` or `unclear`. Preferred checks never change the verdict.
Do not average scores: strong writing cannot compensate for missing or
wrong-target proof. Eval mode always uses this full-package rule.

For a **live claim-only draft**, grade `claim-specific-and-respectful`,
`repo-conventions-followed`, and `ai-policy-followed` using only the
claim and rules applicable at the claim stage. Do not require repro
details before the report exists. Mark every other check `unclear`
with evidence `not yet applicable: claim-only draft` and exclude it
from the verdict. Return `accept` only if all three applicable checks
pass; otherwise return `reject`. This accepts only the claim draft,
not a future reproduction package.

Report each check's deciding evidence and use the JSON format in
`SKILL.md`, with `pass`, `fail`, or `unclear` grades and an `accept` or
`reject` verdict. For the classroom worksheet, use the equivalent
P/F/? grades and ready/hold verdict.
