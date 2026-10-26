# Ports and Syncs

<a id="p.imported-work"></a>

**[P.imported-work](#p.imported-work). Distinguish imported work from local changes and explain omissions.**

*Requirement. [Coherence](../PRINCIPLES.md#coherence), [Provenance](../PRINCIPLES.md#provenance), [Proportionality](../PRINCIPLES.md#proportionality)*

Identify the sources and explain adaptations and conflict resolutions.

Reviewers need to compare the source work with the local result. Identify the sources and explain adaptations, omissions, and independent local changes, including conflict resolutions. The [Port and Sync conventions](#ports-and-syncs) recommend description groups and explain when upstream explanations can be reused.

<a id="c.ports-syncs"></a>

**[C.ports-syncs](#c.ports-syncs). Upstream scope groups**

*Default. Policies [P.change-scope](../4-history.md#p.change-scope), [P.imported-work](#p.imported-work), [P.source-credit](../4-history.md#p.source-credit), [P.pr-explanations](pr.md#p.pr-explanations).*

<a id="c.ports-syncs.scope"></a>**[C.ports-syncs.scope](#c.ports-syncs.scope). Limit each Port to one upstream PR and its necessary local adaptations.** This restates [P.change-scope](../4-history.md#p.change-scope) so reviewers can compare the original work with the local result. Independent local changes belong in another PR. A Sync may cover broader upstream changes and related local work.

<a id="c.ports-syncs.explanations"></a>**[C.ports-syncs.explanations](#c.ports-syncs.explanations). Reuse upstream explanations only when they cover the adopted design and its local assumptions.** Ports link their upstream PR in Motivation. Syncs link the comparison range or reference state being adopted.

The local PR should summarize why the work is needed here and what result it brings. Link sufficient upstream explanations instead of repeating them. Explain any missing reasoning or local design differences in the local PR.

<a id="c.ports-syncs.groups"></a>**[C.ports-syncs.groups](#c.ports-syncs.groups). Use `Ported`, `Adapted`, `Omitted`, and Sync-only `Local Changes` as upstream scope headings.** Use `###` headings within `## Scope`. Include the applicable groups and omit empty ones.

| Group | Work to describe |
| --- | --- |
| `Ported` | Upstream work taken nearly directly. |
| `Adapted` | Upstream work adjusted for the local context. |
| `Omitted` | Upstream work not taken, with the reason. |
| `Local Changes` | Related local-origin work included in a Sync. |

An omission does not by itself promise later adoption. Include it under Deferred Tasks only when its later adoption has been explicitly deferred.

<a id="c.ports-syncs.references"></a>**[C.ports-syncs.references](#c.ports-syncs.references). Use GitHub source references in upstream scope groups.** Identify origins, for example `Original: org/repo@sha`, or link a comparison range or reference file for a Sync.

## Port attribution

<a id="c.sources.port-attribution"></a>**[C.sources.port-attribution](#c.sources.port-attribution). Give `Ported from <project>.` its own paragraph in a port commit.** Place it after the solution and before the source records. Name the actual source project. Explain local adaptations in the solution, separately from this attribution paragraph.

```text
Ported from P4-SpecTec.

Original-commit: https://github.com/kaist-plrg/p4-spectec/commit/<12-character-sha>
```

## Merge summaries

<a id="c.merge-summary.imports"></a>**[C.merge-summary.imports](#c.merge-summary.imports). Use a single bullet list with source labels for Port and Sync merge summaries.** Label bullets `PORTED:`, `ADAPTED:`, `OMITTED:`, or Sync-only `LOCAL:`. Follow the PR's distinctions under [C.ports-syncs](#c.ports-syncs), with `LOCAL:` corresponding to its Local Changes category. Include only applicable labels.

Group related work into concise bullets under [C.merge-summary.reuse](landing.md#c.merge-summary.reuse). Explain adaptations and reasons for omissions. Repeat a label when distinct changes need separate bullets. Use the source label and its colon as the only prefix. Source references may use an `Original: <ref>` suffix when they add useful context.
