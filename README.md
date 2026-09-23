# Agentic Development Convention

ADC is a compact, implementation-agnostic proposal for preserving the meaning, state, decisions, and trustworthy outcomes of work performed by humans and agents.

**Standardize meaning, not execution.** Another capable participant should be able to continue or evaluate the work without reconstructing a conversation or installing an ADC-specific product.

Status: **0.1.0-draft.1 — proposal, not an established standard.** The design has been reviewed against worked cases; it has not been validated through organizational adoption or measured overhead reduction.

## Start here

| Document | Purpose |
| --- | --- |
| [Quick reference](ADC-QUICK-REFERENCE.md) | Approximately one page for day-to-day use. |
| [Specification](ADC-SPEC.md) | Standalone normative core and conformance rules. |
| [Practitioner guide](ADC-GUIDE.md) | Apply ADC through ordinary records and existing tools. |
| [Worked examples](ADC-EXAMPLES.md) | Seven contrasting undertakings, including inconclusive and abandoned work. |
| [Research synthesis](ADC-RESEARCH.md) | Primary-source comparisons, design decisions, limitations, and quality tests. |

## Applying ADC

The [adoption plan](ADC-ADOPTION.md) gives a small pilot and guidance for choosing where records live. It includes two non-normative application patterns: [a solo GitHub developer](ADC-SOLO-GITHUB.md) and [a platform team using GitHub, Jira, and qTest](ADC-TEAM-PLATFORM.md). Each has a copyable prompt and a worked example; neither changes the specification's core.

## The model

An **undertaking** is a distinguishable scope of purposeful work. Its account preserves:

- **Intent:** why the work exists and what outcome or question it addresses.
- **State:** what is currently true and what remains unresolved.
- **Assessment:** what can be claimed, on what basis, and with what limits.

These are semantic facets, not required documents. Material constraints and decisions belong wherever they can be represented adequately. A correction may fit in one sentence; a consequential migration may reuse plans, operational records, and observations maintained elsewhere.

Completion is not shipment. A decision can be complete without implementation; an investigation can be complete but inconclusive; abandoned work can preserve useful knowledge. An activity, output, and achieved outcome are different facts.

## What ADC does not require

No CLI, model, agent harness, fixed roles, repository layout, Markdown, Git, pull requests, tickets, test suite, CI/CD, hooks, state-machine engine, phase sequence, or approval ceremony is part of the core. Existing organizational controls continue to apply. Optional profiles may add requirements, but this draft standardizes only one core level.

The files in this repository publish the convention; they are **not** a file set to create for every undertaking. The specification alone defines conformance. All other documents are informative.

## Research scope

The first draft examines AI-DLC and its adaptive variants, Proof of Done, Spec Kit, OpenSpec, BMAD, established development and architecture methods, operations, evidence practices, and compact semantic conventions. Research was checked on 2026-09-16; mutable-source and retrieval limitations are recorded in the synthesis.

## License

[MIT](LICENSE). Cited works remain the work of their respective authors; citations do not imply endorsement of ADC.
