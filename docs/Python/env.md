# Virtual environements 


## Packaging

### Pip

Pip <badge-stars repo='pypa/pip'></badge-stars> <badge-doc href="https://pip.pypa.io/en/stable"></badge-doc> is the package installer for Python.

### Wheel


This library <badge-stars repo='pypa/wheel'></badge-stars> <badge-doc href="https://wheel.readthedocs.io/"></badge-doc> <badge-pep nr='427'></badge-pep> <badge-pep nr='425'></badge-pep> is the reference implementation of the Python wheel packaging standard, as defined in PEP 427. It has two different roles:

- A setuptools extension for building wheels that provides the bdist_wheel setuptools command
- A command line tool for working with wheel files

### PyOxyder

PyOwyder <badge-stars repo='indygreg/PyOxidizer'></badge-stars> <badge-doc href='https://pyoxidizer.readthedocs.io'></badge-doc> is a utility for producing binaries that embed Python.

It can be used in case of virtualenv with symlink to the python interpreter (e.g. in the case of pipx)

### PyInstaller

PyInstaller <badge-stars repo='pyinstaller/pyinstaller'></badge-stars> <badge-doc href='https://pyoxidizer.readthedocs.io'></badge-doc> bundles a Python application and all its dependencies into a single package.

## `pyproject.toml`

This file lists the minimal dependencies of the build system of a project in a declarative fashion.  <badge-pep nr='518'></badge-pep> <badge-pep nr='517'></badge-pep>

??? Cite "About PEP 0518" 
    

    [distutils](https://docs.python.org/3/library/distutils.html#module-distutils)
    When Python first developed its tooling for building distributions of
    software for projects, was the chosen solution. As time went on,
    [setuptools](https://pypi.python.org/pypi/setuptools) gained popularity to
    add some features on top of distutils. Both used the concept of a setup.py
    file.

### Tables

#### `build-system`

`[build-system]` table is used to store build-related data. Initially only one key of the table will be valid and is mandatory for the table: `requires`.

??? Example
  
    ```toml
    [build-system]
    # Minimum requirements for the build system to execute.
    requires = ["setuptools", "wheel"]  # PEP 508 specifications.
    ```

Tools should not require the existence of the `[build-system]` table. A pyproject.toml file may be used to store configuration details other than build-related data and thus lack a `[build-system]` table legitimately.

#### `tool`

The `[tool]` table is where any tool related to your Python project, not just build tools, can have users specify configuration data as long as they use a sub-table within `[tool]`, e.g. the flit tool would store its configuration in `[tool.flit]`.


## Python distribution

### Conda

### Pipenv



<a href="https://pipenv-fork.readthedocs.io" target="_blank">
	<img src="https://readthedocs.org/projects/pipenv-fork/badge/?version=latest" alt="Pipenv documentation"/>
</a>

[editable-dependencies](https://pipenv-fork.readthedocs.io/en/latest/basics.html#editable-dependencies-e-g-e)


```bash
pipenv install --dev -e .
```

## Dependency manager

### Conda

### Pipenv

### Poetry

<badge-stars repo='python-poetry/poetry'></badge-stars> <badge-doc href="https://python-poetry.org/docs/"></badge-doc>

**Tab completion**

```bash
poetry completions zsh > ~/.zfunc/_poetry
```

## Application manager

### Pipx

**pipx** <badge-stars repo='pipxproject/pipx'></badge-stars> <badge-doc href="https://pipxproject.github.io/pipx"></badge-doc> installs and run python applications in isolated environments.
