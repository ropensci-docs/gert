# Push and pull

Functions to connect with a git server (remote) to fetch or push
changes. The 'credentials' package is used to handle authentication, the
[credentials
vignette](https://docs.ropensci.org/credentials/articles/intro.html)
explains the various authentication methods for SSH and HTTPS remotes.

## Usage

``` r
git_fetch(
  remote = NULL,
  refspec = NULL,
  password = askpass,
  ssh_key = NULL,
  prune = FALSE,
  verbose = interactive(),
  repo = "."
)

git_remote_ls(
  remote = NULL,
  password = askpass,
  ssh_key = NULL,
  verbose = interactive(),
  repo = "."
)

git_push(
  remote = NULL,
  refspec = NULL,
  set_upstream = NULL,
  password = askpass,
  ssh_key = NULL,
  mirror = FALSE,
  force = FALSE,
  verbose = interactive(),
  repo = "."
)

git_clone(
  url,
  path = NULL,
  branch = NULL,
  password = askpass,
  ssh_key = NULL,
  bare = FALSE,
  mirror = FALSE,
  depth = 0,
  verbose = interactive()
)

git_pull(remote = NULL, rebase = FALSE, ..., repo = ".")
```

## Arguments

- remote:

  Optional. Name of a remote listed in
  [`git_remote_list()`](https://docs.ropensci.org/gert/reference/git_remote.md).
  If unspecified and the current branch is already tracking branch a
  remote branch, that remote is honored. Otherwise, defaults to
  `origin`.

- refspec:

  string with mapping between remote and local refs. Default uses the
  default refspec from the remote, which usually fetches all branches.

- password:

  a string or a callback function to get passwords for authentication or
  password protected ssh keys. Defaults to
  [askpass](https://r-lib.r-universe.dev/askpass/reference/askpass.html)
  which checks `getOption('askpass')`.

- ssh_key:

  path or object containing your ssh private key. By default we look for
  keys in `ssh-agent` and
  [`credentials::ssh_key_info()`](https://docs.ropensci.org/credentials/reference/ssh_credentials.html).

- prune:

  delete tracking branches that no longer exist on the remote, or are
  not in the refspec (such as pull requests).

- verbose:

  display some progress info while downloading

- repo:

  The path to the git repository. If the directory is not a repository,
  parent directories are considered (see
  [`git_find()`](https://docs.ropensci.org/gert/reference/git_repo.md)).
  To disable this search, provide the filepath protected with
  [`I()`](https://rdrr.io/r/base/AsIs.html). When using this parameter,
  always explicitly call by name (i.e. `repo = `) because future
  versions of gert may have additional parameters.

- set_upstream:

  change the branch default upstream to `remote`. If `NULL`, this will
  set the branch upstream only if the push was successful and if the
  branch does not have an upstream set yet.

- mirror:

  use the `--mirror` flag

- force:

  use the `--force` flag

- url:

  remote url. Typically starts with `https://github.com/` for public
  repositories, and `https://yourname@github.com/` or `git@github.com/`
  for private repos. You will be prompted for a password or pat when
  needed.

- path:

  Directory of the Git repository to create. By default, the "humanish"
  part of the URL. For instance, "git@github.com:someone/myrepo.git"
  will be cloned to `myrepo/`.

- branch:

  name of branch to check out locally

- bare:

  use the `--bare` flag

- depth:

  number of commits to fetch when creating a shallow clone. The default
  `0` clones the entire history. A positive value truncates the history
  to the given number of commits from the tip of each branch. Requires
  libgit2 \>= 1.7.0.

- rebase:

  if TRUE we try to rebase instead of merge local changes. This is not
  possible in case of conflicts (you will get an error).

- ...:

  arguments passed to `git_fetch()`

## Details

Use `git_fetch()` and `git_push()` to sync a local branch with a remote
branch. Here `git_pull()` is a wrapper for `git_fetch()` which then
tries to
[fast-forward](https://docs.ropensci.org/gert/reference/git_branch.md)
the local branch after fetching.

## See also

Other git:
[`git_archive`](https://docs.ropensci.org/gert/reference/git_archive.md),
[`git_branch()`](https://docs.ropensci.org/gert/reference/git_branch.md),
[`git_commit()`](https://docs.ropensci.org/gert/reference/git_commit.md),
[`git_config()`](https://docs.ropensci.org/gert/reference/git_config.md),
[`git_diff()`](https://docs.ropensci.org/gert/reference/git_diff.md),
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

[`remote`](https://libgit2.org/docs/reference/main/remote/index.html),
[`clone`](https://libgit2.org/docs/reference/main/clone/index.html).

## Examples

``` r
{# Clone a small repository
git_dir <- file.path(tempdir(), 'antiword')
git_clone('https://github.com/ropensci/antiword', git_dir)

# Change into the repo directory
olddir <- getwd()
setwd(git_dir)

# Show some stuff
git_log()
git_branch_list()
git_remote_list()

# Add a file
write.csv(iris, 'iris.csv')
git_add('iris.csv')

# Commit the change
jerry <- git_signature("Jerry", "jerry@hotmail.com")
git_commit('added the iris file', author = jerry)

# Now in the log:
git_log()

# Cleanup
setwd(olddir)
unlink(git_dir, recursive = TRUE)
}
```
