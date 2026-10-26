# Collaboration

<a id="p.rules"></a>

**[P.rules](#p.rules). Follow the requirements in this outline and agree exceptions with the core maintainer before proceeding.**

*Requirement. [Responsibility](#responsibility), [Coordination](#coordination)*

Discuss departures from project defaults when they affect shared interfaces, meaning, compatibility, or another contributor’s work. Preferences alone do not block merging.

Shared requirements protect contributors and the project. Defaults and preferences settle routine choices without requiring discussion of every difference.

The outline is the source of shared contribution requirements and permissions. Exceptions need agreement with the core maintainer before proceeding. Conventions and component guides supply recommended forms and procedures.

Follow project defaults unless another approach better serves the work. Discuss departures when they affect shared interfaces, meaning, compatibility, or another contributor’s work. Guidance and editorial preferences help contributors write and organize their work. They do not require an explanation for every departure. Optional steps may be skipped.

Reviewers should distinguish requirements from recommendations when requesting changes. Differences in editorial preference alone should not block merging. Concrete problems can still be raised under [P.review-blockers](#p.review-blockers).

Contributors are welcome to raise issues with this guide or CONVENTIONS.md when they have ideas for improving the contribution process.

<a id="p.responsibility"></a>

**[P.responsibility](#p.responsibility). Take responsibility for the work you submit, regardless of tools or assistance.**

*Requirement. [Verification](../PRINCIPLES.md#verification), [Responsibility](#responsibility)*

Understand your changes well enough to explain them. Disclose tool use when needed to explain a research method, result, or limitation. Routine AI disclosures are not required.

Contributors are responsible for the work they submit, and reviewers are responsible for the edits they make. Contributors must understand their changes well enough to explain them and answer review questions. AI tools, code generators, and other assistance do not change these responsibilities or the contribution requirements.

Routine AI-use disclosures are not required. Explain tool use when it is part of the research method or necessary to understand a result or its limits. Contributors remain responsible for submitted work, including work copied or adapted from others.

<a id="p.renames"></a>

**[P.renames](#p.renames). Agree when a temporary compatibility alias will be removed.**

*Requirement. [Coherence](../PRINCIPLES.md#coherence) ↔ [Coordination](#coordination)*

Record the consumer’s migration obstacle and agree the removal point with the core maintainer.

A compatibility alias creates a migration obligation that can outlast the contribution. When a consumer cannot migrate in the same change, record the obstacle and agree with the core maintainer on when the alias will be removed. Complete renames are the default under [C.names.renames](../2-factoring.md#c.names.renames).

Resolve questions about the contribution's behavior, design, and readiness.

<a id="p.reviewer-tasks"></a>

**[P.reviewer-tasks](#p.reviewer-tasks). Announce review tasks and coordinate edits with the contributor.**

*Requirement. [Responsibility](#responsibility), [Coordination](#coordination)*

Let the contributor take announced tasks instead, except final editorial polish. Discuss behavior, design, or stated reasoning changes before making them. Agree history rewrites and PR metadata edits unless covered by P.final-cleanup.

Reviewers should tell the contributor which tasks they plan to take on, including edits, commits, pushes, history rewrites, and PR metadata changes. This lets the contributor avoid duplicate work or take on those tasks themselves. Final editorial polish remains the maintainer's responsibility under [P.final-cleanup](landing.md#p.final-cleanup).

Before changing behavior, design, or the contributor's stated reasoning, the reviewer should discuss the change with the contributor. History rewrites and PR metadata edits also need agreement unless they fall within P.final-cleanup.

<a id="p.review-blockers"></a>

**[P.review-blockers](#p.review-blockers). Ground review blockers in required rules or concrete problems.**

*Requirement. [Responsibility](#responsibility), [Coordination](#coordination)*

Identify the required rule or explain what would go wrong if merged. Present preferences as suggestions and ask for clarification when a rule is unclear.

A reviewer who asks for a change that must be made before merging should explain why it is necessary. The explanation should identify a required rule under [P.rules](#p.rules) that the contribution does not follow, or describe what would go wrong if the contribution were merged as written. For concerns about correctness, usability, documentation, or maintenance, the reviewer should explain the specific consequences.

Reviewers should present preferences as suggestions. If a rule's meaning is unclear, the reviewer should ask for clarification.

## Review

<a id="c.review-labels"></a>**[C.review-labels](#c.review-labels). Label a review comment when its status could be unclear.**

*Default. Policy [P.review-blockers](#p.review-blockers).*

Use `Required:`, `Suggestion:`, or `Question:` to distinguish blockers, preferences, and requests for clarification. A label is unnecessary when the status is already clear. Explain blockers under [P.review-blockers](#p.review-blockers).

## Working together

<a id="responsibility"></a>

### Responsibility: Assign decisions to the people accountable for them.

Contributors choose how to implement their work. The core maintainer decides on shared architecture, public interfaces, and project rules because they must maintain those decisions as contributors come and go.

<a id="coordination"></a>

### Coordination: Agree before disrupting another person's work.

Parallel exploration saves time when contributors can trust that their work will not be unexpectedly disrupted. Agreeing on shared changes before making them lets others adjust their plans and avoids wasted effort.
