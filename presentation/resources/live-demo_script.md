# Demo

## Setup

- Linux Mint VM (distro doesn't matter much...)
- system installation of Python, the one that comes pre-installed (`python3`)
- no pip

### what I already installed

- nicer shell, git, my nvim config etc.

... none of this is needed specifically for uv.

## Install uv

```sh
curl -LsSf https://astral.sh/uv/install.sh | sh
```

- restart shell
- test: "uv --help"

## Run a script

- make a simple script;

```sh
uv run myscript.py
```

- this works out-of-the-box

## Python versions

- check python versions:

```sh
uv python list
```

- add a version check to the script;

```py
import sys
print(sys.version_info)
```

- run

- install a python version and run again:

```sh
uv python install 3.11
uv run --python 3.11 myscript.py
```

- set a requirement within the script:

```sh
uv init --script ./myscript.py --python 3.11
```

- look at the top of the script; see [PEP 723](https://peps.python.org/pep-0723/) inline script metadata

## Dependencies

- add to script

```sh
uv add --script myscript.py rich
```

```py
import sys
from rich.pretty import pprint

pprint(sys.version_info)
```

- show how to change the version of a dependency, e.g. by setting "# "rich <= 12"," and running the script again
- ...or add a dependency with a spec. version (e.g. numpy == 1.26)

## Projects

This is where it gets more interesting, this is where dependency hell is in sight and a reproducible build system is very handy.

```sh
uv init myproject # new project from template
lx ./myproject
```

- we have a git repo with the very basic stuff for a python package :)

- add dependency, show pyproject.toml (see also: PEP 621)

- use the dependency

- note that we can run main.py with the added dependency without activating the venv; uv will automatically use this. Of course you can also activate it, to use tools like pytest directly (show how to add a dev dependency)

- you can also use `pip install`, via `uv pip install` - note that this is a bit dangerous since it allows you to install packages to the venv which are not specified as a dependency, so things might work on your machine but not on your collegoue's machine...

### locking the environment

- make a requirements.txt with exact version specs: `uv pip compile pyproject.toml -o requirements.txt`

    - could also use `setup.py` as source for the requirements

- install from requirements file: `uv pip install -r requirements.txt`

## misc

- `uvx` to use Python tools. Can be convenient for non-Python projects that don't have a venv for example.
