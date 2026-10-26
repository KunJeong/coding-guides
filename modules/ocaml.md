# OCaml

<a id="r.ocaml"></a>**[R.ocaml](#r.ocaml). OCaml conventions**

*Default. Principles [Coherence](../PRINCIPLES.md#coherence), [Proportionality](../PRINCIPLES.md#proportionality).*

<a id="r.ocaml.casing"></a>**[R.ocaml.casing](#r.ocaml.casing). Follow OCaml's casing conventions.** Use `snake_case` for values and types and `PascalCase` for modules and constructors.

<a id="r.ocaml.callback-wrappers"></a>**[R.ocaml.callback-wrappers](#r.ocaml.callback-wrappers). Reserve `with_*` for scoped callback execution.** Restore the context or release the resource when the callback exits.

<a id="r.ocaml.accumulators"></a>**[R.ocaml.accumulators](#r.ocaml.accumulators). Prefer accumulator-first parameter order for accumulator updates.** Follow `fold_left`.

<a id="r.ocaml.application"></a>**[R.ocaml.application](#r.ocaml.application). Use `@@` only when it clearly reduces indentation around a single callback body.**

<a id="r.ocaml.library-apis"></a>**[R.ocaml.library-apis](#r.ocaml.library-apis). Prefer established library operations when their semantics fit.** Avoid wrappers solely for naming. Evaluate migrations by simpler callers and reduced custom code. Preserve duplicate handling, failures, ordering, and equality and hashing semantics. Measure performance claims.

Prefer direct code when handling exceptions.
