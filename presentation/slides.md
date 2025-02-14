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

Florian Obersteiner (<f.obersteiner@kit.edu>), DM group, IMKASF

- data management & IT
- background: experimental atmospheric research
- tech stack: Python, go, LabVIEW, Zig, ...
  - mostly on Linux
  - current projects: web applications and containerization

---

# Outline

- challenges in Python version and package management
- what is `uv` and how can it help?
- live demo, Q&A

---
layout: image-right
image: ./resources/python_environment.png
---

# Motivation

- multiple Python versions and virtual environments required for package development and collaboration
- many existing tools like pyenv, pip, pipx, poetry, venv, conda ...
- especially for beginners, this can become a waste of time
  - ...or even scare them away from Python, back to Matlab 😳

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

- Python version management: <span class="text-lime font-bold text-xl"> `pyenv` </span>
  - user installations and [`win-pyenv`](https://github.com/pyenv-win/pyenv-win) on Windows, back in the days
- package installation: <span class="text-lime font-bold text-xl"> `pip` </span>
- virtual environments: Python / <span class="text-lime font-bold text-xl"> `venv` </span>
- package development / management:  <span class="text-lime font-bold text-xl"> `poetry` </span> (comes with its own venv...)

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

```sh {1|3|5|7|9|all}{lines:true,startLine:1}
uv python install 3.12.7 # install a Python version

uv init [project-name] # create a Python project, including a venv

uv add [name-of-dependency] # add a dependency to a project

uv lock -U && uv sync # make a lock file and upgrade everythin in the venv

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
