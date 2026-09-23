# Putting ADC into practice

Informative adoption plan for [ADC 0.1.0-draft.1](ADC-SPEC.md). This document and the two application patterns below add no core requirements or standardized ADC profiles. They illustrate how to use existing records without installing anything.

## The decision to make for each undertaking

Choose the existing record that will answer **why this work exists, where it stands, and what can be claimed about it**. Use references to other records for the facts they establish. A single undertaking can span several repositories without being split just to fit a tool. Separate undertakings when their purpose, authority, evaluation, or ownership genuinely differs.

| Need | Solo GitHub developer | Multi-repo platform team |
| --- | --- | --- |
| Work identity and current disposition | A commit for a tiny finished correction; otherwise a PR or an issue if work outlives a PR/session. | Existing Jira work item, at the level the team already plans and tracks. A PI objective or sprint supplies scheduling context, not outcome evidence. |
| Proposed and actual source/configuration changes | Git commit and PR when one exists. | PRs in the affected repositories, linked from the Jira item. Each PR describes its own scope; the Jira item holds the overall outcome. |
| Material decision | Issue/PR discussion if local to the work; tracked document if it will govern later work. | Jira discussion for an undertaking-specific choice; a maintained document in the owning repository or existing knowledge base for a durable cross-repo decision. Jira links to it. |
| Testing | Actual test result in the PR, check run, or compact summary; no test tracker merely for ADC. | Existing qTest **test log / run result** for a test already managed there; the test case alone is a definition, not proof of execution. Other checks remain in their existing systems. |
| Live or operational state | Record a bounded observation in the issue/PR or existing operational record. | Existing change/incident record or appropriately retained observation, linked from Jira. A merged PR or passed staging run does not establish production state. |
| Sensitive or expiring evidence | Restricted existing location and a shareable, bounded summary where needed. | Retain a non-secret summary with target, time, method, result, and limits in the authorized record; disclose restricted or expired links to the intended audience. |

These are defaults for the two pilots, not prescribed ADC storage rules. When a system is unavailable, use the closest existing durable record that preserves the same meaning. Avoid copying the same outcome narrative into a PR, Jira, and qTest. Let each system speak for the fact it knows; a short link and interpretation connects them.

## Pilot sequence

1. **Select representative work.** Solo: a small correction, a multi-session change, and an investigation or decision without code. Team: one cross-repository integration/configuration change, one operational investigation or remediation, and one decision or experiment that can end without delivery. Use already planned work; do not create tasks for the sake of the pilot.
2. **Name the current account for each undertaking.** The solo account will usually be its issue or PR. The team account will usually be its existing Jira item. Identify where the authoritative source revision, qTest execution (if relevant), and operational observation live. Record the links only where there is a material reason for a later reader to follow them.
3. **Apply the smallest useful text.** Copy the appropriate [solo pattern](ADC-SOLO-GITHUB.md) or [team pattern](ADC-TEAM-PLATFORM.md) into the existing record as needed; delete inapplicable prompts. Reuse the ticket's existing goal, acceptance notes, and ownership instead of restating them. Do not add ADC labels, forms, or special agents yet.
4. **Update at meaningful boundaries.** New information changes intent, a material decision is made, someone hands work off, the work is deliberately suspended, or an outcome is claimed. Ordinary commits and routine status moves need no special ADC ceremony.
5. **Review actual use after those cases.** Have the solo developer return after another session and an unfamiliar team member read one team account. Ask them to state the original purpose, actual current state, basis and limits of the result, and next action without reconstructing a chat. Note any missing facts, duplicate upkeep, time spent maintaining the account, and cases where “Done” overstates an outcome. Remove prompts that add no value; strengthen only the gaps found.

The pilot succeeds if existing records allow accurate continuation and bounded evaluation at an acceptable cost. A filled template, qTest entry, number of links, or mere PR merge is not a success measure. If a particular tool mapping fails, adjust the mapping rather than modifying ADC core to match that tool.

## What to standardize after the pilot

Standardize a **reading convention** first: where the current account is, what a closure claim says, and how to find evidence. If repeated PRs benefit from prefilling a small prompt, an optional [GitHub PR template](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/creating-a-pull-request-template-for-your-repository) can be placed in the relevant repositories or an account/organization default; its mere presence does not prove conformance. Team Jira fields and statuses should be mapped to ADC meanings only after checking their actual local configuration. A qTest–Jira integration can be used if already configured; direct links to the appropriate qTest result are sufficient without it.

Avoid automatic closure triggered by a link when the undertaking includes deployment, live verification, or more than one repository. GitHub can [auto-close a linked issue on merge](https://docs.github.com/en/issues/tracking-your-work-with-issues/using-issues/linking-a-pull-request-to-an-issue); that system event establishes a merge, not completion of a broader undertaking. Use ordinary references where appropriate or configure the repository's behavior consciously.

The specific templates, repo names, sample Jira key, and fictitious observations below are demonstrations. An organization that later wants binding local obligations can publish a named, versioned profile under the extension rules in the specification. Until then these are adaptable application patterns.

## Application patterns

- [Solo developer on GitHub](ADC-SOLO-GITHUB.md): consistent historical record across repositories with no collaboration workflow.
- [Platform team with GitHub, Jira, and qTest](ADC-TEAM-PLATFORM.md): existing scrum and PI planning, cross-repo work, tests where they add evidence, and operational outcomes.
