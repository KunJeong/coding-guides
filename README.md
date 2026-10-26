# Coding guides

Personal guides for coding style, technical writing, and commit and PR practices. The numbered stage files follow the order in which a change is prepared. Functionality settles first, then factoring, then prose, and then history.

| File | Covers |
| --- | --- |
| [PRINCIPLES.md](PRINCIPLES.md) | The reasons behind the guidance |
| [1-functionality.md](1-functionality.md) | Guarantees, construction, and runtime validation |
| [2-factoring.md](2-factoring.md) | Names, types, abstractions, and mutation |
| [3-prose.md](3-prose.md) | Sentences, comments, and documentation |
| [4-history.md](4-history.md) | Commit messages, source records, and commit preparation |
| [modules/ocaml.md](modules/ocaml.md) | OCaml conventions |
| [modules/pr.md](modules/pr.md) | PR titles and descriptions |
| [modules/ports.md](modules/ports.md) | Ports and Syncs of upstream work |
| [modules/landing.md](modules/landing.md) | Integration, merge messages, and landing recipes |
| [modules/collaboration.md](modules/collaboration.md) | Working with other contributors and reviewing their PRs |
| [modules/spectec.md](modules/spectec.md) | SpecTec layout, specification commits, and build commands |

## Load map

Read only the files a task needs. PRINCIPLES.md applies to every task. In SpecTec repositories, add the spectec module.

| Task | Files |
| --- | --- |
| Writing or reviewing staged code | 1, 2, and 3, plus ocaml for `.ml` or `.mli` changes |
| Writing commits or reviewing a branch | 1 to 4, plus ports when source records appear |
| Writing or checking a PR body | 4 and pr, plus ports for a Port or Sync |
| Landing a PR | 4, pr, and landing |
| Reviewing a collaborator's PR | 1 to 4, pr, collaboration, and the project's CONTRIBUTING.md, plus ocaml or ports when relevant |

## Rules and labels

Each rule has an ID, such as `P.invariants` or `C.names.helpers`. IDs name topics and stay stable when rules move or their wording changes.

Entries are defaults unless marked as requirements, permissions, or editorial preferences, or identified as restatements of a requirement. Defaults describe the usual approach and allow judgment under [P.rules](modules/collaboration.md#p.rules). Editorial preferences guide writing and final polish.

Links below a rule's title identify the requirements or principles that support it. `↔` marks a tradeoff between principles.

As a rule of thumb, document a routine choice after similar decisions have been made three times. State the choice and when it applies.

The recipes in these guides do not authorize a rewrite or publication by themselves.

## Source

The collection comes from the contribution-guide revision discussed in [consensus-spectec #29](https://github.com/kaist-plrg/consensus-spectec/pull/29), at [revision 7ba5f4eb3031](https://github.com/kaist-plrg/consensus-spectec/commit/7ba5f4eb3031d2ace5ad3419d42efe7d1b5be944). Links to SpecTec repository files use that revision so they can be read outside a checkout.
