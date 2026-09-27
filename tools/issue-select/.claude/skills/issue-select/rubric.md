# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check            | Evidence                                                                              | Pass condition                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | Weight   |
| ---------------- | ------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------- |
| Active Project   | The `repo-facts` block ("last push to any branch", "last 5 default-branch commits") and the comment thread.                                        | Fail immediately if the repository is archived. Otherwise pass if "last push to any branch" is within the last 12 months. If it is older than 12 months, pass only if a maintainer (owner/member/collaborator) has actually commented in this issue's own thread within the last 12 months — a maintainer first-response *sample* full of "no maintainer comment in thread" entries does not satisfy this; that pattern, combined with a stale last push, is the signature of a repo that no longer engages issues even though the code still exists.                                                                     | required |
| Policy Check     | The `repo-facts` block (specifically the contributing guidelines) and the issue body. | Fail immediately if the issue proposes work that violates an explicit rule in the contributing guidelines (e.g., if the issue is a typo/cosmetic fix, and the guidelines ban "typo fixes" or "trivial changes"). Also fail immediately if the contributing guidelines impose a blanket, unconditional ban on AI-generated contributions with no carve-out for disclosed, reviewed, or assistive AI use (e.g., "we do not accept AI-generated code or documentation" with no exception). Do NOT fail when the policy merely discourages, restricts, or conditions AI use (requires review/disclosure, bans only fully-autonomous/undisclosed output while allowing assistive use, or closes untested AI PRs) — those are workable constraints, not a ban. Otherwise, pass.                                                                  | required |
| Actionable Scope | The issue body and the comment thread.                                                | Pass if the issue reports a bug or requests a specific feature with an actionable spec. Fail immediately if any of: (a) it is a user support question, an open-ended discussion, or maintainers state they do not want the change; (b) it is a meta/tracking issue that lists or indexes many other issues rather than describing one concrete change (a "megaissue"); (c) the thread or repo-facts show a pattern of the work stalling out despite the friendly label — two or more linked PRs against this issue were closed without merging, and/or a string of different contributors claimed the issue and then went quiet or were auto-unassigned for inactivity — signalling that the issue is harder in practice than the label suggests, even without a single explicit maintainer rejection; (d) the request has no concrete spec and leaves a product decision unmade (placeholder/TBD details, an unvalidated ask with no maintainer confirming the direction). Do NOT fail an issue just because it lacks exact file paths. | required |
| Unclaimed        | The comment thread and linked PRs in the `repo-facts` block.                          | Pass if there are 0 open pull requests linked to the issue, AND no contributor has claimed the issue in the comments (unless they claimed it over a month ago or abandoned it).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | required |

## Verdict rule

Accept if every required check passes. Any check that is marked as failed or unclear counts as a fail, resulting in immediate rejection of the issue.
