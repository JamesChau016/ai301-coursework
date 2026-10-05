# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

Where it lives: the plan's stated-cause line (eval: in the candidate
plan section, usually near the top; live: the "cause" or "diagnosis"
part of the draft plan.md), read against the repro-evidence block
(eval) or the student's posted repro comment / house repro pack
(live) — specifically the steps and the observed behavior they pin
down.

What good looks like: the stated cause explains the exact behavior the
repro evidence shows (including its control runs), and the planned
change fixes that cause. A diagnosis that explains a different symptom,
leans on causes the evidence never touched, or is paired with a
workaround (document the workaround, wrap it in recover/retry) does
not pass.

## Scope

Where it lives: the plan's scope/in-scope statement, its "files and
areas" line, its proposed-changes or approach list, and its "not in
scope" line.

What good looks like: one bounded change. Every proposed item is
needed to fix this bug, and each location is findable: a file, a
function (e.g. `AdaptDispatch::EraseInDisplay`), or a named code path
(e.g. "the reattach path in `zellij-server`'s client connection
handling, exact functions pinned via debug logs"). It also names what
it leaves alone. Red flags: "while in there", "rather than spot-fix",
dependency upgrades, new user-facing options, module restructures,
"somewhere around", "look into".

## Test plan

Where it lives: the plan's test plan or "how success will be
verified" section (eval: the candidate plan; live: plan.md), read
against the repro-evidence block's steps and artifacts.

What good looks like: the test plan names concrete, specific steps —
the exact actions to take and the exact observable result that
confirms the fix, mapped onto the repro steps — not "test manually" or
"verify it works." An automated test (a test file/function to add, or
a command/CI check that runs it) whose failure before the fix and pass
after the fix maps onto those steps is a plus, not a minimum.

## Executability

Not used by this rubric's checks (no check currently reads
executability). Leave unfilled unless a future check names it.

## Honesty

Not used by this rubric's checks (no check currently reads stated
unknowns or deviations). Leave unfilled unless a future check names
it.

## Comms

Read by the `thread` check.

Where it lives: the thread highlights (live: the issue thread) for
maintainer signals, and the repo-facts contribution-policy line, read
against the candidate plan and plan comment.

What good looks like: the plan follows or explicitly engages with
what maintainers said, building on an identified culprit, taking a
proposed approach or avoiding a rejected one, and acknowledging an
existing patch or open PR instead of racing it. A plan that rules out
the code change a maintainer has already located or patched fails.
On policy, the comment meets every rule that applies to comments.
When the policy requires AI-use disclosure covering comments ("all AI
usage in any form must be disclosed"), the comment states the tool and
extent. When disclosure is required only in the PR, the comment needs
none.
