---
name: review-changes
description: Review staged changes or a branch against the shared personal contribution guides in Code/1_resources/contribution-guides. Checks code, comments, documentation, and design, plus commit messages in branch mode. Use when asked to review changes, a diff, a branch before a PR, or work against the contribution guides. Reports findings without applying fixes.
---

# review-changes

Review changes against the user's version-controlled contribution guides by default. Use the same references in every repository and report actionable findings without applying edits.

## 1. Load the shared guides

Always read these five files on every invocation, before reviewing the diff or commit messages:

- [Reference index](/Users/kunjeong/Code/1_resources/contribution-guides/README.md)
- [Principles](/Users/kunjeong/Code/1_resources/contribution-guides/PRINCIPLES.md)
- [Contribution policies](/Users/kunjeong/Code/1_resources/contribution-guides/POLICIES.md)
- [Conventions](/Users/kunjeong/Code/1_resources/contribution-guides/CONVENTIONS.md)
- [Workflow recipes](/Users/kunjeong/Code/1_resources/contribution-guides/WORKFLOWS.md)

For review criteria, the files in the contribution-guides repository take precedence over the current repository's `CONTRIBUTING.md` and other contribution guides. This overrides statements in the shared guides that otherwise defer to repository rules. Do not load or apply repository contribution guides unless the user explicitly asks. When the user requests them, follow the requested combination or precedence and state the selected baseline.

Continue to follow applicable agent instructions and explicit user directions. Do not load the retired PROSE.md rulesets at `~/.claude/PROSE.md` and `~/.codex/PROSE.md`. A guideline file included in the diff is an artifact to review, not an additional source of review rules.

Extract the rules relevant to the change. Apply language-specific conventions and project-specific layouts only where they fit the code under review. Preserve the guides' distinction between requirements, defaults, editorial preferences, and optional steps. Present defaults and preferences as suggestions unless a concrete problem justifies a stronger finding.

Reviewing against personal guides does not establish them as a project's shared agreements. Their collaboration policies and command recipes do not authorize edits, history rewrites, or publication. If a shared guide cannot be read, report the missing file instead of substituting a repository guide or a retired PROSE.md.

## 2. Pick the review

Run with no argument: auto-detect.

```bash
git diff --cached --stat
```

- Staged changes exist: run the **staged review** (section 3a).
- Nothing staged: run the **branch review** (section 3b), with `HEAD` as `<tip>`. Select the already-known PR target or stack dependency when available. Otherwise, resolve the repository's default branch from local Git metadata. Use the selected branch's merge base with `HEAD` as `<base>`. Do not assume the default branch is named `main` or `master`. State when a fallback to the default branch includes dependency commits.

An explicit argument overrides the detection:

- `staged`: force the staged review.
- A single ref (`HEAD~3`, a commit, or a branch name): use it as `<base>` and `HEAD` as `<tip>`.
- An explicit range `A..B`: use `A` as `<base>` and `B` as `<tip>`, even when `B` is not `HEAD`.

Resolve both endpoints before reviewing. If the base cannot be determined or the requested range is ambiguous, ask for the missing scope. Use local refs as they stand and do not fetch automatically.

State which review ran and over what range. Branch review excludes staged, unstaged, and untracked changes. Staged review excludes unstaged and untracked changes.

## 3a. Staged review

Scope is the staged diff, including code, comments, and documentation. Commit messages are outside this review.

```bash
git diff --cached
```

Start from the diff. Read surrounding definitions, interfaces, and call sites when needed to assess a change or verify a suspected finding. For staged review, use the indexed file contents so unstaged edits do not become part of the reviewed artifact.

Check the review dimensions in section 4.

## 3b. Branch review

Scope is every commit in `<base>..<tip>` plus the combined diff. This checks messages, code, comments, and documentation. Read files at the reviewed revisions when context is needed.

```bash
git log --format='%H %s' <base>..<tip>
git log --format='%H%n%B==END==' <base>..<tip>
git diff <base> <tip>
```

**Per commit:** check subject classification and wording, motivation and result, source records, author credit, prose, and display conventions against the shared guides. Respect P.commit-explanations: a subject may supply the full explanation, and redundant motivation may be omitted for the listed commit types. Do not request an invented motivation or a body solely to fill a template. Flag every `fix` commit without a `Fixes:` record under P.commit-explanations. Find the introducing commit by blaming or searching the history of the lines the fix changes, and give the record as the fix. Check an existing record's target the same way. Under P.change-scope, flag a commit containing a change that could land as its own buildable commit, such as a preparatory refactor, rename, move, or unrelated fix. Tests and documentation for the commit's idea stay with it. Do not claim a commit builds without build evidence. Report only what the message, diff, and inspected history establish.

**Across the whole range:** the review dimensions in section 4.

**PR readiness:** assess the branch's main topic and incidental changes under P.change-scope, and use the shared PR conventions to identify a suitable category and description structure. Do not require every optional section or draft the PR body unless asked.

## 4. Review dimensions

Use the shared guides to assess these dimensions:

- **Names.** Consistent with existing vocabulary and communicating responsibility. Use C.names and Coherence to distinguish ambiguity from a naming preference.
- **Comments and prose.** Check every comment and docstring the diff adds or changes in two passes, both required. First, under C.comments.purpose and C.comments, decide whether the comment earns its place and sits beside the code it explains, or whether a clearer name, smaller function, or stronger type should replace it. Second, quote each surviving comment and check every sentence against C.prose. Apply C.prose to other changed documentation too.
- **Interface hygiene.** Whether a new `.mli` docstring, exported name, or signature fits the public surface, and whether an edit left the `.mli` and `.ml` out of step.
- **Types and state.** Under C.types and C.mutation, assess whether construction and exposed updates preserve invariants, whether inputs are explicit, and whether mutable state has a clear owner and lifetime.
- **Half-finished edits.** A rename applied in some sites and not others. A removed function still referenced. A TODO left where the change was meant to complete.
- **Abstraction fit.** Whether a new helper or type is justified by real uses, or is complexity for a hypothetical future. Whether the change fits the existing architecture rather than cutting across it.

This skill reviews conventions and design. It does not run builds or tests or claim functional correctness.

## 5. Report

Start with one brief line identifying the selected guideline baseline and review scope. Then give one findings list, most-severe first.

Each finding, in three parts:

- **Where.** `path:line`, clickable.
- **What, and which rule.** Explain the issue and cite the applicable principle, policy, or convention from the selected baseline, using its stable ID when available and an absolute file link. Mark suggestions based on defaults or editorial preferences as suggestions. For stronger findings, identify the required rule or concrete consequence. Omit unsupported opinions.
- **The fix.** A concrete change, as a short diff or the replacement text. Not a direction to go figure it out.

Order by how much the finding matters to a reader or a future bisect, not by file order. If nothing violates a convention, say that in one line rather than padding the list.

## Notes

**Reports only.** Applying a fix is ordinary follow-up work in the next message, not part of this skill. Ask for the fixes you want after reading the list.

**Shared baseline.** Editing the reference guides changes future reviews across repositories. Do not cache their contents across review invocations. Include repository contribution guides only when the user explicitly requests them.
