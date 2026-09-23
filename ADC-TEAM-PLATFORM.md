# ADC pattern: platform team across GitHub, Jira, and qTest

Informative application of [ADC 0.1.0-draft.1](ADC-SPEC.md). The team retains its scrum and PI planning. Jira, GitHub, qTest, and operational records each hold the facts they are already good at holding. Names, URLs, issue keys, observations, and results in the worked example are fictional. The template does not install a new status flow or impose qTest on every kind of work.

## Assign meaning to the existing systems

| System | Typical authoritative fact | What its status alone does not establish |
| --- | --- | --- |
| Jira work item | Overall intent, planning/PI context, scope, current undertaking disposition, material decisions, unresolved work and final bounded assessment. | A `Done` workflow status does not by itself establish all effects across repositories or production. |
| GitHub PRs and commits | Exact proposed and merged code/configuration revisions, discussion and checks tied to those revisions. | Merge does not establish deployment, successful operation, or the broader Jira outcome. |
| qTest Manager, when tests are managed there | Defined case and the particular **test run/log** result against its relevant environment and revision. | A test case's existence or a stale passing run does not establish current execution or every operational effect. |
| Change/incident/observability records | Applied action and time-bounded observation of the actual environment; rollback, cleanup and impact. | A request accepted by an API does not alone establish effective configuration. |
| Maintained architecture or runbook document | A decision or operational rule intended to outlive the undertaking. | A document update does not establish a deployed change. |

The Jira item is usually the **current work account**; its references point to the evidence held elsewhere. A qTest–Jira integration is useful when present but not a prerequisite. Tricentis distinguishes [test cases from test runs and their logs](https://docs.tricentis.com/qtest-saas/content/manager/execute_test_runs.htm); use the relevant run/log, not only a generic coverage link. Jira can [link work items across projects](https://support.atlassian.com/jira-software-cloud/docs/link-issues/) when the local configuration permits. A PI objective and sprint may organize and prioritize the undertaking; they need not become extra ADC artifacts.

For several repositories, put the overall expected outcome and disposition in one existing Jira item where possible. Link each affected PR and state which portion it covers. Use separately tracked work only when authority, ownership, evaluation, or planning already makes the work separable. If Jira issues in different projects are required, designate the issue whose account governs the overall outcome and link the others; conflicting status labels remain explicitly unresolved until reconciled.

## Copyable Jira account text

Use existing description, acceptance notes, comments, and links before adding headings. The following is a compact update at a material boundary, not a recurring form. Delete irrelevant prompts.

```markdown
Outcome and bounds: [What must become true, for whom/where; relevant exclusions.]
Current state: [Observed state and undertaking disposition, distinct from Jira status.]
Changes and decisions: [Affected repo PRs, material choices and their reasons.]
Basis and limits: [Exact qTest run/log if applicable, code revision, operational observation; unsupported claims.]
Remaining/closure: [Who/what is needed next, or which scope is complete/abandoned and why.]
```

An agent taking over reads the Jira account and links, then checks relevant current conditions before acting. On handoff, the person or agent leaving work updates the same account with live state and material uncertainty. A peer can then read the basis for an outcome without replaying agent sessions. Team-specific change approvals and security controls retain their own authority; this example does not grant access or define an approval gate.

## Worked example: SSM connectivity filter across two repositories

The fictional Jira work item `PLAT-482` belongs to a PI objective to reduce avoidable automation failures. The undertaking is to exclude AWS instances whose SSM connection is unavailable from a specific AAP job launch **without hiding excluded hosts**. One GitHub repo implements the inventory/filter logic; another changes the affected AAP job configuration. The PI objective groups planning; it does not supply the acceptance evidence.

**Jira `PLAT-482`, intent and boundaries.**

> A qualifying launch should attempt connected hosts, mark unreachable hosts as excluded with a visible count, and preserve the pre-existing inventory behavior for hosts not in this target group. Do not silently reinterpret an unavailable SSM connection as a successful job. Change only the identified job template; no account-wide inventory policy change. Evaluation: staging tests on connected/unavailable scenarios and an observed production launch on the named job after both repository changes are applied.

**Linked source and test records.**

| Record | Fictional observation | What it supports |
| --- | --- | --- |
| Filter repo PR `#31` at revision `f31` | Unit checks show 12 connected and 3 unavailable hosts: connected hosts selected, 3 excluded; review confirms excluded-host count is emitted. | Filter behavior against synthetic cases. |
| AAP config repo PR `#12` at revision `c12` | Staging job template points to the new filter; configuration review finds no other template changed. | Proposed configuration for the named job in that revision. |
| qTest test run `RUN-812`, log `LOG-812a`, staging at 10:20 | Connected/unavailable case passed against staging revisions `f31` and `c12`; explicit steps found 12 attempted and 3 excluded, with exclusion visible. | The staging integration observation; no claim about production. |

**Jira update at the end of a sprint.**

> State: open. Both PRs merged; qTest staging run passed for the two recorded revisions. Production application and launch have not been observed. No live outcome is claimed. Next: authorized operator applies the job change, then records target, time, effective configuration, attempted/excluded host counts, and monitoring interval in the existing operations record. Sprint completion does not close this undertaking.

**Later Jira closure, if the following fictional operational evidence existed.**

> Operations record `OPS-91` reports the named production job at 14:10 using filter revision `f31` and effective configuration `c12`; the 14:15 launch attempted 12 connected hosts and recorded 3 unavailable hosts as excluded with their identifiers. No broader fleet behavior was examined. Complete for the named-job launch and visibility scope, supported by `OPS-91`, PRs `#31`/`#12`, and staging run `RUN-812`/log `LOG-812a`. The fallback behavior when an SSM connection drops *during* a run is untested and remains a separately identified follow-up; it was not part of this undertaking's declared scope.

If the production observation instead shows hidden hosts, retain the failed result, keep the undertaking open or abandon it with reason, and record recovery. Do not rewrite acceptance conditions after seeing the result. For a pure operational incident investigation, the Jira item and incident log can hold all relevant meaning; GitHub PRs and qTest results need not exist.

For example, a separate fictional Jira investigation `PLAT-483` asks whether the retained controller and SSM logs explain a one-hour spike in `TargetNotConnected`. The incident log shows 18 such failures, but its timestamps cannot distinguish transient disconnection from a credential problem. The Jira item can close as **investigation complete, cause unresolved**, with the log interval and missing evidence identified and a proposed telemetry change recorded as separate, unstarted work. No PR, qTest entry, or product increment is needed for that outcome.

## Keep coordination proportional

Retain the team's existing Jira issue types, PI planning, sprint board and qTest practices. Do not create an extra Jira ticket, qTest case, and repo file per undertaking. Preserve a significant decision in its durable owner, then point related work at it. A Jira item may close after a bounded investigation reports an unknown cause; a deployment item must not close merely because implementation is merged. Cross-repo links make a single outcome review possible without copying every PR description into Jira.

After representative work, run the small recovery check in the [adoption plan](ADC-ADOPTION.md): someone outside the work should be able to explain the original purpose, actual state, evidence coverage and remaining obligations using the existing records. Adjust the mapping where this fails.
