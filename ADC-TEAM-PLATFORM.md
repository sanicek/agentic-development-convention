# ADC pattern: platform team across repositories

Informative example under [ADC 0.1.0-draft.1](ADC-SPEC.md). Git holds the agent-readable work account; Jira retains scrum/PI planning and required workflow. qTest and operations systems hold their own observations. Names, keys, revisions, and results below are fictional.

## Choose one discoverable work root

For a cross-repo undertaking, choose the repo that owns its outcome. If no product repo owns platform work across many repos, use a small `platform-workspace` repository. Its root `WORK.md` indexes active work; each `work/` account points to affected repos, checked branches/revisions, Jira items, tests, and operational observations. This is a work map, not a monorepo or a copy of every repository.

Each affected repo also contains a short active pointer in its own `WORK.md`:

```markdown
| Work | Local branch/revision at checkpoint | Canonical account |
| --- | --- | --- |
| PLAT-482 SSM filter | `ssm-filter` / `f31` | https://github.com/ORG/platform-workspace/blob/main/work/PLAT-482.md |
```

From an affected repo clone, an agent finds local work and reaches the broader account; from the work-root clone it finds the entire cross-repo undertaking. The full account is not available offline from every affected repo without replication. Keep one canonical account to prevent divergence. Publish pointers and checkpoints to discoverable default branches under ordinary review controls. An unpublished worktree is outside what a clean clone can know.

## Copyable cross-repo account

```markdown
# PLAT-482 — [Outcome or question]

Intent: [Desired effect or bounded question; constraints and evaluation.]
State at checkpoint: [When observed; disposition; actual versus proposed.]
Repos: [URL, branch, checked revision, merged/applied status for each repo.]
External: [Jira item; qTest run/log if relevant; operations observation.]
Assessment: [Result and evidence scope, conflicts, limits, unknowns.]
Next: [Action or resumption condition; authority if material.]
```

Jira decides priority, PI/sprint placement, assignment, and local approvals. Git is authoritative for the undertaking's last *recorded* intent, state, and assessment. A qTest run/log, CI check, or operations record establishes its own bounded observation. If Jira says `Done` but the account says “deployment unverified,” reconcile the conflict rather than accepting either label as proof. A bot may post a link or brief checkpoint to Jira; two-way prose synchronization is not assumed.

## Worked example: SSM filter across two repos

`PLAT-482` aims to exclude instances whose SSM connection is unavailable at launch from one AAP job, while reporting their identifiers and count. Acceptance requires staging checks for connected and unavailable hosts and an observed launch of the named production job after both changes are applied. Account-wide inventory behavior is out of scope.

The work root's `WORK.md` links `work/PLAT-482.md`. The filter and AAP configuration repos each point there from their `WORK.md`. The account checkpoint reads:

```markdown
# PLAT-482 — Visible SSM exclusion for named AAP job

Intent: Attempt connected hosts, report unavailable hosts as excluded, and
preserve behavior outside the named job. Evaluate with staging cases and a
production launch after both changes are applied.

State at checkpoint: Open, 2026-09-25 10:20 UTC. Both changes merged and
staging checked. Production application and launch are unobserved.

Repos: filter repo revision `f31` merged; AAP config repo revision `c12`
merged. Confirm effective deployed revisions before claiming live behavior.

External: Jira PLAT-482 (planning); qTest run RUN-812, log LOG-812a
(staging). No production operations record yet.

Assessment: RUN-812 observed 12 attempted and 3 visibly excluded hosts
with `f31` and `c12` in staging. This supports that staging case only.

Next: Authorized operator applies both changes, confirms effective target
configuration, records the production launch and exclusion counts in the
operations record, then updates this account with the bounded conclusion.
```

If an operations record later confirms the intended behavior, update the account with target, time, effective revisions, result, and limits; mark complete for that scope and remove active pointers. If production differs, record the discrepancy and recovery. Jira status alone cannot resolve the conflict.

For a no-code investigation, omit `Repos` and qTest. An investigation of a one-hour `TargetNotConnected` spike may finish with “18 failures observed; cause unresolved because retained logs cannot distinguish disconnection from credentials.” The investigation can be complete while the causal claim remains unknown. Jira still supplies planning and ownership.

## Consistency limit

Checked commit IDs across repos describe a reproducible *source snapshot* only if those revisions remain fetchable. They do not constitute an atomic transaction or prove that live infrastructure matches. A rolling “latest” loses reproducibility. A new agent fetches checked revisions and current branch tips, inspects drift, and reads current Jira and live state as needed. Concurrent changes to one account use ordinary Git conflict resolution and a fresh state check.

Pilot one existing cross-repo outcome before adding `WORK.md` everywhere. The [adoption plan](ADC-ADOPTION.md) defines the recovery check.
