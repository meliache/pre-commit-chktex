# ChkTeX pre-commit hooks

This package provides the minimal [ChkTeX](https://www.nongnu.org/chktex) [pre-commit](https://pre-commit.com) hooks `chktex-conda` and `chktex-system` for LaTeX.


## Installation

Make sure you have [`pre-commit` installed](https://pre-commit.com/index.html#install).

Create a `.pre-commit-confing.yaml` file in the root of your repository with the contents:

``` yaml
repos:
  - repo: https://github.com/meliache/pre-commit-chktex
    rev: v0.2.0  # use the latest tagged version in the releases of this repository
    hooks:
      - id: chktex-conda  # install and use chktex via a conda
      # - id: chktex-system  # alternative: uncomment to use system chktex
```

As an ID use `chktex-conda` if you want to have ChkTeX to be automatically installed via `conda`[^1] into a dedicated environment or use `chktex-system` to use the conda-executable that is available system-wide. If you already have ChkTeX installed, the system-version requires less setup but it has the disadvantage of not being fixed to a specific ChkTeX version. If you have multiple contributors, they might use different ChkTeX releases. `chktex-conda` installs the exact version specified in the [environment.yml](environment.yml) file.


## Configuration

This pre-commit hook executes `chktex` with the `--localrc` command line option. Therefore, you can configure `chktex` rules, e.g. warnings to exclude, via a local `chktexrc` (Windows) or `.chktexrc` (Unix/Linux/Mac) configuration in the project root, named  depending on your operating system[^2].
Check the [ChkTeX manual](https://www.nongnu.org/chktex/ChkTeX.pdf) for the extensive configuration options or start from an example configuration, e.g. https://github.com/overleaf/chktex/blob/master/chktexrc. This configuration should then also be used by IDE's, editors and language servers[^3] that use ChkTeX as a LaTeX linter.

## Similar project

- [https://flake.parts/options/pre-commit-hooks-nix.html](flake-parts pre-commit-hooks.nix) for [NixOS](https://nixos.org) contains a ChkTeX hook.
- [mKaloer/pre-commit gist](https://gist.github.com/mKaloer/f9488142f76b29a2e2e6): *A* custom pre-commit script that can be copied manually to `.git/hooks/pre-commit`. It's simple, and might be all you need, but does not integrate with *the* `pre-commit` framework.
- [jonasbb/pre-commit-latex-hooks](https://github.com/jonasbb/pre-commit-latex-hooks) : Custom LaTeX pre-commit hooks, independent of available linters. That means you won't see the errors in your editor/IDE until you actually try to commit.

[^1]: The conda version requires a conda installer. If you're not using conda anyway, I recommend installing a minimal conda installer like [Miniconda]( https://docs.conda.io/en/latest/miniconda.html) or the newer [Micromamba](https://mamba.readthedocs.io/en/latest/installation.html#micromamba). The latter requires setting the `PRE_COMMIT_USE_MICROMAMBA=1` environment variable (see the [pre-commit conda](https://pre-commit.com/index.html#conda) documentation).

[^2]: Personally, I create a `chktexrc` file and a relative symbolic link to `.chktexrc`, on linux for example with `ln -s chktexrc .chktexrc`, and commit both, to ensure it works on all systems.

[^3]: I use the [texlab](https://github.com/latex-lsp/texlab) language server, which can be used with any editor/IDE that has LSP support, e.g. emacs, vim or vscode. It allows enabling chktex via [configuration options](https://github.com/latex-lsp/texlab/wiki/Configuration#texlabchktexonopenandsave).
