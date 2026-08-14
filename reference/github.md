# GitHub Wrappers

Fetch and checkout pull requests.

## Usage

``` r
git_checkout_pull_request(pr = 1, remote = NULL, repo = ".")

git_fetch_pull_requests(pr = "*", remote = NULL, repo = ".")
```

## Arguments

- pr:

  number with PR to fetch or check out. Use `"*"` to fetch all pull
  requests.

- remote:

  Optional. Name of a remote listed in
  [`git_remote_list()`](https://docs.ropensci.org/gert/reference/git_remote.md).
  If unspecified and the current branch is already tracking branch a
  remote branch, that remote is honored. Otherwise, defaults to
  `origin`.

- repo:

  The path to the git repository. If the directory is not a repository,
  parent directories are considered (see
  [`git_find()`](https://docs.ropensci.org/gert/reference/git_repo.md)).
  To disable this search, provide the filepath protected with
  [`I()`](https://rdrr.io/r/base/AsIs.html). When using this parameter,
  always explicitly call by name (i.e. `repo = `) because future
  versions of gert may have additional parameters.

## Details

By default `git_fetch_pull_requests()` will download all PR branches. To
remove these again simply use [git_fetch(prune =
TRUE)](https://docs.ropensci.org/gert/reference/git_fetch.md).
