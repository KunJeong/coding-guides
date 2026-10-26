# Functionality

<a id="p.invariants"></a>

**[P.invariants](#p.invariants). Preserve the guarantees callers rely on.**

*Requirement. [Coherence](PRINCIPLES.md#coherence), [Verification](PRINCIPLES.md#verification)*

Construction must establish those guarantees, and exposed updates must preserve them.

Callers need to know which guarantees hold when they use a value or operation. Construction must establish those guarantees, and exposed updates must preserve them. The [construction and validation conventions](#functionality) describe ways to enforce them.

The [invariants policy](#p.invariants) requires construction and updates to preserve the guarantees callers rely on. These conventions cover construction and runtime validation. [Factoring](2-factoring.md#factoring) covers how types and interfaces express those guarantees.

*Default. Policy [P.invariants](#p.invariants).*

## Contracts and invariants

- <a id="c.types.construction"></a>**[C.types.construction](#c.types.construction). Protect invariants at construction.** When callers rely on a value already being validated, use an abstract or private type with checked constructors. Every exposed operation that constructs or updates a value must preserve those constraints.

## Runtime validation

- <a id="c.types.runtime-checks"></a>**[C.types.runtime-checks](#c.types.runtime-checks). Keep checks for constraints the type does not enforce.** A type may guarantee a value's structure without guaranteeing its meaning or its relationship to other values. Validate those remaining constraints at runtime.

As guidance, prefer explicit checks when encoding a constraint in a type would make ordinary operations harder to understand.
