# Python Virtual environment

Python provides mechanisms to create isolated conditions to safely run, test, and develop codes without bad interactions with your main system or other projects.

:::{note}
As [jupyter-book](https://github.com/jupyter/jupyter-book) is the format of this repository, you will find throughout these pages Python codes and notebooks that you can run with [Binder](https://mybinder.org/) by clicking on the top right icon.
:::


Python applications often use packages and modules that don’t come as part of the standard library. Applications sometimes need a specific library version because the application may require particular bug fixes or an older version of APIs.

It may not be possible to meet the requirements of every application, especially if the conditions are in conflict, and installing either version 1.0 or 2.0 will leave one application unable to run.
The solution to this problem is to create a virtual environment. This self-contained directory tree contains a Python installation, plus several additional packages, for a particular version of Python.

`````{admonition} Python good practice: virtual environment per project
:class: tip
Use a virtual environment for each project you wish to work on. It will prevent interfering between projects' libraries and make package managements more transparent.
`````

`````{admonition} [Virtual environment](https://docs.python.org/3/glossary.html#term-virtual-environment)
:class: tip
A cooperatively isolated runtime environment that allows Python users and applications to install and upgrade Python distribution packages without interfering with the behaviour of other Python applications running on the same system.
`````

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


## Using (mini)conda

:::{note}
I personally recommend using `venv` instead of `conda`. The latter is a big machinery if all you need is `pip install`.
:::

Similar to `venv`` in functions and syntax, you can use [(mini)conda](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html) to create a virtual environment.

```bash
conda create --name <projectname>
conda activate <projectname>
pip install --upgrade pip
# example of packages to install
pip install matplotlib numpy
# better: make a list of packages
pip install -e requirements.txt
```

The files from the virtual environment configuration and files are in your home directory. _(This could sometimes be an issue on some systems, but there are workarounds)_

All you need later on is to activate the virtual environment when required:
```bash
conda activate <projectname>
```

To deactivate a virtual environment, type:
```bash
conda deactivate
```