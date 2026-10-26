# Landing

Prepare the reviewed contribution for `main` and record its integration. Substantive changes made during preparation return to review.

<a id="r.final-cleanup"></a>

**[R.final-cleanup](#r.final-cleanup). The core maintainer may polish existing comments and commit messages and prepare reviewed commits during final integration.**

*Permission. Principles [Coherence](../PRINCIPLES.md#coherence), [Provenance](../PRINCIPLES.md#provenance), [Responsibility](collaboration.md#responsibility) ↔ [Coordination](collaboration.md#coordination).*

The core maintainer bears most of the lasting cost of unclear prose and fragmented history. During final integration, the maintainer may perform the routine cleanup below without asking for separate approval.

**Editorial corrections**

- Correct spelling, grammar, formatting, and wording in existing comments while preserving their facts, constraints, and reasons.
- Correct spelling, grammar, and wording in commit subjects and bodies without changing their meaning or motivation.
- Apply commit-message format and wrapping rules.
- Format existing source and attribution trailers without changing their facts or credit.
- Add the PR number to a single-commit PR's commit subject.

**Commit preparation**

- Fold review fixups into the commits they complete. Their messages may stay brief until then.
- Combine or reorder reviewed commits when needed to make them coherent and buildable under [R.commit-buildability](../4-history.md#r.commit-buildability).

Combining or reordering commits must preserve the branch's final file contents on the same base. Rebasing onto a new base follows [R.conflict-resolution](#r.conflict-resolution). Editorial edits are limited to the prose and record corrections above. Preserve each change's motivation, source references, and author credit. Keep independent changes distinguishable under [R.change-scope](../4-history.md#r.change-scope).

The maintainer may amend commits, rebase them, and publish the rewritten PR branch using a lease for this cleanup. [Publishing a rewritten branch](#publishing-a-rewritten-branch) gives the commands. Before rewriting, coordinate with contributors whose branches depend on the affected commits. When merging, tell the contributor what was edited and how the commits were reorganized.

New explanations, factual corrections, changes to assumptions or motivation, and resolving ambiguous intent need discussion under [R.reviewer-tasks](collaboration.md#r.reviewer-tasks). Changes to attribution or PR metadata also follow R.reviewer-tasks. Executable-code changes and substantive conflict resolutions return to review under [R.conflict-resolution](#r.conflict-resolution).

<a id="r.conflict-resolution"></a>

**[R.conflict-resolution](#r.conflict-resolution). Resolve integration conflicts on the PR branch before landing.**

*Required. Principles [Coherence](../PRINCIPLES.md#coherence), [Coordination](collaboration.md#coordination).*

Integration conflicts are resolved on the PR branch, where reviewers can inspect the resolutions. Those resolutions can change behavior, so substantive changes need an explanation and a return to review before landing. The landing merge must introduce no further conflict-resolution edits.

<a id="r.merge-method"></a>

**[R.merge-method](#r.merge-method). Preserve final commits and record the contribution when landing.**

*Required. Principles [Coherence](../PRINCIPLES.md#coherence), [Provenance](../PRINCIPLES.md#provenance), [Proportionality](../PRINCIPLES.md#proportionality).*

The history should preserve reviewed units of work and explain their integration. Land multi-commit PRs with a merge commit that explains the contribution as a whole. Count commits after cleanup and preserve the resulting commits without squashing during landing.

For single-commit PRs, the [integration default](#r.integration.method) is a fast-forward. Their commit message supplies the permanent record under [R.single-commit-record](#r.single-commit-record). Add the PR number through authorized final cleanup under [R.final-cleanup](#r.final-cleanup).

<a id="r.direct-pushes"></a>

**[R.direct-pushes](#r.direct-pushes). The maintainer may push bounded repairs and current-state documentation directly to `main`.**

*Permission. Principles [Responsibility](collaboration.md#responsibility), [Coordination](collaboration.md#coordination) ↔ [Proportionality](../PRINCIPLES.md#proportionality).*

The core maintainer may push a fix directly to `main` when it addresses an identified fault with known expected behavior and affected callers. Documentation edits may also go directly to `main` when they describe existing behavior or clarify existing rules. This keeps routine corrections from waiting for a separate PR that would add little value.

New design or interfaces, multiple independent behaviors, uncertain impact, and changes to contribution rules need a PR. Other contributors use PRs by default. Direct commits must meet the same requirements as other commits. The [SpecTec module](spectec.md#spectec-build-and-checks) describes available checks.

## Integration defaults

<a id="r.integration"></a>**[R.integration](#r.integration). Integration defaults**

*Default. Rules [R.rules](collaboration.md#r.rules), [R.reviewer-tasks](collaboration.md#r.reviewer-tasks), [R.merge-method](#r.merge-method).*

<a id="r.integration.rebase"></a>**[R.integration.rebase](#r.integration.rebase). Rebase onto current `main` during final integration by default.**

*Default. Principles [Coordination](collaboration.md#coordination), [Proportionality](../PRINCIPLES.md#proportionality).*

Update earlier when dependencies or conflicts require it. Contributors need not rebase every open branch after each merge. Before replacing commits that dependent branches use, coordinate with affected contributors under [R.rules](collaboration.md#r.rules). Reviewer rewrites also follow [R.reviewer-tasks](collaboration.md#r.reviewer-tasks). Agree another integration method if rebasing would disrupt shared work.

<a id="r.integration.method"></a>**[R.integration.method](#r.integration.method). Fast-forward single-commit PRs by default.**

*Default. Rule [R.merge-method](#r.merge-method).*

Count commits after final cleanup. A fast-forward avoids an extra merge commit because the single commit supplies the contribution’s permanent record.

## Single-commit records

<a id="r.single-commit-record"></a>**[R.single-commit-record](#r.single-commit-record). A single-commit PR’s message must explain the PR’s motivation, result, and scope.**

*Required. Rules [R.commit-explanations](../4-history.md#r.commit-explanations), [R.pr-explanations](pr.md#r.pr-explanations), [R.merge-method](#r.merge-method).*

A fast-forward creates no merge message, so the commit message is the permanent landing record. Include the PR’s motivation, result, and scope, along with applicable source records. The motivation exception in [R.commit-explanations](../4-history.md#r.commit-explanations) also applies here.

## Merge messages

<a id="r.merge-subjects"></a>**[R.merge-subjects](#r.merge-subjects). Use `Merge: <lowercase summary> (#PR)` for merge subjects.**

*Default. Rules [R.commit-explanations](../4-history.md#r.commit-explanations), [R.merge-method](#r.merge-method).*

The summary uses the PR title with ordinary words in lowercase. Preserve proper names and acronyms. A framing paragraph explains the PR's motivation and overall result. Summary bullets describe the affected work under [R.merge-summary](#r.merge-summary).

<a id="r.merge-summary"></a>

**[R.merge-summary](#r.merge-summary). Merge-message summaries**

*Default. Rules [R.pr-explanations](pr.md#r.pr-explanations), [R.merge-method](#r.merge-method).*

<a id="r.merge-summary.overview"></a>**[R.merge-summary.overview](#r.merge-summary.overview). Use a framing paragraph followed by summary bullets.** The paragraph explains the motivation and overall result. For contributions other than Ports and Syncs, summarize the affected work by area and theme with typed bullets. A bullet can summarize several commits. Choose types and scopes for the contribution as a whole under [R.commit-format](../4-history.md#r.commit-format). Use `type: Description.` when a narrower scope adds no useful distinction. One broad bullet can suffice. Ports and Syncs use the source distinctions under [R.merge-summary.imports](ports.md#r.merge-summary.imports).

<a id="r.merge-summary.reuse"></a>**[R.merge-summary.reuse](#r.merge-summary.reuse). Use Scope and Minor Changes as the basis for a shorter merge summary.** Condense and regroup their bullets by theme, preserving the main outcome and significant incidental work. Do not reproduce the PR's inventory of APIs, tests or packaging details. Include source references only when they add useful context beyond the provenance preserved in the constituent commits.

Keep identifier backticks and use plain prefixes without bolding. Render Markdown links as their labels followed by URLs in parentheses. Wrap the text under [R.commit-display](../4-history.md#r.commit-display). For contributions other than Ports and Syncs, use `Changes:` and `Minor Changes:` sections when separating the main and incidental work helps scanning. A compact summary can use one list without headings. If the PR has no Scope list, compose summary bullets from its motivation, result, and affected work under [R.merge-summary.overview](#r.merge-summary.overview). The PR does not need a Scope section solely to supply these bullets.

```text
Merge: <lowercase summary> (#PR)

Framing paragraph explaining the motivation and resulting change.

- refactor(scope): Description.
- docs(scope): Description.
```

<a id="r.deferred-work"></a>**[R.deferred-work](#r.deferred-work). Reserve `DEFERRED:` for work explicitly postponed from the contribution.**

*Default. Rules [R.follow-ups](collaboration.md#r.follow-ups), [R.merge-method](#r.merge-method).*

Carry only the explicitly deferred items identified in the PR's Deferred Tasks subsection or review discussion. These can include a known shortcoming accepted for this PR that should be repaired soon, or work intentionally omitted from a Port or Sync for later adoption. Ideas and Open Questions do not become deferred commitments.

Use separate bullets without a deferred-work heading. Record the unfinished task and the reason for postponing it. This keeps the searchable backlog deliberately selective.

```text
- DEFERRED: Port the omitted input forms after their dependency lands.
```

<a id="r.pr-number"></a>**[R.pr-number](#r.pr-number). Append `(#PR)` to a single-commit PR's commit subject during authorized final cleanup.**

*Default. Rules [R.final-cleanup](#r.final-cleanup), [R.merge-method](#r.merge-method).*

[R.merge-method](#r.merge-method) requires the PR number in the permanent landing record. Appending `(#PR)` to the subject is the default format. The [landing recipes](#landing-recipes) contain amendment and integration commands.

## Landing recipes

These examples use `origin` as the publication remote and `topic` as the reviewed branch. Start with a clean integration checkout and update `main` without creating an incidental merge.

```bash
git fetch origin
git switch main
git merge --ff-only origin/main
```

### Multi-commit PRs

For a multi-commit PR, prepare the merge before recording its cover letter.

```bash
git merge --no-ff --no-commit topic
```

If this merge reports conflicts, run `git merge --abort`. Resolve the conflicts on the PR branch and make the resolutions available for review under [R.conflict-resolution](#r.conflict-resolution). Repeat integration after resolving any review blockers. Follow the existing component checking instructions, then record the merge message and publish.

```bash
git commit
git push origin main
```

### Single-commit PRs

For a single-commit PR, the commit message is the permanent landing record. Before fast-forward landing, use `git commit --amend` on its branch, preserving the author and the complete message. An amend changes the commit ID. Publish the reviewed result with the [lease procedure](#publishing-a-rewritten-branch).

The proposed branch must be exactly one commit ahead of current `main`, with `main` as an ancestor. Check both conditions from the integration checkout.

```bash
git merge-base --is-ancestor main topic
git rev-list --count main..topic
```

The ancestry check must succeed and the count must be `1`. `--ff-only` checks whether fast-forwarding is possible, not the number of commits. If the ancestry check fails, update the branch through the agreed integration process. Once both conditions hold, land it with these commands.

```bash
git merge --ff-only topic
git push origin main
```

## Publishing a rewritten branch

Publish a rewritten branch within the agreement under [R.reviewer-tasks](collaboration.md#r.reviewer-tasks) or the maintainer's final-cleanup permission under [R.final-cleanup](#r.final-cleanup). Use a lease against the remote tip you reviewed so another contributor's intervening push prevents replacement. For an example branch named `topic`, capture the tip before rewriting.

```bash
git fetch origin
git switch topic
reviewed_tip=$(git rev-parse origin/topic)
```

After reviewing the remote work, completing the authorized rewrite, and coordinating any dependent branches, publish with this command.

```bash
git push --force-with-lease=refs/heads/topic:"$reviewed_tip" origin HEAD:refs/heads/topic
```

If the lease fails, inspect the remote updates before preparing another rewrite.
