---
name: pull
description: Bring the current branch up to date by merging its upstream, keeping uncommitted work and both sides of every conflict.
disable-model-invocation: true
---

Goal: the branch is up to date with its upstream and nothing that existed before the pull is gone. Committed work, uncommitted changes and untracked files all survive. Merge rather than rebase, so both histories stay intact.

The user typing `/pull` is the approval for every command below. Do not ask for it again.

## 1. Anchor

```sh
git status --short --branch
git rev-parse HEAD
git stash list
```

Note the HEAD SHA, it is what step 6 compares against and the way back if the merge goes wrong. Note which stash entries already existed too, those are not yours to touch.

## 2. Park uncommitted work

Skip this when the tree is clean. Otherwise:

```sh
git stash push -u -m "pull: <short SHA>"
```

`-u` takes untracked files along. The entry stays until step 6 confirms the work landed again.

## 3. See what you are merging

```sh
git fetch
git rev-parse --abbrev-ref '@{u}'
git log --oneline HEAD..@{u}
git log --oneline @{u}..HEAD
```

- No upstream configured: restore the stash, report, stop. Picking a remote branch is the user's call.
- `HEAD..@{u}` empty: nothing to pull. Restore the stash and report that the branch is already current.
- Both ranges non-empty: the histories diverged and step 4 does real work.

## 4. Merge

```sh
git pull --no-rebase
```

The flag is deliberate. A rebase rewrites the local commits, and a fast-forward-only pull just refuses when the branches diverged. It overrides `pull.rebase` for this run only and leaves the repo config alone.

## 5. Resolve, keeping both sides

Default: every conflict ends with both changes present in the file. Dropping a side is the exception you have to justify.

Walk the conflicted files (`git diff --name-only --diff-filter=U`) one at a time:

- Read the full hunk and enough surrounding code to see what each side was doing.
- Combine them: both imports, both functions, both list entries, both config keys, ordered the way the rest of the file is ordered.
- When both sides set the same single value differently they cannot both survive. Take the incoming one and name the file, the value and your choice in the report.
- Leave the file valid in its language: no conflict markers, no declaration or key that now exists twice.

`git checkout --merge -- <file>` puts the markers back when you lose them. `git merge --abort` returns to the anchor SHA when the merge turns out to be the wrong move.

Then `git add` the resolved files and `git commit --no-edit`, keeping the merge message git wrote.

## 6. Unpark and verify

`git stash pop` only works once the merge is committed, so this comes after step 5. Conflicts from the pop get the same treatment as step 5. A conflicting pop keeps its stash entry, which is exactly the safety net you want, so drop it by ref only after the files below check out.

```sh
git status --short --branch
git stash list
git log --oneline <anchor SHA>..HEAD
```

- Every file that step 1 listed as modified or untracked is back, with its content.
- The local commits from step 3 are still in the log.
- No stash entry of yours is left over.

## 7. Report

Branch and upstream, how many commits came in, which files conflicted and how each one was resolved, and every place you had to pick a side. Committing further and pushing are the user's call.
