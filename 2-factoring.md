# Factoring

## Checklist

**Each name**

- Does it match the name the project uses for the same concept? [R.names](#r.names)
- Is it the only name for its concept, with no alias? [R.names.renames](#r.names.renames)
- Does it say what the thing owns, computes, or holds, rather than how it works or what type it has? [R.names.modules](#r.names.modules), [R.names.functions](#r.names.functions), [R.names.parameters](#r.names.parameters), [R.names.locals](#r.names.locals), [R.names.helpers](#r.names.helpers), [R.names.type-repetition](#r.names.type-repetition)
- Does it follow the [naming patterns](#naming-patterns)?

**Each function**

- Is the primary subject positional, with every other semantic input labeled by its role? [R.names.arguments](#r.names.arguments), [R.names.labels](#r.names.labels)
- Does every input that affects the result arrive as an argument rather than from mutable global state? [R.mutation.inputs](#r.mutation.inputs)
- Does it keep computation apart from loading and saving data? [R.abstractions.io](#r.abstractions.io)

**Each abstraction**

- Does it perform an operation that its callers can name? [R.abstractions.operations](#r.abstractions.operations)
- Do current callers use it? [R.abstractions](#r.abstractions)
- Does it expose only what callers need? [R.abstractions.exposure](#r.abstractions.exposure)
- If several callers share it, do they all need the same operation and the same constraints? [R.abstractions.sharing](#r.abstractions.sharing)

**Each type**

- Does each variant carry the data it needs, without flags or optional fields that allow combinations the program cannot handle? [R.types.alternatives](#r.types.alternatives)

**Each piece of mutable state**

- Does one component own it, with a clear lifetime? [R.mutation.ownership](#r.mutation.ownership)
- Would recursion or a fold express the same control flow more clearly? [R.mutation.recursion](#r.mutation.recursion)

**Each form**

- Does it match the form the surrounding code uses for the same purpose, unless another form makes an operation, dependency, or relationship clearer? [R.established-forms](#r.established-forms)

The [Swift API Design Guidelines](https://www.swift.org/documentation/api-design-guidelines/#naming) explain naming from a caller's perspective. Robert C. Martin's [Clean Code](https://www.oreilly.com/library/view/clean-code-a/9780136083238/) includes chapters on meaningful names and functions. These are optional background reading. The rules below state this project's choices.

<a id="r.established-forms"></a>**[R.established-forms](#r.established-forms). Prefer established code and prose forms when alternatives offer no clear benefit.**

*Default. Principles [Coherence](PRINCIPLES.md#coherence), [Proportionality](PRINCIPLES.md#proportionality).*

Familiar forms let readers focus on meaning and avoid repeated decisions. When alternatives express the same idea equally clearly, follow the surrounding code or prose. Use a different form when it makes an operation, dependency, or relationship clearer.

## Names and boundaries

As general guidance, use names and interfaces to make a component's meaning and responsibility clear to its callers. Choose names from the project's vocabulary and use them consistently for the same concept. As a default, keep code that maintains the same invariant together. [R.invariants](1-functionality.md#r.invariants) requires operations to preserve the guarantees callers rely on.

As guidance, spend naming effort in proportion to how widely and how long a name is used. The default order of attention is module names, function names, labeled parameters, positional parameters, local bindings, and bindings in lambdas or match arms. Use compact names in small local scopes when the surrounding code makes their roles clear. Keep public function names and argument labels explicit, using established domain abbreviations where appropriate.

<a id="r.names"></a>**[R.names](#r.names). Names**

*Default. Principle [Coherence](PRINCIPLES.md#coherence). Rule [R.renames](modules/collaboration.md#r.renames).*

<a id="r.names.modules"></a>**[R.names.modules](#r.names.modules). Name modules for the responsibilities they own.**

<a id="r.names.functions"></a>**[R.names.functions](#r.names.functions). Name functions for operations or results.** Use verbs for actions and semantic passes, nouns for properties, and parallel names across recursive types. Keep established domain abbreviations. Omit subjects already clear from the module, as in `Value.equal`.

<a id="r.names.parameters"></a>**[R.names.parameters](#r.names.parameters). Name parameters for what callers supply.** Use role names that can be referenced clearly in the function's contract.

<a id="r.names.locals"></a>**[R.names.locals](#r.names.locals). Name local values for their roles in the computation.**

<a id="r.names.helpers"></a>**[R.names.helpers](#r.names.helpers). Name recursive helpers for what they compute or traverse.** Do not use generic names such as `aux`, `go`, or `loop` as defaults.

<a id="r.names.type-repetition"></a>**[R.names.type-repetition](#r.names.type-repetition). Avoid prefixes that only repeat a value's OCaml type.** Prefer role names such as `expected`, `remaining`, and `result`. When several values share a role, add a short, recognizable concept qualifier. For example, `td_left` and `v_left` distinguish a type definition from its value on the left side of a comparison. Use these qualifiers where they clarify the roles, without requiring a prefix for every value of a particular type.

<a id="r.names.conversions"></a>**[R.names.conversions](#r.names.conversions). Name representation conversions by their endpoints.** Use `to_destination` in the source module, `of_source` in the destination module, and `destination_of_source` elsewhere. Semantic passes keep purpose names such as `elaborate` and `annotate`.

<a id="r.names.predicates"></a>**[R.names.predicates](#r.names.predicates). Name predicates for the conditions they test.** Use `is_*`, `has_*`, or a relation such as `contains` or `equal`. Prefer `equal` consistently. Preserve distinct relations such as `equivalent`.

<a id="r.names.arguments"></a>**[R.names.arguments](#r.names.arguments). Keep one primary subject positional and label other semantic inputs by default.** The subject is the transformed value or the container being operated on. Label every input when none is primary. Preserve positional conventions for symmetric operations, arithmetic, formatter callbacks, and external protocols. Fold callbacks take the accumulator first. Check partial applications and callback uses.

<a id="r.names.labels"></a>**[R.names.labels](#r.names.labels). Label arguments by role, adding direction when needed.** Use specific role names such as `~ctx`, `~subst`, and `~pattern`. Include a preposition when it distinguishes a relationship, as in `~to_pattern`. Avoid vague labels such as `~using` when a specific role name is available. Use `~f` for an ordinary callback, `~init` for an initial accumulator, and distinct role labels for multiple callbacks.

```ocaml
subst_typ typ ~subst
bind value ~to_pattern:pattern
```

External labels may differ from local parameter names, as in `let bind value ~to_pattern:pattern = ...`.

<a id="r.names.failures"></a>**[R.names.failures](#r.names.failures). Make failure variants predictable.** Use `find_*_opt` and `as_*_opt` for absence or mismatch, with `_exn` variants that raise. Use `option` or `optional` for input constructs. Preserve domain result types and library naming conventions.

<a id="r.names.printing"></a>**[R.names.printing](#r.names.printing). Distinguish building a presentation from writing it.** Name presentation functions according to their result or destination.

| Function form | Meaning |
| --- | --- |
| `doc_of_exp exp` | Return a composable document |
| `string_of_exp exp` or `Exp.to_string exp` | Return text |
| `pp_exp fmt exp` | Write formatted text to the supplied formatter |
| `render_exp exp ~ctx` | Produce a particular presentation, such as prose |
| `print_summary summary` | Write a summary to the operation's output destination |

Apply the conversion ownership rule to document and string production. Keep the formatted representation clear from the module or function name when several presentations exist.

<a id="r.names.effects"></a>**[R.names.effects](#r.names.effects). Name persistence and event delivery by their responsibilities.** Use domain names such as checkpoint `save` and event `emit` where appropriate. Their contracts should identify the destination and effects.

<a id="r.names.construction"></a>**[R.names.construction](#r.names.construction). Use one default name for general construction.** Prefer `make` for project-owned constructors. Use `of_*` for representation conversions and `empty` for empty values. Reserve `init` for initializing existing state. Preserve library constructor names such as `Hashtbl.create`.

Check existing uses of a concept before choosing its name. Evaluate a name at its call sites as well as in its declaration. Names are part of the specification vocabulary, so misleading names can obscure semantic errors.

Rename a component once its boundary and responsibility support the new name. Public APIs should express the intended semantic model even when dependency constraints require different internal module paths. Prefer explicit organization over broad buckets such as `core` when distinct responsibilities can be named.

### Naming patterns

| Kind | Pattern | Rule |
| --- | --- | --- |
| Conversion between representations | `to_<target>` in the source module, `of_<source>` in the target module, `<target>_of_<source>` elsewhere | [R.names.conversions](#r.names.conversions) |
| Predicate | `is_*`, `has_*`, or a relation such as `equal` or `contains` | [R.names.predicates](#r.names.predicates) |
| Lookup that can fail | `find_*_opt` or `as_*_opt`, with an `_exn` variant that raises | [R.names.failures](#r.names.failures) |
| Presentation | `doc_of_*` builds a document, `string_of_*` returns text, `pp_*` writes to a formatter, `render_*` builds one particular presentation, `print_*` writes to the output | [R.names.printing](#r.names.printing) |
| Constructor | `make`, plus `of_*` for conversions and `empty` for empty values | [R.names.construction](#r.names.construction) |
| Persistence or event delivery | Domain verbs such as `save` or `emit` | [R.names.effects](#r.names.effects) |
| Callback label | `~f` for a single callback, `~init` for an initial accumulator | [R.names.labels](#r.names.labels) |
| Recursive helper | Named for what it computes, not `aux`, `go`, or `loop` `[auto]` | [R.names.helpers](#r.names.helpers) |
| Traversal | `map_*_children`, `rewrite_*_postorder`, `iter_*_preorder`, or `fold_*_preorder` | [R.traversals](#r.traversals) |

<a id="r.names.renames"></a>**[R.names.renames](#r.names.renames). Rename declarations and callers together by default.**

*Default. Principle [Coherence](PRINCIPLES.md#coherence). Rule [R.renames](modules/collaboration.md#r.renames).*

Do not retain compatibility aliases by default. Two names can suggest different meanings. When a consumer cannot migrate in the same change, record the obstacle and agree the alias’s removal under [R.renames](modules/collaboration.md#r.renames).

## Types and data

<a id="r.types"></a>**[R.types](#r.types). Type constraints**

*Default. Rule [R.invariants](1-functionality.md#r.invariants).*

Types let callers rely on constraints without checking them at every use. As guidance, make invalid states unrepresentable with the simplest type that captures the constraint.

<a id="r.types.alternatives"></a>**[R.types.alternatives](#r.types.alternatives). Prefer representing alternatives with their required data.** Use variant constructors for cases that require different data. Avoid flags and optional fields that allow combinations the program cannot handle.

Construction and updates follow [R.types.construction](1-functionality.md#r.types.construction). Constraints outside the type follow [R.types.runtime-checks](1-functionality.md#r.types.runtime-checks).

## Abstractions and interfaces

As a default, give abstractions responsibilities that current callers need. An abstraction adds a concept readers must learn, so hypothetical future uses alone do not justify generic options or extension points. This applies [YAGNI](https://martinfowler.com/bliki/Yagni.html) to abstractions.

Names and interfaces should express the responsibility, what callers supply, and what they can rely on. Callers should be able to use operations without knowing their internal steps. Inputs that affect results should be explicit by default.

<a id="r.abstractions"></a>**[R.abstractions](#r.abstractions). Abstraction boundaries**

*Default. Principle [Coherence](PRINCIPLES.md#coherence).*

<a id="r.abstractions.operations"></a>**[R.abstractions.operations](#r.abstractions.operations). Extract meaningful operations.** Give each helper or module an operation or responsibility that its callers can name. One caller can justify an abstraction when it expresses a distinct operation.

<a id="r.abstractions.sharing"></a>**[R.abstractions.sharing](#r.abstractions.sharing). Share implementations only when callers need the same operation and constraints.** Similar syntax alone does not justify sharing. Keep mutually recursive semantic operations together. Introduce shared signatures for consumers that need interchangeable implementations. Pass a function when one operation suffices.

<a id="r.traversals"></a>**[R.traversals](#r.traversals). Share structural traversal with explicit scope and order.** Use `map_*_children` for shallow transformation, `rewrite_*_postorder` for recursive rewriting, and `iter_*_preorder` or `fold_*_preorder` for visits or accumulation. Use the corresponding suffix for other orders. Define visited nodes, sibling order, and replacement behavior. Preserve metadata by default, and keep binding rules and conversions explicit. Extract against demonstrated duplication.

<a id="r.abstractions.exposure"></a>**[R.abstractions.exposure](#r.abstractions.exposure). Expose what callers need.** Keep representations private when callers need operations rather than direct inspection. Expose data when inspecting it is part of the caller's task.

<a id="r.abstractions.io"></a>**[R.abstractions.io](#r.abstractions.io). Separate computation from loading and saving data by default.** Functions that compute results should accept data directly. Functions whose purpose is loading or saving data should handle the corresponding I/O.

## Mutation

As general guidance, prefer functional updates that return new values over mutation. Returning an updated value makes the change explicit to callers. Other computations can keep using the original value. When mutation is useful, make its dependencies and ownership explicit.

<a id="r.mutation"></a>**[R.mutation](#r.mutation). Mutation**

*Default. Principle [Coherence](PRINCIPLES.md#coherence). Rule [R.invariants](1-functionality.md#r.invariants).*

<a id="r.mutation.inputs"></a>**[R.mutation.inputs](#r.mutation.inputs). Pass inputs as arguments instead of reading mutable global state by default.** Pass settings and environments that affect a result at the call site. This lets readers see the function's dependencies.

<a id="r.mutation.ownership"></a>**[R.mutation.ownership](#r.mutation.ownership). Give mutable state a clear owner and lifetime.** Keep state needed by one operation local to that operation. Put shared state and the operations that update it in the component responsible for maintaining it.

<a id="r.mutation.recursion"></a>**[R.mutation.recursion](#r.mutation.recursion). Prefer readable recursion or folds over mutable references when they make control flow clearer.**

Mutation can serve caches, registries, usage tracking, and resource management.
