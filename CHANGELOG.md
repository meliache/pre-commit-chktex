# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

- Improve readme.
- Add GPL2 LICENSE.md

## [v0.2.2]

### Fixed

- Fix verbosity option, short form with space `-v 2` didn't work for me. Use long form now `--verbosity=2`, which also improves readability.

## [v0.2.1]

### Fixed

- Remove wrong call to `--localrc` parameter without argument in `entry`.
- Add pre-commit hook for checking the yaml in this repo

## [v0.2.0]

### Added

- Add `chktex-system` hook that uses system executable
- Add README.md

### Changed

- Rename conda-based hook ID to `chktex-conda`, add `chktex` as alias ID for backwards compatibility.


## [v0.1.0]

### Added

- Add initial WIP pre-commit `chktex` hook using condda
