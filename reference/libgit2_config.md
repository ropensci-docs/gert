# Show libgit2 version and capabilities

`libgit2_config()` reveals which version of libgit2 gert is using and
which features are supported, such whether you are able to use ssh
remotes.

## Usage

``` r
libgit2_config()
```

## Examples

``` r
libgit2_config()
#> $version
#> [1] ‘1.7.2’
#> 
#> $ssh
#> [1] TRUE
#> 
#> $https
#> [1] TRUE
#> 
#> $threads
#> [1] TRUE
#> 
#> $config.global
#> [1] "/github/home/.gitconfig"
#> 
#> $config.system
#> [1] ""
#> 
#> $config.home
#> [1] "/github/home"
#> 
```
