  # Evidence guide: where evidence lives in a PR package

  ## Plan fidelity (harness category: silent-drift)

  Where it lives: This evidence comes from the issue context, the plan block or `plan.md`, and the candidate PR's diff and description. In eval bundles, read the plan-context block for the stated scope, deviation notes, and test plan, then compare it to the PR diff and the description claims. In live mode, compare `plan.md` plus its deviation notes to the working tree diff and the draft PR description.

  What good looks like: every changed file and every user-visible behavior is inside the plan's stated boundary or an honestly noted deviation. The description says only what the diff actually changes; it does not claim a broader fix or a narrower one than the code actually delivers.

  ## Test evidence (harness category: not-tested)

  Where it lives: This lives in the PR's test-evidence section, the reproduction or verification steps in the plan, and any repo checks the PR names. The decisive evidence is observable: commands run, observed output, before/after behavior, or the repo's own CI/test results attached to the package.

  What good looks like: the evidence states the exact scenario or command, the expected outcome, and the actual result. A valid claim is not “tests pass” in the abstract; it is a named command or check with a visible outcome tied to the behavior being fixed.

  ## Diff quality (harness category: unreviewable)

  Where it lives: The unified diff, the changed-file list, and the commit list are the source of truth for this family. The PR's title and description may help explain intent, but the diff itself decides whether the patch is reviewable.

  What good looks like: the fix is obvious, the scope is focused, and the patch does not carry unrelated changes or dead code. There are no debug leftovers, commented-out blocks, formatting churn, or unrelated cleanup that bury the actual fix.

  ## Standards and comms (harness category: standards-wall)

  Where it lives: This is read from the repo-facts block, the PR template, the contribution policy, and any stated AI-use or disclosure requirement. In live mode, the same information lives in the repo's PR template and contribution guidance. The candidate PR title and description are compared against those asks.

  What good looks like: required sections are filled with real content, any required disclosure is present, and the PR follows the repo's communication standards without boilerplate or ignored asks. The template is used as written; the PR does not hide a required section or silently ignore a documented rule.
