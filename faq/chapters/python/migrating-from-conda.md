# Migrating from Anaconda/Miniconda install to a Miniforge installation

The Anaconda Python Distribution has been the foundation for Python user applications, offering a large selection of important packages such as NumPy, SciPy, matplotlib, etc. in compatible versions and using optimized builds and libraries.

However, earlier this year, Anaconda Inc. has changed its [software licensing model](https://legal.anaconda.com/policies/en?name=terms-of-service#terms-of-service) such that it would cost licensing fees to use the Anaconda distribution of Python (this includes the conda). The individual scope of the free tier remains unclear. For those reasons, MPCDF/MPIA is not allowed to install new versions of Anaconda Python any more.

There are alternatives to the Anaconda ecosystem. You can look at [Python Package and Environment Management](virtualenv.md) article for more information. As MPCDF/MPIA are adopting miniforge as a replacement for Anaconda, this article will guide you through the migration process from Anaconda/Miniconda to Miniforge.

[Miniforge](https://github.com/conda-forge/miniforge) is a minimalistic, community-driven distribution of the Conda package manager and the Python programming language. It is designed to be a lightweight alternative to the larger Anaconda distribution, focusing on providing only the essential tools needed for package management and Python development. Miniforge is particularly useful for users who want a more streamlined and customizable environment without the extensive set of pre-installed packages that come with Anaconda. It supports various platforms, including Windows, macOS, and Linux, and allows users to easily create and manage virtual environments for their projects. Miniforge is maintained by the community and is often updated to include the latest features and improvements from the Conda ecosystem.

We detail below a step-by-step guide to migrate your environment(s) from Anaconda/Miniconda to Miniforge. Of course some of these steps are fully applicable to migrating to other package/environment managers as well.

## Step 1 – Get info on current conda install

You first need to get a list of packages and an environment export in YML format from your current conda installation

```bash
# list all packages in the activated environment
conda list > base_pkg_list.txt
conda env export --name base > base_env.yml 
```

If you have several environments in your distribution, repeat the above steps for each one after activating them. Ensure you modify the filenames accordingly (e.g., replace "base" in the filenames).

## Step 2 - Clean up your conda references

- Edit all the environment YML files you created and remove `defaults` and anything with the full term `anaconda` from the channels. In addition, make sure `conda-forge` is in the channels or add it manually.

Example of yaml file before cleaning:
```yaml
name: base
channels:
  - defaults
  - conda-forge
dependencies:
  - _libgcc_mutex=0.1=main
  - _openmp_mutex=5.1=1_gnu
  - anaconda-anon-usage=0.4.4=py310hfc0e8ea_100
  - anaconda-client=1.12.3=py310h06a4308_0
  - anaconda-cloud-auth=0.5.1=py310h06a4308_0
  - anaconda-navigator=2.6.0=py310h06a4308_0
  - anaconda-project=0.11.1=py310h06a4308_0
  - annotated-types=0.6.0=py310h06a4308_0
  - archspec=0.2.3=pyhd3eb1b0_0
  - attrs=23.1.0=py310h06a4308_0
  - backports=1.1=pyhd3eb1b0_0
  - backports.functools_lru_cache=1.6.4=pyhd3eb1b0_0
  - backports.tempfile=1.0=pyhd3eb1b0_1
  - backports.weakref=1.0.post1=py_1
  - beautifulsoup4=4.12.2=py310h06a4308_0
  - boltons=23.0.0=py310h06a4308_0
  - brotli-python=1.0.9=py310h6a678d5_8
  - bzip2=1.0.8=h5eee18b_6
  - c-ares=1.19.1=h5eee18b_0
  - ca-certificates=2024.3.11=h06a4308_0
  - certifi=2024.2.2=py310h06a4308_0
  - cffi=1.16.0=py310h5eee18b_1
  - chardet=4.0.0=py310h06a4308_1003
  - charset-normalizer=2.0.4=pyhd3eb1b0_0
  ...
  - pip:
    - absl-py==2.1.0
    - astunparse==1.6.3
    - contourpy==1.2.1
    - cycler==0.12.1
    - flatbuffers==24.3.25
    - fonttools==4.52.4
  ```

If you want to try to recover the exact same python and package versions you had
in your Anaconda install then we clean the yaml file by first removing the
`defaults` channel (and other anaconda ones) and then removing the build strings from the package lines.

The following line will do this for you if you adapt it to you file names:
```bash
grep -v -ie '.*anaconda.*' base_env.yml | grep -v 'defaults' | sed -E 's/([^=])=[^=]*$/\1/'
```

if you want the latest versions of the packages instead, you can replace the sed expression
```bash
grep -v -ie '.*anaconda.*' base_env.yml | grep -v 'defaults' | sed -E 's/=*$//'
```

The yaml file should then look like this:
```yaml
name: base
channels:
  - conda-forge
dependencies:
  - _libgcc_mutex=0.1
  - _openmp_mutex=5.1
  - annotated-types=0.6.0
  - archspec=0.2.3
  ...
  - pip:
    - absl-py==2.1.0
    - astunparse==1.6.3
    - contourpy==1.2.1
    - cycler==0.12.1
    - flatbuffers==24.3.25
    - fonttools==4.52.4
  ```

- Save a copy of potential profile information files (you can skip if the files do not exist on your system):
    
```bash
mv ~/.condarc ~/bkp.condarc
mv ~/.anaconda ~/bkp.anaconda
```

- Remove potential cached files from `pip` to avoid reusing Anaconda licensed packages:

```bash
rm -rf ~/.cache/pip
```

## Step 3 - Install Miniforge (if not already done)

Download the Miniforge installer for your platform from the [Miniforge GitHub releases page](https://github.com/conda-forge/miniforge)

```bash
# on Mac and Linux
curl -LsSf "https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-$(uname)-$(uname -m).sh" | bash

# on Windows
powershell -c "irm https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-Windows-x86_64.exe | iex"
```

After this, follow the instructions on the screen (agree to terms and where to install)

The default location is `~/miniforge3`. If you want a seemless replacement of anaconda, use the path where anaconda was installed (but move it aside first) although this may have unexpected side effects.

After the installation, you should make sure the channels are configured properly. 
Check the list, which by default shows only `conda-forge`

```bash
conda config --show channels
```
```yaml
channels:
  - conda-forge

```
If you see `defaults`, remove it with `conda config -remove channel defaults` (Anaconda channel which requires a license).

Add any other channels `conda config --add channels <....>`

## Step 4 - recreate environments using the cleaned yaml files

First, do not forget to activate the new miniforge installation in your shell environment with

```bash
eval "$(/path/to/miniforge3/bin/conda shell.bash hook)"
```
where you update the path that corresponds to your installation.

or in some HPCs it is available as a module

```bash
module load miniforge
```

You can then create an enviroment with the specific configuration you had in your Anaconda environment with

```bash
conda env create --name <name> --file=<config>.yml
```
  
  where `<name>` is the name of the environment you want to create and `<config>.yml` is the cleaned yaml file you created in step 2.

If you directly want to update the active (base) one, you can use

```bash
conda env update --file=base_environment.yml
```

but this could sometimes fail with some old packages that are incompatible with new base enviroment.

As a good practice, you should not install a lot of packages in your `base` enviroment but prefer to create new environments for each project (or groups of projects) you are working on.