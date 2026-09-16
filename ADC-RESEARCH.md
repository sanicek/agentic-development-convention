# ADC research synthesis and design rationale

Research cutoff: **2026-09-16** · Supports **ADC 0.1.0-draft.1** · Informative

## 1. Scope, method, and limits

Question: what meaning should survive between participants and systems, independently of how development work is executed?

The review sampled the requested methodology families using maintainer documentation, specifications, original authors, and operational practice sources. It separated conceptual commitments from shipped implementation requirements; examined non-code and unsuccessful outcomes; and tested proposed semantics against seven contrasting undertakings. Sources below are linked at the relevant comparison, not presented as a popularity ranking.

**Facts** in comparison tables summarize the cited sources. **Adopt / modify / reject** and all ADC design decisions are our synthesis. The proposed three-facet model and core requirements are original proposals, not an existing standard or an endorsement by these projects. This is a targeted design review, not a systematic literature review, runtime evaluation, or benchmark of overhead, token use, safety, or team performance.

The agentic-tool ecosystem has changed substantially. “These tools all require Git, greenfield software, fixed agents, and a linear pipeline” is not supported by the reviewed sources. ADC's proposed distinction is the absence of required execution and representation machinery, not an exclusive discovery of proportionality, evidence, or negative outcomes.

### Source snapshots

These release pages and commit identities were verified. Detailed guides were reviewed as mutable documentation on the cutoff date; they were **not** proven byte-identical to these releases. Exact-commit content retrieval was unavailable. Release anchors therefore establish release facts, not immutable provenance for every behavior described below.

| Project | Verified release | Release commit |
| --- | --- | --- |
| AWS AI-DLC Workflows | [v2.9.0, 2026-09-15](https://github.com/awslabs/aidlc-workflows/releases/tag/v2.9.0) | `22f5d1b15a064c9ae80046e5b1761d5877e2f69f` |
| GitHub Spec Kit | [v1.0.7, 2026-09-15](https://github.com/github/spec-kit/releases/tag/v1.0.7) | `fe1d00e3ccaf495880aaf90fb0e17679e82f065b` |
| OpenSpec | [v1.13.0, 2026-09-09](https://github.com/Fission-AI/OpenSpec/releases/tag/v1.13.0) | `9d4e5974e5c0d9a09b9c6c1e1eb0975e80ec4461` |
| BMAD | [v6.12.0, published 2026-09-04](https://github.com/bmad-code-org/BMAD-METHOD/releases/tag/v6.12.0) | `05bfbd46d00766ec88eb9b42e76be2c575d64d7b` |

Proof of Done was identified specifically as Sergey Sheleg's **POD/001 v1.1**, updated 2026-08-26, not a generic name for every evidence-oriented practice. Essence 1.2 was examined in detail; OMG also lists **2.0 Beta2**, an in-process March 2026 version with the broader title *Kernel & Language for Engineering Methods*. Its PDF exceeded retrieval limits, so detailed 1.2 findings below are not claims about 2.0. [OMG version listing](https://www.omg.org/spec/Essence/2.0/Beta2/About-Essence).

## 2. Agentic development: concepts versus machinery

| Source and observed facts | Useful semantic concept | Boundary, machinery, and ADC disposition |
| --- | --- | --- |
| [AWS original AI-DLC introduction](https://aws.amazon.com/blogs/devops/ai-driven-development-life-cycle/) frames software development through Inception, Construction, and Operations, AI proposals, retained project context, and human validation. | Recoverable intent, design context, and accountable judgment. | **Adopt** retained intent and consequential decisions. **Modify** validation into consequence-dependent assurance. **Reject** importing the phases and ceremonies. Human validation is substantive in this source, not merely an incidental installer choice. |
| [Current AI-DLC implementation](https://github.com/awslabs/aidlc-workflows) separates harness-neutral core from adapters but supplies an engine, agents, state, hooks, and audit machinery. [Profiles](https://awslabs.github.io/aidlc-workflows/guide/workflow-profiles/) include bugfix, infrastructure, and prototype routes with variable depth. [State reference](https://awslabs.github.io/aidlc-workflows/reference/12-state-machine/) distinguishes sessions from workflows and ties completion to included-stage gates. | Proportional scope; session end differs from work completion; unfinished intent can survive archiving. | **Adopt** those distinctions. **Modify** gate closure into scoped completion semantics. **Reject** engine transitions, agent roster, audit-event schema, and hooks as universal requirements. Multi-harness support is not machinery independence; nevertheless, neither CI nor a full fixed route is universally required across its profiles. |
| [Spec Kit](https://github.com/github/spec-kit) has independent SDD, repair, and idea-assessment entry points. Its [quickstart](https://github.github.io/spec-kit/quickstart.html) explicitly permits Git-free operation. [Brownfield guidance](https://github.github.io/spec-kit/guides/existing-projects.html) favors bounded adoption and offers alternative artifact-maintenance strategies. | Separate intent from implementation planning; preserve guardrails; decide what remains authoritative. | **Adopt** bounded intent and reconciliation. **Modify** the record to fit existing media. **Reject** mandatory CLI, feature directories, constitution files, templates, and command sequencing. Git and greenfield assumptions cannot fairly be attributed to current Spec Kit as universal requirements. |
| Spec Kit's [assessment guide](https://github.github.io/spec-kit/guides/assessment.html) supports non-software decisions and justified stopping, but specifies a staged artifact set. [Task template](https://github.com/github/spec-kit/blob/main/templates/tasks-template.md) makes tests conditional. [Agentic SDD guidance](https://github.github.io/spec-kit/reference/agentic-sdd.html) distinguishes reviewer-owned checklists from implementation status. Its [philosophy essay](https://github.com/github/spec-kit/blob/main/spec-driven.md) is more strongly specification-to-code and test-first oriented. | Assessment can produce a valid no-go result; review and implementation claims differ. | **Adopt** negative outcomes and claim distinctions. **Reject** a universal staged assessment packet. Treat the stronger essay and conditional operational guidance as distinct source layers, not proof that all uses require automated tests or code output. |
| OpenSpec's [concepts](https://github.com/Fission-AI/OpenSpec/blob/main/docs/concepts.md) separate agreed behavior from proposed deltas. [OPSX](https://github.com/Fission-AI/OpenSpec/blob/main/docs/opsx.md) supports iterative actions and artifact dependencies; artifact state is discovered from file existence. [Workflows](https://github.com/Fission-AI/OpenSpec/blob/main/docs/workflows.md) make verification optional and not archive-blocking. | Baseline versus proposal; concise deltas; revisable understanding. | **Adopt** delta and baseline semantics. **Modify** baseline to include knowledge or observed operations. **Reject** directories, artifact packages, delta syntax, and treating archive/file existence as evidence of achieved behavior. Its [README](https://github.com/Fission-AI/OpenSpec) targets brownfield; Git-backed Stores is a specific feature, not proof that ordinary local use universally requires Git. |
| BMAD's [planning guide](https://docs.bmad-method.org/plan/choose-a-planning-path/) right-sizes planning and permits independent research or validation. Its [build guide](https://docs.bmad-method.org/build/build-a-change/) uses conditional planning depth, review, and local commits. [Skills and agents](https://docs.bmad-method.org/reference/skills-and-agents/) permit direct skill use without a persona conversation. | Consequence-sensitive detail; retained context; review dispositions and deferred work. | **Adopt** proportionality and explicit deferrals. **Modify** evaluation beyond source diffs. **Reject** mandatory skills runtime, personas, and build/review/commit loop. Its [README](https://github.com/bmad-code-org/BMAD-METHOD) permits planning artifacts to feed an existing delivery workflow; not every use requires the full roster or a PRD. |
| [Proof of Done manifesto](https://podmanifesto.org/) links completion claims to scoped, reachable evidence and limitations. It explicitly permits proportionate, non-test evidence and rejects a mandatory toolchain. It distinguishes implementation verification from unobserved product effects. | Claims need an applicable basis; evidence can expire; uncertainty is not failure to fill a form. | **Adopt** those semantics. **Modify** its evidence-carrying-change and acceptance framing into undertakings that can produce knowledge or cessation. **Reject** universal graphs, gate categories, and provenance fields. It is incorrect to characterize the manifesto itself as simply CI-only or a mandatory pipeline. |
| [Proof of Done reference implementation](https://github.com/ssheleg/task-pipeline) supplies orchestration, skills, artifact conventions, and staged delivery. Stage count and gates are configurable; brownfield is supported. | Traceable intent, actual-target verification, and reusable knowledge. | **Adopt** the meanings, **reject** mandated intake interviews, stage progression, repository layout, and model policy. Distinguish this implementation's machinery from the manifesto's narrower contract. |
| [Evidence-Carrying Changes proposal](https://rmax.ai/notes/evidence-carrying-changes/) connects claims to provenance, residual uncertainty, and policy decisions, and addresses correlated producer/checker mistakes. | Evidence independence depends on its origin and assumptions, not the number of agents. | **Adopt** provenance and evidence limits proportionately. **Reject** a universal classifier/verifier/policy-engine architecture or certificate. This is an explicitly unvalidated architectural proposal, not demonstrated evidence that its harness improves outcomes. |

### Assumption audit of current agentic implementations

This is our classification of the sources above. “Not established” is not a claim that no integration uses it. “Conditional” is different from universally required.

| Assumption | AI-DLC | Spec Kit | OpenSpec | BMAD |
| --- | --- | --- | --- | --- |
| Linear SDLC | Adaptive routes; staged engine remains | Ordered SDD with iteration; separate entry points | Explicitly iterative | Independent planning; structured build loop |
| Product/feature delivery | Dominant; infrastructure and PoC included | Dominant SDD; assessment broader | System-behavior changes dominate | Build dominates; research/planning broader |
| Git | Git-centric execution features; universal method requirement not established | Explicitly optional | Stores uses Git; ordinary-use requirement not established | Build commits; planning exportable |
| Automated tests | Profile-dependent strategy | Generated tasks conditional | Verification optional | Existing-suite condition |
| CI/CD | Profile-dependent | Not established as prerequisite | Not established | Not established |
| Issue tracker | Not established as prerequisite | Optional conversion | Not established | Input option |
| Fixed agent roles | Supplied specialized-agent machinery | No mandatory roster established | No mandatory roster established | Supplied personas; direct skills allowed |
| Formal transitions | Engine-owned | Command/artifact dependencies | Artifact dependency state | Within chosen workflows |
| Approval gates | Central to stage mechanism | Extra gates; reviewer ownership | Verification does not block archive | Conditional planning route |
| Greenfield | Not required | Not required | Brownfield emphasis | Not required |
| Code primary output | Common, not exclusive | SDD yes; assessment no | Implementation-centered | Build yes; research no |

## 3. Established methods and architecture conventions

| Primary source / observed position | Useful concept | Limitation, rejected machinery, and ADC disposition |
| --- | --- | --- |
| [Agile Manifesto](https://agilemanifesto.org/) and [principles](https://agilemanifesto.org/principles.html) prioritize collaboration, adaptation, simplicity, feedback, and working software. | Plans and records serve purposeful work. | **Adopt** adaptation and simplicity; **modify** progress to include learning and restoration. **Reject** a universal software-increment measure. The manifesto does not require sprints, Git, tickets, or agent roles. |
| [Lean thinking](https://www.lean.org/lexicon-terms/lean-thinking-and-practice/) and [practice](https://www.lean.org/explore-lean/what-is-lean/) connect value, flow, pull, experimentation, and improvement. | Information has beneficiaries and carrying costs. | **Adopt** a reason for maintaining each record. **Reject** mandatory value-stream maps or flow-control mechanisms. Lean is not intrinsically code- or Git-based; useful continuity records are not automatically waste. |
| [Kanban Guide, May 2025](https://kanbanguides.org/the-kanban-guide/) requires contextual workflow definition and flow measures. [Kanban University](https://kanban.university/kanban-guide/) emphasizes starting from existing work. | Work identity, explicit state, impediments, local completion meaning. | **Adopt** these semantics; **reject** required boards, WIP controls, metrics, and forecasts in ADC. Kanban is not linear SDLC. Borrowing concepts does not establish Kanban conformance. |
| [Shape Up boundaries](https://basecamp.com/shapeup/1.2-chapter-03) and [size adaptation](https://basecamp.com/shapeup/4.1-appendix-02) bound investment and uncertainty; small teams can omit much formal ceremony. | Scope, exclusions, appetite, and deliberate stopping. | **Adopt** bounded investment where material. **Modify** software shipping into broader outcomes. **Reject** required shaping/betting/building stages or cadence. It is inaccurate to impose the book's larger-team ceremony on every use. |
| [Ron Jeffries on Extreme Programming](https://ronjeffries.com/xprog/what-is-extreme-programming/) describes feedback, simple design, pairing, tests, small releases, and continuous integration as a related practice set. | Fast feedback and shared interpretation. | **Adopt** feedback; **reject** universal engineering practices or release outputs in ADC. XP genuinely concerns software and includes engineering discipline; it is neither Git-specific nor a linear phase model. |
| [Kent Beck's Canon TDD](https://newsletter.kentbeck.com/p/canon-tdd) iterates behavioral cases, executable tests, implementation, and optional refactoring. | Expected behavior differs from observed behavior; discoveries revise remaining work. | **Modify** test-first into explicit evaluation basis. **Reject** obligatory automated tests or red/green/refactor for every undertaking. TDD is programming-specific, not “write all tests before all code”; it needs no CI service or Git. |
| [Agile Alliance on ATDD](https://agilealliance.org/glossary/atdd/) uses collaborative acceptance examples before implementation; automation is optional. | Concrete examples expose divergent understanding. | **Adopt** understandable evaluation criteria. **Modify** examples to findings, operational observations, or document review. **Reject** fixed staffing, automation, and universal acceptance-first sequencing. Software-functionality roots remain. |
| [Michael Nygard's ADR practice](https://www.cognitect.com/blog/2011/11/15/documenting-architecture-decisions) preserves significant decisions, context, consequences, and superseded status in small records. | Decisions remain interpretable after people forget the alternatives. | **Adopt** significance and replacement semantics; **modify** scope beyond architecture. **Reject** mandatory numbered files or a separate ADR per routine choice. The proposed repository representation is separable from the meaning. |
| [Rust RFC process](https://github.com/rust-lang/rfcs) distinguishes substantial proposals, review, acceptance, postponement, and closure; acceptance does not schedule implementation. | Proposal, choice, and implementation are different facts. | **Adopt** rationale and dispositions. **Reject** required GitHub PRs, final-comment periods, subteams, and consensus ceremonies. Those are actual requirements of this particular RFC process, not of every RFC-like practice. |
| [C4 diagrams](https://c4model.com/diagrams) and [notation guidance](https://c4model.com/diagrams/notation) separate architectural abstractions from drawing notation and advise using useful levels only. | Representation independence and audience-appropriate detail. | **Adopt** those principles; **reject** required diagrams or transplanting system/container/component/code into ADC. C4 addresses software architecture, not universal work state. |
| [arc42 overview](https://arc42.org/overview/) and [method](https://arc42.org/method/) organize architecture concerns and describe interrelated activities without fixed order, with proportionate detail. | Relevant context, constraints, decisions, quality, and risks. | **Adopt** these categories when material; **reject** a twelve-section packet per undertaking. Architecture focus limits direct generalization, but neither docs-as-code nor a fixed lifecycle is its universal foundation. |

Across these sources, the strongest genuine software assumptions occur in XP, TDD, ATDD's functional focus, and software-oriented architecture abstractions. Lean and Kanban cover broader work. The Rust process has concrete GitHub/review machinery. None requires AI, fixed agent roles, or greenfield starting conditions. Operational conventions below demonstrate work that does not follow a feature-delivery pipeline.

## 4. Evidence, science, and operations

| Primary source / observed position | Useful concept | Limitation and ADC disposition |
| --- | --- | --- |
| [DORA metrics guide](https://dora.dev/guides/dora-metrics/) treats delivery performance in application/service context and cautions against gaming, unlike comparisons, and measurement cost. | Evidence is contextual; improvement needs balanced observation. | **Adopt** context and proportional measurement. **Reject** mandatory delivery metrics or per-undertaking scorecards. Aggregate delivery performance does not prove an individual decision or investigation complete. |
| [Google SRE troubleshooting](https://sre.google/sre-book/effective-troubleshooting/) tests hypotheses against observations and interventions, preserving useful negative results and awareness of side effects. | Separate observation, explanation, and intervention; mitigation can precede explanation. | **Adopt** bounded conclusions, eliminated hypotheses, and operational residue. **Reject** a universal troubleshooting sequence or root-cause certainty as a condition for restoration. It requires domain-specific instruments, not necessarily code changes. |
| [SRE incident response](https://sre.google/workbook/incident-response/) separates restoring service from managing response and preserves shared investigative state. | Continuity survives responder changes. | **Adopt** current condition and remaining obligations. **Reject** universal incident-command roles or communication ceremonies. Incident logs can already carry ADC meanings. |
| [SRE postmortems](https://sre.google/sre-book/postmortem-culture/) preserve impact, mitigation, contributing causes, and follow-up; selected triggers justify their cost. | Learning is a result; mitigation, explanation, and prevention differ. | **Adopt** proportional learning records. **Reject** mandatory postmortems or Google-scale review for every task. A completed report does not prove preventive work has happened. |
| [Center for Open Science preregistration](https://www.cos.io/initiatives/prereg) distinguishes planned tests from exploration and makes planned and unplanned analyses interpretable. | Expectations, observations, and later interpretations are different. | **Adopt** honest negative/inconclusive findings and visible criteria changes. **Reject** mandatory preregistration, hypotheses for every exploration, or fixed statistical thresholds. Exploration is legitimate, not defective confirmation. |
| [NIST TN 2045](https://nvlpubs.nist.gov/nistpubs/TechnicalNotes/NIST.TN.2045.pdf) treats confirmation of performance thresholds for binary experimental responses. | Failing to establish a threshold is not itself proof of the opposite. | **Adopt** evidence insufficiency versus refutation. **Reject** universal sample sizes, p-values, or binary pass/fail. The statistical method has a specialized scope; its conclusions cannot be transplanted into every qualitative judgment. |
| [AWS operational testing and rollback practice](https://docs.aws.amazon.com/wellarchitected/latest/framework/ops_mit_deploy_risks_auto_testing_and_rollback.html) couples operational checks with recovery from unsuccessful changes. | Applied action, observed state, and recovery are distinct. | **Adopt** the distinctions for operations. **Reject** its automated deployment/testing machinery as core ADC obligations. This is domain guidance, not proof that every undertaking deploys anything. |
| [W3C PROV overview](https://www.w3.org/TR/prov-overview/) describes origins and relationships used to assess information quality and trust. | Evidence has sources and applicability relationships. | **Adopt** proportionate provenance. **Reject** mandatory RDF, serializers, exhaustive activity graphs, and audit ledgers. Knowing a source does not establish the truth of its claim. |

## 5. Small conventions and universal-kernel attempts

| Source | Extraction and boundary |
| --- | --- |
| [OMG Essence 1.2](https://www.omg.org/spec/Essence/1.2/PDF), especially sections 7 and 8.4.2.2 | Separates domain concepts and state from work products and practices. Its Work discussion explicitly allows abandonment and reversal; it is not simply waterfall. **Adopt** semantic/representation separation. **Modify** the software-system-centered kernel. **Reject** importing predefined state checklists, competencies, modeling language, and conformance classes. Its breadth exceeds the desired convention. |
| [Ivar Jacobson International's explanation](https://www.ivarjacobson.com/essence-explained-agile-tools) | Describes a kernel with separately composable practices, and records as representations rather than the things being progressed. **Adopt** that separation, **reject** mandatory cards, activity spaces, and competency levels. ADC need not model the whole practice of engineering to preserve a bounded account of work. |
| [Semantic Versioning 2.0.0](https://semver.org/) | Makes a small set of version signals meaningful against a declared public API, without prescribing an implementation tool. **Adopt** explicit scope, fixed published meanings, and concise normative rules. **Reject** API compatibility and release numbering as universal undertaking semantics. |
| [Conventional Commits 1.0.0](https://www.conventionalcommits.org/en/v1.0.0/) | Attaches agreed meaning to compact commit syntax with optional tooling. **Adopt** a small, understandable interoperability contract. **Reject** commits and literal message grammar as required carriers. Unlike its grammar, ADC's medium independence cannot promise automatic parsing. |
| [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119.html) and [RFC 8174](https://www.rfc-editor.org/rfc/rfc8174.html) | Supply requirement levels and uppercase interpretation. RFC 2119 section 6 advises reserving mandates for interoperability or harm prevention. **Adopt** that editorial discipline, not a standards-committee workflow. |
| [Boeckeler's hands-on SDD exploration](https://martinfowler.com/articles/exploring-gen-ai/sdd-3-tools.html), 2025-10-15 | Distinguishes spec-first, spec-anchored, and spec-as-source patterns and exposes maintenance ambiguity. This is a primary practitioner account, not a universal definition. **Adopt** explicit authority and maintenance choices; **reject** assuming all SDD means one frozen upfront specification. Current product facts come from their newer primary documentation above. |

## 6. Proposed abstraction boundary

The convention answers: **What is intended, what is now true, and on what basis can that be asserted or continued?** It does not answer who runs which prompt, how tasks are scheduled, where files belong, or which approval system enforces policy.

### Why an undertaking and three facets?

“Change” excludes investigation without intervention. “Task” often implies a scheduler unit. “Session” is a runtime boundary. “Product increment” excludes decisions and operations. **Undertaking** names a distinguishable purpose and scope without imposing its size or carrier. A small correction remains one record; interdependent efforts can refer to each other without a compulsory decomposition tree.

Intent, State, and Assessment are perspectives on one account, not independent entities needing three documents. The candidate concepts are consolidated as follows:

| Candidate | Proposal | Why it earns its place or is not universal |
| --- | --- | --- |
| Intent | Core facet; includes desired outcome/question and evaluation scope | Prevents activity from replacing the purpose. |
| Context, constraints, assumptions, risk | Material qualifiers, not universal registers | Needed when they change action or interpretation; otherwise omission is cheaper and sufficient. |
| Decision | Conditional durable content | Preserve consequential choices, not every reversible implementation step. |
| Change | Possible activity or result | Not every undertaking changes an external system. |
| Evidence | Basis linked to material claims | Makes evaluation possible outside trust in an agent's final message. |
| State | Core facet, including unresolved work | Enables continuation without a transcript or phase engine. |
| Outcome | Actual result assessed against intent | Can be a finding, failure, uncertainty, rejection, or recovery; not synonymous with output. |

### Consequential design decisions

| Choice | Selected design and rejected alternative |
| --- | --- |
| State vocabulary | Distinguish open, suspended, completed, and abandoned meanings; do not require these labels or a transition sequence. Treat failure as result and supersession as a replacement relationship. One overloaded `done` loses information; a universal lifecycle adds machinery. |
| Completion | Completion conditions concern the declared scope. A bounded investigation may complete inconclusively; “restore production” cannot complete merely because the attempt stopped. Explicitly changing scope preserves the unmet prior intent. |
| Evidence minimum | Enough source, method, target, result, and limits to interpret a material claim. A sentence can carry them. Neither a universal evidence form nor “any confident narrative counts” is acceptable. |
| Recording moment | Understand the action boundary before acting; preserve durable continuity before relinquishing context. No new form before each action. Urgent response can precede recording, with reconstruction identified afterward. |
| Authority | Preserve relevant authorization constraints and decisions, but ADC creates no authority or universal approval board. More capable models do not remove this distinction. |
| Proportionality | Consider impact, reversibility, uncertainty, and dependencies. Add information or independent checking because it addresses a need, not because an undertaking reached a higher ceremonial tier. |
| Conformance | One semantic core, assessed for a particular undertaking and point in time. No maturity ladder, filename test, or tool certification. Profiles may add domain controls without redefining the core. |
| Portability | Human-interpretable equivalence first; medium-specific mappings remain optional. A future serialization could aid automation but is not hidden inside this draft. |
| Durability | Retrieval for the expected continuation/evaluation period, not permanent history. Preserve material supersession, expiry, and conflicts without demanding an event-sourced ledger. |

## 7. Unresolved tensions and alternatives

1. **Meaning without a schema.** Human interpretation preserves medium independence but cannot guarantee automated interchange. The examples demonstrate equivalent meanings; they do not prove arbitrary natural-language parsers will agree. Consider a separate interchange profile only after real mappings expose demand.
2. **Materiality without box-ticking.** A universal field list creates empty records; entirely subjective “enough context” is unverifiable. C1–C7 supply explicit distinctions and an unfamiliar-participant test. Inter-rater agreement still needs field trials.
3. **Completion versus revised intent.** Honest revisions are necessary, but can launder failure. Preserve the old scope, change reason, and actual outcome. A revised completion does not retroactively fulfill the old undertaking.
4. **Durability versus cost and access.** Links avoid duplication but expire or restrict access. Summaries reduce cost but can lose evidential detail. Preserve what the intended audience needs and disclose missing access; do not equate a redacted assertion with available evidence.
5. **Risk tailoring versus under-assurance.** No universal score captures production blast radius, uncertainty, reversibility, and coordination. C6 requires a basis for high-consequence assurance but leaves domain-specific thresholds to local policy. ADC alone does not prove such thresholds are adequate.
6. **Small core versus extensions.** Standardizing collaboration/audit/operations profiles now would add untested commitments. This draft defines the extension mechanism and offers sketches only. No profile is necessary for core conformance.
7. **Benefit versus upkeep.** No empirical efficiency claim is made. Practical evaluation should measure handoff reconstruction, erroneous outcome claims, duplicated information, and maintenance effort on actual small and consequential work—not documentation volume.

## 8. Adversarial quality tests

These are document-level design checks, not results from production adoption or independent certification. Clause references refer to [ADC-SPEC.md](ADC-SPEC.md); cases refer to [ADC-EXAMPLES.md](ADC-EXAMPLES.md).

| Failure case | Design response and test witness |
| --- | --- |
| Silently assumes Git | C7 and section 6 permit any carrier; cases 4–7 require no repository. |
| Silently assumes source code | Undertaking definition includes decisions/findings; cases 4, 5, 6, and 7. |
| Automated tests are the only evidence | C4 permits observation, judgment, and analysis; cases 3–6 use them. |
| Assumes linear work | C5 permits reversal/reopening and prescribes no transition graph; paused work in case 2. |
| Requires a product increment | Cases 5–7 close on findings, decisions, and abandonment. |
| Cannot represent learning without implementation | C4 separates inference from observation; cases 5 and 6. |
| Cannot represent abandonment | C5 preserves abandoned intent, reasons, partial results, and residue; case 7. |
| Recreates information in another system | C3/C7 permit reuse and links; guide mappings place meaning in existing records. |
| Mandates artifacts only to satisfy ADC | Three facets are meanings, not files; case 1 is a compact existing record. |
| Becomes a workflow engine in prose | No transition prerequisites, mandatory roles, timers, ceremonies, or phase gates; C1/C2 are action and handoff invariants. |
| Depends on current model limitations | Human participants also need provenance, context, and reliable authority; no context-window size or prompt prescription appears in the core. |
| Costs more than its continuity value | C3/C6 favor material information and proportionate rigor; case 1 avoids separate planning or evidence artifacts. Actual cost remains unmeasured. |
| Equivalent records cannot be recognized | C5 gives distinct state meanings; C7 defines relationships; examples include a two-medium equivalence mapping. Automatic parsing remains out of scope. |
| Empty templates establish conformance | Section 4 requires substantive meaning, not filled headings; examples include nonconforming accounts. |

### Draft review result

A focused core critique and a subsequent six-document consistency review were performed. Revisions narrowed decision-retention triggers, removed continuation bookkeeping for abandoned work, allowed adequate historical findings to survive raw-data expiry, made evidence independence proportional, and clarified the conformance boundary. The final review found no critical contradiction across the specification, guide, examples, and quick reference. Structural checks found no missing local Markdown targets, malformed tables, or version mismatches; the existing repository license was checked separately and preserved. These checks do not establish empirical usability, rendered pagination, or continuing availability of external sources.

The draft therefore has a coherent proposed boundary, but not demonstrated universal adequacy. The next substantive evidence would come from applying it to existing records and testing whether independent participants recover the same state and scope with less reconstruction cost.
