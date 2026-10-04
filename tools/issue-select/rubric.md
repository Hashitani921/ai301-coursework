# Rubric: is this a good first issue?

Six required checks decide the verdict; three preferred checks rank the
issues that survive. Every check names a source someone else can open and
a threshold they can apply without me. Recency is measured against the
bundle's capture date in eval mode, and against today in live mode.

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| repo-not-archived | Repo facts, the `repo:` line, `archived:` flag. Live mode: the archived banner across the top of the repo front page. | `archived: no`. An archived repo is read-only, so no pull request can ever land. | required |
| recent-commits | Repo facts, the "last 5 default-branch commits" list: the newest date in it, and that commit's author. Live mode: the commit line above the file list on the repo front page. | The newest default-branch commit is dated within 90 days of the capture date. A commit authored by a bot counts toward this only when it is a merge of a human contributor's pull request; a list of nothing but bot chores does not. | required |
| unclaimed | Repo facts, the "this issue:" line (assignees, linked PRs with state), plus every comment in the Comments section with its date and author_association. | Fail on any of these. One, `assignees:` is anything other than `none`. Two, any linked pull request is in `open` state, in this repo or in a fork. Three, a comment dated within 90 days of the capture date says someone is taking, starting, or working on the issue, and no later maintainer comment releases it. Four, a maintainer comment reserves the work for a named person. A claim older than 90 days is stale and does not block, unless a maintainer has since confirmed it is still live. | required |
| bounded-scope | The issue body and the whole comment thread, including the opener's author_association. | Pass when the issue asks for one change a newcomer could finish in a single pull request, and states the end state concretely enough to know when it is done: named files or functions, the specific behaviour to change, or a reproduction plus the expected result. Fail on any of these. One, it is a tracking, umbrella, or self-described mega issue: its body is mainly a list of other issue numbers, or it invites an open-ended series of pull requests across the codebase rather than one change. Two, the approach is still unsettled at the end of the thread: a design question from a maintainer or the opener is never answered, or a maintainer says a decision has not been made. Three, it requests a new user-facing capability and nobody with commit rights has endorsed it: no OWNER, MEMBER, or COLLABORATOR either filed the issue or commented accepting the design. A wish nobody on the team has agreed to is a product decision, not a task, whatever acceptance criteria the opener wrote for themselves. Four, it has been open more than 365 days and has two or more linked pull requests in `closed` unmerged state, which is a record of abandoned attempts. Five, it is a usage or support question rather than a change to the project. Three clarifications keep this check from over-rejecting. Several instances of the same defect, or several sub-steps of one fix, inside one module or feature area are ONE change: grade the area the work touches, not the number of bullets, and a trailing `etc.` in such a list does not make it an umbrella. A bug filed by an OWNER, MEMBER, or COLLABORATOR that names the affected area and the wrong behaviour passes this check even when the body is a single line. A label never passes this check on its own. | required |
| ai-policy-allows | Repo facts, the "contribution policy" line. Live mode: `CONTRIBUTING.md` in the repo root or `.github/`, any contributor docs it links out to, a dedicated AI policy file, and the pull request template. | Pass when the policy states no restriction on contribution tooling, or permits AI-assisted work under conditions such as disclosure, human review, personal understanding, or testing. Silence passes; most repos say nothing, and that is not a restriction. Fail only when the policy refuses AI-assisted contributions outright and leaves no compliant path, for example "we do not accept AI-generated code or documentation". Conditions are terms to follow, not reasons to walk away, and a policy that bans fully-AI-generated work while allowing assisted work has stated a compliant path. | required |
| issue-still-open | The issue header line, `state:`. | `state: open`. A closed issue is not available to work on. | required |
| maintainer-responds | Repo facts, the "maintainer first-response sample". | At least one sampled issue drew a first owner, member, or collaborator comment within 30 days. | preferred |
| newcomer-signposted | The issue's `labels:` list and the opener's author_association on the issue header line. | The issue carries a starter label such as `good first issue`, `help wanted`, `documentation`, `easy`, or an equivalent, or the opener is an OWNER, MEMBER, or COLLABORATOR of the repo. | preferred |
| small-blast-radius | The issue body: the kind of change it asks for. | The work is confined to documentation, tests, configuration, or a single named function or file, and implies no database schema change, no public API contract change, and no cross-cutting refactor. | preferred |

## Verdict rule

- **accept** if and only if every `required` check grades `pass`.
- **reject** if any `required` check grades `fail` or `unclear`.
- `unclear` on a required check counts as `fail`. The evidence for all six
  required checks is present in every bundle, so `unclear` there means the
  evidence was genuinely absent, and a first issue I cannot verify is not
  a first issue to take.
- Required checks do not trade off against each other. There is no score
  to total and no majority vote: one required `fail` is a reject, however
  strong the rest look.
- `preferred` checks never change a verdict, in either direction. Grade
  them and report them. On an accepted issue they are the ranking signal:
  among accepted candidates, more preferred passes ranks higher, and the
  summary says which ones carried the top-ranked issue. A rejected issue
  is never rescued by passing all three.
