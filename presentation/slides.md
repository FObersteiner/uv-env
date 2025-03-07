---
theme: default
title: uv
background: https://images.unsplash.com/photo-1617982324703-442ecdc0fbab?q=80&w=1740&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
transition: slide-left
fonts:
  sans: Robot
  serif: Robot Slab
  mono: Fira Code
---

# `uv`

## A unified tool for Python version and package management

No sunscreen required ☀

---

# About

Florian Obersteiner <f.obersteiner@kit.edu>, DM group, IMKASF

- research software engineer, data management & IT
- background: experimental atmospheric research

---

# Outline

- challenges in Python version and package management
- what is `uv` and how can it help?
- live demo, Q&A

---

# Motivation `#1`

From Samuel & Mietchen, 2024 (<https://doi.org/10.1093/gigascience/giad113>), <br> "Computational reproducibility of Jupyter notebooks from biomedical publications"

<v-clicks>

- PubMed Central --> search full text --> find Jupyter notebook on github --> try to reproduce results
- analyzed `n` = 27271 notebooks from 2660 repositories (3467 publications)

</v-clicks>


<v-click>

<h2 style="font-style: italic;">results</h2>

</v-click>

<v-clicks>

- `m` = 15817 had requirements file (requirements.txt, setup.py, pipfile etc.) (58% of `n`)
- for `k` = 10388 of those, dependencies could be installed (66% of `m`)
- `l` = 1203 of those ran without errors (12% of `k`)
- 879 of those produced identical results as noted within the notebooks (8.5% of `k`, 73% of `l`)

</v-clicks>


<style>
  ul li {
    color: cyan;
  }
</style>


---
layout: image-right
image: ./resources/python_environment.png
---

# Motivation `#2`

- multiple Python versions and virtual environments required for package development and collaboration
- many existing tools like pyenv, pip, pipx, poetry, venv, conda, jupyter ...
- especially for beginners, this can become a waste of time
  - ...or even scare them away from Python, to Matlab or Julia 😳

<style>

footer {
  position: absolute;
  bottom: 10px;
  left: 35px;
  width: calc(100% - 20px);
  text-align: left;
  font-size: 0.8em;
  color: #888;
}
</style>

<footer>
  image source: <a href="https://xkcd.com/1987">xkcd</a>
</footer>

---

## What I have worked with
<br>

- Python version management: <span class="text-green font-bold text-xl"> `pyenv` </span>
  - user installations and [`win-pyenv`](https://github.com/pyenv-win/pyenv-win) on Windows, back in the days
- package installation: <span class="text-green font-bold text-xl"> `pip` </span>
- virtual environments: Python / <span class="text-green font-bold text-xl"> `venv` </span>
- package development / management:  <span class="text-green font-bold text-xl"> `poetry` </span> (comes with its own venv...)

**⅀ 5+ tools** - and no code written...

<div class="text-red-400 font-bold text-xl">A simplified, all-in-one solution ?! </div>

---

# Introducing... What is `uv`?
<br>

- 👾 a CLI tool
- Python version, package, and project manager in one executable
- based on [rye](https://rye.astral.sh/), now developed by Astral, the creators of the `ruff` Python linter
- available for Linux, Mac and Windows

---

# Exemplary commands

```sh {1|3|5|7|9|11|all}{lines:true,startLine:1}
uv python install 3.12.7 # install a Python version

uv init [project-name] # create a Python project, including a venv

uv add [name-of-dependency] # add a dependency to a project

uv lock -U && uv sync # make a lock file and upgrade everythin in the venv

uv pip compile pyproject.toml -o requirements.txt # make requirements file with exact versions

uv run [script-name] # run a script in the project
```

[CLI reference](https://docs.astral.sh/uv/reference/cli/#uv)

---

# Demo

(TODO)

- installation
- running single file scripts
- project configuration
- version pinning for reproducible environments

---

# Conclusion: why use uv?

- simplifies environment setup and management, from Python itself to virtual environments
- reduces the learning curve associated with multiple tools
- easily reproduces environments across different systems
  - `uv.lock` and derived `requirements.txt` for use with other package managers
  - CI/CD integration
  - Docker support
- overall pleasant user experience; fast dependency resolution and intelligent caching

---

# Q&A
