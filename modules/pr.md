# PR titles and descriptions

## Checklist

**Each PR body**

- Does Motivation state the problem or research goal without describing the result? [R.pr-body.motivation](#r.pr-body.motivation)
- Does Solution state what the PR makes true? [R.pr-body.solution](#r.pr-body.solution)
- Does Core Concepts explain the central idea a reviewer needs before reading the diff? [R.pr-body.concepts](#r.pr-body.concepts)
- Does Solution account for every commit, in its prose or in a Scope or Minor Changes bullet? [R.pr-body.scope](#r.pr-body.scope), [R.change-scope](../4-history.md#r.change-scope)
- Does every Scope bullet describe work the branch contains? [R.pr-body.scope](#r.pr-body.scope)
- Does Validation hold only evidence that the diff, Solution, and CI do not show, including what was not checked? [R.pr-body.validation](#r.pr-body.validation)
- Does every sentence follow the prose rules? [R.prose](../3-prose.md#r.prose)
- Does the body match the [PR form](#pr-form)?

<a id="r.pr-explanations"></a>**[R.pr-explanations](#r.pr-explanations). Each PR body should explain its motivation, result, and scope.**

*Principles [Motivation](../PRINCIPLES.md#motivation), [Coherence](../PRINCIPLES.md#coherence), [Verification](../PRINCIPLES.md#verification), [Proportionality](../PRINCIPLES.md#proportionality).*

The PR body should give reviewers enough context to assess the contribution as a whole. Motivation explains the problem or research goal. Solution explains the resulting change, the components it affects, and the kinds of change. In a small PR, each section can be one short paragraph.

The PR body should identify commits outside the main topic and explain their inclusion. Section formats are described in [R.pr-titles](#r.pr-titles) and [R.pr-body](#r.pr-body).

Choose a title that identifies the main concept. When several changes form one idea, name that idea. Account for accompanying work in the body under [R.pr-explanations](#r.pr-explanations). Concrete titles are easier to understand than abstract labels whose meaning depends on the body.

<a id="r.pr-titles"></a>**[R.pr-titles](#r.pr-titles). Match the PR title form to its category.**

| Type | Title form |
| --- | --- |
| Refactor | `Refactor <concept>` |
| Feature | A concept-led title without a fixed prefix |
| Port | Use the title form of the feature, fix, test, refactor, or reorg being ported |
| Sync | `Sync <area>` |
| Reorg | `Reorg <concept>` |

A Port names the work being adopted. A Sync names the area being brought to a reference state because it can combine several kinds of change. Other PR categories use a concept-led title describing the change.

## PR form

```markdown
## Motivation

The problem or research goal.

## Solution

What the PR makes true.

### Core Concepts

#### <concept>

The central idea a reviewer needs before reading the diff.

### Scope

- **type(scope):** What the change affects, grouped by area.

### Minor Changes

- **type(scope):** Incidental work, and why it is included.

## Validation

- Evidence the diff, Scope, and CI do not show, and what was not checked.

## Future Work

### Deferred Tasks

### Ideas and Open Questions

## Commit Log

- type(scope): subject
```

Sections appear in this order. Motivation and Solution are required. Other sections and subsections are omitted when empty. A Port or Sync divides Scope into the subsections of [R.ports-syncs.groups](ports.md#r.ports-syncs.groups).

<a id="r.pr-body"></a>**[R.pr-body](#r.pr-body). PR sections**

<a id="r.pr-body.sections"></a>**[R.pr-body.sections](#r.pr-body.sections). Add sections when they answer additional review questions.** Use the standard headings for the purposes defined below. Give additional sections headings that describe their content. Omit sections that repeat information already covered elsewhere.

<a id="r.pr-body.plan"></a>**[R.pr-body.plan](#r.pr-body.plan). Draft the PR body as the plan for the branch.** Write the draft in the final format before the branch is final. Start with the Motivation, the planned Solution, and the checks Validation will report. Change the draft as the commits change. A commit outside the draft's Solution belongs in Minor Changes or in another PR. Planned work in the Solution with no commit marks unfinished or dropped work. Keep the draft in a file until the PR opens, in a location each repository chooses.

<a id="r.pr-body.motivation"></a>**[R.pr-body.motivation](#r.pr-body.motivation). Start PR bodies with a Motivation section.** Use `## Motivation` and explain the problem or research goal. Leave the resulting change to Solution.

<a id="r.pr-body.solution"></a>**[R.pr-body.solution](#r.pr-body.solution). Follow Motivation with a Solution section.** Use `## Solution` and describe in prose what the PR makes true. Core Concepts, Scope, and Minor Changes are its subsections, under the rules below. A single-commit PR can reuse its commit message, with the motivation paragraph under Motivation and the solution paragraph under Solution.

<a id="r.pr-body.concepts"></a>**[R.pr-body.concepts](#r.pr-body.concepts). Explain the central idea under Core Concepts.** Core Concepts covers what a reviewer must understand before reading the diff. Omit it when the Solution prose already says this. Under `### Core Concepts`, use `#### <concept>` headings for explanations with paragraphs or code examples. Use bolded bullets only when each concept fits compactly in one bullet. Explain how the concepts fit together when their relationship is not already clear.

The heading format appears in [SpecTecX #100](https://github.com/kaist-plrg/spectecx/pull/100) and [consensus-spectec #12](https://github.com/kaist-plrg/consensus-spectec/pull/12). Compact bolded bullets appear in [SpecTecX #88](https://github.com/kaist-plrg/spectecx/pull/88) and [consensus-spectec #20](https://github.com/kaist-plrg/consensus-spectec/pull/20). Those PRs place their headings one level higher than this form does.

<a id="r.pr-body.scope"></a>**[R.pr-body.scope](#r.pr-body.scope). List everything the change affects under Scope.** Scope covers the full extent of the change, including effects outside the central idea, such as updated callers, moved files, and added tests. Omit it when the Solution prose already names every affected area. Group changes by affected area and theme. A single bullet can summarize several commits. Use `### Minor Changes` for incidental work outside the main topic, and say why it is included.

In both sections, use `**type(scope):** Description.` for summary bullets. Choose types and scopes under [R.commit-format](../4-history.md#r.commit-format), capitalize descriptions, and end sentences with periods. Describe related work as a whole instead of repeating individual commit subjects. Split a bullet when no single type and scope accurately describes the work. Rename lists under a summary follow [R.commit-format.moves](../4-history.md#r.commit-format.moves). Use the same format within [Port and Sync scope groups](ports.md#r.ports-syncs). When these lists are present, their shared format lets the merge summary reuse the reviewed bullets without reclassifying or regrouping the work.

```markdown
### Scope

- **fix(lsp):** Checks unsaved specification files together and reports diagnostics using the editor's negotiated position encoding.

### Minor Changes

- **docs(readme):** Clarifies compiler setup instructions.
```

<a id="r.pr-body.validation"></a>**[R.pr-body.validation](#r.pr-body.validation). Under Validation, give the evidence that the diff, the Solution section, and CI do not show.** Report the measurements and other checks that [R.evidence](../1-functionality.md#r.evidence) asks for, taken on the final branch. State what was not checked. Leave out CI status, which the PR page shows, and added tests, which Solution lists. Omit the section when nothing remains.

<a id="r.pr-body.commit-log"></a>**[R.pr-body.commit-log](#r.pr-body.commit-log). End multi-commit PR bodies with `## Commit Log` for GitHub searchability.** List final commit subjects verbatim and in order, including their `type(scope):` prefixes. Do not add backticks or hyperlinks around them. Preserve any literal characters already in a subject and keep the list synchronized with the final history.

<a id="r.pr-body.follow-ups"></a>**[R.pr-body.follow-ups](#r.pr-body.follow-ups). Separate deferred tasks from ideas and open questions under Future Work.** Use `## Future Work` when the PR has follow-ups to record. Include only subsections with content.

Under `### Deferred Tasks`, identify specific work deliberately postponed from this contribution and explain why it was postponed. These tasks are expected to be completed later and carried into the merge message under [R.deferred-work](landing.md#r.deferred-work).

Under `### Ideas and Open Questions`, describe possible improvements or open design questions without implying a commitment to pursue them. These possibilities do not belong in the merge message's `DEFERRED:` records. Select follow-up items deliberately instead of treating every possible improvement as backlog.

<a id="r.pr-body.tool-use"></a>**[R.pr-body.tool-use](#r.pr-body.tool-use). Omit routine tool-use disclaimer sections by default.** AI use alone does not require a disclosure section. Put relevant tool details with the method, source, or limitation they explain.

## Opening a PR

Drafting the body in a file preserves its formatting when opening a PR.

```bash
gh pr create --title "Refactor <concept>" --body-file pr-body.md
```
