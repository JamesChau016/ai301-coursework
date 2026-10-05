# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| diagnosis | The plan's stated cause read against the repro evidence (steps, artifacts, control runs) | Passes if the plan states a specific cause that explains what the repro evidence shows AND its planned change fixes that cause; fails if it only restates the symptom, states a cause the evidence contradicts, or plans a workaround/safety net (docs note, catch-all recover, retry) instead of fixing the cause | required |
| scope | The plan's scope/files statement and its proposed-changes list | Passes if every planned change is needed to fix this bug, each change's location is precise enough for a stranger to find (a file, function, or named code path; an unpinned exact function is fine if the plan says so and says how it will be pinned), and the plan says what it will not touch. Fails if it bundles extra work (refactors, rewrites, dependency upgrades, new options/features, "while in there" fixes), names locations only vaguely ("somewhere", "look into"), or has no not-in-scope statement | required |
| test | The plan's test plan read against the repro evidence's steps | Passes if the plan gives concrete steps for verifying the fix (exact actions, usually the repro steps, and the specific observable result that confirms success); fails if the test plan is vague ("should feel fast", "should work correctly"), generic, or absent. An automated test is not required to pass, but see `automated-test` below | required |
| thread | The plan and plan comment read against the thread highlights and the repo-facts contribution policy | Passes if (a) the plan follows, or explicitly engages with, what maintainers already said in the thread (an identified culprit, a proposed or rejected approach, an existing patch or open PR) rather than ignoring or contradicting it, and (b) the comment meets every requirement the contribution policy places on comments. If the policy requires AI-use disclosure in any form that covers comments, the comment must include one (these plans are AI-assisted); a disclosure required only in the PR does not apply to the comment | required |
| automated-test | The plan's test plan section | Passes if the test plan adds at least one automated test (a test file/function or CI check) that fails before the fix and passes after; fails otherwise | preferred |

## Verdict rule

Verdict is `accept` (ready) if every required check (diagnosis, scope, test, thread) passes. Any required check graded fail or unclear results in `reject` (hold). `automated-test` is preferred and never changes the verdict.
