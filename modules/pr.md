# PR titles and descriptions

<a id="p.pr-explanations"></a>

**[P.pr-explanations](#p.pr-explanations). Each PR body should explain its motivation, result, and scope.**

*Requirement. [Motivation](../PRINCIPLES.md#motivation), [Coherence](../PRINCIPLES.md#coherence), [Verification](../PRINCIPLES.md#verification), [Proportionality](../PRINCIPLES.md#proportionality)*

One short description may cover all three.

The PR body should give reviewers enough context to assess the contribution as a whole. It explains the problem or research goal, the resulting change, and the affected components and kinds of change. One short description may cover all three.

The PR body should identify commits outside the main topic and explain their inclusion. Section formats are described in [C.pr-titles](#c.pr-titles) and [C.pr-body](#c.pr-body).

<a id="p.follow-ups"></a>

**[P.follow-ups](#p.follow-ups). Do not delay a ready contribution for independent follow-up work.**

*Requirement. [Coherence](../PRINCIPLES.md#coherence), [Proportionality](../PRINCIPLES.md#proportionality)*

Record deliberately postponed tasks and their reasons, and preserve the record when landing. Possible improvements are not deferred commitments.

Once review blockers are resolved, the contribution can proceed towards landing. Newly discovered work belongs in another PR unless it is needed to implement or verify the current contribution. Independent follow-up work should not hold up a ready contribution or other work that depends on it.

The PR should identify work explicitly postponed from the contribution and explain why it was postponed. Preserve that record when landing. Possible future improvements are not deferred commitments.

Choose a title that identifies the main concept. When several changes form one idea, name that idea. Account for accompanying work in the body under [P.pr-explanations](#p.pr-explanations). Concrete titles are easier to understand than abstract labels whose meaning depends on the body.

<a id="c.pr-titles"></a>**[C.pr-titles](#c.pr-titles). Match the PR title form to its category.**

*Default. Policy [P.pr-explanations](#p.pr-explanations).*

| Type | Title form |
| --- | --- |
| Refactor | `Refactor <concept>` |
| Feature | A concept-led title without a fixed prefix |
| Port | Use the title form of the feature, fix, test, refactor, or reorg being ported |
| Sync | `Sync <area>` |
| Reorg | `Reorg <concept>` |

A Port names the work being adopted. A Sync names the area being brought to a reference state because it can combine several kinds of change. Other PR categories use a concept-led title describing the change.

<a id="c.pr-body"></a>

**[C.pr-body](#c.pr-body). PR sections**

*Default. Policies [P.change-scope](../4-history.md#p.change-scope), [P.pr-explanations](#p.pr-explanations), [P.follow-ups](#p.follow-ups), [P.responsibility](collaboration.md#p.responsibility).*

<a id="c.pr-body.sections"></a>**[C.pr-body.sections](#c.pr-body.sections). Add sections when they answer additional review questions.** Use the standard headings for the purposes defined below. Give additional sections headings that describe their content. Omit sections that repeat information already covered elsewhere.

<a id="c.pr-body.motivation"></a>**[C.pr-body.motivation](#c.pr-body.motivation). Start PR bodies with a Motivation section.** Use `## Motivation` and explain the problem or research goal.

<a id="c.pr-body.concepts"></a>**[C.pr-body.concepts](#c.pr-body.concepts). Use a Core Concepts section when design ideas need a separate explanation.** Under `## Core Concepts`, use `### <concept>` headings for explanations with paragraphs or code examples. Use bolded bullets only when each concept fits compactly in one bullet. Explain how the concepts fit together when their relationship is not already clear.

The heading format appears in [SpecTecX #100](https://github.com/kaist-plrg/spectecx/pull/100) and [consensus-spectec #12](https://github.com/kaist-plrg/consensus-spectec/pull/12). Compact bolded bullets appear in [SpecTecX #88](https://github.com/kaist-plrg/spectecx/pull/88) and [consensus-spectec #20](https://github.com/kaist-plrg/consensus-spectec/pull/20).

<a id="c.pr-body.scope"></a>**[C.pr-body.scope](#c.pr-body.scope). Add Scope only when the affected work needs a separate overview.** Omit `## Scope` when other sections already explain the affected areas and kinds of change. Do not add it solely to supply merge-message bullets. When Scope is useful, group changes by affected area and theme. A single bullet can summarize several commits. Use `## Minor Changes` for incidental work outside the main theme.

In both sections, use `**type(scope):** Description.` for summary bullets. Choose types and scopes under [C.commit-format](../4-history.md#c.commit-format), capitalize descriptions, and end sentences with periods. Describe related work as a whole instead of repeating individual commit subjects. Split a bullet when no single type and scope accurately describes the work. Rename lists under a summary follow [C.commit-format.moves](../4-history.md#c.commit-format.moves). Use the same format within [Port and Sync scope groups](ports.md#c.ports-syncs). When these lists are present, their shared format lets the merge summary reuse the reviewed bullets without reclassifying or regrouping the work.

```markdown
## Scope

- **fix(lsp):** Checks unsaved specification files together and reports diagnostics using the editor's negotiated position encoding.

## Minor Changes

- **docs(readme):** Clarifies compiler setup instructions.
```

<a id="c.pr-body.commit-log"></a>**[C.pr-body.commit-log](#c.pr-body.commit-log). End multi-commit PR bodies with `## Commit Log` for GitHub searchability.** List final commit subjects verbatim and in order, including their `type(scope):` prefixes. Do not add backticks or hyperlinks around them. Preserve any literal characters already in a subject and keep the list synchronized with the final history.

<a id="c.pr-body.follow-ups"></a>**[C.pr-body.follow-ups](#c.pr-body.follow-ups). Separate deferred tasks from ideas and open questions under Future Work.** Use `## Future Work` when the PR has follow-ups to record. Include only subsections with content.

Under `### Deferred Tasks`, identify specific work deliberately postponed from this contribution and explain why it was postponed. These tasks are expected to be completed later and carried into the merge message under [C.deferred-work](landing.md#c.deferred-work).

Under `### Ideas and Open Questions`, describe possible improvements or open design questions without implying a commitment to pursue them. These possibilities do not belong in the merge message's `DEFERRED:` records. Select follow-up items deliberately instead of treating every possible improvement as backlog.

<a id="c.pr-body.tool-use"></a>**[C.pr-body.tool-use](#c.pr-body.tool-use). Omit routine tool-use disclaimer sections by default.** AI use alone does not require a disclosure section. Put relevant tool details with the method, source, or limitation they explain under [P.responsibility](collaboration.md#p.responsibility).

## Opening a PR

Drafting the body in a file preserves its formatting when opening a PR.

```bash
gh pr create --title "Refactor <concept>" --body-file pr-body.md
```
