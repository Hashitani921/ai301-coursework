# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/69

**Verdict output**

Live-mode output of `issue-select`, run against `rubric.md` sha256 `3e7b34a5a94b6aab` —
the same rubric fingerprinted in the committed `eval-run.txt`.

<pre>
Scope: codepath/pathreview-ai301-fa26-s3 is the repo named in scope.md, so this
candidate is in the field. Path Review house rule noted (classmates' claim comments do
not block); it has nothing to bite on here, since the issue has no comments.

Check                       Grade  Evidence
--------------------------  -----  ---------------------------------------------------
repo-not-archived           pass   repo record reports archived: false
recent-commits              pass   newest default-branch commit 2026-09-16 by
                                   Aburke225, a human, 4 days before today
unclaimed                   pass   assignees: none; 0 comments; timeline holds only
                                   four 'labeled' events; repo has 0 open pull
                                   requests, so no linked PR can be open
bounded-scope               pass   one bug in one module, filed by a COLLABORATOR,
                                   naming rag/generator/output_parser.py and
                                   tests/unit/test_output_parser.py, the wrong
                                   behaviour (AttributeError: 'list' object has no
                                   attribute 'items') and the expected behaviour (the
                                   fallback path should handle array responses)
ai-policy-allows            pass   no CONTRIBUTING.md, .github/CONTRIBUTING.md,
                                   AI_POLICY.md or AGENTS.md in the repo; silence
                                   passes
issue-still-open            pass   state: open
maintainer-responds (pref)  pass   first COLLABORATOR response on #52 and #43 at 6.0
                                   days, inside the 30-day threshold
newcomer-signposted (pref)  pass   labels include 'good first issue'; opener
                                   Aburke225 is COLLABORATOR
small-blast-radius (pref)   pass   one parser module plus its unit test; no schema
                                   change, no public API contract change, no
                                   cross-cutting refactor

All six required checks pass, so the verdict rule returns accept. All three preferred
checks also pass, which is why this ranked first among the three candidates graded
(#69, #68 and #72 were all accepted; the fit profile in scope.md broke the tie).

```json
{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/69",
  "checks": [
    {"name": "repo-not-archived", "grade": "pass", "evidence": "repo record reports archived: false"},
    {"name": "recent-commits", "grade": "pass", "evidence": "newest default-branch commit 2026-09-16 by Aburke225, a human, 4 days before today (2026-09-20)"},
    {"name": "unclaimed", "grade": "pass", "evidence": "assignees: none; 0 comments; timeline holds only four 'labeled' events; repo has 0 open pull requests so no linked PR can be open"},
    {"name": "bounded-scope", "grade": "pass", "evidence": "one bug in one module filed by a COLLABORATOR, naming rag/generator/output_parser.py and tests/unit/test_output_parser.py, the wrong behaviour (AttributeError: 'list' object has no attribute 'items') and the expected behaviour (fallback path should handle array responses)"},
    {"name": "ai-policy-allows", "grade": "pass", "evidence": "no CONTRIBUTING.md, .github/CONTRIBUTING.md, AI_POLICY.md or AGENTS.md in the repo; silence passes"},
    {"name": "issue-still-open", "grade": "pass", "evidence": "state: open"},
    {"name": "maintainer-responds", "grade": "pass", "evidence": "first COLLABORATOR response on #52 and #43 at 6.0 days, inside the 30-day threshold"},
    {"name": "newcomer-signposted", "grade": "pass", "evidence": "labels include 'good first issue'; opener Aburke225 is COLLABORATOR"},
    {"name": "small-blast-radius", "grade": "pass", "evidence": "one parser module plus its unit test; no schema change, no public API contract change, no cross-cutting refactor"}
  ],
  "verdict": "accept"
}
```
</pre>

---

## Eval iterations

**Run history**

Five runs, in order:

1. `--limit 3` smoke run — **3/3**. A plumbing check, not a score.
2. Full 20-issue run — **17/20**, below the 18 bar. The category floor held
   (claimed 4/4, clear-accept 6/8, dead-repo 3/3, policy 1/1, scope 3/4), so no whole
   family was invisible to the rubric; three issues were simply graded wrong, and all
   three failed on the same check, `bounded-scope`: `issue-04` and `issue-19` rejected
   against a gold `accept`, `issue-20` accepted against a gold `reject`.
3. `--only issue-04,issue-19,issue-20`, after rewriting `bounded-scope` — **3/3**. All
   three flipped to agree.
4. `--only issue-01,issue-05,issue-10` — **3/3**. A deliberate regression check rather
   than a fix. The rewrite widened the "several instances of one defect is one change"
   allowance, which could have let the umbrella issues `issue-05` and `issue-10` slip
   through, and narrowed the feature-request clause, which could have caught the docs
   task `issue-01`. None of the three moved.
5. Full 20-issue run — **19/20, PASS**; category floor held (claimed 4/4,
   clear-accept 7/8, dead-repo 3/3, policy 1/1, scope 4/4). This is the run committed as
   `eval-run.txt`.

One honest note about run 5: `issue-19` agreed in run 3 and disagreed again in run 5,
with no change to the rubric between them. The same check read the same bundle both ways
across two runs. That is a property of the check rather than of the rubric text — see
Trade-offs for which check wobbles and why.

**Issue analysis**

`issue-20` (excalidraw/excalidraw#11811, "Add company logo shape to the toolbar").
Gold label: **reject**, categorised as a scope failure. My final rubric: **reject**. My
first rubric: **accept** — one of the three issues that put run 2 below the bar, and the
one that taught me the most.

Why v1 read it as acceptable. My `bounded-scope` check disqualified a feature request
only when three things were absent together: "no named files, no acceptance criteria, and
no maintainer comment stating the design". The issue body ends with "Success looks like:
logo tool in the shapes toolbar → place/resize/move like other elements → correct
export." That is a sentence shaped exactly like acceptance criteria, so one of my three
conditions was satisfied, the `and` never resolved, and the clause never fired. Every
other required check then passed honestly — excalidraw commits daily, the issue is open,
unassigned, with no linked PRs, no comments and no AI policy — so the rubric accepted it.

What my rubric could not see is who was asking. The issue was filed by `cursor[bot]`,
author_association `NONE`, on a 129,000-star product, and no OWNER, MEMBER or COLLABORATOR
ever replied. "Add *our company logo* as a first-class shape" is not a defect anyone can
confirm; it is a product decision belonging to Excalidraw's maintainers, and nobody with
commit rights had agreed to make it. A newcomer who built it would most likely have the
pull request closed on product grounds after writing perfectly correct code.

So I had been grading the wrong thing — the polish of the write-up rather than whether the
change had been agreed to. The clause now reads "it requests a new user-facing capability
and nobody with commit rights has endorsed it: no OWNER, MEMBER, or COLLABORATOR either
filed the issue or commented accepting the design", with the explicit rider that this
holds "whatever acceptance criteria the opener wrote for themselves". That keys the check
to endorsement instead of prose, which is the signal that actually separates `issue-20`
from `issue-09` — a feature request the gold labels accept, because a MEMBER filed it and
invited takers.

**Check rationale**

The check I want to defend is `unclaimed`, quoted as it is currently written in the
`rubric.md` uploaded to `tools/issue-select/`:

> | unclaimed | Repo facts, the "this issue:" line (assignees, linked PRs with state),
> plus every comment in the Comments section with its date and author_association. |
> Fail on any of these. One, `assignees:` is anything other than `none`. Two, any linked
> pull request is in `open` state, in this repo or in a fork. Three, a comment dated
> within 90 days of the capture date says someone is taking, starting, or working on the
> issue, and no later maintainer comment releases it. Four, a maintainer comment reserves
> the work for a named person. A claim older than 90 days is stale and does not block,
> unless a maintainer has since confirmed it is still live. | required |

Three decisions produced that wording.

*It reads four surfaces, not one.* The obvious version of this check looks at the assignee
box and stops. That version misses `issue-13`, where nobody is assigned and nobody has
commented, but two linked pull requests are already open on an issue filed hours earlier.
It also misses `issue-18`, where the assignee box is empty and the whole claim lives in
comments and fork PRs. Claims leak across four surfaces, so the check reads four.

*The 90-day staleness window is the part I argued with myself about.* A claim comment is
not a lock; it is evidence that somebody intended to do this, and intentions decay.
`issue-09` forced the number. Someone wrote "I'd like to take a swing at this as my first
open-source contribution" in January 2022, a maintainer answered "Think you can just give
it a try if you are interested", and then nothing happened for four and a half years.
Treating that as a live claim throws away a good issue on the strength of an abandoned
intention. I did not want an open-ended amnesty either, so the window is 90 days with one
explicit exception: a maintainer re-confirming a claim keeps it alive however old it is.

*The fork clause exists because of `issue-03`.* The pull request that actually blocks it
is `quick123-666/pylint#1`, an open PR in a contributor's own fork. A check that only
looks for open PRs "in this repo" reads that field as empty. "in this repo or in a fork"
costs seven words and closes the hole.

One thing the check deliberately refuses to do: it does not read a `good first issue`
label as evidence that an issue is free. The label is a maintainer saying the work is
friendly, not that it is unclaimed, and three of the four issues my rubric rejects as
claimed carry it.

**Trade-offs**

The 90-day staleness window is the clause that gives something up, and I can name the
issue whose result it changes: `issue-09`. Without it, the 2022 "I'd like to take a swing
at this" comment plus the maintainer's go-ahead fails `unclaimed`, and my rubric rejects
an issue the gold labels accept. With it, the claim is 1,658 days old, goes stale, and the
issue is accepted. That one clause is worth a full point of agreement on its own.

What it will miss: somebody who claimed an issue 100 days ago and is still working,
quietly, on a branch they never opened as a pull request. My check reads that issue as
free, I claim it, and we collide. Nothing in a snapshot distinguishes that person from the
four-year-old abandoned claim in `issue-09` — the evidence is identical and only the
outcome differs. I accepted that exposure because the opposite error is worse and far more
common: treating every historical comment as a permanent lock rules out most well-labelled
older issues, which is exactly the pool a newcomer should be shopping in.

The clause pulls in the other direction too. `unclaimed` counts *any* open linked PR as a
live claim, with no staleness window on PRs at all. On `issue-18` one of the blocking PRs
has been open since mid-2025; by the logic I applied to comments, a year-old open PR is
arguably an abandoned attempt rather than an active claim. The gold label happens to agree
with my reject there, so nothing in the eval set punished the inconsistency, and I left it
alone rather than tune a threshold no case was testing. It is the first thing I would
revisit if this rubric met a repo where open PRs go stale instead of being closed.

A closing note, because the run history raises it. `unclaimed` is reproducible precisely
because every input is a field read — a name, a state, a date. `bounded-scope` is the
opposite, and `issue-19` is the proof: it agreed in run 3 and disagreed in run 5 with
identical rubric text, because "is this one change?" is a reading rather than a
measurement. That is the cost of carrying any judgment check at all, and I would rather
carry one honest judgment check than pretend scope can be measured.

---

## Selection rationale

**Selection rationale**

*1. Fit to my interests and to the time available.* #69 sits in `rag/generator/`, the part
of this codebase I most want to learn: it is where an LLM's raw response gets turned into
the structured object the rest of the app relies on. I work in Python on FastAPI backends
and I have built retrieval pipelines, so the vocabulary costs me nothing and the learning
is in the codebase rather than in the concepts. On time, the issue estimates 2–4 hours,
the change lives in one module plus one test file, and there is no environment to stand up
beyond installing the project and running pytest. That fits a week in which I also have to
claim and reproduce the issue for Unit 2.

*2. What the verdict identified correctly, and what I weighed that the rubric could not.*
The verdict got the mechanical facts right, and right for stated reasons: the repo's
newest commit is four days old, the issue is open with no assignee and no linked PRs in a
repo with zero open PRs, the body names both files it touches, and there is no
CONTRIBUTING.md to bar an AI-assisted workflow. What the rubric has no check for, and what
actually decided it for me, is that **the failing test already exists**. The body says the
covering test is marked `@pytest.mark.xfail` against manifest id H-02, and that removing
the marker is part of the fix. That makes my definition of done executable before I write
a line: delete the marker, watch it go red, make it green. Across three candidates my
rubric graded identically — all nine checks pass on #69, #68 and #72 — that is the
difference invisible to every check I wrote. I also weighed one thing against #68: its fix
turns on `rank-bm25`'s internals, a third-party library I would have to read first, and my
fit profile says to avoid exactly that ramp-up on a first contribution.

*3. The anticipated difficulty in claiming it.* Low. There is no assignee, no linked pull
request and no comment of any kind on #69, and the Path Review house rule in my `scope.md`
means a classmate's claim would not have blocked me even if there were one — #68 already
carries one, and I would still have been free to take it. The maintainer answers issues in
about six days, so I should not wait long for acknowledgement, and course credit attaches
to the pull request I open rather than to whether it merges. The real difficulty is not
claiming; it is the one thing the issue leaves open. It says the fallback "should handle
array responses" without saying what a top-level array should become. I will need to read
the object path in `output_parser.py` and mirror its shape, and say in my claim comment
which reading I am taking, so a maintainer can correct me early rather than in review.

---

Related paths: `eval-run.txt` in this directory; the skill's files in
`tools/issue-select/`.
