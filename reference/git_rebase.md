# Cherry-Pick and Rebase

- `git_cherry_pick()` applies the changes from a given commit (from
  another branch) onto the current branch. \*`git_rebase_commit()`
  resets the branch to the state of another branch (upstream) and then
  re-applies your local changes by cherry-picking each of your local
  commits onto the upstream commit history. \*`git_rebase_list()` shows
  your local commits that are missing from the `upstream` history, and
  if they conflict with upstream changes.

## Usage

``` r
git_rebase_list(upstream = NULL, repo = ".")

git_rebase_commit(upstream = NULL, repo = ".")

git_cherry_pick(commit, repo = ".")

git_ahead_behind(upstream = NULL, ref = "HEAD", repo = ".")
```

## Arguments

- upstream:

  branch to which you want to rewind and re-apply your local commits.
  The default uses the remote upstream branch with the current state on
  the git server, simulating
  [`git_pull()`](https://docs.ropensci.org/gert/reference/git_fetch.md).

- repo:

  The path to the git repository. If the directory is not a repository,
  parent directories are considered (see
  [`git_find()`](https://docs.ropensci.org/gert/reference/git_repo.md)).
  To disable this search, provide the filepath protected with
  [`I()`](https://rdrr.io/r/base/AsIs.html). When using this parameter,
  always explicitly call by name (i.e. `repo = `) because future
  versions of gert may have additional parameters.

- commit:

  id of the commit to cherry pick

- ref:

  string with a branch/tag/commit

## Details

To find if your local commits are missing from `upstream`,
`git_rebase_list()` first performs a rebase dry-run, without committing
anything. If there are no conflicts, you can use `git_rebase_commit()`
to rewind and rebase your branch onto `upstream`.

Gert only support a clean rebase; it never leaves the repository in
unfinished "rebasing" state. If conflicts arise, `git_rebase_commit()`
will raise an error without making changes.

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
[`git_merge()`](https://docs.ropensci.org/gert/reference/git_merge.md),
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

[`rebase`](https://libgit2.org/docs/reference/main/rebase/index.html),
[`cherrypick`](https://libgit2.org/docs/reference/main/cherrypick/index.html),
[`graph`](https://libgit2.org/docs/reference/main/graph/index.html).
