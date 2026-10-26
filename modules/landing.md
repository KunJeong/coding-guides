# Landing

Prepare the reviewed contribution for `main` and record its integration. Substantive changes made during preparation return to review.

<a id="p.final-cleanup"></a>

**[P.final-cleanup](#p.final-cleanup). The core maintainer may polish existing comments and commit messages and prepare reviewed commits during final integration.**

*Permission. [Coherence](../PRINCIPLES.md#coherence), [Provenance](../PRINCIPLES.md#provenance), [Responsibility](collaboration.md#responsibility) ↔ [Coordination](collaboration.md#coordination)*

Without separate approval, this permits meaning-preserving wording and formatting corrections, formatting existing source trailers, adding a single-commit PR number, and folding, combining, or reordering reviewed commits for coherence and buildability. Combining or reordering must preserve final file contents on the same base. All cleanup must preserve motivation, sources, and author credit. Keep independent changes distinguishable. The maintainer may amend, rebase, and publish with a lease after coordinating dependent branches, and must report the cleanup at merge. New explanations, factual corrections, changed assumptions or motivation, ambiguous intent, attribution changes, and PR metadata changes need discussion. Executable-code changes and substantive conflict resolutions return to review.

The core maintainer bears most of the lasting cost of unclear prose and fragmented history. During final integration, the maintainer may perform the routine cleanup below without asking for separate approval.

**Editorial corrections**

- Correct spelling, grammar, formatting, and wording in existing comments while preserving their facts, constraints, and reasons.
- Correct spelling, grammar, and wording in commit subjects and bodies without changing their meaning or motivation.
- Apply commit-message format and wrapping conventions.
- Format existing source and attribution trailers without changing their facts or credit.
- Add the PR number to a single-commit PR's commit subject.

**Commit preparation**

- Fold review fixups into the commits they complete.
- Combine or reorder reviewed commits when needed to make them coherent and buildable under [P.commit-buildability](../4-history.md#p.commit-buildability).

Combining or reordering commits must preserve the branch's final file contents on the same base. Rebasing onto a new base follows [P.conflict-resolution](#p.conflict-resolution). Editorial edits are limited to the prose and record corrections above. Preserve each change's motivation, source references, and author credit. Keep independent changes distinguishable under [P.change-scope](../4-history.md#p.change-scope).

The maintainer may amend commits, rebase them, and publish the rewritten PR branch using a lease for this cleanup. [Publishing a rewritten branch](#publishing-a-rewritten-branch) gives the commands. Before rewriting, coordinate with contributors whose branches depend on the affected commits. When merging, tell the contributor what was edited and how the commits were reorganized.

New explanations, factual corrections, changes to assumptions or motivation, and resolving ambiguous intent need discussion under [P.reviewer-tasks](collaboration.md#p.reviewer-tasks). Changes to attribution or PR metadata also follow P.reviewer-tasks. Executable-code changes and substantive conflict resolutions return to review under [P.conflict-resolution](#p.conflict-resolution).

<a id="p.conflict-resolution"></a>

**[P.conflict-resolution](#p.conflict-resolution). Resolve integration conflicts on the PR branch before landing.**

*Requirement. [Coherence](../PRINCIPLES.md#coherence), [Coordination](collaboration.md#coordination)*

Return substantive resolutions to review. The landing merge must introduce no further conflict-resolution edits.

Integration conflicts are resolved on the PR branch, where reviewers can inspect the resolutions. Those resolutions can change behavior, so substantive changes need an explanation and a return to review before landing. The landing merge must introduce no further conflict-resolution edits.

<a id="p.merge-method"></a>

**[P.merge-method](#p.merge-method). Preserve final commits and record the contribution when landing.**

*Requirement. [Coherence](../PRINCIPLES.md#coherence), [Provenance](../PRINCIPLES.md#provenance), [Proportionality](../PRINCIPLES.md#proportionality)*

Land multi-commit PRs with a merge commit explaining the whole contribution. Count commits after cleanup and preserve them without squashing during landing. A single-commit PR’s message must carry its result, scope, and the motivation required by P.commit-explanations. Add its PR number through authorized cleanup.

The history should preserve reviewed units of work and explain their integration. Land multi-commit PRs with a merge commit that explains the contribution as a whole. Count commits after cleanup and preserve the resulting commits without squashing during landing.

For single-commit PRs, the [integration default](#c.integration.method) is a fast-forward. Their commit message supplies the permanent record under [C.single-commit-record](#c.single-commit-record). Add the PR number through authorized final cleanup under [P.final-cleanup](#p.final-cleanup).

<a id="p.direct-pushes"></a>

**[P.direct-pushes](#p.direct-pushes). The maintainer may push bounded repairs and current-state documentation directly to `main`.**

*Permission. [Responsibility](collaboration.md#responsibility), [Coordination](collaboration.md#coordination) ↔ [Proportionality](../PRINCIPLES.md#proportionality)*

Repairs must address an identified fault with known expected behavior and affected callers. Documentation edits must describe existing behavior or clarify existing rules. New designs or interfaces, multiple independent behaviors, uncertain impact, and changes to contribution rules need a PR. Other contributors use PRs by default. Direct changes must meet the same requirements.

The core maintainer may push a fix directly to `main` when it addresses an identified fault with known expected behavior and affected callers. Documentation edits may also go directly to `main` when they describe existing behavior or clarify existing rules. This keeps routine corrections from waiting for a separate PR that would add little value.

New design or interfaces, multiple independent behaviors, uncertain impact, and changes to contribution rules need a PR. Other contributors use PRs by default. Direct commits must meet the same outline requirements. The [SpecTec module](spectec.md#spectec-build-and-checks) describes available checks.

## Integration defaults

<a id="c.integration"></a>**[C.integration](#c.integration). Integration defaults**

*Default. Policies [P.rules](collaboration.md#p.rules), [P.reviewer-tasks](collaboration.md#p.reviewer-tasks), [P.merge-method](#p.merge-method).*

<a id="c.integration.rebase"></a>**[C.integration.rebase](#c.integration.rebase). Rebase onto current `main` during final integration by default.**

*Default. Principles [Coordination](collaboration.md#coordination), [Proportionality](../PRINCIPLES.md#proportionality).*

Update earlier when dependencies or conflicts require it. Contributors need not rebase every open branch after each merge. Before replacing commits that dependent branches use, coordinate with affected contributors under [P.rules](collaboration.md#p.rules). Reviewer rewrites also follow [P.reviewer-tasks](collaboration.md#p.reviewer-tasks). Agree another integration method if rebasing would disrupt shared work.

<a id="c.integration.method"></a>**[C.integration.method](#c.integration.method). Fast-forward single-commit PRs by default.**

*Default. Policy [P.merge-method](#p.merge-method).*

Count commits after final cleanup. A fast-forward avoids an extra merge commit because the single commit supplies the contribution’s permanent record.

## Single-commit records

<a id="c.single-commit-record"></a>**[C.single-commit-record](#c.single-commit-record). A single-commit PR’s message must explain the PR’s motivation, result, and scope.**

*Outline requirement. Policies [P.commit-explanations](../4-history.md#p.commit-explanations), [P.pr-explanations](pr.md#p.pr-explanations), [P.merge-method](#p.merge-method).*

A fast-forward creates no merge message, so the commit message is the permanent landing record. Include the PR’s motivation, result, and scope, along with applicable source records. The motivation exception in [P.commit-explanations](../4-history.md#p.commit-explanations) also applies here.

## Merge messages

<a id="c.merge-subjects"></a>**[C.merge-subjects](#c.merge-subjects). Use `Merge: <lowercase summary> (#PR)` for merge subjects.**

*Default. Policies [P.commit-explanations](../4-history.md#p.commit-explanations), [P.merge-method](#p.merge-method).*

The summary uses the PR title with ordinary words in lowercase. Preserve proper names and acronyms. A framing paragraph explains the PR's motivation and overall result. Summary bullets describe the affected work under [C.merge-summary](#c.merge-summary).

<a id="c.merge-summary"></a>

**[C.merge-summary](#c.merge-summary). Merge-message summaries**

*Default. Policies [P.pr-explanations](pr.md#p.pr-explanations), [P.merge-method](#p.merge-method).*

<a id="c.merge-summary.overview"></a>**[C.merge-summary.overview](#c.merge-summary.overview). Use a framing paragraph followed by summary bullets.** The paragraph explains the motivation and overall result. For contributions other than Ports and Syncs, summarize the affected work by area and theme with typed bullets. A bullet can summarize several commits. Choose types and scopes for the contribution as a whole under [C.commit-format](../4-history.md#c.commit-format). Use `type: Description.` when a narrower scope adds no useful distinction. One broad bullet can suffice. Ports and Syncs use the source distinctions under [C.merge-summary.imports](ports.md#c.merge-summary.imports).

<a id="c.merge-summary.reuse"></a>**[C.merge-summary.reuse](#c.merge-summary.reuse). Use Scope and Minor Changes as the basis for a shorter merge summary.** Condense and regroup their bullets by theme, preserving the main outcome and significant incidental work. Do not reproduce the PR's inventory of APIs, tests or packaging details. Include source references only when they add useful context beyond the provenance preserved in the constituent commits.

Keep identifier backticks and use plain prefixes without bolding. Render Markdown links as their labels followed by URLs in parentheses. Wrap the text under [C.commit-display](../4-history.md#c.commit-display). For contributions other than Ports and Syncs, use `Changes:` and `Minor Changes:` sections when separating the main and incidental work helps scanning. A compact summary can use one list without headings. If the PR has no Scope list, compose summary bullets from its motivation, result, and affected work under [C.merge-summary.overview](#c.merge-summary.overview). The PR does not need a Scope section solely to supply these bullets.

```text
Merge: <lowercase summary> (#PR)

Framing paragraph explaining the motivation and resulting change.

- refactor(scope): Description.
- docs(scope): Description.
```

<a id="c.deferred-work"></a>**[C.deferred-work](#c.deferred-work). Reserve `DEFERRED:` for work explicitly postponed from the contribution.**

*Default. Policies [P.follow-ups](pr.md#p.follow-ups), [P.merge-method](#p.merge-method).*

Carry only the explicitly deferred items identified in the PR's Deferred Tasks subsection or review discussion. These can include a known shortcoming accepted for this PR that should be repaired soon, or work intentionally omitted from a Port or Sync for later adoption. Ideas and Open Questions do not become deferred commitments.

Use separate bullets without a deferred-work heading. Record the unfinished task and the reason for postponing it. This keeps the searchable backlog deliberately selective.

```text
- DEFERRED: Port the omitted input forms after their dependency lands.
```

<a id="c.pr-number"></a>**[C.pr-number](#c.pr-number). Append `(#PR)` to a single-commit PR's commit subject during authorized final cleanup.**

*Default. Policies [P.final-cleanup](#p.final-cleanup), [P.merge-method](#p.merge-method).*

[P.merge-method](#p.merge-method) requires the PR number in the permanent landing record. Appending `(#PR)` to the subject is the default format. The [landing recipes](#landing-recipes) contain amendment and integration commands.

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

If this merge reports conflicts, run `git merge --abort`. Resolve the conflicts on the PR branch and make the resolutions available for review under [P.conflict-resolution](#p.conflict-resolution). Repeat integration after resolving any review blockers. Follow the existing component checking instructions, then record the merge message and publish.

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

Publish a rewritten branch within the agreement under [P.reviewer-tasks](collaboration.md#p.reviewer-tasks) or the maintainer's final-cleanup permission under [P.final-cleanup](#p.final-cleanup). Use a lease against the remote tip you reviewed so another contributor's intervening push prevents replacement. For an example branch named `topic`, capture the tip before rewriting.

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
