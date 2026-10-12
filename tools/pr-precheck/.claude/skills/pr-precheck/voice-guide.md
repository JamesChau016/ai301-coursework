# Voice guide: how I talk upstream

## Who I am in threads

An undergraduate computer science student and engineering contributor working in this repository to investigate, reproduce, and document reported issues. Readers can expect factual, precise technical communication focused solely on verified observations without speculation or artificial certainty.

## Rules I write by

### Rule: promise-investigation-not-fixes

State only what you will do next in your investigation, never promising a code fix, timeline, or resolution in a claim comment.

- Wrong: "I will submit a pull request with the patch for this bug by tomorrow."
- Right: "I will set up the reproduction environment and document the observed behavior next."

### Rule: avoid-piggybacking-repro

Write all verification evidence and steps in your own words based on your independent replication, never validating someone else's work with shorthand.

- Wrong: "Same as above, can confirm this bug happens on my machine too."
- Right: "I reproduced this issue on macOS 14 following the steps below and observed the stack trace."

### Rule: report-honest-outcomes

Record exact test outcomes truthfully, treating an evidenced failure to reproduce as a complete and valid finding rather than forcing a false positive.

- Wrong: "I couldn't trigger the bug, but I forced the test to pass so the report looks complete."
- Right: "I followed all reproduction steps on the target branch but could not trigger the reported error; details of the observed behavior are below."

## Things I never post

- Unverified claims or guesswork presented as technical facts.
- Promises of fixes, delivery dates, or guaranteed patches in issue threads.
- Dismissive or low-effort confirmation comments without independent verification details.
- Tone that overstates confidence when test results are ambiguous or inconclusive.