# Collaboration

These proposed policies are derived from SpecTec research and collaboration practices. They apply as shared requirements and permissions only where a project adopts them. Repository rules and explicit agreements take precedence, including when revising history or publishing changes. These policies do not establish agreements or grant permission to change another contributor's work.

<a id="r.rules"></a>**[R.rules](#r.rules). Follow the requirements in this outline and agree exceptions with the core maintainer before proceeding.**

*Requirement. [Responsibility](#responsibility), [Coordination](#coordination)*

Discuss departures from project defaults when they affect shared interfaces, meaning, compatibility, or another contributor’s work. Preferences alone do not block merging.

Shared requirements protect contributors and the project. Defaults and preferences settle routine choices without requiring discussion of every difference.

The outline is the source of shared contribution requirements and permissions. Exceptions need agreement with the core maintainer before proceeding. Conventions and component guides supply recommended forms and procedures.

Follow project defaults unless another approach better serves the work. Discuss departures when they affect shared interfaces, meaning, compatibility, or another contributor’s work. Guidance and editorial preferences help contributors write and organize their work. They do not require an explanation for every departure. Optional steps may be skipped.

Reviewers should distinguish requirements from recommendations when requesting changes. Differences in editorial preference alone should not block merging. Concrete problems can still be raised under [R.review-blockers](#r.review-blockers).

Contributors are welcome to raise issues with these guides when they have ideas for improving the contribution process.

<a id="r.responsibility"></a>**[R.responsibility](#r.responsibility). Take responsibility for the work you submit, regardless of tools or assistance.**

*Requirement. [Verification](../PRINCIPLES.md#verification), [Responsibility](#responsibility)*

Understand your changes well enough to explain them. Disclose tool use when needed to explain a research method, result, or limitation. Routine AI disclosures are not required.

Contributors are responsible for the work they submit, and reviewers are responsible for the edits they make. Contributors must understand their changes well enough to explain them and answer review questions. AI tools, code generators, and other assistance do not change these responsibilities or the contribution requirements.

Routine AI-use disclosures are not required. Explain tool use when it is part of the research method or necessary to understand a result or its limits. Contributors remain responsible for submitted work, including work copied or adapted from others.

<a id="r.renames"></a>**[R.renames](#r.renames). Agree when a temporary compatibility alias will be removed.**

*Requirement. [Coherence](../PRINCIPLES.md#coherence) ↔ [Coordination](#coordination)*

Record the consumer’s migration obstacle and agree the removal point with the core maintainer.

A compatibility alias creates a migration obligation that can outlast the contribution. When a consumer cannot migrate in the same change, record the obstacle and agree with the core maintainer on when the alias will be removed. Complete renames are the default under [R.names.renames](../2-factoring.md#r.names.renames).

Resolve questions about the contribution's behavior, design, and readiness.

<a id="r.reviewer-tasks"></a>**[R.reviewer-tasks](#r.reviewer-tasks). Announce review tasks and coordinate edits with the contributor.**

*Requirement. [Responsibility](#responsibility), [Coordination](#coordination)*

Let the contributor take announced tasks instead, except final editorial polish. Discuss behavior, design, or stated reasoning changes before making them. Agree history rewrites and PR metadata edits unless covered by R.final-cleanup.

Reviewers should tell the contributor which tasks they plan to take on, including edits, commits, pushes, history rewrites, and PR metadata changes. This lets the contributor avoid duplicate work or take on those tasks themselves. Final editorial polish remains the maintainer's responsibility under [R.final-cleanup](landing.md#r.final-cleanup).

Before changing behavior, design, or the contributor's stated reasoning, the reviewer should discuss the change with the contributor. History rewrites and PR metadata edits also need agreement unless they fall within R.final-cleanup.

<a id="r.review-blockers"></a>**[R.review-blockers](#r.review-blockers). Ground review blockers in required rules or concrete problems.**

*Requirement. [Responsibility](#responsibility), [Coordination](#coordination)*

Identify the required rule or explain what would go wrong if merged. Present preferences as suggestions and ask for clarification when a rule is unclear.

A reviewer who asks for a change that must be made before merging should explain why it is necessary. The explanation should identify a required rule under [R.rules](#r.rules) that the contribution does not follow, or describe what would go wrong if the contribution were merged as written. For concerns about correctness, usability, documentation, or maintenance, the reviewer should explain the specific consequences.

Reviewers should present preferences as suggestions. If a rule's meaning is unclear, the reviewer should ask for clarification.

<a id="r.follow-ups"></a>**[R.follow-ups](#r.follow-ups). Do not delay a ready contribution for independent follow-up work.**

*Requirement. [Coherence](../PRINCIPLES.md#coherence), [Proportionality](../PRINCIPLES.md#proportionality)*

Record deliberately postponed tasks and their reasons, and preserve the record when landing. Possible improvements are not deferred commitments.

While a PR is under review, its planned topic should remain stable. Newly discovered independent work normally belongs in another PR, unless a separate PR would add little value.

Once review blockers are resolved, the contribution can proceed towards landing. Newly discovered work belongs in another PR unless it is needed to implement or verify the current contribution. Independent follow-up work should not hold up a ready contribution or other work that depends on it.

The PR should identify work explicitly postponed from the contribution and explain why it was postponed. Preserve that record when landing. Possible future improvements are not deferred commitments.

## Review

<a id="r.review-labels"></a>**[R.review-labels](#r.review-labels). Label a review comment when its status could be unclear.**

*Default. Policy [R.review-blockers](#r.review-blockers).*

Use `Required:`, `Suggestion:`, or `Question:` to distinguish blockers, preferences, and requests for clarification. A label is unnecessary when the status is already clear. Explain blockers under [R.review-blockers](#r.review-blockers).

## Working together

<a id="responsibility"></a>

### Responsibility: Assign decisions to the people accountable for them.

Contributors choose how to implement their work. The core maintainer decides on shared architecture, public interfaces, and project rules because they must maintain those decisions as contributors come and go.

<a id="coordination"></a>

### Coordination: Agree before disrupting another person's work.

Parallel exploration saves time when contributors can trust that their work will not be unexpectedly disrupted. Agreeing on shared changes before making them lets others adjust their plans and avoids wasted effort.
