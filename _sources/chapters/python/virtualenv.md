# Python Package and Environment Management

## Introduction

Writing programs in Python, especially for astronomy, will often use Python packages don’t come as part of the standard library.
In addition, certain Python packages and/or workflows will also require certain system packages to be installed. 
Not only will Python packages require specific packages/modules to be installed, but they will also require certain versions (or ranges of versions) of a package to be installed. 
These installed packages in turn have their own set of requirements! 
What's worse is that a single user may want to have access to several versions of packages for different projects, or even different versions of Python as well! 

`````{admonition} [Package manager](https://en.wikipedia.org/wiki/Package_manager)
:class: tip
Software that handles installing packages and dependency resolution. 
`````

It may not be possible to meet the requirements of every application, especially if the conditions are in conflict, and installing either version 1.0 or 2.0 will leave one application unable to run.
The solution to this problem is to create a virtual environment. 
This self-contained directory tree contains a Python installation with additional packages, potentially even non-Python packages. 

`````{admonition} [Virtual environment](https://docs.python.org/3/glossary.html#term-virtual-environment)
:class: tip
A cooperatively isolated runtime environment that allows Python users and applications to install and upgrade Python distribution packages without interfering with the behaviour of other Python applications running on the same system.
`````

For this reason, package managers *and* virtual environment managers are essential for modern day workflows in astronomy.
Many of these exist and you are already likely familiar with a few of them, such as `pip` and `venv`.
Some tools can even handle both virtual environment managing and package managing, all in one tool! 
This is the case for `conda`, which you also might be familiar with.

In this article we will go through and describe several common resources, ranging from tools included in Python itself to relatively new software that is actively being developed. 

`````{note}
In this article we will describe a few different resources and tools to manage virtual environments. They broadly fall into two categories with slightly different philosophies:

1. **Namespace-Based:**

    In this paradigm, virtual environments are associated with a "name" and are designed to be activated from anywhere in the system. Typically the environments are all held in a single location. A good example of this paradigm is `conda`, where the user creates environments, which are all stored in a configured location, and can be activated at will from anywhere on the system.  

2. **Project-Based / Project-Scoped**

    In this paradigm, virtual environments are associated with a specific directory tree on the filesystem and are designed to be activated within this tree. A good example of this paradigm is `venv` where invoking the command creates a folder in the specified directory which contains scripts that the user can invoke to activate the environment. It should be noted that it is still possible to activate/access the environment from other locations on the filesystem, but it might be slightly more tedious. 

`````

`````{admonition} Python good practice: virtual environment per project
:class: tip
Regardless of the paradigm you prefer to use, it is good practice to use a virtual environment for each project you wish to work on. It will prevent interfering between projects' libraries and make package managements more transparent. In addition, it can make sharing your more straightforward, ensuring the reproducibility. 
`````

`````{admonition} Python workspace: shared virtual environment for multiple projects
:class: tip
Workspaces help organize large codebases by splitting them into multiple packages with independent dependencies. Each package in a workspace has its own definition, but they are all locked together in a shared shared virtual environment.

It is a common workflow in academic research to combine multiple projects in one environment (probably coming from the conda ecosystem). Be aware that there are good tools like `poetry` and `uv` that can protect you from conflicts between packages and versions. 
`````

**In this article, we review a few ways to create and manage virtual environments. This is only intended to give you a high level understanding of the pros and cons between each tool, so you can better make your own decision about what tools you need. As always, *consult the documentation* for these tools directly, many of them have quite lengthy tutorials. You can also check out YouTube for demos for quite a few of these as well!**

`````{admonition} Shell completion
:class: tip
Quite a few of these tools allow for shell completion, e.g. using <TAB> to autocomplete parts of the commands. Check the documentation for each tool on how to enable these features.
`````


## `pip`

[`pip`](https://pip.pypa.io/en/stable/installation/) is the Python package manager. It's hard to think about Python without thinking of `pip`! Nearly all installations of python come with `pip`. You can even invoke a special command in python to install `pip`: `python -m ensurepip`

Pip is able to install Python packages by pulling code from the Python Package Index ([PyPI](https://pypi.org/)), from GitHub repos, or from the local filesystem. It handles dependency installation and resolution for you! Simply typing `pip install <package name>` (or `pip3 install` depending on which is available in the path) will install Python packages to the current environment. 

Pros: It's as straightforward as they come! If you need a purely Python package manager, `pip` is almost always there for you, and can get you set up quickly. 

Cons: `pip` can only install Python packages, not any other kinds of packages which those packages might depend on. `pip` is also relatively slow. `pip` is also not ideal for reproducibility or package development, since it's relies on `requirements.txt` files to lock in dependencies, but it cannot handle more than single order dependencies (e.g. you cannot fix the dependencies of dependencies), you can get inconsistent package installations between systems, etc. 

## `venv`

[`venv`](https://docs.python.org/3/tutorial/venv.html) is the module used to create and manage virtual environments since Python 3.6. It is project-based, as it creates a directory that contains all of the relevant scripts to activate/deactivate the environment. As long as you have Python on your system, you can use `venv`!

To create a virtual environment, decide upon a directory where you want to place it, and run the `venv` module as a script with the directory path:

```bash
python -m venv <dirname> 
source <dirname>/bin/activate # If you are not using bash/zsh, there are other scripts to use
pip install numpy # This will install only to the local environment. 
```

This snippet above creates a local directory `<dirname>` (if not existing), which contains all the information of your virtual environment.

Some additional options to `python -m venv` include:
- The `--symlink` option allows you to avoid duplicating libraries from the main system (overwritten if you require specific versions.)
- The `--prompt` options overwrites the default name of the project, so you can customize how it appears in your shell. 

To deactivate a virtual environment, simply type:
```bash
deactivate
```

Pros: It comes default with any version of Python since 3.6. It's straightforward, simple, and works well with `pip`. 

Cons: The `venv` module does not offer to install a different Python version than the one used to create the environment. It is also not easy/designed to make environments reproducible. 

```{attention}
The `venv` module does not offer to install a different python version than the one used to create the environment. If you need to use a different version of Python, consider using the other options below.
```

## `mamba` (replacement for `conda`)

We're now going to talk about `conda/mamba`, one of the staples in Python configuration management. It can handle both package and virtual environment management. 

[(micro)mamba](https://mamba.readthedocs.io/en/latest/) is a reimplementation of the conda package manager in C++. It is fully compatible with `conda`, but it is much faster. `mamba` is a drop-in replacement for the conda package manager, utilizing the same configuration files, and only changing the package solving part. `micromamba` is comparable to `miniconda` as the smaller packaging that doesn't come with any installed packages by default and is the preferred method. 

```{warning} conda licensing update

The Anaconda Python Distribution has been the foundation for Python user applications, offering a large selection of important packages such as NumPy, SciPy, matplotlib, etc. in compatible versions and using optimized builds and libraries. 

However, earlier this year, Anaconda Inc. has changed its [software licensing model](https://legal.anaconda.com/policies/en?name=terms-of-service#terms-of-service) such that it would cost licensing fees to use the Anaconda distribution of Python (this includes the conda). The individual scope of the free tier remains unclear. For those reasons, MPCDF/MPIA is not allowed to install new versions of Anaconda Python any more.

As a drop-in replacement, `mamba` uses [conda-forge](https://conda-forge.org/), a community-driven initiative that develops conda packages which do not fall under the strict licensing of Anaconda Inc. and can therefore be used freely. Note that a lot if not most of packages are available in conda-forge, but some might be missing or slightly outdated.
```

One of the most powerful aspects of `mamba` (like `conda`) that set it apart from all of the other solutions we have talked about before is that `mamba` can install *non Python dependencies* in your environments. The ability to specify system Packages as dependencies in environmnets means that, in essence, `mamba` is not a Python virtual environment manager, but an environment manager for packages that exist in the `conda-forge` ecosystem. 

You can install `micromamba`, the preferred `mamba` implementation, with their provided installation script or with your system's package manager (`apt-get`, `brew`, etc.):
```bash
"${SHELL}" <(curl -L micro.mamba.pm/install.sh)
```

You can use `mamba` to create namespace-based virtual environments: 

```bash
micromamba create --name <projectname>
micromamba activate <projectname>
micromamba install python=3.11 numpy cuda 
```
Just like that we've installed Python, Python packages, and even non-Python packages, all in one line! These can all be written out to a share-able file with `micromamba env export --no-build`

You can also use pip to install packages to the environment if they are not available in conda-forge, though it's usually recommended you do this after installing packages with conda. 
```bash
# example of packages to install
pip install matplotlib numpy
# better: make a list of packages
pip install -e requirements.txt
```

All you need later on is to activate the virtual environment when required, anywhere on the filesystem:
```bash
micromamba activate <projectname>
```

To deactivate a virtual environment, type:
```bash
micromamba deactivate
```

Pros: `mamba` is currently the best namespace-based Python environment manager that exists, due quite largely to the fact that it is also able to install non-Python dependencies! It is relatively fast (though not the fastest we've talked about), relatively reproducible, and has a large list of packages available from `conda-forge` (you can, of course, pull packages from Anaconda, however as discussed above this may have other consequences). 

Cons: The `conda` recipe format is not the most reproducible, and `mamba` is not the fastest code out there. In addition, `mamba` still has some legacy baggage that it ports over from being an attempt to replace `conda`, such as the base environment. 

Conclusion: If you are used to `conda`, switch to `mamba`. 

## `Poetry`

So far we have focused on creating isolated environments and installing packages with the purpose of using them for our own work. However, we have neglected reproducibility as a core aspect of Python workflows. 

[Poetry](https://python-poetry.org/) is a tool for dependency management and packaging in Python.
`Poetry` enforces the best practice of creating a virtual environment for each project and manages the dependencies (and versions) for you. `Poetry` generates and updates the `pyproject.toml` file of your project. The `pyproject.toml` file is a standardized configuration file used in Python projects to specify build system requirements, dependencies, and project metadata. 

You can [install](https://python-poetry.org/docs/#installation) poetry as any python package or with your system's package manager (`apt-get`, `brew`, etc.):

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
You'll notice that this automatically updates the `pyproject.toml` file with the dependencies.
You can edit the file manually or use the `Poetry` CLI as demonstrated above.
If you've edited manually, you can install all packages to the environment using the `poetry install` command.

To activate the virtual environment, use the following command:
```bash
poetry shell
```
This sets a shell environment with your project parameters and dependencies.
To deactivate the virtual environment and exit this new shell type `exit`.

```{note} poetry run
To run a script, you can simply use `poetry run python your_script.py`. Likewise if you have command line tools such as `pytest` or `black` you can run them using `poetry run pytest`.
```

More information on poetry can be found in the [official documentation](https://python-poetry.org/docs/). It comes with a lot of great features, include the ability to directly publish your package to PyPI! 

Pros: In terms of project-scoped environment management, it's hard to think of what features would be better suited for reproducibility than what is provided by Poetry. If you are developing a Python package, Poetry is a great option. 

Cons: Some parts of Poetry can be slightly slow and it also cannot specify non-Python dependencies (other than Python itself). 

## `uv`

If `conda` and `poetry` seem like overkill and you just wish you could use `venv` and `pip` with different versions of Python (and you also wish `pip` was faster), you're in luck.[uv](https://docs.astral.sh/uv/) is an extremely fast Python package installer and resolver, written in Rust. It is designed as a drop-in replacement for `pip`, `pip-tools`, `pipx`, `poetry`, `pyenv`, `virtualenv` and their associated worflows.

You can install `uv` using `pip` but it is recommended to avoid using the system's python and instead to use the `uv` installer script, or installing with your system's package manager (`apt-get`, `brew`, etc.):
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

You can create a virtual environment (similar to `venv`) with `uv`:

```bash
uv venv <directory name> --python 3.12.0
```

We can activate and add packages to 
```bash
source <directory name>/bin/activate
uv pip install numpy
```

If you've been following along and trying this, you may notice that `uv` is orders of magnitude faster than pip. This is a major selling point of the software, the authors of `uv` have a track record of making fast, performant, software for Python, such as the `ruff` linter. 

To deactivate the virtual environment, use the following command:
```bash
deactivate
```

You can create a project/workspace (similar to `Poetry`) with `uv`, though this feature is still experimental. 

```bash
uv init <projectname>
uv add <package>
```

Pros: If your workflow only requires `pip` and `venv` and different version of Python, look no farther than `uv`. Not only is it ludicrously fast, but it is feature rich and supports nearly all of `pip` and `venv` syntax. Just add `uv` before your regular commands and you're good to go!

Cons: As with `pip`, `uv` can only install Python packages, with the exception that it can install different versions of Python. In addition, reproducible project/workspaces with `uv` are still experimental, therefore this suffers from many of the same reproducibility cons as `pip`.

## `pixi`

[`pixi'](https://pixi.sh/latest/) attempts to have the reproducibility of Poetry with the ability to add non-Python packages like `mamba` as well as be a global installation tool (more on that later). In fact, `pixi` doesn't claim to be a Python manager at all! It works with Python, R, C/C++, Rust, etc. It is a project-scoped package and environment manager that is designed with reproducibility and workflows in mind. 

You can install `pixi` with their provided installation script or with your system's package manager (`apt-get`, `brew`, etc.):
```bash
curl -fsSL https://pixi.sh/install.sh | bash
```

To create a project, we can use the following:
```bash
pixi init pixi-hello-world
cd pixi-hello-world
pixi add python numpy astropy
```
We can add packages for `conda-forge` or `PyPI` or any other configurable source, see their documentation to learn more.

Similair to other tools we can activate the environment with `pixi shell` (exiting it with `exit`) or run commands with `pixi run` like `pixi run python --version`.

What's great is we can even add automated actions that can run for us:
```
pixi task add checkversion "python --version"
pixi run checkversion
```

Pixi can even be used to install packages globall, which can be extremely useful on systems were you don't have root access, for example MPCDF. You can use this to install your favorite command line tools.
```
pixi global install bat # Like cat, but with wings
```

It even promises to be able to allow you to publish projects to conda-forge in the future, though this has not been implemented yet. 

Pros: Want one tool that can do it all? `pixi` appears to promise this. It doesn't matter what language you develop in or what platform you are on, `pixi` enables you to make highly reproducible packages and workflows with minimal effort. If you are a fan of project-scoped environments, this might be for you. 

Cons: This package is still in development. It has high promise, but still has much ground to cover. 