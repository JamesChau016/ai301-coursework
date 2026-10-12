---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

This tool answers one question about one candidate pull request: is this PR ready to submit?
A PR package is the candidate PR itself — its title, description, commit list, diff, and attached test evidence — read against the issue it addresses and the plan it claims to implement. It grades only that package, never a different repo, never a broader workflow, and never a gut-feel judgment. Every check must be grounded in facts visible in the package or in the repo evidence it names.

## Inputs and modes

Run in two modes.

Live mode: read the student's own package from their repository state. The required inputs are the issue being fixed, the plan.md with its deviation notes, the branch diff (`git diff main...HEAD` from the working copy, three-dot diff against the repo's default branch), the draft PR title and description, and the test evidence captured for the change. If a house-chain student is grading a sandbox submission, they read the same materials in the house plan and reproduction pack instead of a GitHub issue thread.

Eval mode: the bundle is the whole world. Read the package bundle text only; do not fetch anything else, do not read the repo, and do not infer extra facts. Grade every check with the full rubric and the full verdict rule, ignoring `scope.md` and `voice-guide.md` entirely.

## The scope seam (live mode only)

In live mode, read `scope.md` before any PR judgment. The scope file names the repo this PR must live in and the house rules for that environment. Refuse to grade any work outside the scoped repo. If the `Repo:` line in `scope.md` is still an unfilled placeholder, stop immediately and tell the student to fill it with the Path Review repo before grading; do not guess a repo.

The scope file is binding in live mode because it defines the field of view. In eval mode, ignore it completely; the bundle is the only valid evidence source and the whole world is already scoped.

## The voice seam (live mode only)

In live mode, also read `voice-guide.md` before judging the outgoing PR text. Check the draft PR title and description against those written rules, and report any violated rule in the summary, but do not treat voice violations as an automatic verdict change unless the rubric explicitly names a check that reads that guide.

The voice guide never changes the verdict on its own: it only tells you whether the outgoing text follows the student's own communication standards. In eval mode, ignore it entirely because voice is personal and the bundle has no real issue thread to compare against.

## Component reads

Use the components in this order and in this way:

- `rubric.md` defines the checks and the verdict rule. The tool must grade exactly the checks named there.
- `references/evidence-guide.md` maps each evidence family to the exact place in a PR package or repo context where it lives.
- `procedure.md` is the grading procedure; execute it as written. If a step is left silent or ambiguous, do not improvise around it; report the gap and refuse to guess.

If `rubric.md` or `procedure.md` has no written content, the tool refuses to grade and says so by design. Empty templates are not judgment; they are a stop signal.

## Verdict and output

This tool uses a binary verdict space: `accept` means ready to submit, and `reject` means hold. The final reply must end with the fenced JSON block below, and nothing must follow it.

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

Grade under these standing rules:

- Evidence first: no check is graded without a named fact or quote that decided it.
- Grade the thing, not the polish: a terse but complete PR can be acceptable, and a polished PR can still be wrong if the diff drifts, the evidence is missing, or the standards are ignored.
- The rubric decides, not the run: if a check passes under its stated condition, it passes even if the run feels uncomfortable; fix the rubric, not the grade.
- The procedure decides how, not the run: execute the steps in `procedure.md` and report any procedure gap instead of inventing a step.
- Unclear defaults to fail: if the evidence cannot verify a claim, grade it `unclear`; where the rubric is silent, an unclear fact counts as a failure.

The tool must never answer a different question, never grade more than one PR package in a run, and never claim readiness without traceable evidence.
