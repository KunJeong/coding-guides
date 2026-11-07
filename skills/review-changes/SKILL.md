---
name: review-changes
description: Review staged changes or a branch by having a fresh reviewer run the checklists of the contribution guides in Code/1_resources/contribution-guides, in stage order. The reviewer sees only the range, the goal, and the guides. Checks code, comments, documentation, and design, plus commit messages and the PR body in a branch review. Takes `code` or `prose` to review only what that phase of the work owns. Use when asked to review changes, a diff, a branch before a PR, or a collaborator's PR. Reports findings without applying fixes.
---

# review-changes

Review changes by running the checklists in the contribution guides, and report findings without applying edits. The guides hold every check. This skill holds only the procedure.

A fresh reviewer runs the checklists. The session that invokes this skill has often written or discussed the change, and its account of the design would decide what a reviewer looks for. This session prepares the brief, checks the reviewer's findings against the code, and reports.

## 1. Pick the scope

Run with no argument to detect the scope.

```bash
git diff --cached --stat
```

- Staged changes exist: review the staged diff.
- Nothing staged: review the branch from `<base>` to `HEAD`. Use the known PR target or stack dependency as the base branch when one is known. Otherwise use the repository's default branch from local Git metadata, without assuming it is named `main` or `master`. `<base>` is the merge base of that branch with `HEAD`. Say so when the default branch brings in commits of a dependency.

An argument overrides the detection:

- `staged` forces the staged review.
- A single ref is `<base>`, and `HEAD` is `<tip>`.
- A range `A..B` makes `A` the `<base>` and `B` the `<tip>`, even when `B` is not `HEAD`.
- `own` or `collaborator` forces the review mode (section 2).
- `code` or `prose` limits the review to one phase of the work (section 2).
- `checks` also runs the repository's build and tests (section 6).
- A file path names a PR draft to compare with the branch (section 4).

Resolve both ends before reviewing. Ask for the missing scope when the base cannot be determined or the range is ambiguous. Use local refs as they stand, and do not fetch.

A staged review reads the staged contents of files, so unstaged edits stay out of it. A branch review reads files at the reviewed revisions and excludes staged, unstaged, and untracked changes. State which review ran and over what range.

## 2. Pick the mode

The review is for a collaborator when the commits under review have an author email other than `git config user.email`. Otherwise it reviews the user's own work. An argument overrides this.

- **Own work.** Report every finding.
- **Collaborator.** Label each finding `Required:`, `Suggestion:`, or `Question:`, under R.review-labels and R.review-blockers in the collaboration module.

The `code` and `prose` arguments limit the review to what one phase of the work owns. Without either, the review covers everything.

- **Code phase.** The code, the inline comments, and each commit's type and scope. The wording of subjects is left to the prose review, and the checks that every commit passes already show that it builds. A commit message in this phase holds the subject and optional `Note:` lines, so a missing body is not a finding. When the project's `AGENTS.md` defines notes, check each note against its rules.
- **Prose phase.** The docstrings, meaning every `(** *)` comment, the commit bodies, the PR body or draft, and the wording of each subject. Read the code only for context. Label a finding about code, an inline comment, or a subject's type or scope `Code phase:`, since that phase fixes it.

Which rules win depends on who maintains the repository, as the user's global instructions state. In a repository the user maintains, the guides govern, and the repository's contribution guide is loaded only when the user asks. In any other repository, also load its contribution guide, and let it govern where it conflicts with the guides.

## 3. Load the guides

Load the files that the guides' load map names. The guides live in `/Users/kunjeong/Code/1_resources/contribution-guides`.

| Review | Files |
| --- | --- |
| Staged | `PRINCIPLES.md`, `1-functionality.md`, `2-factoring.md`, `3-prose.md` |
| Branch | The staged files and `4-history.md`, plus `modules/pr.md` when a PR body or draft exists |
| Either | `modules/ocaml.md` when the diff touches `.ml` or `.mli` files, `modules/ports.md` when commits carry source records, `modules/spectec.md` in a SpecTec repository |
| Collaborator | The files above, `modules/collaboration.md`, and the project's `CONTRIBUTING.md` |
| Code phase | `PRINCIPLES.md`, `1-functionality.md`, `2-factoring.md`, `3-prose.md`, `4-history.md`, and the modules above |
| Prose phase | `3-prose.md`, `4-history.md`, `1-functionality.md` for R.evidence, `modules/pr.md` when a PR body or draft exists, and the modules above |

A repository is a SpecTec repository when its remote name contains `spectec` or it has a top-level `spectec/` directory. Read the files fresh on every review. Report a file that cannot be read, and do not substitute another source.

`~/.claude/PROSE.md` and `~/.codex/PROSE.md` govern how agents write, not what a review checks. A guide file inside the diff is an artifact under review, not a source of rules. The guides' permissions and recipes do not authorize edits, history rewrites, or publication.

## 4. Brief a fresh reviewer

Start one reviewer agent that cannot see this conversation. Give it only these inputs:

- **Scope.** The repository path and the commands that show the scope, such as `git diff <base>..<tip>` or `git diff --cached`.
- **Goal.** The goal in the requester's own words, quoted from the user's request, the issue, or the Motivation section of the PR body.
- **Rules.** The mode from section 2 and the paths of the guide files from section 3.
- **Instructions.** The checklist instructions below and the report form in section 7.

Leave out every other account of the change. That includes the author's description of the design, lists of new modules or functions, the planned structure, the reasons for choices, and earlier review findings. A reviewer that needs context reads the code.

When the environment cannot start a separate reviewer, run the checklists in this session. Say in the report's opening line that the review was not independent. A session started only for this review, such as one that `claude-worker` starts from Codex, has no account of the change. It runs the checklists itself and counts as a fresh reviewer.

### Checklist instructions

Run the checklist of each loaded file in stage order: Functionality, Factoring, Prose, History, then the PR or import body. Each item is a question, and a no is a finding that cites the item's rules.

A phase review runs only the items for what that phase owns:

- **Code phase.** The Functionality and Factoring checklists. The comment items of Prose, for inline comments. From History, each commit's type under R.commit-format.classification and its scope under R.change-scope.
- **Prose phase.** The comment items of Prose, for docstrings. The general writing items, for docstrings, commit bodies and the PR body. The rest of History, and the PR checklist. R.evidence applies only to what the messages and the PR body claim.

Read commit messages and any PR body or draft only after finishing the code checklists. Both give the author's account of the change.

Findings cover only what the scope adds, changes, or removes. Read unchanged code for context, but report on it only to show a site that an incomplete edit missed or an existing function that the change repeats.

Report each finding at the stage where its cause lies. A name that cannot be made accurate is a Factoring finding, or a Functionality finding when the code does something other than its name says. A comment that explains confusing control flow is a Factoring finding. A commit whose subject needs "X and Y" is a scope finding.

In a branch review, run the History checklist for each commit and once for the branch. Find the commit that a `Fixes:` record should name by blaming or searching the history of the lines the fix changes. Do not claim that a commit builds without evidence.

When the branch has a PR body or draft, compare the branch with it under R.pr-body.plan. Read the open PR's body with `gh pr view --json body`, or the draft file that the argument names. Without either, skip the comparison and say so.

## 5. Check the findings

Check each finding against the code before reporting it. Read the cited lines, and keep each finding the code confirms. Drop a finding the code contradicts, and list it at the end of the report with one sentence on what the code shows.

Keep a finding that questions the design, even when it challenges an earlier decision. A decision made before the code existed does not settle a finding about the code. Report it, and let the user decide.

## 6. Run the checks

Run the script for the rules marked `[auto]`, and report its output as findings under the rules it names. In a phase review, report only findings owned by that phase.

```bash
python3 /Users/kunjeong/Code/1_resources/contribution-guides/skills/review-changes/check_auto.py <base>..<tip>
python3 /Users/kunjeong/Code/1_resources/contribution-guides/skills/review-changes/check_auto.py --staged
```

With the `checks` argument, also run the build and the quick tests that the repository defines, through the `build-runner` agent when it is available. Without that argument, check that the evidence R.evidence asks for exists, and report what is missing.

## 7. Report

Open with one line that names the scope, the mode, the guides loaded, and whether a fresh reviewer ran the checklists. Then list findings grouped by stage, in stage order. Mark a finding that depends on an earlier one, since fixing the earlier one may remove it.

Each finding has three parts:

- **Where.** A clickable `path:line`, or the commit.
- **What.** The problem and the rule it breaks, with the rule ID linked to its file.
- **Fix.** A concrete change, as a short diff or replacement text.

For docstrings, commit messages and PR bodies, describe the required change without drafting replacement text. Mark requests for missing content for the user to decide.

In a prose-phase review, list the findings labeled `Code phase:` last.

Leave out a stage with no findings. When nothing is found, say so in one line.

Applying fixes is follow-up work after the report, not part of this skill.
