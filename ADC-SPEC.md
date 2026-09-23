# Agentic Development Convention

Version: **0.1.0-draft.1** · Status: proposal · 2026-09-16

## 1. Purpose and scope

ADC preserves enough meaning about development work for another capable participant to continue or evaluate it without the previous participant's private reasoning. Participants can be humans or agents. Work can produce code, infrastructure, operational changes, documents, decisions, knowledge, or a justified decision not to implement anything.

ADC standardizes a semantic contract, not an execution process. It does not prescribe a lifecycle, sequence, approvals, roles, tools, models, storage, version control, programming language, tests, pipelines, schemas, filenames, or artifact counts. It is not an assurance certification or a substitute for applicable authorization and domain rules.

Sections 1–8 are normative. Section 9 is illustrative. Uppercase **MUST**, **MUST NOT**, **SHOULD**, **SHOULD NOT**, and **MAY** use the requirement meanings in [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119.html) and [RFC 8174](https://www.rfc-editor.org/rfc/rfc8174.html): obligations, prohibitions, recommendations, discouraged practices, and options. A departure from a recommendation needs a considered reason, not an automatic exception to an obligation.

## 2. Minimal model

An **undertaking** is a distinguishable scope of purposeful work whose state or result needs to survive a handoff or be evaluated. It can be a correction, investigation, decision, intervention, or larger effort. It need not be a ticket, session, commit, or product increment. Split work only when independent purposes, constraints, coordination, or evaluation warrant it; there is no universal smallest duration or size.

An undertaking has three semantic facets, not three required artifacts:

| Facet | Meaning |
| --- | --- |
| Intent | Why this work exists, the desired outcome or question, and the scope against which it will be evaluated. |
| State | What is currently true about the work and its relevant surroundings, whether it remains pursued, and what remains unresolved. |
| Assessment | What is claimed about results, the basis for those claims, and their limits. |

**Context** explains relevant circumstances; **constraints** bound acceptable action or results; **assumptions** are premises not established as facts; **risks** are possible adverse consequences. A **decision** is a choice with consequences for the work. An **activity** is something done; an **output** is something produced; an **actual outcome** is the resulting condition or knowledge. None implies the next: issuing a command is not evidence that its intended effect occurred.

**Evidence** is an observation, record, analysis, or attributable judgment used to support or challenge a claim. **Material** information is information whose omission could reasonably alter action, continuation, or interpretation of a result within the undertaking's scope. **Records** are retrievable representations in any medium, including retained conversations. **Durable** means retrievable by the intended participants for the expected continuation or evaluation period, not forever or publicly.

## 3. Core requirements

### C1 — Distinguishable scope and intent

The records MUST distinguish the undertaking and preserve its intent, evaluation basis, and material constraints, assumptions, and risks. An evaluation basis can be a simple expected correction, a decision question, a bounded investigation, or acceptance criteria; it need not be a test or an exhaustive specification.

Before acting, a participant MUST establish the intent and applicable constraints sufficiently for that action; ADC grants no authority. Unknowns affecting the action MUST be identified as unknown, with the permitted scope limited accordingly. Research to resolve uncertainty is itself valid work. Material changes to intent or evaluation criteria MUST preserve what changed and why; results MUST NOT be retroactively redefined as success by silently changing the target.

### C2 — Current state and continuity

Records MUST make the current state distinguishable from plans and historical observations. At a handoff, material interruption, or closure, they MUST preserve the actual resulting state, relevant outputs or their locations, material unresolved matters, and what is needed to continue or deliberately leave the work stopped. This includes consequential external effects, unfinished operations, and recovery obligations when present.

Open or suspended work MUST identify a next action or resumption condition, or explicitly say it is undetermined. Responsibility MUST be identifiable where continuation depends on a particular participant or authority; ADC does not require a named owner otherwise. If an interruption prevents recording, the next participant MUST reconcile observable state and gaps before relying on the old record. A conforming process MUST NOT report a missing handoff as complete.

### C3 — Decisions and relevance

A decision MUST be retained when it changes material constraints or intent, excludes an alternative whose exclusion is material to future work or evaluation, accepts material residual risk, or would be costly or hazardous to reconstruct. Preserve the choice, reason, and consequences necessary for future interpretation; identify the decision-maker or authority when that affects validity. Rejected options need recording only when material.

Information added solely for ADC SHOULD serve continuity, coordination, risk control, or evaluation; existing records need not be pruned. Participants SHOULD NOT duplicate adequately represented information. Existing records MAY satisfy any number of requirements. ADC MUST NOT require private reasoning, exhaustive transcripts, or separate decision, evidence, and state documents.

### C4 — Claims and evidence

Every material outcome claim MUST be connected to its supporting or challenging basis and material limitations. Preserve enough to identify what was observed or judged, its source or method, result, and applicable target, conditions, and time or revision where these affect interpretation. The connection MAY be an ordinary sentence. A command to run later is not an observed result.

Observed facts, inferences, proposals, and unknowns MUST remain distinguishable. Evidence gaps or material limitations—including inaccessibility, staleness, conflict, or relevant dependence—MUST NOT be silently represented as resolved. Material contrary evidence and unexamined scope MUST be disclosed. A claim MUST be narrowed or left unresolved when its basis does not support its breadth; listing a caveat does not repair a contradictory success claim.

Evidence MAY include inspection, consultation, telemetry, calculation, experiment, a decision record, or tests. A reasoned judgment can support a decision but is not observation of its predicted effects. An agent's confidence alone is not evidence. Historical evidence MUST NOT be silently applied to a materially changed target. Rechecking is necessary only to support a claim about that changed target, not to erase an accurate historical finding.

### C5 — Stopping, completion, and replacement

The following meanings MUST be distinguishable when applicable; exact labels and intermediate states are optional:

| Meaning | Required interpretation |
| --- | --- |
| Open | Work remains intended; state says whether it is not started, proceeding, or waiting when that matters. |
| Suspended | Work is deliberately paused without being declared complete; preserve the reason and resumption condition, including if unknown. |
| Completed | The declared scope's completion conditions are satisfied, supported by C4; further work is not silently left inside that scope. |
| Abandoned | The scope will not be completed under the current intent; preserve why and its actual partial results or residue. |

Completion MUST state which scope is complete and how it was evaluated, the actual outcome, and material limitations or follow-up. Finishing a bounded investigation can satisfy its completion conditions without confirming its hypothesis. Finishing an attempt does not establish that a requested operational effect succeeded. Unmet required conditions mean incomplete or abandoned work, unless a material scope revision is explicitly recorded under C1.

Failure describes a result, not necessarily whether work continues. Rejection describes a choice, not necessarily abandonment of the whole undertaking. A rollback MUST distinguish the attempted change's result from the recovery result. Follow-up outside completed scope MUST be identifiable and MUST NOT be implied complete.

Supersession means that an identified record, decision, claim, or scope replaces another as current. The replacement and extent of supersession MUST be identifiable, including partial replacement. Superseding a plan or record does not prove that an external system changed. Material prior reasons and results MUST remain interpretable while they are needed for continuity or evaluation. Iteration, splitting, merging, reopening, and reversal MAY occur in any order; ADC defines no permitted-transition graph.

### C6 — Proportionality

Rigor MUST be sufficient for the consequences and uncertainty of the particular action or claim. Participants MUST consider material impact, reversibility, uncertainty, and coordination dependencies when selecting it. Additional evidence or traceability MUST address an identified need rather than merely increasing document volume.

For high-consequence action or claims, preserve the basis for the chosen assurance, applicable authority, material residual risk, and, where applicable, recovery or containment provisions, including known infeasibility. Independent checking SHOULD be used when shared assumptions could conceal a consequential error. This adds neither a universal approval gate nor a fixed reviewer role.

Trivial work MAY satisfy the core in one short existing record. Irrelevant concepts MAY be omitted; material unknowns MUST NOT be hidden as omission or empty fields. Durable recording SHOULD happen as work changes and MUST happen before relevant context is deliberately relinquished. Urgent action MAY precede recording when delay would increase harm; subsequent records MUST distinguish contemporaneous facts from reconstruction and MUST NOT invent prior authorization.

### C7 — Interpretability and preservation

The intended next participant MUST be able to locate and interpret the required meaning without access to hidden reasoning or an ADC-specific product. Shared context and links MAY supply it, provided their applicability and accessibility are clear. Restricted records need not become public; an inaccessible dependency MUST be disclosed rather than counted as available evidence to that audience.

When records conflict, the authoritative account MUST be identified or the conflict explicitly unresolved. Identifiers need only distinguish their subjects within the relevant context. Moves, conversions, or summaries MUST preserve material relationships: scope to intent, claim to basis and limitation, current to historical state, and replacement to what it supersedes. A conversion that loses required meaning MUST disclose that loss and MUST NOT claim equivalent conformance.

## 4. Conformance

There is one core level: **ADC 0.1.0-draft.1 core**. Conformance applies to an identified undertaking's records and handling at a stated point, not to a directory, tool, or person's general competence. A conformance claim MUST identify that scope and version; surrounding context MAY supply identity and time.

A capable participant unfamiliar with the prior session must be able to determine the intent and constraints, current disposition, substantiated result, material uncertainty, and continuation or closure basis from the available records. All applicable obligations in this specification MUST hold. Empty headings, unsupported assertions, and tools capable of storing records do not establish conformance. Explicit uncertainty can conform; it cannot justify unsupported completion.

## 5. Profiles and extensions

A profile MAY add requirements for a domain or context. It MUST identify its name, version, applicability, and additional obligations, preserve core meanings, and remain distinguishable from core conformance. Extensions MUST NOT weaken the core or silently redefine completion, evidence, or unknown state. Combined profiles MUST disclose conflicts before claiming combined conformance.

Optional examples include collaboration, high-consequence operations, and audit retention. This draft standardizes no such profile. Organizations MAY require local approvals, schemas, tools, or retention periods; these remain local requirements, not ADC core requirements. An unfamiliar extension MUST NOT be required to understand the underlying core account.

## 6. Interoperability boundary

ADC provides semantic, human-interpretable interoperability. Implementations need not parse arbitrary prose automatically or exchange a universal file format. Local mappings MUST retain the distinctions in C1–C7; for example, a tracker label `Closed` alone does not distinguish completion from abandonment. Serialization standards and automated validators are separate possible extensions, not prerequisites.

## 7. Retention and access

Records MUST remain adequate for the expected continuation or evaluation period. When a currently relied-on claim depends on evidence that becomes unavailable or no longer applicable, and no adequate retained account supports it, the claim MUST be qualified or supported again. Loss of raw evidence does not by itself invalidate an adequately recorded, time-bounded historical finding. Retention need and access restrictions MUST be made explicit when material; routine records need no separate retention policy document. ADC requires neither permanent archives nor disclosure of secrets or private reasoning.

## 8. Specification evolution

A published specification identifier MUST identify fixed normative content. Revisions receive a new identifier. This draft has no stability promise; citing `ADC` without a version cannot establish which requirements were followed. Informative guides and examples do not add core obligations.

## 9. Conformance examples — informative

| Account | Assessment |
| --- | --- |
| “Corrected `recieve` to `receive` in the support page; wording-only scope. Inspected the changed sentence and diff: spelling fixed, no other text changed. Complete; nothing remains.” Stored with the identified revision. | Conforms for this narrow task if no other material constraints exist. No separate plan or automated test is needed. |
| “Three scheduled observations completed; logs cannot distinguish causes A and B. No production changes. Investigation complete within its time-box; causal claim remains inconclusive. Next investigation requires request-level traces.” With observation records and the original question. | Can conform: completion of investigation is not confirmation of a cause. |
| “Done; all tests pass.” | Insufficient without identifiable scope, actual results, and material limits. |
| Seven empty ADC-named documents, or a complete transcript without an identifiable current account. | File presence or volume does not establish conformance. |

See [the guide](ADC-GUIDE.md), [quick reference](ADC-QUICK-REFERENCE.md), [worked examples](ADC-EXAMPLES.md), and [research and design rationale](ADC-RESEARCH.md).
