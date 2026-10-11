# Revert a commit

Applies the inverse of the changes introduced by a given commit,
equivalent to `git revert <commit>`. The commit must be reachable from
the current HEAD.

## Usage

``` r
git_revert(ref, commit = TRUE, ..., repo = ".")
```

## Arguments

- ref:

  revision string with a branch/tag/commit value

- commit:

  if `FALSE`, stage the reverted changes without creating a commit.
  Default is `TRUE`, that is to say, by default a commit is made.

- ...:

  parameters passed to `git_commit` such as `message` or `author`

- repo:

  The path to the git repository. If the directory is not a repository,
  parent directories are considered (see
  [`git_find()`](https://docs.ropensci.org/gert/reference/git_repo.md)).
  To disable this search, provide the filepath protected with
  [`I()`](https://rdrr.io/r/base/AsIs.html). When using this parameter,
  always explicitly call by name (i.e. `repo = `) because future
  versions of gert may have additional parameters.

## Value

The SHA of the new revert commit (invisibly), or `NULL` when
`commit = FALSE`.

## Details

By default, a new revert commit is created immediately. Set
`commit = FALSE` to only stage the reverted changes without committing,
leaving you free to amend or combine them before calling
[`git_commit()`](https://docs.ropensci.org/gert/reference/git_commit.md).

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
[`git_restore()`](https://docs.ropensci.org/gert/reference/git_restore.md),
[`git_signature()`](https://docs.ropensci.org/gert/reference/git_signature.md),
[`git_stash`](https://docs.ropensci.org/gert/reference/git_stash.md),
[`git_tag`](https://docs.ropensci.org/gert/reference/git_tag.md),
[`git_worktree`](https://docs.ropensci.org/gert/reference/git_worktree.md)

## Related libgit2 documentation

[`revert`](https://libgit2.org/docs/reference/main/revert/index.html).

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

writeLines("world", file.path(repo, "hello.txt"))
git_add("hello.txt", repo = repo)
bad_commit <- git_commit("Second commit", repo = repo)

# Default: revert and commit with an auto-generated message
git_revert(bad_commit, repo = repo)
git_log(repo = repo)

# Revert with a custom message
writeLines("oops", file.path(repo, "hello.txt"))
git_add("hello.txt", repo = repo)
bad_commit2 <- git_commit("Third commit", repo = repo)
git_revert(bad_commit2, message = "Undo third commit\n", repo = repo)
git_log(repo = repo)

# Stage the revert without committing
writeLines("again", file.path(repo, "hello.txt"))
git_add("hello.txt", repo = repo)
bad_commit3 <- git_commit("Fourth commit", repo = repo)
git_revert(bad_commit3, commit = FALSE, repo = repo)
git_status(repo = repo)

unlink(repo, recursive = TRUE)
}
```
