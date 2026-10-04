# Evidence guide: where proof lives in a reproduction package

Use this guide to locate and interpret evidence for [the rubric](../rubric.md).
The rubric defines the checks, weights, grades, and verdict; this guide
does not add requirements or change them.

## Reading boundaries

- **Eval mode:** the frozen bundle is the whole evidence record. Read
  `Issue`, `Thread highlights`, `Repo facts`, `Candidate claim comment`,
  and `Candidate repro report`. Use equivalent fields in a JSON bundle.
  Do not browse GitHub, run the commands, or assume a named but omitted
  attachment contains proof.
- **Live mode:** follow `SKILL.md` and `scope.md` first. Read the issue
  body and relevant comments for the target behavior, and the repository's
  own documentation for setup and contribution requirements. Candidate
  proof must be contained in or quoted by the outgoing drafts; do not
  repair the package with unquoted local files or a run you perform.
- **Claim-only drafts:** use the Comms section and the rubric's claim-only
  rule. A repro report that has not been written is not a reason to reject
  the claim. Eval bundles are always full packages.

For each grade, cite the location and the deciding quote or fact, such
as `Candidate repro report > Execution: output is a syntax error, not
the panic described in Issue`. If essential evidence is absent, name
the missing item; if present evidence contradicts the claim, name both
sides of the contradiction. The reporter's evidence establishes the
target; only the candidate's evidence establishes their result.

## Rubric map

| Rubric check | Evidence family |
|---|---|
| claim-specific-and-respectful | Comms |
| environment-identifiable | Environment |
| steps-rerunnable | Steps |
| proof-tests-the-issue | Behavior shown |
| outcome-supported-and-honest | Honesty |
| repo-conventions-followed | Comms, with requested details located under Environment and Steps |
| ai-policy-followed | Comms |
| useful-isolation | Steps and Behavior shown |

## Environment

**Where it lives — eval:** In `Candidate repro report`, find the
environment paragraph, version-command output, installation source,
build configuration, and relevant runtime/dependency versions. Compare
these with environment details in `Issue` and `Thread highlights`, and
with the `bug reports` requirements in `Repo facts`.

**Where it lives — live:** Find those facts in the repro draft. Compare
them with the issue thread, the repository's README or linked setup/build
docs, and the applicable bug-report template under `.github/ISSUE_TEMPLATE/`
or its documented equivalent.

**What good looks like:** The candidate identifies the project release
or commit, platform, and details that affect this run, such as shell
version or debug versus release build. Differences from the reporter's
environment are acknowledged, and the conclusion stays within the
environment actually tested.

**Reading cautions:** A `latest release` entry in Repo facts does not
identify the installed version. A panic characteristic of debug builds
does not by itself provide a complete environment record. An explicit
environment statement can be evidence; a separate version-command log
is not mandatory unless the rubric or applicable repo requirements say so.

## Steps

**Where it lives — eval:** In `Candidate repro report`, trace the starting
state, setup commands, input documents or fixtures, configuration values,
ordered CLI/UI actions, and the final inspection. Read them against the
issue's minimal example and any prerequisites clarified in the thread;
use setup instructions quoted in the bundle when available.

**Where it lives — live:** Trace the same chain in the repro draft and
compare the setup with the repository's own installation, development,
or test instructions. Relevant input and commands must be supplied or
unambiguously identified in the draft; an unspecified private file is
not a usable reference.

**What good looks like:** A stranger can recreate the relevant initial
state and perform the same attempt without inventing a command, input,
flag, or UI action. References such as "the issue's exact command" can
work when there is one clear command available to the reader; a vague
reference to "the usual setup" cannot fill a missing essential step.

**Reading cautions:** Compare actual input contents, not just filenames:
a changed delimiter or omitted option can change which behavior is
tested. Steps can be followable yet test the wrong target; record that
separately under Behavior shown. For `useful-isolation`, locate any
reduced input or control setup and identify what relevant condition
changes between runs; controls are preferred, not mandatory.

## Behavior shown

**Where it lives — eval:** Start with the trigger and symptom in `Issue`
and clarifications in `Thread highlights`. Then inspect the candidate's
command/output excerpts, assertions and test results, log lines, or
concrete before/after UI observations in `Candidate repro report`.

**Where it lives — live:** Compare the issue thread with the artifacts
included in the repro draft. Read the actual output or visible screenshot
content and its associated action; a statement that a log or screenshot
exists does not supply its contents.

**What good looks like:** A claimed reproduction connects a materially
faithful trigger to the issue's actual symptom. An explicitly unsuccessful
attempt connects followable steps to an observed result at the relevant
operation and identifies what differed or could not be established; it
can be useful evidence even when a necessary trigger was not achieved.

First identify which outcome the candidate claims. For cannot-reproduce,
look for three things: a concrete attempt at the relevant operation,
its actual output or observation, and an explanation limiting the result
to that attempt. For example, an ordering test can show the observed
marker order while acknowledging that the input may not have forced
one buffer to flush earlier than another. That uncertainty limits the
conclusion; it does not erase the supplied test and its observations.

**Reading cautions:** A version printout, successful install, running
session, or nonzero exit code alone does not establish the bug. For
example, a malformed HCL input that produces `Missing key/value separator`
does not demonstrate the issue's `panic: not a string`; likewise, a
screenshot showing three tabs does not establish that a pane is blank
and ignores input.

Concrete UI observations can be sufficient without a screenshot unless
one is explicitly required. "After pressing Enter, the dialog closed,
the file remained untracked, and the stash list was empty" describes
observable results; "same here" does not. For `useful-isolation`, read
the control's or repeated run's observations as well as its commands;
additional runs strengthen evidence only when they test the relevant behavior.

## Honesty

**Where it lives — eval:** Read the claim comment's statements about
completed work together with the repro report's result, expected/actual
comparison, analysis, and limitations. Check each factual conclusion
against the candidate's supplied artifacts, steps, and environment;
use the issue to distinguish intended behavior from the reported bug.

**Where it lives — live:** Compare both outgoing drafts with the evidence
they include and the issue thread. Do not use an earlier contributor's
successful reproduction as proof that this candidate reproduced it.

**What good looks like:** The conclusion says what happened in the tested
setup, separates observations from suspected causes, and does not claim
more versions, platforms, or certainty than the evidence supports. An
honest cannot-reproduce report supplies the relevant attempt and observed
result, identifies environment differences or unachieved/uncertain trigger
conditions, and does not declare the original issue disproven.

**Reading cautions:** A changed OS or shell can explain a different
result; it is not automatically dishonesty. Look for what the candidate
actually tried and what remains unverified, especially for intermittent
bugs or conditions they could not establish. "I did not observe the bug,
and this condition may not have been reached" is a limited observation;
"this proves the bug is gone" is an unsupported conclusion. A failure before reaching
the target operation is a setup blocker, not proof of reproduction or
of a non-failing target behavior.

Read the meaning of "expected": it may refer to correct behavior or to
the buggy symptom anticipated from the issue. The package must make the
comparison understandable, but a heading alone should not decide the
grade. A proposed cause, a plan to investigate, and a demonstrated result
are different kinds of statements; do not treat a plan as completed work.

## Comms

**Where it lives — eval:** Compare `Candidate claim comment` with the
issue's specific problem and relevant thread context. Read both candidate
comments against `Repo facts > bug reports` and `Repo facts > contribution
policy`, including the exact scope of any AI-use policy.

**Where it lives — live:** Read the issue thread and both drafts alongside
the repository's applicable bug-report template, `CONTRIBUTING.md`, and
any linked policy such as `AI_POLICY.md`. Apply the live course rules in
`scope.md`; consult `voice-guide.md` for separate live feedback as directed
by `SKILL.md`.

**What good looks like:** The claim names a concrete aspect of the issue
and a relevant next action in respectful, factual language, while the
comments satisfy applicable reporting, coordination, and AI-use rules.
Read the policy's actual scope: a requirement for opening a PR or filing
a new issue does not automatically govern a follow-up issue comment.

**Reading cautions:**

- For `claim-specific-and-respectful`, cite the issue-specific detail
  and proposed action, or the actual blame, demand, or unsupported promise.
  Greetings, enthusiasm, or emojis alone do not prove or disprove readiness.
- For `repo-conventions-followed`, match each applicable request to the
  supplied information. Equivalent wording is acceptable unless a specific
  format is required. The absence of extra repository rules is not itself
  missing evidence, and another student's claim does not block a claim
  under the Path Review house rules.
- For `ai-policy-followed`, first locate the policy's scope. No applicable
  AI requirement, or a disclosure rule explicitly limited to PRs, permits
  a pass for these comments. A policy explicitly covering all AI usage in
  any form, including issues/comments, requires a separate compliance check
  even when the technical reproduction is complete.
- Under that broad disclosure policy, locate the candidate's account of AI
  involvement. If AI was used, check the named tool, extent of assistance,
  and any required human review. An explicit statement of no AI involvement
  can establish that conditional disclosure duties do not apply. If the
  comments address neither use nor non-use, record `unclear` with the policy
  and missing account as evidence: the rubric holds unresolved compliance.
  Do not treat silence as proof of no AI use, accuse the author of using AI
  based on prose style, or invent a disclosure/non-use statement for them.
  This is the rubric's readiness standard, not a claim that every repository
  demands a non-use declaration. Known AI use without its required
  disclosure is a `fail`.
- Personal voice rules are checked separately in live mode and are ignored
  in eval mode. They do not create additional rubric gates.
