# Git Branch

Create, list, and checkout branches.

## Usage

``` r
git_branch(repo = ".")

git_branch_list(local = NULL, repo = ".")

git_branch_checkout(branch, force = FALSE, orphan = FALSE, repo = ".")

git_branch_switch(branch, force = FALSE, orphan = FALSE, repo = ".")

git_branch_create(
  branch,
  ref = "HEAD",
  checkout = TRUE,
  force = FALSE,
  repo = "."
)

git_branch_delete(branch, repo = ".")

git_branch_move(branch, new_branch, force = FALSE, repo = ".")

git_branch_fast_forward(ref, repo = ".")

git_branch_set_upstream(upstream, branch = git_branch(repo), repo = ".")

git_branch_exists(branch, local = TRUE, repo = ".")
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

- local:

  set TRUE to only check for local branches, FALSE to check for remote
  branches. Use NULL to return all branches.

- branch:

  name of branch to check out

- force:

  overwrite existing branch

- orphan:

  if branch does not exist, checkout unborn branch

- ref:

  string with a branch/tag/commit

- checkout:

  move HEAD to the newly created branch

- new_branch:

  target name of the branch once the move is performed; this name is
  validated for consistency.

- upstream:

  remote branch from git_branch_list, for example `"origin/master"`

## See also

Other git:
[`git_archive`](https://docs.ropensci.org/gert/reference/git_archive.md),
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
[`git_revert()`](https://docs.ropensci.org/gert/reference/git_revert.md),
[`git_signature()`](https://docs.ropensci.org/gert/reference/git_signature.md),
[`git_stash`](https://docs.ropensci.org/gert/reference/git_stash.md),
[`git_tag`](https://docs.ropensci.org/gert/reference/git_tag.md),
[`git_worktree`](https://docs.ropensci.org/gert/reference/git_worktree.md)

## Related libgit2 documentation

[`branch`](https://libgit2.org/docs/reference/main/branch/index.html),
[`checkout`](https://libgit2.org/docs/reference/main/checkout/index.html).

## Examples

``` r
if (FALSE) { # interactive()
# Creating a branch
repo <- file.path(tempdir(), "myrepo")
git_init(repo)
writeLines("hello", file.path(repo, "hello.txt"))
git_add("hello.txt", repo = repo)
first_commit <- git_commit("First commit", repo = repo)

git_branch_create("new-feat", repo = repo)
writeLines("world", file.path(repo, "hello.txt"))
git_add("hello.txt", repo = repo)
second_commit <- git_commit("Second commit", repo = repo)

# Changing branches
git_branch(repo = repo)
git_branch_switch("main", repo = repo)
git_branch(repo = repo)

git_branch_exists("new-feat", repo = repo)

# Listing branches
git_branch_list(repo = repo)

# Renaming a branch
git_branch_move("new-feat", "better-name", repo = repo)
git_branch_exists("new-feat", repo = repo)
git_branch_list(repo = repo)

# Deleting a branch
git_branch_delete("better-name", repo = repo)
git_branch_exists("better-name", repo = repo)

# clean up
unlink(repo, recursive = TRUE)
# ------------------------
# Creating an orphan branch
repo <- file.path(tempdir(), "myrepo")
git_init(repo)

# Set a user if no default
if (!user_is_configured()) {
  git_config_set("user.name", "Jerry")
  git_config_set("user.email", "jerry@gmail.com")
}
writeLines("hello", file.path(repo, "hello.txt"))
git_add("hello.txt", repo = repo)
first_commit <- git_commit("First commit", repo = repo)

writeLines("world", file.path(repo, "hello.txt"))
git_add("hello.txt", repo = repo)
second_commit <- git_commit("Second commit", repo = repo)

# Check out first commit
git_branch_checkout(first_commit, orphan = TRUE, repo = repo)
git_status(repo)
# clean up
unlink(repo, recursive = TRUE)
}
```
