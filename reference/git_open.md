# Open local repository

Returns a pointer to a libgit2 repository object. This function is
mainly for internal use; users should simply reference a repository in
gert by by the path to the directory.

## Usage

``` r
git_open(repo = ".")
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

## Value

an pointer to the libgit2 repository

## Examples

``` r
r <- tempfile(pattern = "gert")
git_init(r)
r_ptr <- git_open(r)
r_ptr
#> <git repository>: /tmp/RtmpFnfi9o/gert6eb155ad4d0[@NA]
git_open(r_ptr)
#> <git repository>: /tmp/RtmpFnfi9o/gert6eb155ad4d0[@NA]
git_info(r)
#> $path
#> [1] "/tmp/RtmpFnfi9o/gert6eb155ad4d0/"
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

# cleanup
unlink(r, recursive = TRUE)
```
