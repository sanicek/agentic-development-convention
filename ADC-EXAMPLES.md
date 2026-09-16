# ADC worked examples

Informative companion to [ADC 0.1.0-draft.1](ADC-SPEC.md). These examples add no requirements.

**Every undertaking, person, identifier, permission, measurement, and observation below is fictional.** Embedded evidence is illustrative, not executed work. Identifiers resolve within their example. Conformance assessments assume the described handling occurred and records remain accessible; they do not certify real work.

Different consequences justify different record volumes. Labels such as `B1` are local conveniences, not required syntax. Existing records can carry these accounts.

## 1. Trivial code correction: one retained message

An authorized spelling correction leaves one record with its revision:

> T1, revision 18, 09:05. Correct the spelling in the host lookup error without changing behavior. Replaced `raise LookupError("Unkown host")` with `raise LookupError("Unknown host")`. Inspected the before/after statement and the complete one-line change: the exception type and control flow are unchanged. Complete for this wording-only scope. Runtime behavior was not exercised; no behavioral change is claimed. Nothing remains.

Intent, constraint, revision, inspection, limitation, and closure fit together. Separate artifacts add no useful meaning. Inspection supports the spelling claim, not general application correctness.

## 2. Brownfield feature: partially implemented and suspended

### Existing issue B1 — current account at 11:30

**Intent:** Add CSV export to the existing asset search. Completion means that authorized users can export exactly the assets visible to them, retaining non-ASCII names, with regression checks for the existing permission boundary. The feature is not complete merely when a serializer exists.

**Constraints:** Preserve the current endpoint and permission rules. Work only against synthetic data and the isolated development copy. Production access and production-data extraction are not authorized. Existing duplicate display names must not be merged.

**State:** Suspended. The development copy contains serializer revision S2 and an unwired export endpoint. No production changes or background tasks exist. S2 writes the internal asset key as a separate column; the previous S1 proposal to group by display name is superseded because it loses distinct records. This decision changes serialization, not the permission contract.

### B2 — embedded development-check record

The fixture contains three assets: `a1, Bratislava, group-red`; `a2, Žilina, group-red`; `a3, Bratislava, group-blue`. The simulated red-group user should receive the first two only.

| Check on revision S2 | Observed result in this fictional run | What it establishes |
| --- | --- | --- |
| Serialize already-filtered `a1,a2` | Header `id,name`; rows `a1,Bratislava` and `a2,Žilina` | This input preserves both records and the accented name. |
| Serialize all three records | Three distinct rows | Duplicate names are not collapsed. |
| Request export through the existing authorization path | Not executed: representative permission fixture unavailable | No endpoint-level permission claim. |

Producer-written checks support the tested serialization behavior, not authorization, spreadsheet compatibility, or production performance.

### B3 — continuation

The application maintainer must provide an approved synthetic permission fixture representing inherited permissions. Resume when that fixture is available; connect the endpoint, run permission-boundary and regression checks, and inspect actual exported bytes. Until then, retain B1–B3 and the development copy. Another participant can continue without recreating why name-based grouping was rejected. Closing B1 as completed would violate the original scope.

## 3. Infrastructure configuration: attempted change and verified recovery

### Operations record O1 — current account at 12:20

**Intent:** Increase the forwarding retry limit from two to four across eight collectors without exceeding a 200 ms p95 delivery-delay limit during the observation window. Completion requires observed convergence and acceptable forwarding behavior, not merely successful configuration requests.

**Authority and containment:** The service owner authorizes the on-call operator to change only collectors C1 and C2 first. The remaining six require a new rollout decision. Limit the initial observation to ten minutes; restore the previous configuration if delay exceeds the limit. No claim is made that this two-node sample represents the whole fleet.

The risk is delayed forwarding under repeated failures. Previous configuration R2 is retained; R4 is the candidate. A second operator checks effective configuration and receiver telemetry independently of the apply command.

### O2 — embedded observations

| Targets and time | Requested action | Observed state and result |
| --- | --- | --- |
| C1–C2, 12:00 | Apply R4, retry limit four | Requests accepted; effective-configuration reads report four on both. |
| C1–C2, 12:00–12:10 | Observe forwarding | Receiver reports p95 delays of 260 ms and 244 ms, above the 200 ms limit. |
| C1–C2, 12:11 | Restore R2 | Requests accepted; independent reads at 12:12 report retry limit two on both. |
| C1–C2, 12:12–12:20 | Observe recovery | Receiver p95 delays are 112 ms and 119 ms; no missing sequence numbers in that window. |
| C3–C6, 12:18 | Read only | Effective retry limit two; no change attempted. |
| C7–C8, 12:18 | Read only | Unreachable; current configuration and delivery health unknown. Last observation yesterday reported two. |

### O3 — disposition and remaining responsibility

The fleet-wide undertaking is **suspended**, not complete. The initial rollout failed its observed delay criterion. Recovery of C1–C2 is complete for restored configuration and the stated observation window; this does not prove permanent health or recovery of offline collectors. R4 is rejected for further rollout pending explanation of the delay.

The on-call operator must check C7–C8 when connectivity returns. Resumption requires service-owner approval of a revised approach. No update remains queued; further configuration changes are not authorized. Failed change and bounded recovery remain distinct.

## 4. Production incident investigation: complete inquiry, unknown cause

### Incident notebook I1 — 14:45 closure

**Question and scope:** During a 45-minute read-only investigation, determine what the retained telemetry can establish about the 14:00–14:08 error spike. Produce a supported finding and identify missing discriminating evidence. Finding a definitive root cause is desirable, but is not the completion condition of this bounded inquiry.

**Constraints:** Do not change production or access request payloads. Preserve uncertainty between the release-related and connection-exhaustion explanations. Mitigation is handled in the existing incident record, not performed by this investigation.

### I2 — evidence retained in the notebook

| Existing observation | Interpretation and limit |
| --- | --- |
| Release log: revision V8 became active at 14:00. | Establishes timing, not causation. |
| Minute aggregates: 14:01 error rate 12%, connection occupancy 98%; 13:59 values 0.2% and 61%. | Both symptoms increased within the same aggregation interval; ordering is unavailable. |
| Incident action record: V7 restored at 14:08. At 14:10, error rate 0.3% and occupancy 64%. | Recovery followed rollback; the traffic mix was not held constant. |
| Request-level traces: not retained. | Cannot connect individual errors to waiting for connections or specific V8 behavior. |

**Assessment:** The bounded investigation is complete: available evidence was inspected and its discrimination limit identified. Release involvement is plausible, not established. Connection exhaustion may be a cause, consequence, or co-occurring effect. Root cause remains unknown. No production state was changed by I1.

**Follow-up:** Retaining sampled request timings during recurrence is a separate, unstarted proposal requiring service-owner review of privacy and overhead. Neither instrumentation nor prevention is complete. The original incident record remains authoritative for restoration.

## 5. Technical experiment: useful inconclusive result

### Experiment note E1 — complete at 16:00

**Intent:** Spend at most 30 minutes comparing a batched lookup prototype with the current lookup on one synthetic workload. Determine whether the preliminary measurements justify a controlled follow-up. The hypothesis is at least a 20% latency reduction; experiment completion means reporting the measurements and their limits, not making that hypothesis true.

**Constraints and method:** Use the same local machine, dataset of 1,000 keys, and single-client script. No service deployment or real customer data. Run three baseline batches followed by three candidate batches. Each value below is that batch's median request latency.

| Version | Embedded measurement record, in ms |
| --- | --- |
| Baseline L1 | 112, 126, 121 |
| Candidate L2 | 114, 118, 129 |

The median of the three batch values is 121 ms for L1 and 118 ms for L2, approximately a 2.5% difference. This small run does not demonstrate the hypothesized 20% reduction. It also does not establish that batching has no benefit.

**Limitations:** Sequential rather than interleaved runs, uncontrolled cache warming, three batches per version, no uncertainty estimate, and no concurrent clients. The experiment does not support a production or tail-latency claim. The same participant implemented and measured the prototype.

**State and decision:** The experiment is complete; the hypothesis remains inconclusive. Do not adopt L2. Outputs are this note and the unshipped prototype description: batch ten requests before lookup. No background processes remain. Follow-up would need interleaved repeated runs and representative concurrency; none is authorized or scheduled.

## 6. Architecture decision: completed without implementation

### Existing decision record A2 — accepted at 10:00

**Decision question:** Where should a small internal service store durable scheduled-job state? The current requirement is recovery after worker restart, with atomic job claiming. The team can operate its existing relational database; operating an additional datastore is outside the current support agreement.

**Choice:** Use the existing database for the first implementation. The service owner makes this choice within the support agreement. It supersedes only A1's provisional preference for a new queue service, not A1's durability and atomic-claim requirements.

**Basis:** The team review compares two options against those constraints. An in-memory worker queue cannot retain state after process loss without another persistence mechanism. A new queue service introduces an unsupported operational dependency. The existing database already has an assigned operating team and transaction support. These recorded constraints and the reviewer's architectural judgment support the choice; they are not evidence of application performance.

**Consequences and uncertainty:** Implement claiming transactionally; avoid treating a worker's local memory as authoritative. Review the decision if measured contention prevents the required throughput or the support agreement changes. Lock behavior and recovery correctness still require implementation-specific verification. No benchmark or recovery drill has occurred.

**State:** The decision undertaking is complete. No schema, application, or deployment changed. Implementation is separate, unstarted work. A1 remains available as the earlier proposal with its rejection reason; readers must not infer an external migration from A2's accepted status.

## 7. Abandoned work: a necessary assumption disproven

### Migration note M1 — abandoned at 15:30

**Intent:** Prepare a reversible merge of two legacy asset inventories using a supposedly shared, immutable asset identifier. Completion would require a mapping without silently combining different assets. Before modifying either inventory, test the identifier assumption on the approved synthetic reproduction of known troublesome records.

**Constraint:** Read-only investigation until a valid mapping exists. Never select one source arbitrarily when identity conflicts. The assumption of a shared immutable identifier is necessary for this particular merge design, not an established fact.

### M2 — embedded comparison

| Identifier | Inventory North | Inventory South | Finding |
| --- | --- | --- | --- |
| 41 | Router, serial R-100 | Printer, serial P-900 | Same identifier names different assets. |
| 62 | Switch, serial S-210 | Switch, serial S-211 | Identifier does not establish matching identity. |
| 78 | Retired laptop, serial L-050 | Replacement laptop, serial L-090 | Identifier was reused. |

The reproduction contains twelve candidate matches; these three conflicts disprove universal identity equivalence within that sample. No claim is made about the prevalence of conflicts across the full inventories.

**Disposition:** Abandon the ID-based merge under its current intent. The inventory owner rejects this approach because it cannot satisfy identity preservation without additional reconciliation rules. The completed comparison is useful knowledge; the migration itself is neither completed nor merely waiting for execution.

**Residue and closure:** No inventory writes, queued jobs, or allocated infrastructure exist. Retain this note, including the rejected join rule `North.id = South.id`, so another participant does not restart it from the same false premise. A new reconciliation approach would be a new or explicitly revised undertaking. No continuation is currently intended; no hidden implementation task remains.

## Semantic equivalence across two media

T1 can be retained as the conversation message in example 1 or as the following ordinary tracker record. These are **alternative representations**, not instructions to maintain both.

| Meaning | Conversation representation | Tracker representation |
| --- | --- | --- |
| Identity and applicability | Opening `T1, revision 18, 09:05` | Key: T1; revision: 18; updated: 09:05 |
| Intent | Correct the spelling | Summary: Correct host lookup error spelling |
| Constraint | Without changing behavior | Scope: wording only; preserve exception and control flow |
| Actual output | Before/after statement | Change: `Unkown host` → `Unknown host` in the `LookupError` message |
| Claim and basis | Inspection sentence | Assessment: entire one-line change inspected; spelling fixed, exception and control flow unchanged |
| Limitation | Runtime not exercised | Verification limit: no runtime execution; no behavioral claim |
| Disposition and remainder | Complete; nothing remains | Resolution: completed for wording-only scope; remaining work: none |

Field names are optional. The tracker’s change context identifies the same statement. Both representations support the same hypothetical core-conformance claim for T1 at 09:05, without automatic parsing or an ADC plugin.

## Compact nonconforming contrast

| Record | Why it fails |
| --- | --- |
| “B1 done; serializer checks passed.” | Endpoint authorization is required but unexamined; a narrow success cannot complete the broader feature. |
| “All eight collectors updated; two offline.” | Offline state is unknown, six were never changed, and the two-node change was reversed. |
| “I1 complete: V8 caused the incident.” | Completion of inquiry does not establish an unsupported causal conclusion. |
| “E1 proves batching has no benefit.” | Limited observations cannot support that universal negative. |
| “M1 closed.” | Omits whether migration completed, paused, or was abandoned and why. |

Repair these contradictions by narrowing claims and preserving actual state.
