# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/conda/conda/issues/16475

**Verdict output**

Active Project: pass — "last push to any branch: 2026-08-04" and the repo is not archived.
Policy Check: pass — "generative AI tools welcome; you are responsible for all contributions and must review and understand AI-generated content before including it in a pull request"
Actionable Scope: pass — the issue lays out a concrete doc migration: add a permanent task page, update three pages, and keep the older guidance as fallback.
Unclaimed: pass — "assignees: none; linked PRs: none"

```json
{
  "item": "https://github.com/conda/conda/issues/16475",
  "checks": [
    {
      "name": "Active Project",
      "grade": "pass",
      "evidence": "last push to any branch: 2026-08-04; repo archived: no"
    },
    {
      "name": "Policy Check",
      "grade": "pass",
      "evidence": "contribution policy: \"generative AI tools welcome; you are responsible for all contributions and must review and understand AI-generated content before including it in a pull request\""
    },
    {
      "name": "Actionable Scope",
      "grade": "pass",
      "evidence": "the issue specifies a permanent docs page plus concrete updates to manage-pkgs.rst, pip-interoperability.rst, and new-features.md"
    },
    {
      "name": "Unclaimed",
      "grade": "pass",
      "evidence": "assignees: none; linked PRs: none"
    }
  ],
  "verdict": "accept"
}
```

**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

- 20/20

**Issue analysis**

issue-01: rubric decision = accept; gold label = accept. The bundle says: "repo: conda/conda (7481 stars, archived: no)" and "last push to any branch: 2026-08-04". It also says: "contribution policy (CONTRIBUTING.md, section \"Generative AI\"): generative AI tools welcome; you are responsible for all contributions and must review and understand AI-generated content before including it in a pull request" and "this issue: assignees: none; linked PRs: none". The issue body gives a concrete scope: "Create a new task page ... Update `manage-pkgs.rst` ... Update `pip-interoperability.rst` ... Update `new-features.md`". That matches the rubric: Active Project passes, Policy Check passes, Actionable Scope passes, and Unclaimed passes.

**Check rationale**

I used the current `Actionable Scope` check exactly as written:

```text
| Actionable Scope | The issue body and the comment thread.                                                | Pass if the issue reports a bug or requests a specific feature with an actionable spec. Fail immediately if any of: (a) it is a user support question, an open-ended discussion, or maintainers state they do not want the change; (b) it is a meta/tracking issue that lists or indexes many other issues rather than describing one concrete change (a "megaissue"); (c) the thread or repo-facts show a pattern of the work stalling out despite the friendly label — two or more linked PRs against this issue were closed without merging, and/or a string of different contributors claimed the issue and then went quiet or were auto-unassigned for inactivity — signalling that the issue is harder in practice than the label suggests, even without a single explicit maintainer rejection; (d) the request has no concrete spec and leaves a product decision unmade (placeholder/TBD details, an unvalidated ask with no maintainer confirming the direction). Do NOT fail an issue just because it lacks exact file paths. | required |
```

I kept this check in its current form because it captures the biggest reason first issues fail: a proposal that sounds helpful but is too vague, too broad, or already stalled. It makes the pass/fail boundary explicit enough that someone else can apply it consistently without relying on gut feel.

**Trade-offs**

Nothing changed, and here is how I know: the final full run printed the exact result:

```text
categories: claimed 4/4  clear-accept 8/8  dead-repo 3/3  policy 1/1  scope 4/4
agreement: 20/20 scored items  (bar: 18/20: PASS)
```

This is the same final run recorded in `eval-run.txt`, and it confirms the rubric's checks and verdict were stable across the full scoring set.

---

## Selection rationale

**Selection rationale**

1. The issue fits my interests well enough to be a good early contribution: it is documentation-heavy and user-facing, which is low-risk for a first issue while still requiring real product understanding and repository-specific conventions. It also fits the time available because the work is narrow and concrete rather than a large systems change.

2. The verdict correctly identified an active, policy-safe, and concrete issue. The repo was recently pushed, the project is not archived, and the issue had a specific doc plan instead of a vague feature request. What I weighed beyond the rubric was that the task is still valuable even though it is not a code fix: it improves discoverability of a GA workflow and gives users a permanent source of truth.

3. The difficulty in claiming it should be moderate and manageable. There are no linked PRs, no assignees, and no policy blockers, so the claim path is straightforward; the only real work is understanding the docs structure and the exact pages that should be updated.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
