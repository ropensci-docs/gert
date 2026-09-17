# Get or set Git configuration

Get, set, or unset Git options, as `git config` does on the command
line. **Global** settings affect all of a user's Git operations
(`git config --global`), whereas **local** settings are scoped to a
specific repository (`git config --local`). When both exist, local
options always win.

|  |  |  |
|----|----|----|
|  | **local** | **global** |
| get all | `git_config()` | `git_config_global()` |
| get one (local+global) | `git_config_get()` | `git_config_get()` |
| get one (local or global only) | `git_config_local_get()` | `git_config_global_get()` |
| set | `git_config_set()` | `git_config_global_set()` |
| unset | `git_config_unset()` | `git_config_global_unset()` |

## Usage

``` r
git_config(repo = ".")

git_config_global()

git_config_get(name, repo = ".")

git_config_local_get(name, repo = ".")

git_config_global_get(name)

git_config_set(name, value, add = FALSE, repo = ".")

git_config_global_set(name, value, add = FALSE)

git_config_unset(name, pattern = NULL, repo = ".")

git_config_global_unset(name, pattern = NULL)
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

  Name of the option to get or set

- value:

  Value to set. Must be a string, logical, number or `NULL` (to unset).

- add:

  if `TRUE`, append a new entry for `name` instead of replacing existing
  one(s). Equivalent to `git config --add`. Only supported for string
  values.

- pattern:

  optional regular expression, for matching values to unset in case of
  multiple values

## Value

- `git_config()`: a `data.frame` of the Git options "in force" in the
  context of `repo`, one row per option. The `level` column reveals
  whether the option is determined from global or local config.

- `git_config_global()`: a `data.frame`, as for `git_config()`, except
  only for global Git options.

- `git_config_get()`: the value of the named option considering both
  local and global config (local wins), or `NULL` if unset.

- `git_config_local_get()`: as for `git_config_get()`, but restricted to
  local (repository-level) config only.

- `git_config_global_get()`: as for `git_config_get()`, but for global
  config only.

- `git_config_set()`, `git_config_global_set()`: The previous value(s)
  of `name` in local or global config, respectively. If this option was
  previously unset, returns `NULL`. Returns invisibly.

- `git_config_unset()`, `git_config_global_unset()`: The previous
  value(s) of `name` that were unset. Returns invisibly.

## Note

All entries in the `name` column are automatically normalised to
lowercase (see <https://libgit2.org/libgit2/#HEAD/type/git_config_entry>
for details).

## See also

Other git:
[`git_archive`](https://docs.ropensci.org/gert/reference/git_archive.md),
[`git_branch()`](https://docs.ropensci.org/gert/reference/git_branch.md),
[`git_commit()`](https://docs.ropensci.org/gert/reference/git_commit.md),
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

[`config`](https://libgit2.org/docs/reference/main/config/index.html).

## Examples

``` r
# Set and inspect a local, custom Git option
r <- file.path(tempdir(), "gert-demo")
git_init(r)

previous <- git_config_set("aaa.bbb", "ccc", repo = r)
previous
#> NULL
git_config_local_get("aaa.bbb", repo = r)
#> [1] "ccc"

previous <- git_config_set("aaa.bbb", NULL, repo = r)
previous
#> [1] "ccc"
git_config_local_get("aaa.bbb", repo = r)
#> NULL

# Get a single named option (returns NULL if unset)
git_config_get("aaa.bbb", repo = r)
#> NULL
git_config_set("aaa.bbb", "ccc", repo = r)
git_config_get("aaa.bbb", repo = r)
#> [1] "ccc"

unlink(r, recursive = TRUE)

if (FALSE) { # \dontrun{
# Set global Git options
git_config_global_set("user.name", "Your Name")
git_config_global_set("user.email", "your@email.com")
git_config_global()

# Get a single global option (returns NULL if unset)
git_config_global_get("user.name")
git_config_global_get("gert.nonexistent")
} # }
```
