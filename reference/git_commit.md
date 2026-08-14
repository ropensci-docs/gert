# Stage and commit changes

To commit changes, start by *staging* the files to be included in the
commit using `git_add()` or `git_rm()`. Use `git_status()` to see an
overview of staged and unstaged changes, and finally `git_commit()`
creates a new commit with currently staged files.

`git_commit_all()` is a convenience function that automatically stages
and commits all modified files. Note that `git_commit_all()` does
**not** add new, untracked files to the repository. You need to make an
explicit call to `git_add()` to start tracking new files.

## Usage

``` r
git_add(files, force = FALSE, repo = ".")

git_rm(files, repo = ".")

git_commit(message, author = NULL, committer = NULL, repo = ".")

git_commit_all(message, author = NULL, committer = NULL, repo = ".")

git_status(staged = NULL, pathspec = NULL, repo = ".")

git_ls(repo = ".", ref = NULL)
```

## Arguments

- files:

  vector of paths relative to the git root directory. Use `"."` to stage
  all changed files.

- force:

  add files even if in gitignore

- repo:

  The path to the git repository. If the directory is not a repository,
  parent directories are considered (see
  [`git_find()`](https://docs.ropensci.org/gert/reference/git_repo.md)).
  To disable this search, provide the filepath protected with
  [`I()`](https://rdrr.io/r/base/AsIs.html). When using this parameter,
  always explicitly call by name (i.e. `repo = `) because future
  versions of gert may have additional parameters.

- message:

  a commit message

- author:

  A
  [git_signature](https://docs.ropensci.org/gert/reference/git_signature.md)
  value, default is
  [`git_signature_default()`](https://docs.ropensci.org/gert/reference/git_signature.md).

- committer:

  A
  [git_signature](https://docs.ropensci.org/gert/reference/git_signature.md)
  value, default is same as `author`

- staged:

  return only staged (TRUE) or unstaged files (FALSE). Use `NULL` or
  `NA` to show both (default).

- pathspec:

  character vector with paths to match

- ref:

  revision string with a branch/tag/commit value

## Value

- `git_status()`, `git_ls()`: A data frame with one row per file

- `git_commit()`, `git_commit_all()`: A SHA

## See also

Other git:
[`git_archive`](https://docs.ropensci.org/gert/reference/git_archive.md),
[`git_branch()`](https://docs.ropensci.org/gert/reference/git_branch.md),
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

[`commit`](https://libgit2.org/docs/reference/main/commit/index.html),
[`index`](https://libgit2.org/docs/reference/main/index/index.html),
[`status`](https://libgit2.org/docs/reference/main/status/index.html).

## Examples

``` r
oldwd <- getwd()
repo <- file.path(tempdir(), "myrepo")
git_init(repo)
setwd(repo)

# Set a user if no default
if(!user_is_configured()){
  git_config_set("user.name", "Jerry")
  git_config_set("user.email", "jerry@gmail.com")
}

writeLines(letters[1:6], "alphabet.txt")
git_status()
#> # A tibble: 1 × 3
#>   file         status staged
#>   <chr>        <chr>  <lgl> 
#> 1 alphabet.txt new    FALSE 

git_add("alphabet.txt")
#> # A tibble: 1 × 3
#>   file         status staged
#>   <chr>        <chr>  <lgl> 
#> 1 alphabet.txt new    TRUE  
git_status()
#> # A tibble: 1 × 3
#>   file         status staged
#>   <chr>        <chr>  <lgl> 
#> 1 alphabet.txt new    TRUE  

git_commit("Start alphabet file")
#> [1] "415dc8a24defc2b74477e0f41af785a9ed6abfc0"
git_status()
#> # A tibble: 0 × 3
#> # ℹ 3 variables: file <chr>, status <chr>, staged <lgl>

git_ls()
#> # A tibble: 1 × 4
#>   path         filesize modified            created            
#> * <chr>           <dbl> <dttm>              <dttm>             
#> 1 alphabet.txt       12 2026-08-14 18:36:06 2026-08-14 18:36:06

git_log()
#> # A tibble: 1 × 6
#>   commit                          author time                files merge message
#> * <chr>                           <chr>  <dttm>              <int> <lgl> <chr>  
#> 1 415dc8a24defc2b74477e0f41af785… Jerry… 2026-08-14 18:36:06     1 FALSE "Start…

cat(letters[7:9], file = "alphabet.txt", sep = "\n", append = TRUE)
git_status()
#> # A tibble: 1 × 3
#>   file         status   staged
#>   <chr>        <chr>    <lgl> 
#> 1 alphabet.txt modified FALSE 

git_commit_all("Add more letters")
#> [1] "d66015066c1941a0cc4c7abe10a56b2166fb9e8c"

# cleanup
setwd(oldwd)
unlink(repo, recursive = TRUE)
```
