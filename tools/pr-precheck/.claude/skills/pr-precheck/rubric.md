# Rubric: is this pull request ready to submit?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| plan_fidelity | Read the issue context, the plan or scope notes, and the candidate diff together. Verify every changed file, behavior, and user-visible claim falls inside the stated scope or an explicit deviation note, and that the PR description does not claim more or less than the diff delivers. | Pass only when the diff matches the plan boundary and any deviation is honest and explained; no silent drift, no hidden scope expansion, and no description-vs-diff mismatch. | required |
| test_evidence | Read the plan's test plan and the PR's test-evidence section together with the repo's actual checks or reproduction steps. Confirm the evidence names the commands or scenarios run and the observed outcome. | Pass only when the evidence is observable and specific, and it supports the claimed fix or behavior change; missing, vague, or contradictory evidence is not enough. | required |
| diff_quality | Review the unified diff, changed files, and commit list together. Check for unrelated hunk churn, debug leftovers, commented-out code, dead branches, or noisy formatting changes that obscure the actual fix. | Pass only when the diff is reviewable, focused, and directly tied to the issue; unrelated edits or debris fail this check. | required |
| standards_and_comms | Read the repo-facts PR template and contribution policy, then compare the draft PR title and description against those asks, including any AI-use or disclosure requirements. | Pass only when the required sections are filled with real content, disclosures are present where required, and the PR text follows the repo's stated communication rules. | required |

## Verdict rule

Accept only if every required check passes. A `fail` or `unclear` on any required check rejects the PR. Preferred checks, if any are added later, never change the verdict by themselves. `unclear` counts as fail when the rubric is silent on a fact that cannot be verified from the package or the explicitly named evidence.

In plain terms: a PR is ready only when the diff matches the plan, the test evidence actually proves the outcome, the patch is reviewable instead of noisy, and the repo's required communication and disclosure requirements are satisfied. If any required gate fails, the package is not ready to submit.
