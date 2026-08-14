# Restore working tree files

Restores specified paths in the working tree from a given ref,
equivalent to `git restore --source=<ref> <path>` (or the older
`git checkout <ref> -- <path>`). The ref must be reachable from the
current HEAD. By default restores from HEAD, discarding any local
modifications.

## Usage

``` r
git_restore(path, ref = "HEAD", repo = ".")
```

## Arguments

- path:

  character vector with file paths to restore, relative to the
  repository root. Use `"."` to restore all tracked files.

- ref:

  revision string with a branch/tag/commit to restore from. Defaults to
  `"HEAD"`.

- repo:

  The path to the git repository. If the directory is not a repository,
  parent directories are considered (see
  [`git_find()`](https://docs.ropensci.org/gert/reference/git_repo.md)).
  To disable this search, provide the filepath protected with
  [`I()`](https://rdrr.io/r/base/AsIs.html). When using this parameter,
  always explicitly call by name (i.e. `repo = `) because future
  versions of gert may have additional parameters.

## Value

Invisibly, the
[`git_status()`](https://docs.ropensci.org/gert/reference/git_commit.md)
after restoring.

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
[`git_remote`](https://docs.ropensci.org/gert/reference/git_remote.md),
[`git_repo`](https://docs.ropensci.org/gert/reference/git_repo.md),
[`git_reset()`](https://docs.ropensci.org/gert/reference/git_reset.md),
[`git_revert()`](https://docs.ropensci.org/gert/reference/git_revert.md),
[`git_signature()`](https://docs.ropensci.org/gert/reference/git_signature.md),
[`git_stash`](https://docs.ropensci.org/gert/reference/git_stash.md),
[`git_tag`](https://docs.ropensci.org/gert/reference/git_tag.md),
[`git_worktree`](https://docs.ropensci.org/gert/reference/git_worktree.md)

## Examples

``` r
if (FALSE) { # interactive()
repo <- file.path(tempdir(), "myrepo")
git_init(repo)

# Set a user if no default
if (!user_is_configured()) {
  git_config_set("user.name", "Jerry")
  git_config_set("user.email", "jerry@gmail.com")
}

writeLines("hello", file.path(repo, "hello.txt"))
git_add("hello.txt", repo = repo)
git_commit("First commit", repo = repo)

# Modify the file, then restore it from HEAD
writeLines("oops", file.path(repo, "hello.txt"))
git_restore("hello.txt", repo = repo)
readLines(file.path(repo, "hello.txt"))  # "hello"

unlink(repo, recursive = TRUE)
}
```
