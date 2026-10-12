# Procedure: how this tool grades a PR package

## Read order

Read the issue and the plan before opening the diff, because the diff is judged against what the plan actually promised. In live mode, first read `scope.md` to confirm the repo and house rules, then `voice-guide.md` to note the communication rules that constrain the outgoing PR text. In eval mode, skip both because the bundle is the whole world.

Then read the issue context and repo-facts block to capture the actual problem, the repo's required PR sections, and any disclosure expectations. Next read the plan block or `plan.md` with its deviation notes and test plan, noting the intended scope and the expected behavior. Only after that do you read the candidate PR's title, description, commit list, unified diff, and test-evidence section. This ordering matters because it lets you compare each artifact against the evidence source it claims to reflect: the plan against the diff, the test plan against the test output, and the description against both.

As you read, record four facts in brief: (1) the declared scope, (2) the expected behavior or fix, (3) the evidence the PR claims it ran, and (4) the repo's PR-template and disclosure asks. Those notes are the evidence set for the checks.

## Evidence gathering

Gather evidence for each rubric check from the exact places that map to it:

- Plan fidelity: compare the plan’s scope and deviation notes to the changed files and user-visible behavior in the diff. Also compare the PR description to the actual diff: if the description says the patch does more or less than the diff, mark the mismatch as a plan-fidelity failure.
- Test evidence: compare the plan’s test plan or reproduction notes to the PR’s test-evidence section, then check whether the repo’s own checks or the stated verification commands are actually attached and named. Record the commands or scenarios and the observed outcomes.
- Diff quality: inspect the unified diff and commit list for scope creep, unrelated edits, debugging remnants, commented-out code, “drive-by” formatting churn, or noisy revisions that bury the fix.
- Standards and comms: compare the repo-facts block and PR template against the candidate title and description. Confirm required sections are filled, disclosure language is present when required, and the outgoing text satisfies the repo’s communication rules.

If a check has no evidence that can be observed from the named source, mark the check `unclear` rather than guessing. A package cannot be accepted on an invisible claim.

## Check execution

Run the checks in this order: `plan_fidelity`, `test_evidence`, `diff_quality`, then `standards_and_comms`.

For each check, use the evidence you gathered and assign one grade:

- `pass`: the check’s condition is clearly satisfied by direct evidence.
- `fail`: the check’s condition is violated by direct evidence.
- `unclear`: the condition cannot be verified from the package and the named sources.

When the evidence is genuinely absent, do not fill in missing facts. For example, if the PR says “tests pass” but shows no command output or no outcome, that is not proof; it is a failing or unclear test-evidence check depending on whether the repo’s required evidence is absent or contradictory.

A check can often be graded without re-reading the entire package if the relevant evidence has already been recorded; do not re-read broad sections unless the comparison is ambiguous.

## Verdict assembly

Combine the per-check results with the rubric rule: accept only if every required check passes; reject if any required check fails or is `unclear`. Preferred checks never change the verdict by themselves.

When more than one check failed, pick the first failing required check in rubric order as the deciding check to quote in the JSON output. The deciding check is the first required check in this order: `plan_fidelity`, then `test_evidence`, then `diff_quality`, then `standards_and_comms`.

After grading, return the final JSON block with one evidence string per check and the final verdict. The evidence line in the deciding check should quote the exact fact or phrase that carried the verdict; if there are multiple failing checks, the first required failure still wins the output slot.
