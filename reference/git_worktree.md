# Git Worktrees

Worktrees represent an alternative location to checkout a branch into.
Rather than checking out a branch in your main working tree (which
changes the branch you are currently on and forces you to stash any
existing work), you can instead check that branch out into a separate
*linked worktree* with its own working tree. Practically, a worktree is
just a separate folder that a branch is checked out into, with some
extra git metadata that links it back to the main working tree.

`git_worktree_list()` returns a data frame of information about the
worktrees linked to the main working tree.

`git_worktree_exists()` lets you check whether or not a worktree by the
name of `name` exists for this `repo`.

`git_worktree_path()` returns the file path to the worktree.

`git_worktree_add()` creates a new worktree called `name` in the folder
pointed to by `path`, and checks `branch` out into it.

`git_worktree_remove()` removes a worktree. It does so by deleting the
folder provided as the `path` to `git_worktree_add()`, and then cleaning
up some git metadata in the main working tree that linked the main
working tree to the removed worktree. The `branch` checked out by the
worktree is not deleted. Note that this is just a wrapper around
`git_worktree_prune()` that sets some desirable defaults for aggressive
removal.

`git_worktree_prune()` is more cautious than `git_worktree_remove()`. It
refuses to prune *valid* or *locked* worktrees by default, and also
refuses the delete the working tree of the worktree by default (i.e. the
folder at `path`). It is automatically run by git itself on periodic
intervals to prune outdated worktrees. For interactive usage, you
typically want `git_worktree_remove()` instead.
`git_worktree_is_prunable()` lets you check if a worktree is prunable
with the given options.

`git_worktree_lock()`, `git_worktree_unlock()`, and
`git_worktree_is_locked()` help you manage whether or not a worktree is
*locked*. When a worktree is locked, it is not automatically cleaned up
by `git_worktree_prune()` (and git itself) on periodic intervals, even
when it looks *invalid*. This is typically only useful when your
worktree is on a hard drive that isn't always connected (which can make
it look *invalid* when disconnected, typically making it a candidate for
automatic pruning).

`git_worktree_is_valid()` checks whether a worktree is valid or not. A
*valid* worktree requires both the git data structures inside the main
working tree and this worktree to be present.

## Usage

``` r
git_worktree_list(repo = ".")

git_worktree_exists(name, repo = ".")

git_worktree_path(name, repo = ".")

git_worktree_add(name, path, branch, lock = FALSE, local = TRUE, repo = ".")

git_worktree_remove(name, repo = ".")

git_worktree_prune(
  name,
  prune_valid = FALSE,
  prune_locked = FALSE,
  prune_working_tree = FALSE,
  repo = "."
)

git_worktree_is_prunable(
  name,
  prune_valid = FALSE,
  prune_locked = FALSE,
  repo = "."
)

git_worktree_lock(name, repo = ".")

git_worktree_unlock(name, repo = ".")

git_worktree_is_locked(name, repo = ".")

git_worktree_is_valid(name, repo = ".")
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

- name:

  The name of the worktree.

- path:

  The path to checkout `branch` into. Importantly, the path up to the
  folder name must exist, but the folder name itself must not exist yet
  and will be created.

- branch:

  The branch to checkout into `path`.

- lock:

  Whether or not to lock the worktree on creation.

- local:

  set TRUE to only check for local branches, FALSE to check for remote
  branches. Use NULL to return all branches.

- prune_valid:

  Whether or not to forcibly prune a *valid* worktree.

- prune_locked:

  Whether or not to forcibly prune a *locked* worktree.

- prune_working_tree:

  Whether or not to also remove the folder that the worktree was using,
  i.e. the `path` supplied to `git_worktree_add()`.

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
[`git_revert()`](https://docs.ropensci.org/gert/reference/git_revert.md),
[`git_signature()`](https://docs.ropensci.org/gert/reference/git_signature.md),
[`git_stash`](https://docs.ropensci.org/gert/reference/git_stash.md),
[`git_tag`](https://docs.ropensci.org/gert/reference/git_tag.md)

## Related libgit2 documentation

[`worktree`](https://libgit2.org/docs/reference/main/worktree/index.html).

## Examples

``` r
repo <- git_init(tempfile("gert-examples-repo"))

writeLines("hello", file.path(repo, 'hello.txt'))
git_add('hello.txt', repo = repo)
#> # A tibble: 1 × 3
#>   file      status staged
#>   <chr>     <chr>  <lgl> 
#> 1 hello.txt new    TRUE  
git_commit("First commit", author = "jeroen <jeroen@blabla.nl>", repo = repo)
#> [1] "f2171903695598ad692b901c1d6102ceb3ceb379"

# Create a branch that is going to be used for the worktree,
# but don't check it out!
git_branch_create(branch = "branch", checkout = FALSE, repo = repo)

path <- tempfile("gert-examples-worktree")

# Add a worktree for this branch
git_worktree_add(
  name = "worktree",
  path = path,
  branch = "branch",
  repo = repo
)

# Worktree info
git_worktree_list(repo = repo)
#> # A tibble: 1 × 4
#>   name     path                                              valid locked
#> * <chr>    <chr>                                             <lgl> <lgl> 
#> 1 worktree /tmp/RtmpFnfi9o/gert-examples-worktree6eb1d258da3 TRUE  FALSE 

# Note how the files are checked out here
dir(path, all.files = TRUE)
#> [1] "."         ".."        ".git"      "hello.txt"

# And the branch that we are on at `path` is `"branch"`
git_branch(repo = path)
#> [1] "branch"

# Cleanup worktree, and the folder at `path`
git_worktree_remove("worktree", repo = repo)

# Cleanup repo
unlink(repo, recursive = TRUE)
```
