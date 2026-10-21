# Submodules

Interact with
[submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules) in the
repository.

## Usage

``` r
git_submodule_list(repo = ".")

git_submodule_info(submodule, repo = ".")

git_submodule_init(submodule, overwrite = FALSE, repo = ".")

git_submodule_set_to(submodule, ref, checkout = TRUE, repo = ".")

git_submodule_add(url, path = basename(url), ref = "HEAD", ..., repo = ".")

git_submodule_fetch(submodule, ..., repo = ".")
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

- submodule:

  name of the submodule

- overwrite:

  overwrite existing entries

- ref:

  a branch or tag or hash with

- checkout:

  actually switch the contents of the directory to this commit

- url:

  full git url of the submodule

- path:

  relative of the submodule

- ...:

  extra arguments for
  [`git_fetch()`](https://docs.ropensci.org/gert/reference/git_fetch.md)
  for authentication things

## Related libgit2 documentation

[`submodule`](https://libgit2.org/docs/reference/main/submodule/index.html).
