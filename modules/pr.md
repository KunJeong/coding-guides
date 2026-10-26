# PR titles and descriptions

<a id="r.pr-explanations"></a>

**[R.pr-explanations](#r.pr-explanations). Each PR body should explain its motivation, result, and scope.**

*Required. Principles [Motivation](../PRINCIPLES.md#motivation), [Coherence](../PRINCIPLES.md#coherence), [Verification](../PRINCIPLES.md#verification), [Proportionality](../PRINCIPLES.md#proportionality).*

The PR body should give reviewers enough context to assess the contribution as a whole. It explains the problem or research goal, the resulting change, and the affected components and kinds of change. One short description may cover all three.

The PR body should identify commits outside the main topic and explain their inclusion. Section formats are described in [R.pr-titles](#r.pr-titles) and [R.pr-body](#r.pr-body).

Choose a title that identifies the main concept. When several changes form one idea, name that idea. Account for accompanying work in the body under [R.pr-explanations](#r.pr-explanations). Concrete titles are easier to understand than abstract labels whose meaning depends on the body.

<a id="r.pr-titles"></a>**[R.pr-titles](#r.pr-titles). Match the PR title form to its category.**

*Default. Rule [R.pr-explanations](#r.pr-explanations).*

| Type | Title form |
| --- | --- |
| Refactor | `Refactor <concept>` |
| Feature | A concept-led title without a fixed prefix |
| Port | Use the title form of the feature, fix, test, refactor, or reorg being ported |
| Sync | `Sync <area>` |
| Reorg | `Reorg <concept>` |

A Port names the work being adopted. A Sync names the area being brought to a reference state because it can combine several kinds of change. Other PR categories use a concept-led title describing the change.

<a id="r.pr-body"></a>

**[R.pr-body](#r.pr-body). PR sections**

*Default. Rules [R.change-scope](../4-history.md#r.change-scope), [R.pr-explanations](#r.pr-explanations), [R.follow-ups](collaboration.md#r.follow-ups), [R.responsibility](collaboration.md#r.responsibility).*

<a id="r.pr-body.sections"></a>**[R.pr-body.sections](#r.pr-body.sections). Add sections when they answer additional review questions.** Use the standard headings for the purposes defined below. Give additional sections headings that describe their content. Omit sections that repeat information already covered elsewhere.

<a id="r.pr-body.plan"></a>**[R.pr-body.plan](#r.pr-body.plan). Draft the PR body as the plan for the branch.** Write the draft in the final format before the branch is final. Start with the Motivation, the Core Concepts, the planned Scope, and the checks Validation will report. Change the draft as the commits change. A commit outside the draft's Scope belongs in Minor Changes or in another PR. A Scope bullet with no commit marks unfinished or dropped work. Keep the draft in a file until the PR opens, in a location each repository chooses.

<a id="r.pr-body.motivation"></a>**[R.pr-body.motivation](#r.pr-body.motivation). Start PR bodies with a Motivation section.** Use `## Motivation` and explain the problem or research goal.

<a id="r.pr-body.concepts"></a>**[R.pr-body.concepts](#r.pr-body.concepts). Explain the central idea under Core Concepts.** Core Concepts covers what a reviewer must understand before reading the diff. Omit it when the Motivation already says this. Under `## Core Concepts`, use `### <concept>` headings for explanations with paragraphs or code examples. Use bolded bullets only when each concept fits compactly in one bullet. Explain how the concepts fit together when their relationship is not already clear.

The heading format appears in [SpecTecX #100](https://github.com/kaist-plrg/spectecx/pull/100) and [consensus-spectec #12](https://github.com/kaist-plrg/consensus-spectec/pull/12). Compact bolded bullets appear in [SpecTecX #88](https://github.com/kaist-plrg/spectecx/pull/88) and [consensus-spectec #20](https://github.com/kaist-plrg/consensus-spectec/pull/20).

<a id="r.pr-body.scope"></a>**[R.pr-body.scope](#r.pr-body.scope). List everything the change affects under Scope.** Scope covers the full extent of the change, including effects outside the central idea, such as updated callers, moved files, and added tests. Omit it when the change affects only the area its title names. Group changes by affected area and theme. A single bullet can summarize several commits. Use `## Minor Changes` for incidental work outside the main topic, and say why it is included.

In both sections, use `**type(scope):** Description.` for summary bullets. Choose types and scopes under [R.commit-format](../4-history.md#r.commit-format), capitalize descriptions, and end sentences with periods. Describe related work as a whole instead of repeating individual commit subjects. Split a bullet when no single type and scope accurately describes the work. Rename lists under a summary follow [R.commit-format.moves](../4-history.md#r.commit-format.moves). Use the same format within [Port and Sync scope groups](ports.md#r.ports-syncs). When these lists are present, their shared format lets the merge summary reuse the reviewed bullets without reclassifying or regrouping the work.

```markdown
## Scope

- **fix(lsp):** Checks unsaved specification files together and reports diagnostics using the editor's negotiated position encoding.

## Minor Changes

- **docs(readme):** Clarifies compiler setup instructions.
```

<a id="r.pr-body.validation"></a>**[R.pr-body.validation](#r.pr-body.validation). Under Validation, give the evidence that the diff, the Scope section, and CI do not show.** Report the measurements and other checks that [R.evidence](../1-functionality.md#r.evidence) asks for, taken on the final branch. State what was not checked. Leave out CI status, which the PR page shows, and added tests, which Scope lists. Omit the section when nothing remains.

<a id="r.pr-body.commit-log"></a>**[R.pr-body.commit-log](#r.pr-body.commit-log). End multi-commit PR bodies with `## Commit Log` for GitHub searchability.** List final commit subjects verbatim and in order, including their `type(scope):` prefixes. Do not add backticks or hyperlinks around them. Preserve any literal characters already in a subject and keep the list synchronized with the final history.

<a id="r.pr-body.follow-ups"></a>**[R.pr-body.follow-ups](#r.pr-body.follow-ups). Separate deferred tasks from ideas and open questions under Future Work.** Use `## Future Work` when the PR has follow-ups to record. Include only subsections with content.

Under `### Deferred Tasks`, identify specific work deliberately postponed from this contribution and explain why it was postponed. These tasks are expected to be completed later and carried into the merge message under [R.deferred-work](landing.md#r.deferred-work).

Under `### Ideas and Open Questions`, describe possible improvements or open design questions without implying a commitment to pursue them. These possibilities do not belong in the merge message's `DEFERRED:` records. Select follow-up items deliberately instead of treating every possible improvement as backlog.

<a id="r.pr-body.tool-use"></a>**[R.pr-body.tool-use](#r.pr-body.tool-use). Omit routine tool-use disclaimer sections by default.** AI use alone does not require a disclosure section. Put relevant tool details with the method, source, or limitation they explain under [R.responsibility](collaboration.md#r.responsibility).

## Opening a PR

Drafting the body in a file preserves its formatting when opening a PR.

```bash
gh pr create --title "Refactor <concept>" --body-file pr-body.md
```
