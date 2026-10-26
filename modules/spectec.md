# SpecTec

## SpecTec compiler layout

<a id="r.compiler-layout"></a>**[R.compiler-layout](#r.compiler-layout). Place compiler code according to its responsibility.**

*Default. Principle [Coherence](../PRINCIPLES.md#coherence).*

| Responsibility | Location |
| --- | --- |
| Semantic operations usable without command-line handling | `spectec/lib/` |
| Shared argument parsing and command coordination | `spectec/lib/cli/` |
| Executable startup and handoff to the CLI | `spectec/bin/` |

Keep semantic logic out of executable entrypoints so other callers can use it without starting the CLI.

## Specification commits

<a id="r.commit-format.specifications"></a>**[R.commit-format.specifications](#r.commit-format.specifications). Use `spec` or `spec/<target>` scopes for specification work, such as `fix(spec/deneb): correct blob validation`.**

Specification messages should distinguish changes in modeled behavior from changes in notation or organization. A change in modeled behavior is a `fix` or `feat`. A change in notation or organization is a `refactor` or `reorg`. [R.evidence](../1-functionality.md#r.evidence) gives the evidence each type needs.

Other scopes name compiler areas, such as `converter`, `cli`, `elaborate`, `il`, `interp`, `instrumentation`, or `targets/p4`.

The `spec` commit type is deprecated. Historical `spec` commits denote specification changes. Do not rewrite existing history solely to replace the deprecated type.

## SpecTec build and checks

Run commands from the repository root after following the [README setup instructions](https://github.com/kaist-plrg/consensus-spectec/blob/7ba5f4eb3031d2ace5ad3419d42efe7d1b5be944/README.md#installation). The [Makefile](https://github.com/kaist-plrg/consensus-spectec/blob/7ba5f4eb3031d2ace5ad3419d42efe7d1b5be944/Makefile) defines the available targets. It selects an opam switch through `SWITCH`, which can be overridden for the environment being used.

| Command | Purpose |
| --- | --- |
| `make fmt` | Format OCaml with ocamlformat 0.27.0, pinned in [spectec/.ocamlformat](https://github.com/kaist-plrg/consensus-spectec/blob/7ba5f4eb3031d2ace5ad3419d42efe7d1b5be944/spectec/.ocamlformat). Use to format OCaml changes before committing. |
| `make fmt-check` | Check OCaml formatting without applying edits. |
| `make check` | Type-check libraries and executables without building the final executable. |
| `make exe` | Build the executable with the release profile. |
| `make test-quick` | Run the fast test groups, including package ownership and plugin discovery. |
| `make test` | Run the broader compiler and interpreter tests. |
| `make promote` | Accept generated test expectations after running the affected tests and reviewing their output. |

Install the formatter with `opam install ocamlformat.0.27.0` in the selected switch if needed. Override `SWITCH` when the local switch has a different name from the Makefile default. Check the Makefile for narrower test targets when a change affects only one component.

Use component documentation for other tools, including [converter usage](https://github.com/kaist-plrg/consensus-spectec/blob/7ba5f4eb3031d2ace5ad3419d42efe7d1b5be944/Converter/README.md) and [editor setup](https://github.com/kaist-plrg/consensus-spectec/blob/7ba5f4eb3031d2ace5ad3419d42efe7d1b5be944/editors/README.md). Converter checks and external-client integration have different prerequisites and coverage.

When `.expected` files conflict, resolve the source changes first, run the affected tests to produce current output, then promote and inspect the expectations. `make promote` accepts available output. It does not run the tests that generate it. Rerun the affected tests after promotion.
