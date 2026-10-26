# Functionality

<a id="r.invariants"></a>

**[R.invariants](#r.invariants). Preserve the guarantees callers rely on.**

*Requirement. [Coherence](PRINCIPLES.md#coherence), [Verification](PRINCIPLES.md#verification)*

Construction must establish those guarantees, and exposed updates must preserve them.

Callers need to know which guarantees hold when they use a value or operation. Construction must establish those guarantees, and exposed updates must preserve them. The [construction and validation conventions](#functionality) describe ways to enforce them.

The [invariants policy](#r.invariants) requires construction and updates to preserve the guarantees callers rely on. These conventions cover construction and runtime checks. [Factoring](2-factoring.md#factoring) covers how types and interfaces express those guarantees.

*Default. Policy [R.invariants](#r.invariants).*

## Contracts and invariants

- <a id="r.types.construction"></a>**[R.types.construction](#r.types.construction). Protect invariants at construction.** When callers rely on a value already being validated, use an abstract or private type with checked constructors. Every exposed operation that constructs or updates a value must preserve those constraints.

## Runtime checks

- <a id="r.types.runtime-checks"></a>**[R.types.runtime-checks](#r.types.runtime-checks). Keep checks for constraints the type does not enforce.** A type may guarantee a value's structure without guaranteeing its meaning or its relationship to other values. Validate those remaining constraints at runtime.

As guidance, prefer explicit checks when encoding a constraint in a type would make ordinary operations harder to understand.
