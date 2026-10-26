# History

## Checklist

**Each commit**

- Does it hold one idea, together with its tests and documentation? [R.change-scope](#r.change-scope)
- Is it free of changes that could land as their own buildable commit, such as a preparatory refactor, rename, or move? [R.change-scope](#r.change-scope)
- Does it build without anything that a later commit adds? [R.commit-buildability](#r.commit-buildability)
- Does it carry the evidence its type requires? [R.evidence](1-functionality.md#r.evidence)
- For a refactor, reorg, or performance change, are test expectations unchanged? [R.evidence.preservation](1-functionality.md#r.evidence.preservation)

**Each commit message**

- Does the message explain the resulting change, and the motivation wherever the subject does not already make it clear? [R.commit-explanations](#r.commit-explanations)
- For a fix, does the body name the incorrect behavior? [R.commit-explanations](#r.commit-explanations)
- For a refactor, does the body name the structural limitation? [R.commit-explanations](#r.commit-explanations)
- Does the subject name the concept, so that a reader scanning the log understands the change? [R.change-summaries](#r.change-summaries)
- Do the type and scope fit the intent and the affected area? [R.commit-format.classification](#r.commit-format.classification)
- For a fix, does the `Fixes:` record point at the commit that introduced the fault? [R.sources.regressions](#r.sources.regressions)
- For copied or adapted work, does a source record cite the origin, with author credit preserved? [R.source-credit](#r.source-credit)
- Does every coauthor credit name a person who wrote part of the change? [R.sources.coauthors](#r.sources.coauthors)
- Does the body leave out what the diff shows, including measurements? [R.commit-prose.diff](#r.commit-prose.diff), [R.evidence.locations](1-functionality.md#r.evidence.locations)
- Does every sentence follow the prose rules? [R.prose](3-prose.md#r.prose)
- Does the message match the [commit form](#commit-form)?

**Each branch**

- Does it develop one main topic, with incidental commits kept distinct? [R.change-scope](#r.change-scope)

<a id="r.change-scope"></a>**[R.change-scope](#r.change-scope). Each commit should express one idea, and each PR should develop one main topic.**

*Required. Principles [Coherence](PRINCIPLES.md#coherence) ↔ [Proportionality](PRINCIPLES.md#proportionality).*

A commit carries one idea with its tests and documentation. A refactor, rename, or move that the idea depends on is a separate commit placed before it. Split along ideas, not along files or rules. One idea applied in several places stays one commit. Combine commits when separating them would need placeholders or break the build, under [R.commit-buildability](#r.commit-buildability). Separate commits let readers understand, review, and bisect each change on its own.

A PR may include commits outside its main topic when a separate PR would add review and landing overhead without enough practical benefit. Those commits should remain distinct, and the PR body should explain why they belong.

Final commit preparation follows [R.commit-buildability](#r.commit-buildability).

<a id="r.commit-explanations"></a>**[R.commit-explanations](#r.commit-explanations). Each final commit message should explain the motivation and resulting change.**

*Required. Principles [Motivation](PRINCIPLES.md#motivation), [Coherence](PRINCIPLES.md#coherence).*

A commit message should let readers understand why the change was needed and what it accomplishes without having seen the original discussion. Motivation explains the prior problem, limitation, or research goal. Solution describes the resulting change. Put motivation and solution in separate paragraphs, with motivation first.

Fixes must identify the incorrect behavior and the commit that introduced it. Refactors must identify the structural limitation and explain how the new structure addresses it. Both always require motivation.

For `feat`, `test`, `docs`, and `chore` commits, motivation may be omitted when it would only restate the solution. Include any user need, research goal, or maintenance reason the change addresses. Do not invent a problem to fill the format.

When the subject already conveys the required explanation, the message does not need a body. Source records still follow [R.source-credit](#r.source-credit). [R.sources.regressions](#r.sources.regressions) supplies the format for recording a fix's introducing commit.

<a id="r.commit-wrapping"></a>**[R.commit-wrapping](#r.commit-wrapping). Wrap final commit messages at 72 columns.** `[auto]`

*Required. Principle [Coherence](PRINCIPLES.md#coherence).*

Terminals, `git log`, and emailed patches show commit messages as written, without rewrapping. Longer lines break at arbitrary points or run off the screen. URLs, identifiers, and quoted subjects in source records stay whole, even past 72 columns, so readers can follow and search them. Markdown paragraphs and PR bodies follow [R.markdown-wrapping](3-prose.md#r.markdown-wrapping) instead.

<a id="r.source-credit"></a>**[R.source-credit](#r.source-credit). Commits containing copied or adapted work must cite its source and preserve author credit.**

*Required. Principle [Provenance](PRINCIPLES.md#provenance).*

Source references let readers trace inherited work and preserve its contributors' credit. A commit containing copied or adapted work should identify the source revision and explain local differences in behavior or design. When several commits are folded together, all their source references should remain in the resulting message.

Rewrites must preserve source references and author attribution. Credit records do not change responsibility under [R.responsibility](modules/collaboration.md#r.responsibility). Coauthor credit is optional and limited to actual human joint authorship. Tools are not coauthors. Recommended source-trailer formats are described in [Sources and credit](#sources-and-credit).

<a id="r.commit-buildability"></a>**[R.commit-buildability](#r.commit-buildability). Finalize each commit as a buildable unit.**

*Required. Principles [Coherence](PRINCIPLES.md#coherence), [Verification](PRINCIPLES.md#verification), [Proportionality](PRINCIPLES.md#proportionality).*

Each final commit should express one idea under [R.change-scope](#r.change-scope) and leave the project buildable, so maintainers can investigate regressions without first repairing intermediate states. If separating commits would require placeholders or break the build, they should be combined.

Review fixups are folded into the commits they complete before landing.

Apply the [prose rules](3-prose.md#r.prose) to writing in change records. The rules below supply record-specific forms.

<a id="r.change-summaries"></a>**[R.change-summaries](#r.change-summaries). Summarize the conceptual change in commit subjects and PR titles.**

*Default. Principle [Coherence](PRINCIPLES.md#coherence). Rules [R.commit-explanations](#r.commit-explanations), [R.pr-explanations](modules/pr.md#r.pr-explanations).*

Name the action and affected concept so readers can identify the change before opening its details. A commit subject describes that commit’s idea. A PR title names the contribution’s main topic, and its body accounts for accompanying work.

## Commit messages

### Commit form

```text
type(scope): imperative summary of the concept

The prior problem, limitation, or goal, in the past tense.

What the change does, in the third person present, with identifiers
such as `make_env` in backticks.

Original-commit: https://github.com/org/repo/commit/0123456789ab
Fixes: 0123456789ab ("subject of the commit that introduced the fault")
Co-authored-by: Name <email>
```

The rules below define each part of the form.

<a id="r.commit-format"></a>**[R.commit-format](#r.commit-format). Commit classification and format**

*Default. Principle [Coherence](PRINCIPLES.md#coherence). Rule [R.commit-explanations](#r.commit-explanations).*

<a id="r.commit-format.subject"></a>**[R.commit-format.subject](#r.commit-format.subject). Use `type(scope): summary`, with standard types and the additional `reorg` type.** `[auto]`

Use this format, with the omissions allowed by [R.commit-explanations](#r.commit-explanations).

```text
type(scope): imperative summary

Motivation describing the prior problem, limitation, or research goal.

Solution describing the resulting change.
```

<a id="r.commit-format.classification"></a>**[R.commit-format.classification](#r.commit-format.classification). Choose the type by intent and the scope by affected area, regardless of implementation language.**

Commit types include `feat`, `fix`, `refactor`, `test`, `docs`, `ci`, `chore`, `perf`, and `style`. Classification applies across implementation languages. The additional `reorg` type covers directory renames, file moves, and layout changes that preserve code structure and behavior. Mechanical caller updates can remain `reorg`. Use `refactor` when responsibilities or APIs change. Use `ci` for CI configuration and automated build, check, or release workflows. Use `chore` for other build configuration or dependencies.

Classify structural or behavioral changes by their own intent, even when they accompany reorganization or formatting. Explain those changes separately. A `reorg` label does not establish behavior preservation by itself.

Choose the narrowest accurate scope.

For documentation changes, choose the scope by topic. Use `docs(principles)` for project principles, `docs(conventions)` for routine conventions, and `docs(contributing)` for contribution policies or changes spanning the contribution process. Name affected documents in the body when that helps readers locate the work.

<a id="r.commit-format.moves"></a>**[R.commit-format.moves](#r.commit-format.moves). List renamed or moved paths in a `reorg` message as `old -> new` bullets and describe mechanical reference updates.** In a PR, put the rename list beneath the relevant scoped summary bullet using the same path format.

<a id="r.commit-prose"></a>**[R.commit-prose](#r.commit-prose). Commit prose**

*Default. Rule [R.commit-explanations](#r.commit-explanations).*

<a id="r.commit-prose.subjects"></a>**[R.commit-prose.subjects](#r.commit-prose.subjects). Use imperative subjects.** Name the concept. Put code identifiers in the body, where there is room to explain them. For example, `refactor(cli): group shared flags by role` gives the reader a concept, while its body can identify the modules and flag groups.

<a id="r.commit-prose.bodies"></a>**[R.commit-prose.bodies](#r.commit-prose.bodies). Separate motivation and solution into paragraphs, with motivation first.** Exceptions for omitting motivation or the whole body follow [R.commit-explanations](#r.commit-explanations). Section headings are optional. Source citations still follow [R.source-credit](#r.source-credit).

<a id="r.commit-prose.motivation-tense"></a>**[R.commit-prose.motivation-tense](#r.commit-prose.motivation-tense). Describe prior problems in past tense by default.** A `Currently, ...` framing is also acceptable.

<a id="r.commit-prose.solution-tense"></a>**[R.commit-prose.solution-tense](#r.commit-prose.solution-tense). Describe solutions in third-person present.** The opening sentence may omit "This commit" and begin with an action verb such as "Adds" or "Replaces". Give following sentences clear subjects, usually the components whose behavior they describe. Avoid first-person and future-tense accounts of the solution. The same structure applies to solution bullets.

<a id="r.commit-prose.solution-verbs"></a>**[R.commit-prose.solution-verbs](#r.commit-prose.solution-verbs). Use specific verbs to describe what the change does.** Prefer "Removes expired cache entries" to "Updates the cache so expired entries are no longer retained". Omit temporal wording that only repeats context already supplied by the motivation. Sentence structure follows [R.commit-prose.solution-tense](#r.commit-prose.solution-tense).

<a id="r.commit-prose.diff"></a>**[R.commit-prose.diff](#r.commit-prose.diff). Leave out what the diff shows.** The body explains why the change was made and what it achieves. How the change was made, which files it touches, and its edits line by line belong to the diff.

<a id="r.commit-prose.grouping"></a>**[R.commit-prose.grouping](#r.commit-prose.grouping). Use paragraphs for a change within one affected area and bullets for changes across distinct areas.** Keep the motivation in prose. Use solution bullets when separating changes to different components or responsibilities makes the result easier to scan. Name concrete identifiers where they help explain the result.

<a id="r.commit-prose.identifiers"></a>**[R.commit-prose.identifiers](#r.commit-prose.identifiers). Use backticks around code identifiers in commit bodies.** This distinguishes identifiers from ordinary prose.

<a id="r.commit-display"></a>**[R.commit-display](#r.commit-display). Commit character set**

*Default. Principles [Coherence](PRINCIPLES.md#coherence), [Proportionality](PRINCIPLES.md#proportionality).*

<a id="r.commit-display.characters"></a>**[R.commit-display.characters](#r.commit-display.characters). Prefer ASCII in commit-message prose for predictable terminal display.** Use UTF-8 when accurate names, identifiers, or exact source text require it. `[auto]`

## Sources and credit

<a id="r.sources"></a>**[R.sources](#r.sources). Source and related-revision records**

*Default. Rules [R.source-credit](#r.source-credit), [R.commit-explanations](#r.commit-explanations), [R.responsibility](modules/collaboration.md#r.responsibility).*

In commit messages, source records use full URLs so they remain useful outside GitHub's PR view. Repeat records when a local commit combines several sources. Describe meaningful adaptations in the body. Preserve credit under [R.source-credit](#r.source-credit).

<a id="r.sources.commits"></a>**[R.sources.commits](#r.sources.commits). Identify specific source commits with `Original-commit:`.** Use this record for work ported or adapted from an upstream or sibling-repository commit.

<a id="r.sources.trees"></a>**[R.sources.trees](#r.sources.trees). Identify imported files or trees with `Copied-from:`.** Link the source at the revision and path that were copied.

<a id="r.sources.states"></a>**[R.sources.states](#r.sources.states). Identify synchronized source states with `Reference:`.** For an upstream Sync, link the incoming comparison range. For a feature Sync, link the reference revision and the file or tree location being adopted. This records the source state when the work does not follow specific source commits.

Upstream commits retained by a merge already preserve their origins and need no duplicate source records. Local commits adapting specific upstream work still use `Original-commit:`.

<a id="r.sources.cherry-picks"></a>**[R.sources.cherry-picks](#r.sources.cherry-picks). Use `Cherry-picked-from:` as an optional record for transfers between maintained branches.** It helps trace a release backport or another transfer between histories that remain in use. Omit it for a move from a superseded branch. Preserve existing source records under [R.source-credit](#r.source-credit). Work imported from another repository follows [R.sources.commits](#r.sources.commits).

<a id="r.sources.regressions"></a>**[R.sources.regressions](#r.sources.regressions). Record the commit that introduced a fixed fault as `Fixes: <12-character SHA> ("<subject>")`.** Find it by blaming the lines the fix changes, or by searching history for the code the fix replaces. Preserve the introducing commit's full subject. Hash-length exceptions follow [R.sources.hashes](#r.sources.hashes). This format is an exception to the full-URL default. It may coexist with source records. `[auto]`

If a one-line `Fixes:` record exceeds 72 characters, move the complete quoted subject, including its parentheses, to a second line indented by one space. Do not wrap the quoted subject, even if that line exceeds 72 characters. Leave short records and existing two-line records unchanged.

<a id="r.sources.hashes"></a>**[R.sources.hashes](#r.sources.hashes). Use 12-character commit hashes in same-repository references and Git URLs that accept abbreviated hashes.** This includes prose references, GitHub shorthand, commit URLs, revision paths, and both endpoints of comparison URLs. Use a longer hash when 12 characters would be ambiguous or the URL requires it. Shortening a hash changes its length while retaining the URL and the identified revision. Preserve hashes in verbatim source quotations and copied commit subjects. `[auto]`

<a id="r.sources.coauthors"></a>**[R.sources.coauthors](#r.sources.coauthors). Credit human coauthors with optional `Co-authored-by: Name <email>` trailers.** Use the trailer only for actual joint authorship and place it in the final record block. Do not add AI or other tool names as coauthors. Existing attribution records remain subject to preservation under [R.source-credit](#r.source-credit) and agreement on attribution changes under [R.reviewer-tasks](modules/collaboration.md#r.reviewer-tasks).

<a id="r.sources.order"></a>**[R.sources.order](#r.sources.order). Place records after the body in one block, in this order: source records, then `Fixes:`, then `Co-authored-by:`.** Source records come first so that a Port's attribution paragraph sits directly above them, under [R.sources.port-attribution](modules/ports.md#r.sources.port-attribution). `[auto]`

In PR bodies and merge summaries, GitHub shorthand such as `org/repo@sha` or `org/repo#number` is appropriate. Preserve author information during a rewrite, while allowing Git to record who created the rewritten commit as its committer. The committer field alone does not determine responsibility under [R.responsibility](modules/collaboration.md#r.responsibility).

## Revising reviewed commits

Incremental review commits can be folded once review settles. Use an interactive rebase against the chosen review base, which may be a dependency branch for a stacked PR.

```bash
git rebase -i <review-base>
```

Use `fixup` for a follow-up whose message has no independent information to preserve. Use `squash` when combining commits with source trailers or useful rationale, then retain that information explicitly in the resulting message. Describe the final change after folding.

When per-commit buildability needs checking, an interactive rebase can run a check after each resulting commit.

```bash
git rebase -i --exec 'make exe' <review-base>
```

Use the opam switch available in the chosen environment and substitute a more relevant check when appropriate. A failure stops the rebase so the commit can be repaired or folded. This recipe does not imply that every review update needs a rebase or an expensive rerun.

## A small contribution

As a hypothetical example, a parser fix can add a diagnostic for an incomplete field declaration and one negative test demonstrating that failure. Keep both in a single commit.

```text
fix(parser): diagnose incomplete field declarations

An incomplete field declaration reached an internal exception, leaving
the user without a useful location for the error.

Reports a syntax diagnostic at the declaration and adds a negative test
for the missing field type.

Fixes: 0123456789ab ("feat(parser): parse field declarations")
```

Its PR can contain a short Motivation explaining the same problem and result. It needs no separate Core Concepts, Scope, or Commit Log. If the maintainer performs cleanup within [R.final-cleanup](modules/landing.md#r.final-cleanup), the merge notice can say what was corrected. After final cleanup adds the PR number, this single commit is fast-forwarded and its message carries the landing record.
