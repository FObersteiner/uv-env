-   [uv](#uv){#toc-uv}
    -   [motivation](#motivation){#toc-motivation}
    -   [background](#background){#toc-background}
        -   [package
            management](#package-management){#toc-package-management}
    -   [wishlist](#wishlist){#toc-wishlist}
    -   [what is uv?](#what-is-uv){#toc-what-is-uv}
        -   [who is astral, the company behind
            uv?](#who-is-astral-the-company-behind-uv){#toc-who-is-astral-the-company-behind-uv}
        -   [minor annoyances](#minor-annoyances){#toc-minor-annoyances}
    -   [installation](#installation){#toc-installation}
        -   [basic commands](#basic-commands){#toc-basic-commands}
        -   [python version
            management](#python-version-management){#toc-python-version-management}
        -   [project management /
            venvs](#project-management--venvs){#toc-project-management--venvs}
        -   [python tools](#python-tools){#toc-python-tools}
        -   [single-file
            scripts](#single-file-scripts){#toc-single-file-scripts}
    -   [editor
        integration](#editor-integration){#toc-editor-integration}
        -   [VSCode (VSCodium)](#vscode-vscodium){#toc-vscode-vscodium}
        -   [Spyder](#spyder){#toc-spyder}
        -   [Zed](#zed){#toc-zed}
        -   [Neovim](#neovim){#toc-neovim}
        -   [Jupyter Notebook](#jupyter-notebook){#toc-jupyter-notebook}
    -   [move a pyenv/poetry managed project to
        uv](#move-a-pyenvpoetry-managed-project-to-uv){#toc-move-a-pyenvpoetry-managed-project-to-uv}
        -   [CI](#ci){#toc-ci}
    -   [Misc](#misc){#toc-misc}
    -   [Overall
        experience](#overall-experience){#toc-overall-experience}
    -   [TODO](#todo){#toc-todo}

# uv

"There should be one -- and preferably only one -- obvious way to do
it." \-- The Zen of Python

See also: [What is the difference between venv, pyvenv, pyenv,
virtualenv, virtualenvwrapper, pipenv,
etc?](https://stackoverflow.com/q/41573587/10197418)

## motivation

Recently, I stumbled across [Conda: A Package Management
Disaster?](https://mail.python.org/pipermail/python-list/2024-May/912306.html)
and [Problems With Python's Package Management And Venv
Philosophy](https://mail.python.org/pipermail/python-list/2024-May/912341.html).
Those texts made me rethink my Python workflow\...

## background

-   I run Python scripts almost daily and do Python package development
    now and then
-   I\'m using `pyenv` on Linux
-   had issues with the system trying to use Python for something,
    system trying to use one of the pyenv versions, which then fails
    because it\'s a user-specific version or not the correct one that
    has the needed dependencies installed etc.
-   work-around: create a `.python-version` (`pyenv local ...`) file for
    every location where I have some script - one global version would
    be fine, but the system should not use that - so `pyenv global`
    won\'t do
-   using `pip` to install stuff to my \"local\" Python versions
-   don\'t want a venv for script, this would be just bloat\...

### package management

-   I\'ve used `poetry` in the past for package management, that is to
    say managing the dependencies (`pyproject.toml`; see also:
    [packaging.python.org](https://packaging.python.org/en/latest/guides/writing-pyproject-toml/)),
    running tests in a virtual environment for reproducibility etc.
-   actually never really got into poetry; feels still a bit unnecessary
    as I also have/need pyenv to manage Python versions, which come with
    `venv`\...
-   there are many other tools out there around Python and Python
    package management (e.g. conda - you still need pip? - git is a
    separate install?!), some of which I tried, but none of them ever
    felt very intuitive or useful for me
-   comparison to other, \"more modern\" languages:
    -   Go: one tool, go mod cli
    -   Rust: one tool, cargo cli
    -   Zig: one tool, directly via zig cli / build system / son file

## wishlist

-   manage Python versions, venvs and packages with one tool!
-   easily include local, editable packages
-   should overall be a reproducible process, not too complicated
    (towards FAIR research software\...)
-   it shouldn\'t interfere with \"normal\" Python usage; e.g. just type
    `$ python` to get into the newest installed Python interpreter etc.

------------------------------------------------------------------------

## what is uv?

A Python version, package and project manager,
<https://docs.astral.sh/uv/> / <https://github.com/astral-sh/uv>.

### who is astral, the company behind uv?

-   founded by Charlie Marsh, the creator of the `ruff` Python
    linter/formatter
-   self-described as \"We build high-performance developer tools for
    the Python ecosystem.\", with a \"small, distributed team of
    software engineers\"
-   backed by Accel (venture capital, <https://www.accel.com/>),
    Caffeinated Capital (another venture capital firm,
    <https://caffeinatedcapital.com/>) and Guillermo Rauch / Vercel Inc.

### minor annoyances

astral/uv seems to be very focused on performance. That is great. I\'m a
fan of good and performant software. But they rub it in your face
everywhere. Why? I came here because of the mess that is Python package
management, not because the tools are slow. And they\'re using Rust btw.
Come on, it\'s just a programming language after all\...

## installation

I started from a clean system (no pyenv etc., just the Python
installation that comes with the system/Linux base); you can e.g. use a
VM for testing if you don\'t want to mess up your system.

The easiest method is probably running their install script (could use
cargo or pip as well):
`curl -LsSf https://astral.sh/uv/install.sh | sh`.

On Arch Linux, you can get it via `sudo pacman -S uv`. Updates then also
come via the Arch package manager instead of having to run
`uv self update`.

### basic commands

After install, you have

-   `uv` : binary / command, which combines with subcommands like
    `uv python`, `uv venv`, `uv run` etc. (see below).
-   `uvx` : shortcut for `uv tool run`, runs tools provided by Python
    packages

### python version management

-   List available versions: `uv python list`
-   install a specific version: `uv python install 3.12.7`
-   get a Python interpreter / repl: `uv run python` (latest version).
    e.g. `uv run --python 3.12.7 -- python` to get a specific version.
    -   I didn\'t find this very useful though, since that Python
        interpreter won\'t have any third party packages available

### project management / venvs {#project-management--venvs}

-   create a new project, with git, pyproject.toml, with \"project\"
    table etc.: `uv init [name-of-project]`
-   add a dependency to a project: `uv add [name-of-dependency]`. Note
    that flags such as \--dev, \--group, or \--optional can be used.

Adding the first dependency will create a virtual environment, in
directory `.venv`. To run a script of the project via `uv run ...`, the
venv does not need to be activated explicitly.

Lock files. Allow a reproducible build, but aren\'t standardized. A lock
file generated by uv is specific to uv.

-   `uv lock`: make the lock file. `uv lock -U` to update dependencies
    in the lock file
-   `uv sync`: synchronize the venv with the lockfile;
    `uv lock -U && uv sync` to update everything

#### dependencies: special cases

-   from a git repo: e.g.
    `uv add git+https://github.com/FObersteiner/pyFuppes.git --tag v0.5.2`
    (could also be a branch etc.) adds it to `[tool.uv.sources]` in the
    pyproject toml, so it\'s not a \"normal\" dependency. A
    `pip install ...` should respect it however.
-   from a local directory: under `[tool.uv.sources]`, add the
    dependency path like `pyfuppes = { path = "../../pyFuppes" }` (path
    is relative to the project\'s root). Add the `editable = true`
    option inside the curly braces to have the dependency editable.

### python tools

`uvx` runs tools in a temporary environment; e.g.
`uvx pycowsay 'uv kills!'` gets pycowsay and runs it. This is cached so
that the package is not downloaded each time. The cache can be refreshed
by the `--refresh` (all packages) or `--refresh-package <PKG NAME>`
option.

The tools functionality is also useful for stuff like getting an ipython
console for running some small code snippets (`uvx ipython`). As with
`uv run python`, this is only partly useful since ipython won\'t have
third party packages available.

Install frequently used stuff to a persistent environment:
`uv tool install ...`. Since this did not seem well-suited for a kind of
playground, I came up with the following solution:

#### python playground

I like to have a \"playground\", a Python environment with a bunch of
packages installed, from where I can run an IPython console to quickly
test a code snippet for example.

My solution with uv: create a uv project with e.g.
`mkdir uv-env && cd uv-env && uv init --python 3.12.8 && uv venv`, then
add all the required packages to the pyproject file as dependencies. Now
I can easily upgrade all packages by calling `uv lock -U && uv sync` and
get the same environment on a different system by putting the
\"project\" on gitlab. As a nice side-effect, this \"hack\" also allows
to have local packages in editable mode, i.e. changes I make locally are
immediately reflected in the playground, I don\'t have to publish them
first etc.

To get an IPython shell or Python interpreter quickly, I have set
aliases for those in my shell config file.

### single-file scripts

<https://docs.astral.sh/uv/guides/scripts/>

Suppose we have a script that just needs some version of a package;

``` py
import numpy as np

print(np.arange(20))
```

We can set that up and run it with

``` sh
uv add --script example_np.py numpy
uv run example_np.py
```

This adds an \"inline dependency specification\" (see [PEP
723](https://peps.python.org/pep-0723/));

``` py
# /// script
# requires-python = ">=3.12"
# dependencies = [
#     "numpy",
# ]
# ///
```

We could also create this \"manually\" in advance or modify e.g. the
required Python or package versions.

Note: we can also use git or local dependencies here; see dependencies,
special cases.

## editor integration

Does your IDE recognize uv environments?

### VSCode (VSCodium)

-   venv created by uv is selectable and gets correctly activated
-   if you want to have the \"run file in terminal\" option, you will
    have to install \'ipython\' to the venv of the project by running
    `uv pip install ipython` from the project\'s directory

### Spyder

-   you can install and run spyder as a uvx tool; `uvx spyder` /
    `uv tool install spyder`
-   to use your project\'s venv, add spyder-kernels to it: run
    `uv pip install spyder-kernels` in the activated venv
-   then select the python binary from the venv as spyder\'s interpreter
    and restart the ipython kernel in Spyder

### Zed

-   recognizes the venv, but failed to activate it on my system (tries
    to use bash, but my default shell is fish)

### Neovim

-   works for developing packages that have their venv. Use
    \"linux-cultist/venv-selector.nvim\" to select the venv
-   tried with LazyVim; note that nvim is not my 100% Python editor. I
    also use VSCodium and Spyder from time to time

### Jupyter Notebook

<https://docs.astral.sh/uv/guides/integration/jupyter/>

#### stand-alone

Run an isolated environment with `uv run --with jupyter jupyter lab`.
You can `!uv pip install` packages - however note that these
dependencies will only be available for the lifetime of the jupyter
server.

`uv tool run jupyter lab` achieves basically the same thing.

#### inside a project with its own venv: read-only

``` sh
uv run --with jupyter jupyter lab
```

This gives you a read-only access to the project\'s venv.

#### inside a project: interactive

Create a kernel. Add it as a dependency to the project first;
`uv add --dev ipykernel`, then create the kernel and run jupyter

``` sh
uv run ipython kernel install --user --name=<kernel-name>
#
uv run --with jupyter jupyter lab
```

Now the dedicated kernel with name `<kernel-name>`{=html} can be
selected. This allows e.g. to `!uv add` dependencies or
`!uv pip install` packages without adding them as a dependency.

## move a pyenv/poetry managed project to uv

-   pyproject.toml: ==\> converting the pyproject.toml to a more
    \"standard\" version; see e.g.
    <https://www.loopwerk.io/articles/2024/migrate-poetry-to-uv/>

-   pytest: remember to create a `__init__.py` in the tests directory,
    then `uv run pytest .` should work. Might need some more fiddling
    around, see `CI`

-   how to use `pre-commit`: should work out-of-the-box, might require
    `uv run pre-commit migrate-config` and/or
    `uv run pre-commit autoupdate`

### CI

#### github actions

<https://docs.astral.sh/uv/guides/integration/github/#pypi>

-   very smooth to switch from poetry in CI to UV
-   runs significantly faster
-   could be better: getting pytest to work was some serious trail and
    error process

#### gitlab

<https://docs.astral.sh/uv/guides/integration/gitlab/>

-   TODO

## Misc

-   what are **workspaces**, what are they good for? Large codebases,
    managed as individual packages with their own pyproject.toml but a
    common .lock file.

## Overall experience

-   very nice to have one tool for everything
-   yes, it is fast\... Good caching is key
-   very good documentation

## TODO

-   uv with projects that aren\'t Python-only
-   CI: gitlab
-   publish a project to pypi with uv
