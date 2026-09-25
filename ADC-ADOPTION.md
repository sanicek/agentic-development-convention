# Putting ADC into practice: repo-first pilot

Informative adoption design for [ADC 0.1.0-draft.1](ADC-SPEC.md). This is a proposed storage and reading convention for two settings, not an added core requirement. It tests whether a repository checkout gives an agent enough context to find and resume work. The templates and observations are illustrative.

## The entry-point requirement

From a known repository's default branch, a new participant should find active undertakings, their canonical accounts, the last recorded state, and how to continue. The participant follows references to source revisions, Jira, qTest, and operational observations as needed. The checkout is a **map and durable checkpoint**; it cannot certify the current state of an external system.

`WORK.md` at the root is the suggested entry point. It indexes unfinished undertakings. Nontrivial work gets one small account in `work/`. Closed work leaves the active index, while its account and Git history remain. A tiny completed change can be accounted for in its commit message. These filenames are local choices, not ADC syntax.

```markdown
# Work entry point

Read this file before selecting work. Each active entry points to its canonical
account. Verify branch/revision and external conditions before acting.

| Work | State at checkpoint | Account | External planning |
| --- | --- | --- | --- |
| EE import repair | Waiting for local build | [EE-17](work/EE-17.md) | none |
```

Update an account at a material checkpoint: handoff, suspension, decision, changed scope, or claimed outcome. Routine commits need no separate status update. The agent edits ordinary source text and reviews the diff. No special parser, CLI, ticket type, or workflow engine is assumed.

## Where authority lives

| Meaning | Solo repository | Multi-repo platform work |
| --- | --- | --- |
| Intent, last recorded state, assessment | Account in the affected repo; `WORK.md` finds active work. | One account in a coordination/owning repo; its `WORK.md` finds active work. Affected repos point to it from their own `WORK.md`. |
| Repository contents | Commits and branches in that repo. | Commits and branches in each affected repo, identified by revision and branch in the account. |
| Planning and coordination | Optional GitHub issue/Project. | Jira owns prioritization, sprint/PI context, assignment, and required workflow; the Git account links the item. |
| Checks and observed live effects | CI run or bounded observation, summarized or linked with target and result. | qTest run/log if used, CI, incident/change record, or telemetry, interpreted in the account. |
| Approvals and access | Existing repository policy. | Existing organizational controls; a Git account grants no approval. |

This changes the previous draft's assumption that a GitHub issue or Jira item is normally the work account. Trackers remain planning views and control points. When a Jira status or PR merge conflicts with an account, reconcile the discrepancy; do not infer an outcome from the status. Avoid automatic two-way copying of prose. Stable IDs and links usually suffice.

## Visibility boundary

An account committed only to a feature branch is invisible to a clone of the default branch. To meet the entry-point requirement, publish the active index and a checkpoint account to a discoverable default branch when work starts or is handed off, under normal review policy. Between checkpoints the implementation branch may advance: the account identifies the branch and checked revision, and the next agent fetches and reconciles drift. If publishing checkpoints is infeasible, the guarantee must be narrowed. A clone cannot discover unpublished work.

Git cannot atomically snapshot several repositories or a live service. Record exact revisions at a handoff; check current branch tips and external conditions before acting. Restricted evidence remains in its authorized system; the account retains a non-secret bounded summary and an access-aware reference. Historical observations are not live truth.

## Pilot

1. [Solo](ADC-SOLO-GITHUB.md): add `WORK.md` to one repo, track one multi-session task, and leave a tiny fix in a commit message. Resume the task from a clean clone in a new session.
2. [Team](ADC-TEAM-PLATFORM.md): select one existing cross-repo outcome. Add one canonical account to an owning or coordination repo and pointers in affected repos. Keep Jira/PI and qTest practices. Resume from the root clone, then from one affected repo.
3. In both cases, ask a fresh agent to state purpose, last known state, exact revisions, evidence limits, and next action without prior chat or starting in a tracker. Check whether it detects changed branches and external conditions.
4. Count duplicate upkeep and missed handoffs. Fix publication/discovery first if the clone cannot reveal active work. Remove fields that do not improve recovery.

This tests an **agent-readable work layer above Git revisions**. It does not make repository files mandatory in ADC core. A future workspace-state tool could automate indexing and projections while preserving these meanings.
