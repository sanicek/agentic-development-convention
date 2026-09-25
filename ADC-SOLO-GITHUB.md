# ADC pattern: solo developer, starting from a clone

Informative example under [ADC 0.1.0-draft.1](ADC-SPEC.md). The repository is the entry point; GitHub issues and Projects are optional planning surfaces. IDs, revisions, and observations below are fictional.

## Minimal layout

```text
WORK.md                 Active work and how to read it
work/EE-17.md           One undertaking spanning sessions
```

Create the index when there is work whose state cannot be recovered from code and commits alone. An active row links its account. For a tiny fix completed in one sitting, a commit message can record purpose and direct check without an index row. Remove completed multi-session work from the active index, retaining its account in Git for history. There is no mandatory archive catalog.

## Copyable account

```markdown
# EE-17 — Restore execution environment imports

Intent: [Desired result or question, evaluation basis, material constraints.]
State at checkpoint: [When, disposition, what is true, branch/revision described.]
Assessment: [Observation, target/revision/environment, result and limits.]
Next: [Action, resumption condition, or reason work has stopped.]
```

Write only material facts. Add a decision and its reason when it changes future interpretation. The state is a dated checkpoint, not a live status after someone changes a branch or environment. An agent opens `WORK.md`, reads the account, checks the named revision and relevant current conditions, then acts. A PR or issue link may help, but is not required to understand the account.

## Worked example

An AAP execution environment update breaks a collection import. The developer starts branch `ee-17-imports`, publishes the opening account and active index row to the default branch through normal repository review, and continues implementation on the feature branch. The opening checkpoint reads:

```markdown
# EE-17 — Restore imports after dependency update

Intent: Build the existing base EE and import the target collection with the
supported Python version. Preserve production image tags. Publishing the
image is outside this undertaking.

State at checkpoint: Open, 2026-09-25. The baseline at `b41` fails its
import check. Work continues on `ee-17-imports`; `b41` is the last checked
revision. The proposed dependency pin is unvalidated.

Assessment: Import failure observed in local image `ee-test:17a`.
The dependency mismatch is a hypothesis, not a verified cause.

Next: Build with the proposed pin, inspect installed versions, and run the
import check against that exact image.
```

At handoff, update the account on the discoverable branch with the checked revision and results. If the feature branch contains newer unrecorded commits, the incoming agent detects and evaluates the drift. After checking the final revision, record the bounded result and remove the active index row. Merge or PR status alone does not supply the assessment.

This pattern has a cost: discoverable in-progress work requires a published checkpoint. A solo developer who does not need that guarantee can keep the account only on the feature branch, accepting that a clean default-branch clone cannot automatically find it.
