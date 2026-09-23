# ADC practitioner guide

Informative guidance for [ADC 0.1.0-draft.1](ADC-SPEC.md). The specification defines conformance; this guide adds no obligations, prescribed workflow, or standardized profiles. Examples are fictional.

## Start with the records you already use

Apply ADC to an undertaking: a distinguishable purpose whose state or result needs to survive a handoff or evaluation. It might occupy one paragraph in an existing document, several related tickets, or an operational record with restricted evidence. It need not match a session, commit, project, or reporting period.

Locate the existing account before creating another. A useful account lets the next participant recover three things:

- **Intent:** why the undertaking exists, what outcome or answer is sought, and what bounds acceptable action and evaluation.
- **State:** what is now true, whether work remains intended, and what is unresolved or needed next.
- **Assessment:** what is claimed, what supports or challenges it, and what the evidence does not establish.

These are meanings, not headings. One sentence can supply several. Shared policies can supply constraints; a linked observation can supply evidence. Record additional explanation only where the existing account leaves a material gap.

For a wording correction, a retained comment attached to the identified revision can be enough:

> Corrected the misspelling in the support-page heading; wording-only scope. Inspected the changed heading and diff: spelling corrected, no other text changed. Complete; no follow-up.

This example assumes no additional material constraints. Its adequacy comes from its narrow scope and direct inspection, not its shortness. The same comment would not substantiate a claim about accessibility, translation quality, or successful publication.

## Enter, leave, and resume work

These are occasions for maintaining continuity, not lifecycle stages. A human may handle all three; several agents may enter the same undertaking concurrently.

### Enter with a usable account

Find the intended outcome, current account, applicable authority and constraints. Separate accepted decisions from proposals, observations from predictions, and live state from historical reports. Follow relevant references rather than loading every surrounding document.

Check the actual conditions that matter for the proposed action. A repository note cannot establish that a remote deployment happened. An incident log cannot establish that a mitigation is still active. Conversely, rereading an unchanged, adequately identified document may need no external check. Verification effort follows the action's consequences and the likelihood that its premises changed.

If a material premise is unknown, keep action within the known safe and authorized scope. Inspection or research can resolve it. Neither an earlier agent's instruction nor a record of someone else's permission automatically grants present authority.

### Leave a usable account

Update the existing account when relinquishing relevant context. Preserve the resulting state, output locations, significant decisions, supported findings, unresolved matters, and a next action or resumption condition where work remains. “Next action undetermined; awaiting service-owner scope decision” is more useful than invented certainty.

Include consequential residue: a running operation, temporary access, an altered configuration, a held resource, or cleanup still owed. Distinguish an intended cleanup from one actually checked. If continuation depends on a particular person or authority, make that dependency identifiable.

A handoff is not a transcript export. A concise explanation of the choice and its consequences is enough where it permits later interpretation. Private reasoning, every attempted command, and routine conversation need not survive.

### Resume after context loss

Treat the preserved account as a navigation aid, not proof that the world remained unchanged. Reconcile its claims with accessible outputs and relevant current state. Identify what changed since the recorded observation, including concurrent work, expired evidence, or interrupted operations.

If two records disagree, identify the authoritative account or preserve the conflict as unresolved. Do not silently pick the most recent prose if its observation concerns an older target. If a crash prevented a handoff, reconstruct what can be established and distinguish that reconstruction from contemporaneous observations. A missing record is a gap, not evidence that nothing happened.

For concurrent participants, a short assignment or shared-record convention can prevent overlapping work. ADC does not provide locking: use the coordination mechanism appropriate to the existing environment, and preserve any consequential unresolved collision.

## Scale persistence and assurance separately

Record volume and assurance strength are different choices. A short recovery record can reference strong independent observations; a long generated report can contain no reliable evidence.

| Situation | Usually useful persistence | Evaluation and coordination |
| --- | --- | --- |
| Small, reversible correction | One existing record with intent, narrow scope, actual result and check. | Direct inspection may suffice; explain any material uncertainty. |
| Medium undertaking, such as a brownfield capability change | Existing requirement and design references, material decisions, current state, validation results and remaining boundaries. | Check affected behavior and relevant existing behavior; coordinate interfaces and dependencies where needed. |
| High-consequence intervention, such as access-policy migration | Precise target and authority, consequential assumptions, assurance rationale, residual risk, containment or recovery provisions, and actual resulting state. | Use evidence matched to failure modes; independent checking is useful where shared assumptions could conceal serious error. |

These are examples, not conformance tiers. Several low-risk edits may need more coordination than one high-risk calculation. A small change can have a large impact; a large document can be easy to reverse.

Persist detail when it prevents expensive rediscovery, enables another participant, explains a consequential choice, or supports a claim. Avoid manufacturing an inventory of irrelevant risks. An explicit material unknown is useful; filling every empty field with “none” is not.

Prefer links to adequately retained records over copies. When access or retention matters, establish who can retrieve the evidence and for how long. A temporary monitoring view may require a retained observation or export; that does not imply permanent storage of every raw event. Restrict sensitive details through existing access controls without pretending inaccessible evidence is available to every reader.

## Match claims to what was established

Begin with the scope's evaluation basis. For implementation it might be observable behavior; for investigation it might be a defined question and bounded observation plan; for architecture it might be a decision supported by stated trade-offs.

Keep activity, output and outcome separate. Running a command is activity. Its report is output. Restoration of the intended service condition is an outcome requiring an appropriate basis. A passing check supports only the target and conditions it actually examined.

Record observations with enough context to interpret them: method or source, result, and relevant target, conditions, time or revision. An ordinary sentence may carry all of this. Preserve contrary evidence and limitations instead of allowing a broad success label to override them. Narrow the claim when needed.

Useful non-product endings include:

- **Decision:** “Use the existing service; option B rejected because its required support model is unavailable. Decision complete; implementation not undertaken.” Preserve the rationale and applicable authority, not a fictional implementation result.
- **Finding:** “Observed failures correlate with the connection pool limit in the sampled period; causal mechanism remains unconfirmed.” A bounded investigation can finish with this finding if it satisfies its original evaluation basis.
- **Rollback:** “The configuration attempt failed its acceptance check. Previous configuration restored and recovery checks passed; original improvement remains unresolved.” Evaluate the attempt and recovery separately.
- **Abandonment:** “The prerequisite cannot be met within the allowed scope. Stop this implementation; retain the prototype and findings, remove temporary resources, and record any cleanup still pending.” Useful partial results do not turn abandonment into completion.

Do not silently recast a promised fix as a successful investigation after the fix fails. A legitimate scope revision preserves what changed and why. Likewise, closing a decision question does not close a separately intended implementation.

## Map the meanings onto existing tools

The following are illustrations, not required layouts or integrations.

| Existing environment | Possible ADC account | Distinction to preserve |
| --- | --- | --- |
| Plain directory or document set | One existing project note identifies purpose, current status, output locations and relevant observations. Larger material decisions can remain in their existing documents. | A filename or folder structure does not establish currentness; identify which account governs when records differ. |
| Git and pull requests | Existing issue or PR description supplies scope; discussion carries decisions; a revision and check results identify evaluated output; handoff notes cover unfinished external work. | Merged does not mean deployed, and a successful build does not establish the intended operational outcome. |
| Issue tracker | Existing fields, comments and linked evidence jointly supply intent, disposition, assessment and continuation. | Translate ambiguous labels such as `Closed`: was this completed, abandoned, replaced, or merely administratively closed? |
| Infrastructure or operations record | Existing change or incident account references target configuration, authority, observations, intervention results and recovery state. | Distinguish desired configuration, attempted application and observed live state; include temporary effects and unfinished cleanup. |
| Investigation with no code | Existing notebook or report states the question, material assumptions, observation method, results, inference limits and remaining questions. | Completion of the investigation is not confirmation of its hypothesis; a negative or inconclusive result can be the useful output. |

During a move between tools, preserve the relationships, not merely text fields: which observation supports which claim, what is current, what remains unresolved, and what replaced which decision. A lossy summary can be useful, but it is not an equivalent substitute when it drops required meaning.

## Optional local profile sketches

ADC currently standardizes no profiles. Organizations can define additional obligations where a concrete need justifies them, while leaving core meanings readable without specialized knowledge.

A collaboration profile could define responsibility handoffs, conflict handling and update expectations. A high-consequence operations profile could specify locally appropriate authorization, independent checks, containment and recovery evidence. An audit-retention profile could identify retention periods, access arrangements and evidence provenance. None is inherently a better maturity level.

For an actual profile, follow the specification's profile rules: identify its name, version, applicability and additional obligations; retain the core meanings; disclose conflicts when combining profiles. A local requirement for a particular approval system remains local, not a condition imposed on every ADC user.

## Avoid creating another maintenance burden

Common failure modes are practical rather than syntactic:

- Recreating information in ADC-named files when an existing account already preserves it.
- Maintaining a detailed future task tree that changes faster than anyone uses it.
- Treating every routine choice as a durable decision, or retaining no rationale for consequential ones.
- Recording elaborate check instructions without actual results.
- Using fluent agent summaries as substitutes for identifiable observations.
- Keeping a complete transcript while leaving readers unable to identify the current state.
- Treating approved, merged, deployed, completed and successful as interchangeable.
- Adding forms or gates without a specific coordination or assurance need.

The practical check is whether another capable participant can locate the purpose, understand the actual state, evaluate the supported claims, and continue or deliberately leave the work stopped. If the account already permits that and satisfies the applicable [core requirements](ADC-SPEC.md), adding more records does not make it more conformant.
