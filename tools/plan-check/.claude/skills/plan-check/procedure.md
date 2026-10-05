# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

1. Repo facts — note the contribution policy, especially any AI-use
   disclosure rule and whether it covers comments or only PRs.
2. Issue + thread highlights (live: the issue thread) — note the
   reported behavior and every maintainer signal: an identified
   culprit, a proposed or rejected approach, an existing patch or open
   PR.
3. Repro evidence (eval: repro-evidence block; live: the student's
   posted repro comment, or the house repro pack) — note the steps,
   observed behavior, and control runs. Read before the plan: the
   diagnosis is graded against this, not on plausibility.
4. Candidate plan — note the stated cause, every proposed change and
   its location, the not-in-scope statement, and the test plan.
5. Plan comment — note whether it engages the thread signals from
   step 2 and meets the policy from step 1.

## Evidence gathering

Record one deciding quote (or noted absence) per check — never "looks
fine":

- **diagnosis**: the stated cause, the repro line(s) that support or
  contradict it, and whether the planned change fixes that cause or
  works around it (docs note, catch-all recover, retry).
- **scope**: list each proposed change and ask "is this needed to fix
  this bug?" — record any that aren't (refactor, upgrade, new
  option/feature, "while in there"). Record each change's location; a
  function or named code path counts, as does an unpinned function
  the plan says it will pin. Record the not-in-scope statement, or
  "not stated."
- **test**: the test plan verbatim. Record (a) whether it gives
  concrete verification steps with a specific observable result, vs.
  vague language, for `test`, and (b) whether it names an automated
  test (file, command, or CI check), for `automated-test`.
- **thread**: each maintainer signal from the thread and whether the
  plan follows, engages, or ignores/contradicts it (e.g., plan rules
  out the code change a maintainer already located and patched).
  Separately, the policy's comment requirements and whether the
  comment meets them (e.g., a required AI disclosure is present).

If evidence is genuinely absent, record the absence itself — don't
search outside the package (eval: the bundle is the whole world; live:
only what the drafts/thread contain).

## Check execution

1. Grade in order: diagnosis, scope, test, thread, automated-test.
2. Grade each independently against its rubric pass condition, using
   only its own recorded evidence — one check's grade never influences
   another's.
3. `P`: evidence satisfies the pass condition. `F`: evidence
   contradicts it or is missing outright. `?`: evidence is genuinely
   ambiguous or split — never a stand-in for not having looked.
4. Grade from the recorded evidence in one pass; re-read the source
   only if that evidence looks contradictory.

## Verdict assembly

1. Apply the rubric's rule: `accept` only if diagnosis, scope, test,
   and thread (the required checks) all grade `P`. Any `F` or `?` on one of
   these → `reject`. `automated-test` is `preferred`: its grade is
   still reported but never changes the verdict either way.
2. `?` counts as `F` for the verdict, per the rubric's stated stance.
3. In the output JSON, each check's `evidence` field is the one quote
   recorded for it above. If multiple required checks fail, name all
   of them.
