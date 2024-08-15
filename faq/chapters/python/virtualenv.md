# Python Virtual environment

Python provides mechanisms to create isolated conditions to safely run, test, and develop codes without bad interactions with your main system or other projects.

Python applications often use packages and modules that don’t come as part of the standard library. Applications sometimes need a specific library version because the application may require particular bug fixes or an older version of APIs.

It may not be possible to meet the requirements of every application, especially if the conditions are in conflict, and installing either version 1.0 or 2.0 will leave one application unable to run.
The solution to this problem is to create a virtual environment. This self-contained directory tree contains a Python installation, plus several additional packages, for a particular version of Python.

`````{admonition} Python good practice: virtual environment per project
:class: tip
Use a virtual environment for each project you wish to work on. It will prevent interfering between projects' libraries and make package managements more transparent.
`````


`````{note} Python workspace: shared virtual environment for multiple projects

Workspaces help organize large codebases by splitting them into multiple packages with independent dependencies. Each package in a workspace has its own definition, but they are all locked together in a shared shared virtual environment.

It is a common workflow in academic research to combine multiple projects in one environment (probably coming from the conda ecosystem). Be aware that there are good tools like `poetry` and `uv` that can protect you from conflicts between packages and versions. 
`````

`````{admonition} [Virtual environment](https://docs.python.org/3/glossary.html#term-virtual-environment)
:class: tip
A cooperatively isolated runtime environment that allows Python users and applications to install and upgrade Python distribution packages without interfering with the behaviour of other Python applications running on the same system.
`````

In this article, we review a few ways to create and manage virtual environments.

## Using the `venv` built-in utility

[`venv`](https://docs.python.org/3/tutorial/venv.html) is the module used to create and manage virtual environments since Python 3.6.

To create a virtual environment, decide upon a directory where you want to place it, and run the `venv` module as a script with the directory path

```bash
python -m <dirname> --prompt <projectname> --symlink <venv directory name>
source <dirname>/bin/activate
pip install --upgrade pip
# example of packages to install
pip install matplotlib numpy
# better: make a list of packages
pip install -e requirements.txt
```

This snippet above creates a local directory `<dirname>` (if not existing), which contains all the information of your virtual environment.
The `--symlink` option allows you to avoid duplicating libraries from the main system (overwritten if you require specific versions.)

All you need later on is to activate the virtual environment when needed:
```bash
source <dirname>/bin/active
```

To deactivate a virtual environment, type:
```bash
deactivate
```

```{attention}
The `venv` module does not offer to install a different python version than the one used to create the environment. If you need to use a different version of Python, consider using the other options below.
```


## Using (micro)mamba

```{warning} conda licensing update

The Anaconda Python Distribution has been the foundation for Python user applications, offering a large selection of important packages such as NumPy, SciPy, matplotlib, etc. in compatible versions and using optimized builds and libraries. 

However, earlier this year, Anaconda Inc. has changed its [software licensing model](https://legal.anaconda.com/policies/en?name=terms-of-service#terms-of-service) such that it would cost licensing fees to use the Anaconda distribution of Python (this includes the conda). The individual scope of the free tier remains unclear. For those reasons, MPCDF/MPIA is not allowed to install new versions of Anaconda Python any more.

As a drop-in replacement, `mamba` uses conda-forge, a community-driven initiative that develops conda packages which do not fall under the strict licensing of Anaconda Inc. and can therefore be used freely. Note that a lot if not most of packages are available in conda-forge, but some might be missing or slightly outdated.
```

[Mamba](https://mamba.readthedocs.io/en/latest/) is a reimplementation of the conda package manager in C++. It is fully compatible with conda, but it is much faster (though not as fast as others). mamba is a drop-in replacement for the conda package manager, utilizing the same configuration files, and only changing the package solving part. Mamba is a standalone package.

```bash
"${SHELL}" <(curl -L micro.mamba.pm/install.sh)
```

Similar to `venv`` in functions and syntax, you can use [(micro)mamba](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html) to create a virtual environment.

```bash
micromamba create --name <projectname>
micromamba activate <projectname>
pip install --upgrade pip
# example of packages to install
pip install matplotlib numpy
# better: make a list of packages
pip install -e requirements.txt
```

The files from the virtual environment configuration and files are in your home directory. _(This could sometimes be an issue on some systems, but there are workarounds)_

All you need later on is to activate the virtual environment when required:
```bash
micromamba activate <projectname>
```

To deactivate a virtual environment, type:
```bash
micromamba deactivate
```

## Using `Poetry`

[Poetry](https://python-poetry.org/) is a tool for dependency management and packaging in Python.
Poetry enforces the best practice of creating a virtual environment for each project and manages the dependencies (and versions) for you. Poetry generates and updates the `pyproject.toml` file of your project.

you can [install](https://python-poetry.org/docs/#installation) poetry as any python package:
```bash
pip install poetry
```
you may need `--user` option if you don't have admin rights.

To create a new project with poetry, use the following command:
```bash
poetry new <projectname>
```

To add a package to your project, use the following command:
```bash
poetry add <package>
```

To activate the virtual environment, use the following command:
```bash
poetry shell
```
This sets a shell enviroment with your project parameters and dependencies.
To deactivate the virtual environment and exit this new shell type `exit`.

```{note} poetry run
To run a script, you can simply use `poetry run python your_script.py`. Likewise if you have command line tools such as `pytest` or `black` you can run them using `poetry run pytest`.
```

more information on poetry can be found in the [official documentation](https://python-poetry.org/docs/).


## Using `uv`

[uv](https://docs.astral.sh/uv/) is an extremely fast Python package installer and resolver, written in Rust. It is designed as a drop-in replacement for `pip`, `pip-tools`, `pipx`, `poetry`, `pyenv`, `virtualenv` and their associated worflows.

You can install `uv` using `pip` but it is recommended to avoid using the system's python and instead to use the `uv` installer script:
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

You can create a virtual environment (similar to `venv`) with `uv`:

```bash
uv venv --python 3.12.0
```

But you can create a project/workspace (similar to poetry) with `uv`:

```bash
uv init <projectname>
```

To add a package to your project, use the following command:
```bash
uv add <package>
```

To activate the virtual environment, use the following command:
```bash
source .venv/bin/activate
```

To deactivate the virtual environment, use the following command:
```bash
deactivate
```



