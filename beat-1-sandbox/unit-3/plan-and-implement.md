# Unit 3 — Plan and Build

## Posted upstream

**GitHub username**

Hashitani921

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/69#issuecomment-5981675526

Following up on [my reproduction of #69](https://github.com/codepath/pathreview-ai301-fa26-s3/issues/69#issuecomment-5981240268): raw, fenced, and empty arrays all raised `AttributeError: 'list' object has no attribute 'items'`, while the object and plain-text controls worked. Source inspection confirms that both JSON paths pass a successfully decoded list into the dict-only `_parse_json_output` helper.

I plan to check for a dictionary before calling that helper in both paths. Arrays will use the existing plain-text fallback, preserving the entire original response in one `general_feedback` section. I will keep object parsing unchanged.

The change is limited to `rag/generator/output_parser.py` and `tests/unit/test_output_parser.py`. I will remove the H-02 xfail marker, strengthen the array assertions, and cover fenced/empty arrays and object controls. I will rerun the posted reproduction inputs and the parser test file; arrays should return preserved feedback without raising, and the controls should retain their current results.

The planned branch is `fix/69-json-array-fallback`. This approach does not introduce a new schema for array entries; if separate structured sections are wanted, I will revise the plan before adding that behavior.

---

## Your branch

**Branch**

`fix/69-json-array-fallback`

**Evidence**

Environment for this before/after rerun: Windows 11 (10.0.26200), CPython 3.13.9, pytest 9.1.1, and structlog 26.1.0. This is a new local rerun of the same Unit 2 steps; the posted Unit 2 report remains the record of the original Ubuntu/Python 3.11 reproduction.

Before the fix, with the expected-failure marker active:

```text
$ .venv/Scripts/python.exe -m pytest tests/unit/test_output_parser.py -k test_json_array_fallback -q -rxX
x                                                                        [100%]
=========================== short test summary info ===========================
XFAIL tests/unit/test_output_parser.py::TestOutputParser::test_json_array_fallback - issue #69 (manifest H-02): output parser calls .items() on a JSON array fallback
18 deselected, 1 xfailed in 0.14s
```

Before the fix, running the same test as a normal test:

```text
$ .venv/Scripts/python.exe -m pytest tests/unit/test_output_parser.py -k test_json_array_fallback --runxfail -q
F                                                                        [100%]
================================== FAILURES ===================================
__________________ TestOutputParser.test_json_array_fallback __________________
tests\unit\test_output_parser.py:149: in test_json_array_fallback
    result = parse_review_output(raw_output)
rag\generator\output_parser.py:48: in parse_review_output
    return _parse_json_output(data)
rag\generator\output_parser.py:68: in _parse_json_output
    for key, value in data.items():
E   AttributeError: 'list' object has no attribute 'items'
=========================== short test summary info ===========================
FAILED tests/unit/test_output_parser.py::TestOutputParser::test_json_array_fallback
1 failed, 18 deselected in 0.11s
```

Before the fix, the direct Unit 2 script and parser test file produced:

```text
$ .venv/Scripts/python.exe repro69.py
array (issue input): AttributeError: 'list' object has no attribute 'items'
array inside json code fence: AttributeError: 'list' object has no attribute 'items'
empty array: AttributeError: 'list' object has no attribute 'items'
control: same items as object: OK -> 2 section(s): ['first', 'second']
control: plain text: OK -> 1 section(s): ['general_feedback']

$ .venv/Scripts/python.exe -m pytest tests/unit/test_output_parser.py -q
........x..........                                                      [100%]
18 passed, 1 xfailed in 0.13s
```

After the fix, the strengthened array regression and the same forced run both passed:

```text
$ .venv/Scripts/python.exe -m pytest tests/unit/test_output_parser.py -k test_json_array_fallback -q -rxX
.........                                                                [100%]
9 passed, 20 deselected in 0.08s

$ .venv/Scripts/python.exe -m pytest tests/unit/test_output_parser.py -k test_json_array_fallback --runxfail -q
.........                                                                [100%]
9 passed, 20 deselected in 0.08s
```

After the fix, the direct Unit 2 script and parser test file produced:

```text
$ .venv/Scripts/python.exe repro69.py
array (issue input): OK -> 1 section(s): ['general_feedback']
array inside json code fence: OK -> 1 section(s): ['general_feedback']
empty array: OK -> 1 section(s): ['general_feedback']
control: same items as object: OK -> 2 section(s): ['first', 'second']
control: plain text: OK -> 1 section(s): ['general_feedback']

$ .venv/Scripts/python.exe -m pytest tests/unit/test_output_parser.py -q
.............................                                            [100%]
29 passed in 0.10s
```

The changed files also passed the repository's code-quality tools:

```text
$ .venv/Scripts/python.exe -m ruff check rag/generator/output_parser.py tests/unit/test_output_parser.py
All checks passed!

$ .venv/Scripts/python.exe -m black --check rag/generator/output_parser.py tests/unit/test_output_parser.py
All done! ✨ 🍰 ✨
2 files would be left unchanged.

$ .venv/Scripts/python.exe -m mypy rag/generator/output_parser.py
Success: no issues found in 1 source file
```

## Eval iterations

**Run history**

1. `agreement: 20/20 scored items  (bar: 18/20: PASS)`

This was the only full eval run. The generated `eval-run.txt` contains the same final score.

**Package analysis**

I analyzed `pkg-20`. My rubric returned `reject`, and the gold label was also `reject`. The package's diagnosis, bounded generation-counter approach, executable steps, regression plan, and uncertainty all passed. It failed `thread-and-policy` because its repo facts require disclosure of all AI use, including the tool and extent, but the candidate plan comment contains no disclosure. Since that check is required, the verdict rule correctly produced `reject`.

**Check rationale**

Exact current row from `tools/plan-check/rubric.md`:

> `| thread-and-policy | Comms: the candidate comment compared with the plan, maintainer thread signals, and explicit contribution, template, and AI-use requirements in repo facts. | The comment conveys this plan's diagnosis, bounded approach, and verification well enough to stand on the thread; it is consistent with the plan, responds to relevant maintainer constraints, and satisfies applicable repository communication rules, including required AI disclosure. It does not contradict an explicit human-authorship rule or substitute agreement with another contributor for its own plan. | required |`

I made this check required because a technically buildable plan can still be unpostable when it ignores an explicit maintainer direction or repository communication policy. I used an outcome rule rather than requiring a fixed comment format, so a concise comment can pass if it communicates the plan and follows the rules. The explicit AI clause catches `pkg-20`, while the wording avoids inventing a disclosure rule for repositories that do not state one.

**Trade-offs**

This check can reject a technically strong implementation plan for a communication-policy omission, as it does for `pkg-20`. I accept that trade-off because the skill answers whether a package is ready to post and build from, and posting in violation of an explicit repository policy is not ready. The cost is that the evidence guide and procedure must distinguish an actual stated policy from silence; they therefore direct the grader not to invent a policy when none appears in the package. The 20/20 full run, including both thread-convention packages, showed that this boundary did not change otherwise-correct package outcomes.
