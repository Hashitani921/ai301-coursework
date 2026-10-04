# Voice guide: how I talk upstream

## Who I am in threads

I am contributing to Path Review through AI301 and learning this repository's Python code.
I write short, specific comments that separate what I plan to do from what I have observed.
I use AI assistance, but I must review the wording and evidence before posting under my name.

## Rules I write by

### Rule: Name the behavior I am investigating

Name the input, operation, or symptom that makes this issue specific; a generic claim could be pasted onto any issue and does not explain my work.

- Wrong: "I'd like to fix this issue."
- Right: "I'd like to investigate the output parser's fallback when the response is a top-level JSON array."

### Rule: Promise the next investigation step, not a fix or deadline

In a claim, say what I intend to try without saying it already happened or guaranteeing a fix; in a report, use completed-work language only for actions supported by my evidence.

- Wrong: "I have confirmed the problem and will definitely fix it tonight."
- Right: "I have not reproduced it yet; I will check the H-02 test and report the command and output before proposing a fix."

### Rule: Compare the actual symptom before saying reproduced

Only say that I reproduced an issue when my output shows that issue's behavior; if an earlier setup or syntax error blocks the attempt, name that blocker instead.

- Wrong: "The command failed, so the bug is reproduced."
- Right: "This attempt stopped with a syntax error before reaching the reported failure, so it does not yet reproduce the issue."

### Rule: Keep my conclusion inside my tested setup

Name the tested environment and code state, separate observations from suspected causes, and avoid claims about versions or platforms I did not test.

- Wrong: "This is broken for everyone on every version."
- Right: "I observed this on the Windows checkout identified below; I have not tested other platforms."

### Rule: Follow repository disclosure rules and keep review claims truthful

Follow any repository requirement to disclose AI assistance, stating the tool and its actual role when required; otherwise, omit a standard AI-assistance footer, and never claim I reviewed, wrote, or ran something unless that claim is accurate.

- Wrong: "I independently wrote and verified everything myself," when AI drafted the steps and I have not checked them.
- Right: "I have not reproduced it yet; I will report the commands and observed output after testing."

## Things I never post

- "Same here" or "can confirm" without my own environment, steps, and observations.
- Guaranteed fixes, promised delivery dates, or claims that a maintainer must prioritize my issue.
- Blame, insults, or claims that the cause is obvious before examining the evidence.
- Another contributor's output presented as my own, or an AI prediction presented as a command result.
- "The bug is fixed" based only on one attempt that did not reproduce it.
