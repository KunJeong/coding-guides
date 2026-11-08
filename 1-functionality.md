# Functionality

## Checklist

Clients are the callers and users who reach the code through its interface.

**Each task the change is meant to support**

- Can a client complete it through the interface the change provides? [R.tasks](#r.tasks)

**Each catch-all branch, such as `| _ ->` or a final `else`**

- Should every value this branch handles get the same result? [R.cases](#r.cases)

**Each search for a value by name or key**

- Does the code handle no match, one match, and several matches? [R.cases](#r.cases)

**Each value read from outside the program, such as a command-line argument, a file, or an editor buffer**

- When the value is missing or invalid, does the program report an error that says how to fix it? [R.cases](#r.cases), [R.types.runtime-checks](#r.types.runtime-checks)

**Each new constructor, definition kind, or flag**

- Does every function that handles the existing ones also handle the new one? [R.cases](#r.cases)

**Each type with an invariant**

- Does every way to create a value establish the invariant? [R.types.construction](#r.types.construction), [R.invariants](#r.invariants)
- Does every public operation that changes a value keep the invariant? [R.invariants](#r.invariants)
- Is each constraint the type cannot express checked at runtime? [R.types.runtime-checks](#r.types.runtime-checks)

<a id="r.tasks"></a>**[R.tasks](#r.tasks). Let clients complete each task the change is meant to support.**

*Principle [Motivation](PRINCIPLES.md#motivation).*

Follow each task named in the motivation through the client interface, from input to result. Check that clients can complete every step.

<a id="r.cases"></a>**[R.cases](#r.cases). Give every case that the inputs allow a defined result.**

*Principle [Verification](PRINCIPLES.md#verification).*

A case is one kind of value the code can receive, such as one constructor, an empty search result, or a missing file. Check these places:

- OCaml cannot warn about a missing constructor covered by a catch-all branch. Check that all values reaching the branch should get the same result.
- A search for a value by name or key can find nothing, one value, or several values.
- A value read from outside the program can be missing or invalid. Report it with an error that says what to fix, under [R.types.runtime-checks](#r.types.runtime-checks).
- A new constructor, definition kind, or flag needs handling in every function that handles the existing ones.

<a id="r.invariants"></a>**[R.invariants](#r.invariants). Preserve the guarantees callers rely on.**

*Principles [Coherence](PRINCIPLES.md#coherence), [Verification](PRINCIPLES.md#verification).*

Callers need to know which guarantees hold when they use a value or operation. Construction must establish those guarantees, and exposed updates must preserve them. [R.types.construction](#r.types.construction) and [R.types.runtime-checks](#r.types.runtime-checks) describe ways to enforce them.

[Factoring](2-factoring.md#factoring) covers how types and interfaces express those guarantees. [Verification](3-verification.md#verification) covers the tests and other evidence that show a change works.

## Contracts and invariants

<a id="r.types.construction"></a>**[R.types.construction](#r.types.construction). Protect invariants at construction.** When callers rely on a value already being validated, use an abstract or private type with checked constructors. Every exposed operation that constructs or updates a value must preserve those constraints.

## Runtime checks

<a id="r.types.runtime-checks"></a>**[R.types.runtime-checks](#r.types.runtime-checks). Keep checks for constraints the type does not enforce.** A type may guarantee a value's structure without guaranteeing its meaning or its relationship to other values. Validate those remaining constraints at runtime.

As guidance, prefer explicit checks when encoding a constraint in a type would make ordinary operations harder to understand.
