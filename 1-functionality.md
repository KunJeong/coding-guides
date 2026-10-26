# Functionality

## Checklist

Clients are the callers and users who reach the code through its interface.

**Each type with an invariant**

- Does every way to create a value establish the invariant? [R.types.construction](#r.types.construction), [R.invariants](#r.invariants)
- Does every public operation that changes a value keep the invariant? [R.invariants](#r.invariants)
- Is each constraint the type cannot express checked at runtime? [R.types.runtime-checks](#r.types.runtime-checks)

**Each behavior clients rely on**

- Does a test exercise it through the interface clients use? [R.tests.interfaces](#r.tests.interfaces)

**Each test**

- Does it catch a failure that no other test catches? [R.tests.purpose](#r.tests.purpose)
- Does it reach the code through the interface clients use? [R.tests.interfaces](#r.tests.interfaces)

<a id="r.invariants"></a>**[R.invariants](#r.invariants). Preserve the guarantees callers rely on.**

*Principles [Coherence](PRINCIPLES.md#coherence), [Verification](PRINCIPLES.md#verification).*

Callers need to know which guarantees hold when they use a value or operation. Construction must establish those guarantees, and exposed updates must preserve them. [R.types.construction](#r.types.construction) and [R.types.runtime-checks](#r.types.runtime-checks) describe ways to enforce them.

<a id="r.evidence"></a>**[R.evidence](#r.evidence). Support each change's claim with evidence others can repeat.**

*Principle [Verification](PRINCIPLES.md#verification).*

A change's type decides what it claims. The claim decides the evidence. Run the checks that produce the evidence before presenting the change for review.

| Type | Claim | Evidence |
| --- | --- | --- |
| `fix` | The fault no longer occurs. | A test that fails without the fix, or a description of the check when no test can reproduce the fault. |
| `feat` | The new behavior works as described. | A test. |
| `refactor` | Behavior is unchanged. | Unchanged test expectations. |
| `reorg` | Only paths and references changed. | Unchanged test expectations, and a diff with rename detection that shows only moves. |
| `perf` | The system is faster or smaller. | Unchanged test expectations, and measurements before and after, with the method. |
| `test` | The suite catches a failure it missed before. | The new test. |
| `docs` | The text matches the system. | Its commands and examples produce what it states. |
| `ci`, `chore`, `style` | Nothing about behavior. | None. |

<a id="r.evidence.preservation"></a>**[R.evidence.preservation](#r.evidence.preservation). Keep test expectations unchanged in a refactor, reorg, or performance change.** A changed expectation reveals a behavior change, which belongs in its own commit under [R.change-scope](4-history.md#r.change-scope).

<a id="r.evidence.locations"></a>**[R.evidence.locations](#r.evidence.locations). Record evidence where it stays accurate.**

- Tests belong in the diff.
- Measurements and other checks belong in the PR's [Validation section](modules/pr.md#r.pr-body.validation), taken on the final branch. Commit messages record no measurements, because a rebase can change the numbers.
- The [landing record](modules/landing.md#r.merge-method) keeps one line with the result of a performance claim.

[Factoring](2-factoring.md#factoring) covers how types and interfaces express those guarantees.

## Contracts and invariants

<a id="r.types.construction"></a>**[R.types.construction](#r.types.construction). Protect invariants at construction.** When callers rely on a value already being validated, use an abstract or private type with checked constructors. Every exposed operation that constructs or updates a value must preserve those constraints.

## Runtime checks

<a id="r.types.runtime-checks"></a>**[R.types.runtime-checks](#r.types.runtime-checks). Keep checks for constraints the type does not enforce.** A type may guarantee a value's structure without guaranteeing its meaning or its relationship to other values. Validate those remaining constraints at runtime.

As guidance, prefer explicit checks when encoding a constraint in a type would make ordinary operations harder to understand.

## Tests

<a id="r.tests"></a>**[R.tests](#r.tests). Tests**

Each test is code to read, run, and maintain.

<a id="r.tests.purpose"></a>**[R.tests.purpose](#r.tests.purpose). Add a test only when it catches a failure that no other test catches, in a behavior clients rely on.** Name that failure. Remove or merge a test that stops meeting this rule. Coverage shows which lines a test runs, not which failures it catches.

<a id="r.tests.suites"></a>**[R.tests.suites](#r.tests.suites). Add a case to an existing suite before adding a new runner, fixture format, or test directory.**

<a id="r.tests.interfaces"></a>**[R.tests.interfaces](#r.tests.interfaces). Test through the interface clients use.** Tests of internal code break when a refactor changes that code, even when clients see no difference. Do not widen an interface only for a test, under [R.abstractions.exposure](2-factoring.md#r.abstractions.exposure). An internal function that seems to need its own tests may deserve its own module, under [R.abstractions.operations](2-factoring.md#r.abstractions.operations). Check properties clients cannot observe, such as speed, by measurement or a [runtime check](#r.types.runtime-checks).
