# Test if a Git user is configured

This function exists mostly to guard examples that rely on having a user
configured, in order to make commits. `user_is_configured()` makes no
distinction between local or global user config.

## Usage

``` r
user_is_configured(repo = ".")
```

## Arguments

- repo:

  An optional `repo`, in the sense of
  [`git_open()`](https://docs.ropensci.org/gert/reference/git_open.md).

## Value

`TRUE` if `user.name` and `user.email` are set locally or globally,
`FALSE` otherwise.

## Examples

``` r
if (FALSE) { # interactive()
user_is_configured()
}
```
