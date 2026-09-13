# View commit history

- `git_commit_stats()` returns information about commit insertion and
  deletion

- `git_commit_info()` a list of commit info

- `git_commit_id()` is a shortcut for `git_commit_info()$id`

- `git_log()` shows the most recent commits

- [`git_ls()`](https://docs.ropensci.org/gert/reference/git_commit.md)
  lists all the files that are being tracked in the repository.

- `git_stat_files()` shows information of when `files` was last
  modified.

## Usage

``` r
git_commit_info(ref = "HEAD", repo = ".")

git_commit_id(ref = "HEAD", repo = ".")

git_commit_stats(ref = "HEAD", repo = ".")

git_log(ref = "HEAD", max = 100, after = NULL, path = NULL, repo = ".")

git_stat_files(files, ref = "HEAD", max = NULL, repo = ".")
```

## Arguments

- ref:

  revision string with a branch/tag/commit value

- repo:

  The path to the git repository. If the directory is not a repository,
  parent directories are considered (see
  [`git_find()`](https://docs.ropensci.org/gert/reference/git_repo.md)).
  To disable this search, provide the filepath protected with
  [`I()`](https://rdrr.io/r/base/AsIs.html). When using this parameter,
  always explicitly call by name (i.e. `repo = `) because future
  versions of gert may have additional parameters.

- max:

  lookup at most latest n parent commits

- after:

  date or timestamp: only include commits starting this date

- path:

  character vector with paths to filter on; only commits that touch
  these paths are included

- files:

  vector of paths relative to the git root directory. Use `"."` to stage
  all changed files.

## Value

- `git_commit_info()` and `git_commit_stats()` return a list.

## See also

Other git:
[`git_archive`](https://docs.ropensci.org/gert/reference/git_archive.md),
[`git_branch()`](https://docs.ropensci.org/gert/reference/git_branch.md),
[`git_commit()`](https://docs.ropensci.org/gert/reference/git_commit.md),
[`git_config()`](https://docs.ropensci.org/gert/reference/git_config.md),
[`git_diff()`](https://docs.ropensci.org/gert/reference/git_diff.md),
[`git_fetch()`](https://docs.ropensci.org/gert/reference/git_fetch.md),
[`git_ignore`](https://docs.ropensci.org/gert/reference/git_ignore.md),
[`git_merge()`](https://docs.ropensci.org/gert/reference/git_merge.md),
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

[`commit`](https://libgit2.org/docs/reference/main/commit/index.html).
