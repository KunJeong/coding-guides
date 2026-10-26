# Collaboration

These rules guide a review of someone else's PR. What the contributor must do comes from the project's CONTRIBUTING.md, which a review of that PR loads together with this module.

<a id="r.reviewer-tasks"></a>**[R.reviewer-tasks](#r.reviewer-tasks). Announce review tasks and coordinate edits with the contributor.**

*Principles [Responsibility](#responsibility), [Coordination](#coordination).*

Reviewers should tell the contributor which tasks they plan to take on, including edits, commits, pushes, history rewrites, and PR metadata changes. This lets the contributor avoid duplicate work or take on those tasks themselves. Final editorial polish remains the maintainer's responsibility under [R.final-cleanup](landing.md#r.final-cleanup).

Before changing behavior, design, or the contributor's stated reasoning, the reviewer should discuss the change with the contributor. History rewrites and PR metadata edits also need agreement unless they fall within R.final-cleanup.

<a id="r.review-blockers"></a>**[R.review-blockers](#r.review-blockers). Ground review blockers in required rules or concrete problems.**

*Principles [Responsibility](#responsibility), [Coordination](#coordination).*

A reviewer who asks for a change that must be made before merging should explain why it is necessary. The explanation should identify a requirement in the project's CONTRIBUTING.md that the contribution does not follow, or describe what would go wrong if the contribution were merged as written. For concerns about correctness, usability, documentation, or maintenance, the reviewer should explain the specific consequences.

Reviewers should present preferences as suggestions. If a rule's meaning is unclear, the reviewer should ask for clarification.

<a id="r.follow-ups"></a>**[R.follow-ups](#r.follow-ups). Do not delay a ready contribution for independent follow-up work.**

*Principles [Coherence](../PRINCIPLES.md#coherence), [Proportionality](../PRINCIPLES.md#proportionality).*

While a PR is under review, its planned topic should remain stable. Newly discovered independent work normally belongs in another PR, unless a separate PR would add little value.

Once review blockers are resolved, the contribution can proceed towards landing. Newly discovered work belongs in another PR unless it is needed to implement or verify the current contribution. Independent follow-up work should not hold up a ready contribution or other work that depends on it.

The PR should identify work explicitly postponed from the contribution and explain why it was postponed. Preserve that record when landing. Possible future improvements are not deferred commitments.

## Review

<a id="r.review-labels"></a>**[R.review-labels](#r.review-labels). Label a review comment when its status could be unclear.**

Use `Required:`, `Suggestion:`, or `Question:` to distinguish blockers, preferences, and requests for clarification. A label is unnecessary when the status is already clear. Explain blockers under [R.review-blockers](#r.review-blockers).

## Working together

<a id="responsibility"></a>

### Responsibility: Assign decisions to the people accountable for them.

Contributors choose how to implement their work. The core maintainer decides on shared architecture, public interfaces, and project rules because they must maintain those decisions as contributors come and go.

<a id="coordination"></a>

### Coordination: Agree before disrupting another person's work.

Parallel exploration saves time when contributors can trust that their work will not be unexpectedly disrupted. Agreeing on shared changes before making them lets others adjust their plans and avoids wasted effort.
