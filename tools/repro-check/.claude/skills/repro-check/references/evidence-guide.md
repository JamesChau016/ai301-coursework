# Evidence guide: where proof lives in a reproduction package

Every rubric check needs an evidence source. This guide maps the five
criterion families to concrete places you can look: on github.com when
you are sizing up a live reproduction by hand, and in the snapshot bundle when
you are in eval mode.

## Environment

- **Where it lives:**
  - _In the eval bundle:_ The reproduction report text, specifically sections labeled "Environment", "System Info", or blocks showing version commands (e.g., `node -v`, `sw_vers`). Compare this against the system constraints mentioned in the original issue description.
  - _In live mode:_ The draft reproduction comment or the linked report file.
- **What good looks like:** The OS (including version, e.g., macOS 14.2) and the specific tool/runtime versions (e.g., Node.js v20.11.0, yq 4.44) used to run the tests are explicitly stated. If the original issue specifies a target environment, the report's environment either matches it or explicitly names the variance.

## Steps

- **Where it lives:**
  - _In the eval bundle / In live mode:_ The "Steps to reproduce" section of the reproduction report or comment.
- **What good looks like:** The steps form an unbroken, sequential chain of executable commands or explicit actions starting from a known baseline (e.g., cloning the repo, checking out the target branch, installing dependencies). A report may identify and run a self-contained script supplied verbatim by the issue, but it must name the script and state the relevant inputs, options, and parameters. Behavior-critical setup must be reproducible; routine boilerplate may be summarized when it cannot change the trigger.

## Behavior shown

- **Where it lives:**
  - _In the eval bundle:_ The "Observed behavior", "Actual Output", or "Logs" section of the reproduction report, read directly against the original issue's description.
  - _In live mode:_ The code blocks, stack traces, or terminal excerpts provided by the student in their draft.
- **What good looks like:** The provided artifacts (terminal output, stack trace, error message) precisely mirror the _core symptom_ described by the issue opener. A controlled cannot-reproduce attempt also passes when it exercises the issue's trigger and records the contrasting expected-versus-actual output. A report fails when it shows only a generic setup failure, a missing dependency error, or an unrelated secondary bug.

## Honesty

- **Where it lives:**
  - _In the eval bundle / In live mode:_ The conclusion, summary, or final verdict stated by the author in the report, read strictly against the evidence provided in the "Behavior shown" section.
- **What good looks like:** The stated outcome perfectly matches the observable evidence. If the author could not trigger the bug, the report plainly states "I could not reproduce this issue" and shows the passing logs (an evidenced cannot-reproduce is a valid pass). A package fails this check if it claims "Successfully reproduced" but the logs show an unrelated error, or if it tries to force a false-positive success.

## Comms

- **Where it lives:**
  - _In the eval bundle:_ The text of the claim comment and the report, read against the "contribution policy" line under the Repo facts block (which summarizes `CONTRIBUTING.md`, AI policies, or templates).
  - _In live mode:_ The draft comment text read against the repository's live contribution guidelines and the Voice Guide rules.
- **What good looks like:** The language is professional, factual, and strictly states what the author observed or will do (e.g., "I will set up the environment", not "I will fix this"). Crucially, if the repo's policy requires AI-use disclosure, the comment explicitly includes that disclosure. It follows conventions without overpromising.

## Current version

- **Where it lives:** The reproduction report's environment and verification statements, compared with the issue description and the repo-facts block.
- **What good looks like:** If the repository's bug-report requirements ask for testing on the latest release and the main branch, the report explicitly records both checks and their outcomes. A report that only tests an older release fails this check even if the older release reproduces the symptom.
