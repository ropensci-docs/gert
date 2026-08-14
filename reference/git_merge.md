# Git merge

Use `git_merge()` to merge a branch into the current head. Based on how
the branches have diverged, the function will select a fast-forward or
merge-commit strategy.

Other functions are more low-level tools that are used by `git_merge()`:

- `git_merge_find_base()` looks up the commit where two branches have
  diverged (i.e. the youngest common ancestor).

- `git_merge_analysis()` is used to test if a merge can simply be fast
  forwarded or not.

- `git_merge_stage_only()` applies and stages changes, without
  committing or fast-forwarding.

- `git_conflicts()` lists merge conflicts.

## Usage

``` r
git_merge(ref, commit = TRUE, squash = FALSE, repo = ".")

git_merge_stage_only(ref, squash = FALSE, repo = ".")

git_merge_find_base(ref, target = "HEAD", repo = ".")

git_merge_analysis(ref, repo = ".")

git_merge_abort(repo = ".")

git_commit_descendant_of(ancestor, ref = "HEAD", repo = ".")

git_conflicts(repo = ".")
```

## Arguments

- ref:

  branch or commit that you want to merge

- commit:

  automatically create a merge commit if the merge succeeds without
  conflicts. Set this to `FALSE` if you want to customize your commit
  message/author.

- squash:

  omits the second parent from the commit, which make the merge a
  regular single-parent commit.

- repo:

  The path to the git repository. If the directory is not a repository,
  parent directories are considered (see
  [`git_find()`](https://docs.ropensci.org/gert/reference/git_repo.md)).
  To disable this search, provide the filepath protected with
  [`I()`](https://rdrr.io/r/base/AsIs.html). When using this parameter,
  always explicitly call by name (i.e. `repo = `) because future
  versions of gert may have additional parameters.

- target:

  the branch where you want to merge into. Defaults to current `HEAD`.

- ancestor:

  a reference to a potential ancestor commit

## Details

By default `git_merge()` automatically commits the merge commit upon
success. However if the merge fails with merge-conflicts, or if `commit`
is set to `FALSE`, the changes are staged and the repository is put in
merging state, and you have to manually run
[`git_commit()`](https://docs.ropensci.org/gert/reference/git_commit.md)
or `git_merge_abort()` to proceed.

## See also

Other git:
[`git_archive`](https://docs.ropensci.org/gert/reference/git_archive.md),
[`git_branch()`](https://docs.ropensci.org/gert/reference/git_branch.md),
[`git_commit()`](https://docs.ropensci.org/gert/reference/git_commit.md),
[`git_config()`](https://docs.ropensci.org/gert/reference/git_config.md),
[`git_diff()`](https://docs.ropensci.org/gert/reference/git_diff.md),
[`git_fetch()`](https://docs.ropensci.org/gert/reference/git_fetch.md),
[`git_history`](https://docs.ropensci.org/gert/reference/git_history.md),
[`git_ignore`](https://docs.ropensci.org/gert/reference/git_ignore.md),
[`git_rebase()`](https://docs.ropensci.org/gert/reference/git_rebase.md),
[`git_remote`](https://docs.ropensci.org/gert/reference/git_remote.md),
[`git_repo`](https://docs.ropensci.org/gert/reference/git_repo.md),
[`git_reset()`](https://docs.ropensci.org/gert/reference/git_reset.md),
[`git_restore()`](https://docs.ropensci.org/gert/reference/git_restore.md),
[`git_revert()`](https://docs.ropensci.org/gert/reference/git_revert.md),
[`git_signature()`](https://docs.ropensci.org/gert/reference/git_signature.md),
[`git_stash`](https://docs.ropensci.org/gert/reference/git_stash.md),
[`git_tag`](https://docs.ropensci.org/gert/reference/git_tag.md),
[`git_worktree`](https://docs.ropensci.org/gert/reference/git_worktree.md)

## Related libgit2 documentation

[`merge`](https://libgit2.org/docs/reference/main/merge/index.html).
