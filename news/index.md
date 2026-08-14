# Changelog

## gert 2.4.1

- Disable owner validation with recent libgit2 versions for backward
  compatibility

## gert 2.4.0

CRAN release: 2026-07-22

- Linux: default to system libgit2 on Ubuntu 24 and up.
- Add
  [`git_config_global_unset()`](https://docs.ropensci.org/gert/reference/git_config.md)
  and
  [`git_config_unset()`](https://docs.ropensci.org/gert/reference/git_config.md)
  ([@iofarm](https://github.com/iofarm),
  [\#273](https://github.com/r-lib/gert/issues/273))
- Add
  [`git_restore()`](https://docs.ropensci.org/gert/reference/git_restore.md)
  function ([\#259](https://github.com/r-lib/gert/issues/259))
- Add
  [`git_config_get()`](https://docs.ropensci.org/gert/reference/git_config.md),
  [`git_config_local_get()`](https://docs.ropensci.org/gert/reference/git_config.md),
  and
  [`git_config_global_get()`](https://docs.ropensci.org/gert/reference/git_config.md)
  to retrieve a single named config option, returning `NULL` if unset
  ([\#267](https://github.com/r-lib/gert/issues/267)).
- [`git_clone()`](https://docs.ropensci.org/gert/reference/git_fetch.md)
  without a `path` argument now clones into a directory named after the
  “humanish” part of the URL, so
  “<git@github.com>:francisbarton/myrepo.git” gets cloned into `myrepo`
  ([@francisbardon](https://github.com/francisbardon),
  [\#192](https://github.com/r-lib/gert/issues/192)).
- [`git_remote_set_pushurl()`](https://docs.ropensci.org/gert/reference/git_remote.md)
  gains an `add` argument to append push URLs instead of replacing them.
  ([@robitalec](https://github.com/robitalec),
  [\#128](https://github.com/r-lib/gert/issues/128))
- Fix
  [`git_info()`](https://docs.ropensci.org/gert/reference/git_repo.md)
  for the case when no upstream is configured
  ([@mpage](https://github.com/mpage),
  [\#263](https://github.com/r-lib/gert/issues/263))
- [`git_branch_create()`](https://docs.ropensci.org/gert/reference/git_branch.md):
  `force` now also applies to the checkout step, allowing branch
  creation even when local changes would be overwritten
  ([@MichaelChirico](https://github.com/MichaelChirico),
  [\#177](https://github.com/r-lib/gert/issues/177)).
- Improve manual pages ([@olivroy](https://github.com/olivroy),
  [\#227](https://github.com/r-lib/gert/issues/227))
- Fix badge links in `README.md`
  ([@dpprdan](https://github.com/dpprdan),
  [\#189](https://github.com/r-lib/gert/issues/189))
- Use `NEWS.md` instead of `NEWS`
  ([@olivroy](https://github.com/olivroy),
  [\#209](https://github.com/r-lib/gert/issues/209))
- Add git_revert() function
  ([\#206](https://github.com/r-lib/gert/issues/206))
- new function
  [`git_branch_switch()`](https://docs.ropensci.org/gert/reference/git_branch.md),
  an alias to
  [`git_branch_checkout()`](https://docs.ropensci.org/gert/reference/git_branch.md)
  ([\#254](https://github.com/r-lib/gert/issues/254))
- Add argument `depth` in
  [`git_clone()`](https://docs.ropensci.org/gert/reference/git_fetch.md)
  ([\#281](https://github.com/r-lib/gert/issues/281),
  [@etiennebacher](https://github.com/etiennebacher)).

## gert 2.3.1

CRAN release: 2026-01-11

- git_stat_files() gains a ‘max’ parameter
- Fix function declaration error

## gert 2.3.0

CRAN release: 2026-01-08

- Add git_worktree() family of functions
  ([\#252](https://github.com/r-lib/gert/issues/252))
- Reformat code with air

## gert 2.0.2

- Workaround for accidental API change in libgit2 1.8.0
- Disable a non-api call in R \>= 4.5.0 for now

## gert 2.0.1

CRAN release: 2023-12-04

- Fix a printf warning for cran

## gert 2.0.0

CRAN release: 2023-09-26

- Windows: update to libgit2-1.7.1 + libssh-1.11.0 + openssl-3.1.2

## gert 1.9.3

CRAN release: 2023-08-07

- Add
  [`git_commit_stats()`](https://docs.ropensci.org/gert/reference/git_history.md)
  function
- Add
  [`git_ignore_path_is_ignored()`](https://docs.ropensci.org/gert/reference/git_ignore.md)
  function
- Fix protect bug in
  [`git_submodule_list()`](https://docs.ropensci.org/gert/reference/git_submodule.md)

## gert 1.9.2

CRAN release: 2022-12-05

- Replace sprintf with snprintf for CRAN

## gert 1.9.1

CRAN release: 2022-10-05

- Fix the Wstrict-prototype warnings
- Use special static libgit2 bundle for openssl-3 distros.

## gert 1.9.0

CRAN release: 2022-09-15

- Add support for the new ED25519 keys when authenticating over SSH

## gert 1.8.0

CRAN release: 2022-09-06

- The static libgit2 for win/mac/linux are all 1.4.2 with a patched
  version of libssh 1.10.1. This should fix problems with the latest
  release versions of libgit2 and libssh2.
- The patched libssh2 builds should now support RSA-SHA2, which
  re-enables authentication with GitHub using an RSA key.
- On production Linux systems (x64 RHEL/Ubuntu) default to building
  using the static libgit2 because of above reasons. Set
  `USE_SYSTEM_LIBGIT2=1` to force building against a local libgit2 on
  these platforms.

## gert 1.7.1

CRAN release: 2022-08-18

- The static libgit2 for linux has been updated to 1.5.0 (this is only
  used on linux systems where no sufficient libgit2 is available).

## gert 1.7.0

CRAN release: 2022-08-07

- [`git_status()`](https://docs.ropensci.org/gert/reference/git_commit.md)
  gains parameter pathspec
- [`git_ls()`](https://docs.ropensci.org/gert/reference/git_commit.md)
  gains paremeter ‘ref’ and works with bare repositories

## gert 1.6.0

CRAN release: 2022-03-29

- We recommend at least libgit2 1.0 now
- Windows: update to libgit2 1.4.2
- Tests: switch to ECDSA keys for ssh remote unit tests
- [`git_log()`](https://docs.ropensci.org/gert/reference/git_history.md)
  gains a parameter ‘after’

## gert 1.5.0

CRAN release: 2022-01-03

- Windows: use $`{HOMEDRIVE}`${HOMEPATH} path as home if it exists, to
  match git-for-windows. On most systems this is the same as
  \${USERPROFILE}.
- [`git_commit_info()`](https://docs.ropensci.org/gert/reference/git_history.md)
  no longer includes \$diff by default because it can be huge. Please
  use
  [`git_diff()`](https://docs.ropensci.org/gert/reference/git_diff.md)
  instead if you need it.

## gert 1.4.3

CRAN release: 2021-11-10

- Fix a unit test for some older versions of libgit2

## gert 1.4.2

CRAN release: 2021-11-03

- Make unit tests more robust against network fail and renamed branches
- Windows / MacOS: update to libgit2 1.3.0

## gert 1.4.1

CRAN release: 2021-09-16

- Fix compile error with some older version of libgit2
- MacOS: automatically use static libs when building in CI

## gert 1.4.0

CRAN release: 2021-09-15

- Windows / MacOS: update to libgit2 1.2.0
- New function
  [`git_branch_move()`](https://docs.ropensci.org/gert/reference/git_branch.md)
- [`git_branch_checkout()`](https://docs.ropensci.org/gert/reference/git_branch.md)
  gains ‘orphan’ parameter

## gert 1.3.2

CRAN release: 2021-08-16

- Fix unit test because GitHub has disabled user/pass auth

## gert 1.3.1

CRAN release: 2021-06-23

- Windows: fix build for ucrt toolchains
- Solaris: disable https cert verfication

## gert 1.3.0

CRAN release: 2021-03-29

- Some encoding fixes for latin1 paths, especially non-ascii Windows
  usernames.

## gert 1.2.0

CRAN release: 2021-02-14

- New
  [`git_stat_files()`](https://docs.ropensci.org/gert/reference/git_history.md)
  function.

## gert 1.1.0

CRAN release: 2021-01-25

- On x86_64 Linux systems where libgit2 is too old or unavailable, we
  automatically try to download a precompiled static version of libgit2.
  This includes CentOS 7/8 as well as Ubuntu 16.04 and 18.04. Therefore
  the PPA should no longer be needed. You can opt-out of this by setting
  an envvar: USE_SYSTEM_LIBGIT2=1
- Add tooling to manually find and set the location of the system SSL
  certificates on such static builds, and also for Solaris.
- Add several functions to work with submodules.
- Globally enable submodule-caching for faster diffing.
- Refactor internal code to please rchk analysis tool.

## gert 1.0.2

CRAN release: 2020-11-12

- [`git_branch_list()`](https://docs.ropensci.org/gert/reference/git_branch.md)
  gains a parameter ‘local’
- Windows / MacOS: update to libgit2 1.1.0
- Do not use bash in configure

## gert 1.0.1

CRAN release: 2020-10-14

- [`git_branch_list()`](https://docs.ropensci.org/gert/reference/git_branch.md)
  and
  [`git_commit_info()`](https://docs.ropensci.org/gert/reference/git_history.md)
  gain a date field
- Bug fixes

## gert 1.0

- Lots of new functions
- Windows and MacOS now ship with libgit2-1.0.0
- Do not advertise HTTPS support in startup message because it should
  always be supported.
- Config setters return previous value invisibly
  ([\#37](https://github.com/r-lib/gert/issues/37))
- Conflicted files are reported by
  [`git_status()`](https://docs.ropensci.org/gert/reference/git_commit.md)
  ([\#40](https://github.com/r-lib/gert/issues/40))
- Windows: libgit2 now finds ~/.gitconfig under \$USERPROFILE (instead
  of Documents)
- A git_signature object is now stored as a string instead of an
  externalptr
- The ‘name’ parameter in git_remote\_ functions has been renamed to
  ‘remote’

## gert 0.3

CRAN release: 2019-10-29

- Support for clone –mirror and push –mirror
  ([\#12](https://github.com/r-lib/gert/issues/12))

## gert 0.2

CRAN release: 2019-07-22

- [`git_open()`](https://docs.ropensci.org/gert/reference/git_open.md)
  now searches parent directories for .git repository
- [`git_push()`](https://docs.ropensci.org/gert/reference/git_fetch.md)
  sets upstream if unset
- workaround for ASAN problem in libssh2
- lots of tweaks and bug fixes

## gert 0.1

CRAN release: 2019-06-19

- Initial CRAN release.
