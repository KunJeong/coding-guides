# OCaml

<a id="c.ocaml"></a>

**[C.ocaml](#c.ocaml). OCaml conventions**

*Default. Principles [Coherence](../PRINCIPLES.md#coherence), [Proportionality](../PRINCIPLES.md#proportionality).*

- <a id="c.ocaml.casing"></a>**[C.ocaml.casing](#c.ocaml.casing). Follow OCaml's casing conventions.** Use `snake_case` for values and types and `PascalCase` for modules and constructors.

- <a id="c.ocaml.callback-wrappers"></a>**[C.ocaml.callback-wrappers](#c.ocaml.callback-wrappers). Reserve `with_*` for scoped callback execution.** Restore the context or release the resource when the callback exits.

- <a id="c.ocaml.accumulators"></a>**[C.ocaml.accumulators](#c.ocaml.accumulators). Prefer accumulator-first parameter order for accumulator updates.** Follow `fold_left`.

- <a id="c.ocaml.application"></a>**[C.ocaml.application](#c.ocaml.application). Use `@@` only when it clearly reduces indentation around a single callback body.**

- <a id="c.ocaml.library-apis"></a>**[C.ocaml.library-apis](#c.ocaml.library-apis). Prefer established library operations when their semantics fit.** Avoid wrappers solely for naming. Evaluate migrations by simpler callers and reduced custom code. Preserve duplicate handling, failures, ordering, and equality and hashing semantics. Measure performance claims.

Prefer direct code when handling exceptions.
