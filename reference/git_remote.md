# Git Remotes

List, add, configure, or remove remotes.

## Usage

``` r
git_remote_list(repo = ".")

git_remote_add(url, name = "origin", refspec = NULL, repo = ".")

git_remote_remove(remote, repo = ".")

git_remote_info(remote = NULL, repo = ".")

git_remote_set_url(url, remote = NULL, repo = ".")

git_remote_set_pushurl(url, remote = NULL, add = FALSE, repo = ".")

git_remote_refspecs(remote = NULL, repo = ".")
```

## Arguments

- repo:

  The path to the git repository. If the directory is not a repository,
  parent directories are considered (see
  [`git_find()`](https://docs.ropensci.org/gert/reference/git_repo.md)).
  To disable this search, provide the filepath protected with
  [`I()`](https://rdrr.io/r/base/AsIs.html). When using this parameter,
  always explicitly call by name (i.e. `repo = `) because future
  versions of gert may have additional parameters.

- url:

  server url (https or ssh)

- name:

  unique name for the new remote

- refspec:

  optional string with the remote fetch value

- remote:

  name of an existing remote. Default `NULL` means the remote from the
  upstream of the current branch.

- add:

  if `TRUE`, append the push URL instead of replacing it. Equivalent to
  `git remote set-url --push --add`.

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
[`git_rebase()`](https://docs.ropensci.org/gert/reference/git_rebase.md),
[`git_repo`](https://docs.ropensci.org/gert/reference/git_repo.md),
[`git_reset()`](https://docs.ropensci.org/gert/reference/git_reset.md),
[`git_restore()`](https://docs.ropensci.org/gert/reference/git_restore.md),
[`git_revert()`](https://docs.ropensci.org/gert/reference/git_revert.md),
[`git_signature()`](https://docs.ropensci.org/gert/reference/git_signature.md),
[`git_stash`](https://docs.ropensci.org/gert/reference/git_stash.md),
[`git_tag`](https://docs.ropensci.org/gert/reference/git_tag.md),
[`git_worktree`](https://docs.ropensci.org/gert/reference/git_worktree.md)

## Related libgit2 documentation

[`remote`](https://libgit2.org/docs/reference/main/remote/index.html).
