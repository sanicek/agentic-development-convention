# ADC pattern: solo developer on GitHub

Informative application of [ADC 0.1.0-draft.1](ADC-SPEC.md). The aim is a reliable history for your future self across repositories, without a coordination process. All examples here are fictional. This is a reusable example, not a requirement to create the named files or headings.

## Pick one account for each piece of work

| Work | Best existing account | What it needs to preserve |
| --- | --- | --- |
| Small reversible correction finished in one sitting | Commit message; optional PR if you already use one. | Purpose, narrow result, and direct check. Example: `Correct offline-host error text. Inspected diff: one message changed; no run attempted.` |
| Change spread over sessions | GitHub issue for intent/current state; PR for the proposed change and evaluated revision. | Link between them; issue remains the current account until the whole intended outcome is evaluated. |
| One PR is the entire undertaking | PR description and its discussion. | Original goal, material boundaries, evidence for the final revision, actual result and remaining limits. No issue needed. |
| Investigation or choice with no code | Existing issue/discussion or maintained project note. | Question, observations or reasoning, conclusion or uncertainty, and whether any implementation remains intended. |
| Long-lived decision affecting later work | Existing architecture/operations document in the owning repo, or a central note if it truly spans repositories. | Decision, reason, applicable scope, and what it supersedes. Link from affected undertakings. |

Apply the same semantic distinctions in every repo; copying a directory structure or a template into every repo is optional. Git history captures *what text changed*. A short account supplies *why*, *what was checked*, and *what the result actually means*. For a one-line correction, that can be a commit message; for a complex prototype, an issue and PR are usually easier to return to than a sequence of commits.

## Copyable prompt for an issue or PR

Use only prompts that add meaning missing from existing fields. An issue can carry intent and current status; a PR can carry evaluated code and checks. If the same undertaking uses both, link them and write each fact once. The headings are suggestions, not required ADC syntax.

```markdown
Purpose and scope: [What question or result is sought? What is excluded if material?]
Current state: [Observed state; proposed work clearly separated from completed work.]
Material decisions: [Only choices whose reason will matter later; otherwise omit.]
Result and basis: [Exact revision/environment/period as needed; check or observation and result.]
Limits and continuation: [Unexamined scope, open work, or why this work stops.]
```

For an interruption, update `Current state` and `Limits and continuation` before leaving the session. For closure, state completed versus abandoned and say which original conditions were met. A passing local test supports only the code revision it ran against; it does not prove a deployment. A document can be complete with a decision that implementation should not proceed.

## Worked example: multi-session correction

Suppose a repository for an AAP execution environment build has a dependency update that breaks a collection import. The following GitHub issue and PR text illustrate a short durable account. IDs, commands, results, and revisions are illustrative; no build was run for this document.

**Issue `#83` — current account.**

> Purpose: restore imports for the existing base execution environment after updating the dependency lock. Constraint: preserve the supported Python version and do not change production image tags in this undertaking. Completion requires a successful build, an import check against that built image, and a reviewed dependency delta. Publishing or deploying the image is separate work.
>
> Current state (session one): open. Import fails in image `ee-test:83a`; the dependency diff points to an incompatible package version. Proposed pin `x.y.z` is under review. No production tag changed. Next: build with the pin and inspect the installed package versions. The suspected incompatibility is a hypothesis, not a verified root cause.

**PR `#84` — source change and observed checks.**

> Related undertaking: issue `#83`. Pin package to `x.y.z` in the build inputs; no production configuration touched. At revision `abc123` in the fictional local build, the container build exited successfully and `ansible-galaxy collection list` showed the target collection. The import check reported success inside that built image. The dependency diff contains the one intended pin. These observations cover `abc123` in the local test environment, not registry publication or production behavior.

**Issue `#83` — closure after the PR merge.**

> Completed for the stated build-and-import scope at revision `abc123`; the build, import result, and reviewed dependency diff are in PR `#84`. No image was published and no production tag changed. Publishing or deployment, if desired, is a separate undertaking; it is not implied complete here.

If the PR changes after the checks, identify whether the evidence still applies to its final revision. If the build fails and you stop, record abandoned or suspended with the failure and useful findings instead of closing the issue as a successful fix. GitHub's [issue auto-closure on a linked PR merge](https://docs.github.com/en/issues/tracking-your-work-with-issues/using-issues/linking-a-pull-request-to-an-issue) is useful only when merge actually satisfies the whole issue scope; ordinary links are safer for work with later checks.

## Cross-repository history without a catalog

Use the native search and links of your GitHub account to recover issue and PR histories. If a single decision governs multiple projects, maintain **one** authoritative decision in the owning repo or a truly shared existing location and link to it. For occasional cross-repo work, a short central issue can identify the purpose and link the affected PRs; avoid creating a permanent central register merely because multiple repositories exist.

Try this pattern on the three cases in the [adoption plan](ADC-ADOPTION.md). Inspect what is missing after returning in a new session, then adjust the prompts rather than adding routine ceremonies.
