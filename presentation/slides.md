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
- background: experimental atmospheric science
- software development: Python, go, LabVIEW, Zig, ...
  - mostly on Linux

---

# Outline

- Challenges in Python version and package management
- What is `uv` and how can it help
- Usage examples

---

layout: image-right
image: ./resources/python_environment.png
---

# Motivation

- Managing multiple Python versions and virtual environments required for package developement and collaboration
- Complexity: many existing tools like pyenv, pip, pipx, poetry, venv, conda ...
- Especially for beginners, this can become a waste of time

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

## what I have worked with

- Python version management: <span class="text-lime font-bold text-xl"> `pyenv` </span>
  - user installations and [`win-pyenv`](https://github.com/pyenv-win/pyenv-win) on Windows, back in the days
- Package installation: <span class="text-lime font-bold text-xl"> `pip` </span>
- Virtual environments: Python / <span class="text-lime font-bold text-xl"> `venv` </span>
- Package development / management:  <span class="text-lime font-bold text-xl"> `poetry` </span> (comes with its own venv...)

**⅀ 5+ tools** - and no code written...

<div class="text-red-400 font-bold text-xl"> ↦ A simplified, all-in-one solution ?! </div>

---

# Introducing

## What is `uv`?

- A CLI tool
- A unified Python version, package, and project manager
- Combines functionalities of multiple tools in one - and is available for Linux, Mac and Windows
- Based on [rye](https://rye.astral.sh/), now developed at Astral, the creators of the `ruff` Python linter

---

# Exemplary commands

```sh {1|3|5|7|all}
uv python install 3.12.7 # install a Python version

uv init [project-name] # create a Python project, including a venv

uv add [name-of-dependency] # add a dependency to a project

uv lock -U && uv sync # make a lock file and upgrade everythin in the venv
```

---

# Demo

<!--

# Installation and Basic Usage

    Getting Started:
        Installation command: pip install uv
        Initialize a new project: uv init
        Add dependencies: uv add numpy pandas
        Run scripts: uv run script.py

# Managing Python Versions with uv

    Version Control:
        Set a specific Python version for a project: uv set-python 3.9
        Switch between versions effortlessly.
        Ensure compatibility across different projects.

# Project Configuration

    pyproject.toml:
        Centralized configuration for project metadata and dependencies.
        Example structure:

        [project]
        name = "example-project"
        version = "0.1.0"
        description = "A sample project using uv"
        dependencies = ["numpy", "pandas"]

# Transitioning to uv

    Migrating Existing Projects:
        Steps to move from tools like pyenv or poetry to uv.
        Benefits of consolidating tools.

# Real-World Application

    Case Study:
        Briefly discuss a scenario where uv streamlined a data science project.
        Highlight improvements in setup time and environment consistency.

-->

---

# Conclusion: why use uv?

- simplifies environment setup and management, from Python version to virtual environment
- reduces the learning curve associated with multiple tools
- uv.lock: ensures consistent environments across different systems
- pleasant user experience; fast dependency resolution, intelligent caching

---

# Q&A
