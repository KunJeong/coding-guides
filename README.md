# Coding guides

Personal guides for coding style, technical writing, and commit and PR practices. Consult the document relevant to the task. Repository rules and explicit agreements take precedence.

- [Principles](PRINCIPLES.md) explain the reasoning behind the guidance, drawn from research and contribution practices.
- [Policies](POLICIES.md) describe proposed collaboration rules derived from SpecTec. They apply where a project adopts them.
- [Conventions](CONVENTIONS.md) organize guidance by functionality, factoring, prose, and change records.
- [Workflow recipes](WORKFLOWS.md) provide Git and GitHub procedures and SpecTec build commands.

OCaml conventions apply to OCaml code. SpecTec compiler paths and build commands apply to SpecTec repositories. The collaboration policies do not establish agreements or grant permission to change another contributor's work.

## Topic index

Start with [PRINCIPLES.md](PRINCIPLES.md) for the reasoning behind the guidance. Use the topics below to locate the applicable conventions and policies. Read each linked section with its exceptions and supporting policies.

| Facet | Topic | Guidance |
| --- | --- | --- |
| [Functionality](1-functionality.md#functionality) | Guarantees and validation | [Invariants policy](1-functionality.md#p.invariants), [construction](1-functionality.md#contracts-and-invariants), [runtime validation](1-functionality.md#runtime-validation) |
| [Factoring](2-factoring.md#factoring) | Names and renames | [Names and boundaries](2-factoring.md#names-and-boundaries), [compatibility aliases](modules/collaboration.md#p.renames) |
| Factoring | Types and representation | [Types and data](2-factoring.md#types-and-data) |
| Factoring | Architecture and state | [Abstractions and interfaces](2-factoring.md#abstractions-and-interfaces), [mutation](2-factoring.md#mutation) |
| Factoring | Language and layout | [OCaml](modules/ocaml.md#ocaml), [SpecTec compiler layout](modules/spectec.md#c.compiler-layout) |
| [Prose](3-prose.md#prose) | Wording across media | [General writing](3-prose.md#general-writing) |
| Prose | Comments and docstrings | [Comments](3-prose.md#comments), [documentation policy](3-prose.md#p.documentation) |
| Prose | Documentation and presentation | [Documentation](3-prose.md#documentation), [build and checking documentation](3-prose.md#build-and-checking-documentation) |
| [Change records](4-history.md#change-records) | Commit messages | [Commit conventions](4-history.md#commit-messages), [explanation policy](4-history.md#p.commit-explanations), [wrapping policy](4-history.md#p.commit-wrapping) |
| Change records | Sources and attribution | [Source records](4-history.md#sources-and-credit), [credit policy](4-history.md#p.source-credit), [imported work](modules/ports.md#p.imported-work) |
| Change records | PR scope and descriptions | [PR conventions](modules/pr.md#pr-titles-and-descriptions), [Ports and Syncs](modules/ports.md#ports-and-syncs), [scope policy](4-history.md#p.change-scope), [explanation policy](modules/pr.md#p.pr-explanations) |
| Change records | Review and landing | [Review comments](modules/collaboration.md#review), [integration and landing records](modules/landing.md#landing), [review blockers](modules/collaboration.md#p.review-blockers) |

[POLICIES.md](POLICIES.md#policy-outline) groups collaboration rules by workflow. [WORKFLOWS.md](WORKFLOWS.md) supplies build, revision, and landing procedures.

## Source

The collection comes from the contribution-guide revision discussed in [consensus-spectec #29](https://github.com/kaist-plrg/consensus-spectec/pull/29), at [revision 7ba5f4eb3031](https://github.com/kaist-plrg/consensus-spectec/commit/7ba5f4eb3031d2ace5ad3419d42efe7d1b5be944). Links to repository files use that revision so the workflow reference can be read outside a checkout.
