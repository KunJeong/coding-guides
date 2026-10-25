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
| [Functionality](CONVENTIONS.md#functionality) | Guarantees and validation | [Invariants policy](POLICIES.md#p.invariants), [construction](CONVENTIONS.md#contracts-and-invariants), [runtime validation](CONVENTIONS.md#runtime-validation) |
| [Factoring](CONVENTIONS.md#factoring) | Names and renames | [Names and boundaries](CONVENTIONS.md#names-and-boundaries), [compatibility aliases](POLICIES.md#p.renames) |
| Factoring | Types and representation | [Types and data](CONVENTIONS.md#types-and-data) |
| Factoring | Architecture and state | [Abstractions and interfaces](CONVENTIONS.md#abstractions-and-interfaces), [mutation](CONVENTIONS.md#mutation) |
| Factoring | Language and layout | [OCaml](CONVENTIONS.md#ocaml), [SpecTec compiler layout](CONVENTIONS.md#c.compiler-layout) |
| [Prose](CONVENTIONS.md#prose) | Wording across media | [General writing](CONVENTIONS.md#general-writing) |
| Prose | Comments and docstrings | [Comments](CONVENTIONS.md#comments), [documentation policy](POLICIES.md#p.documentation) |
| Prose | Documentation and presentation | [Documentation](CONVENTIONS.md#documentation), [build and checking documentation](CONVENTIONS.md#build-and-checking-documentation) |
| [Change records](CONVENTIONS.md#change-records) | Commit messages | [Commit conventions](CONVENTIONS.md#commit-messages), [explanation policy](POLICIES.md#p.commit-explanations) |
| Change records | Sources and attribution | [Source records](CONVENTIONS.md#sources-and-credit), [credit policy](POLICIES.md#p.source-credit), [imported work](POLICIES.md#p.imported-work) |
| Change records | PR scope and descriptions | [PR conventions](CONVENTIONS.md#pr-titles-and-descriptions), [Ports and Syncs](CONVENTIONS.md#ports-and-syncs), [scope policy](POLICIES.md#p.change-scope), [explanation policy](POLICIES.md#p.pr-explanations) |
| Change records | Review and landing | [Review comments](CONVENTIONS.md#review), [integration and landing records](CONVENTIONS.md#landing), [review blockers](POLICIES.md#p.review-blockers) |

[POLICIES.md](POLICIES.md#policy-outline) groups collaboration rules by workflow. [WORKFLOWS.md](WORKFLOWS.md) supplies build, revision, and landing procedures.

## Source

The collection comes from the contribution-guide revision discussed in [consensus-spectec #29](https://github.com/kaist-plrg/consensus-spectec/pull/29), at [revision 7ba5f4eb3031](https://github.com/kaist-plrg/consensus-spectec/commit/7ba5f4eb3031d2ace5ad3419d42efe7d1b5be944). Links to repository files use that revision so the workflow reference can be read outside a checkout.
