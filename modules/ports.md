# Ports and Syncs

## Checklist

**Each Port or Sync body**

- Does Motivation link the source and say why the work is needed here? [R.ports-syncs.explanations](#r.ports-syncs.explanations)
- For a Port, does the PR stay within one upstream PR and the local work it needs? [R.ports-syncs.scope](#r.ports-syncs.scope)
- Does Core Concepts cover only what the source leaves unexplained? [R.ports-syncs.explanations](#r.ports-syncs.explanations)
- Does every upstream change appear under Ported, Adapted, or Omitted, with a reason for each omission? [R.imported-work](#r.imported-work), [R.ports-syncs.groups](#r.ports-syncs.groups)
- Does each Local bullet say why the Port or Sync needs it? [R.imported-work](#r.imported-work)
- Does Validation compare the result with its source? [R.ports-syncs.groups](#r.ports-syncs.groups), [R.pr-body.validation](pr.md#r.pr-body.validation)

<a id="r.imported-work"></a>**[R.imported-work](#r.imported-work). Distinguish imported work from local changes and explain omissions.**

*Required. Principles [Coherence](../PRINCIPLES.md#coherence), [Provenance](../PRINCIPLES.md#provenance), [Proportionality](../PRINCIPLES.md#proportionality).*

Reviewers need to compare the source work with the local result. Identify the sources and explain adaptations, omissions, and independent local changes, including conflict resolutions. The [Port and Sync rules](#r.ports-syncs) recommend description groups and explain when upstream explanations can be reused.

<a id="r.ports-syncs"></a>**[R.ports-syncs](#r.ports-syncs). Upstream scope groups**

*Default. Rules [R.change-scope](../4-history.md#r.change-scope), [R.imported-work](#r.imported-work), [R.source-credit](../4-history.md#r.source-credit), [R.pr-explanations](pr.md#r.pr-explanations).*

<a id="r.ports-syncs.scope"></a>**[R.ports-syncs.scope](#r.ports-syncs.scope). Limit each Port to one upstream PR and the local work it needs.** This applies [R.change-scope](../4-history.md#r.change-scope) to Ports, so reviewers can compare the original work with the local result. Independent local changes belong in another PR. A Sync may cover broader upstream changes and related local work.

<a id="r.ports-syncs.explanations"></a>**[R.ports-syncs.explanations](#r.ports-syncs.explanations). Reuse upstream explanations only when they cover the adopted design and its local assumptions.** Ports link their upstream PR in Motivation. Syncs link the comparison range or reference state being adopted.

The local PR should summarize why the work is needed here and what result it brings. Link sufficient upstream explanations instead of repeating them. Explain any missing reasoning or local design differences in the local PR.

<a id="r.ports-syncs.groups"></a>**[R.ports-syncs.groups](#r.ports-syncs.groups). Use `Ported`, `Adapted`, `Omitted`, and `Local` as the subsections of Scope.** Use `###` headings within `## Scope`. Include the applicable groups and omit empty ones.

```markdown
## Scope

### Ported

- **type(scope):** Upstream work taken nearly directly. Original: org/repo@sha

### Adapted

- **type(scope):** Upstream work adjusted for the local context, including conflict resolutions.

### Omitted

- **type(scope):** Upstream work not taken, and why.

### Local

- **type(scope):** Local work the Port or Sync needs, and why.
```

Validation compares the result with its source, such as upstream tests that now pass locally or reference suites that pass after a Sync.

An omission does not by itself promise later adoption. Include it under Deferred Tasks only when its later adoption has been explicitly deferred.

<a id="r.ports-syncs.references"></a>**[R.ports-syncs.references](#r.ports-syncs.references). Use GitHub source references in upstream scope groups.** Identify origins, for example `Original: org/repo@sha`, or link a comparison range or reference file for a Sync.

## Port attribution

<a id="r.sources.port-attribution"></a>**[R.sources.port-attribution](#r.sources.port-attribution). Give `Ported from <project>.` its own paragraph in a port commit.** Place it after the solution and before the source records. Name the actual source project. Explain local adaptations in the solution, separately from this attribution paragraph.

```text
Ported from P4-SpecTec.

Original-commit: https://github.com/kaist-plrg/p4-spectec/commit/<12-character-sha>
```

## Merge summaries

<a id="r.merge-summary.imports"></a>**[R.merge-summary.imports](#r.merge-summary.imports). Use a single bullet list with source labels for Port and Sync merge summaries.** Label bullets `PORTED:`, `ADAPTED:`, `OMITTED:`, or `LOCAL:`. Follow the PR's distinctions under [R.ports-syncs](#r.ports-syncs), with `LOCAL:` corresponding to its Local subsection. Include only applicable labels.

Group related work into concise bullets under [R.merge-summary.reuse](landing.md#r.merge-summary.reuse). Explain adaptations and reasons for omissions. Repeat a label when distinct changes need separate bullets. Use the source label and its colon as the only prefix. Source references may use an `Original: <ref>` suffix when they add useful context.
