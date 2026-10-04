# Evidence guide: where evidence lives in a plan package

In eval mode, the bundle alone is evidence. Never look up its source issue, read other packages, or consult gold labels while grading. In live mode, use the issue and repository sources below for context, but grade the candidate from what `plan.md` and the draft comment actually contain or quote. A local experiment absent from the drafts cannot silently repair the package.

## Diagnosis and grounding

- Eval: Issue, Thread highlights, Repro evidence (environment, steps, actual/expected behavior, controls), then Candidate plan's diagnosis and approach.
- Live: issue body and relevant maintainer comments; the student's posted Unit 2 reproduction verified by username and permalink; repro quotations and diagnosis in `plan.md`. For a house issue, use the house repro pack quoted in the drafts.
- Record the trigger, failure point, actual/expected behavior, passing controls, and causal mechanism. Trace how the proposed edit changes that mechanism. Distinguish maintainer analysis from another student's proposal.
- Good evidence explains both failure and controls. A hypothesis can be unproved if its uncertainty and a concrete diagnostic step are explicit. Repeating a symptom or targeting a component ruled out by a control does not establish a cause.

## Scope

- Eval: Candidate plan's scope, approach, named files/areas, and Issue's requested outcome.
- Live: `plan.md`'s included/excluded behavior and edit list compared with the issue and relevant repository constraints.
- Record every promised behavior change and why it is necessary. Tests and documentation directly supporting the fix are in scope; file count alone does not determine scope.
- Good scope has an identifiable acceptance boundary. Unrelated cleanup or a new feature remains scope creep even when advertised as small.

## Executability

- Eval: Candidate plan's approach, named modules/functions, prerequisites, and work order; repo facts where relevant.
- Live: edit locations, algorithm or behavior rule, sequence, and prerequisites stated in `plan.md`. Source can verify a location but cannot supply a missing design.
- Record where to begin, what to change, and decisions to settle first. Concrete areas plus an actionable behavior rule can suffice without exact line numbers.
- Good evidence lets a contributor start the central edit without first choosing the solution. A bounded investigation needs a question, diagnostic action, and explanation of how the answer governs the fix.

## Test plan

- Eval: Candidate plan's tests against Repro evidence's trigger, commands, steps, outputs, and controls; test requests in Thread highlights.
- Live: tests and expectations in `plan.md` and the comment against the student's posted reproduction. Completed post-fix results are not required before building.
- Record each test's input/action, execution route, expected observation, and protected control. "The repro above" is usable when the package supplies those steps and the changed expectation.
- Good evidence distinguishes broken from corrected behavior. Full-suite execution complements but cannot replace a targeted regression expectation. A manual UI check can be decisive.

## Honesty

- Eval: assumptions, risks, certainty language, completed-testing claims, and deviations anywhere in Candidate plan/comment, compared with Repro evidence and repo facts.
- Live: those draft claims against posted proof and `plan.md`'s Deviations section when reviewing an updated plan. An unquoted working-tree diff cannot supply a missing deviation.
- Record material uncertainties with verification/containment and differences between planned and described implementation. Do not demand an invented risk section.
- Good evidence separates observation from inference and planned from completed work. A disclosed, justified deviation can pass.

## Comms

- Eval: Candidate plan comment, Candidate plan, Thread highlights, and Repo facts' template, contribution, review, and AI-policy requirements.
- Live: actual draft, issue body and maintainer replies, `CONTRIBUTING.md` or `docs/CONTRIBUTING.md`, linked policies, applicable `.github` templates, and the installed `voice-guide.md`.
- Record applicable requests verbatim and pair them with the comment's response. Apply bug-report templates to relevant reproduction claims, not as an invented requirement to recreate a whole report in every plan comment. Explicit disclosure and human-authorship restrictions apply.
- Good communication states this contributor's approach and verification consistently with the plan and thread. Path Review classmates do not reserve an issue; follow `scope.md`. Personal voice notes do not independently change the rubric verdict.