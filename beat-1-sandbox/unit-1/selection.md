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

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/62

**Verdict output**

Active Project: pass — "Last push Sept 16, 2026; repo not archived"
Policy Check: pass — "No CONTRIBUTING.md found; silence passes"
Actionable Scope: pass — "Bug with specific files (api/routes/health.py, core/config.py), AttributeError on nonexistent field, fix is to use settings.redis_url — bounded"
Unclaimed: pass — "No assignees, no linked PRs, no claim comments in thread (external coursework commit is not a thread claim)"

```json
{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/62",
  "checks": [
    {
      "name": "Active Project",
      "grade": "pass",
      "evidence": "Last push Sept 16, 2026; repo not archived"
    },
    {
      "name": "Policy Check",
      "grade": "pass",
      "evidence": "No CONTRIBUTING.md found; silence passes"
    },
    {
      "name": "Actionable Scope",
      "grade": "pass",
      "evidence": "Bug: settings.redis_host doesn't exist on Settings (only redis_url does); fix is bounded to api/routes/health.py and core/config.py with clear AttributeError reproduction"
    },
    {
      "name": "Unclaimed",
      "grade": "pass",
      "evidence": "No assignees, no linked PRs, no claim comments in thread; external coursework repo commit does not constitute a thread claim"
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

issue-62: rubric decision = accept; gold label = accept. The issue evidence says: "Last push Sept 16, 2026; repo not archived" and "No CONTRIBUTING.md found; silence passes". It identifies a concrete bug: "settings.redis_host doesn't exist on Settings (only redis_url does)". The bounded fix is "to use settings.redis_url" in "api/routes/health.py" and "core/config.py", with a "clear AttributeError reproduction". It also says: "No assignees, no linked PRs, no claim comments in thread". That matches the rubric: Active Project passes, Policy Check passes, Actionable Scope passes, and Unclaimed passes.

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

1. The issue fits my interests well enough to be a good early contribution: it is a focused backend/configuration bug in a health check, directly in my stack and explicitly a "want to improve" area. It is narrow enough for a first contribution while still requiring understanding of the repository's settings and API route conventions.

2. The verdict correctly identified an active, policy-safe, and concrete issue. The repo had a "Last push Sept 16, 2026" and is not archived; no CONTRIBUTING.md was found; and the issue specifies the nonexistent `settings.redis_host`, the existing `settings.redis_url`, and the files involved. The fix is valuable because the health check currently raises an AttributeError instead of checking Redis health.

3. The difficulty in claiming it should be moderate and manageable. There are "No assignees, no linked PRs, no claim comments in thread", so the claim path is straightforward. The implementation is bounded to `api/routes/health.py` and `core/config.py`, with the main work being to reproduce the AttributeError, confirm the Settings field, and update the health check to use `settings.redis_url`.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
