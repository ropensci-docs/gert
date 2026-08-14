# Author Signature

A signature contains the author and timestamp of a commit. Each commit
includes a signature of the author and committer (which can be
identical).

## Usage

``` r
git_signature_default(repo = ".")

git_signature(name, email, time = NULL)

git_signature_parse(sig)
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

  Real name of the committer

- email:

  Email address of the committer

- time:

  timestamp of class POSIXt or NULL

- sig:

  string in proper `"First Last <your@email.com>"` format, see details.

## Details

A signature string has format `"Real Name <email> timestamp tzoffset"`.
The `timestamp tzoffset` piece can be omitted in which case the current
local time is used. If not omitted, `timestamp` must contain the number
of seconds since the Unix epoch and `tzoffset` is the timezone offset in
`hhmm` format (note the lack of a colon separator)

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
[`git_stash`](https://docs.ropensci.org/gert/reference/git_stash.md),
[`git_tag`](https://docs.ropensci.org/gert/reference/git_tag.md),
[`git_worktree`](https://docs.ropensci.org/gert/reference/git_worktree.md)

## Related libgit2 documentation

[`signature`](https://libgit2.org/docs/reference/main/signature/index.html).

## Examples

``` r
# Your default user
try(git_signature_default())
#> Error in libgit2::git_signature_default : 
#>   config value 'user.name' was not found

# Specify explicit name and email
git_signature("Some committer", "sarah@gmail.com")
#> [git signature]
#> Author: Some committer <sarah@gmail.com>
#> Date: Fri Aug 14 18:36:09 2026 +0000

# Create signature for an hour ago
(sig <- git_signature("Han", "han@company.com", Sys.time() - 3600))
#> [git signature]
#> Author: Han <han@company.com>
#> Date: Fri Aug 14 17:36:09 2026 +0000

# Parse a signature
git_signature_parse(sig)
#> $name
#> [1] "Han"
#> 
#> $email
#> [1] "han@company.com"
#> 
#> $time
#> [1] "2026-08-14 17:36:09 UTC"
#> 
#> $offset
#> [1] 0
#> 
git_signature_parse("Emma <emma@mu.edu>")
#> $name
#> [1] "Emma"
#> 
#> $email
#> [1] "emma@mu.edu"
#> 
#> $time
#> [1] "2026-08-14 18:36:09 UTC"
#> 
#> $offset
#> [1] 0
#> 
```
