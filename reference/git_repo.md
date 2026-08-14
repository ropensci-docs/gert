# Create or discover a local Git repository

- `git_init()` creates a new repository

- `git_find()` to discover an existing local repository.

- `git_info()` shows basic information about a repository, such as the
  SHA and branch of the current HEAD.

## Usage

``` r
git_init(path = ".", bare = FALSE)

git_find(path = ".")

git_info(repo = ".")
```

## Arguments

- path:

  the location of the git repository, see the "path" section.

- bare:

  if true, a Git repository without a working directory is created

- repo:

  The path to the git repository. If the directory is not a repository,
  parent directories are considered (see `git_find()`). To disable this
  search, provide the filepath protected with
  [`I()`](https://rdrr.io/r/base/AsIs.html). When using this parameter,
  always explicitly call by name (i.e. `repo = `) because future
  versions of gert may have additional parameters.

## Value

- `git_find()` and `git_init()`: the path to the Git repository.

- `git_info()`: A list of information of the Git repository.

## Path

For `git_init()` the `path` parameter sets the directory of the git
repository to create. If this directory already exists, it must be
empty. If it does not exist, it is created, along with any intermediate
directories that don't yet exist.

For `git_find()`, the `path` parameter specifies the directory at which
to start the search for a git repository. If it is not a git repository
itself, then its parent directory is consulted, then the parent's
parent, and so on.

## Detached head

If `git_info()$shorthand` is equal to `HEAD`, it means the repository is
in a [detached head
state](https://jvns.ca/blog/2023/11/01/confusing-git-terminology/#detached-head-state).

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
[`git_reset()`](https://docs.ropensci.org/gert/reference/git_reset.md),
[`git_restore()`](https://docs.ropensci.org/gert/reference/git_restore.md),
[`git_revert()`](https://docs.ropensci.org/gert/reference/git_revert.md),
[`git_signature()`](https://docs.ropensci.org/gert/reference/git_signature.md),
[`git_stash`](https://docs.ropensci.org/gert/reference/git_stash.md),
[`git_tag`](https://docs.ropensci.org/gert/reference/git_tag.md),
[`git_worktree`](https://docs.ropensci.org/gert/reference/git_worktree.md)

## Related libgit2 documentation

[`repository`](https://libgit2.org/docs/reference/main/repository/index.html).

## Examples

``` r
# directory does not yet exist
r <- tempfile(pattern = "gert")
git_init(r)
git_find(r)
#> [1] "/tmp/RtmpFnfi9o/gert6eb29330e78"
git_info(r)
#> $path
#> [1] "/tmp/RtmpFnfi9o/gert6eb29330e78/"
#> 
#> $bare
#> [1] FALSE
#> 
#> $head
#> [1] NA
#> 
#> $shorthand
#> [1] NA
#> 
#> $commit
#> [1] NA
#> 
#> $remote
#> [1] NA
#> 
#> $upstream
#> [1] NA
#> 
#> $reflist
#> character(0)
#> 

# create a child directory, then a grandchild, then search
r_grandchild_dir <- file.path(r, "aaa", "bbb")
dir.create(r_grandchild_dir, recursive = TRUE)
git_find(r_grandchild_dir)
#> [1] "/tmp/RtmpFnfi9o/gert6eb29330e78"

# cleanup
unlink(r, recursive = TRUE)

# directory exists but is empty
r <- tempfile(pattern = "gert")
dir.create(r)
git_init(r)
git_find(r)
#> [1] "/tmp/RtmpFnfi9o/gert6eb7b461c0e"

# cleanup
unlink(r, recursive = TRUE)
```
