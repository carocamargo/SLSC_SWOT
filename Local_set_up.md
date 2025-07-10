Set up instructions have been modified from [WHOI CMIP Tutorial](https://theo.earth/whoi-climate-tutorial_2025/pages/setup/setup_venv.html)

# Python / virtual environment
First, we'll create a "virtual environment", which contains python and associated software packages (if you're comfortable with python/virtual environments, feel free to skip ahead to [software dependencies](#python-set-up)). 

## (optional) Set up virtual environment
### Manually
If you don't have a preferred package manager, we recommend using ```mamba``` (a faster version of the ```conda``` package manager). To use mamba:
1. Check if conda is installed by typing ```conda info``` at the command line. Also check if mamba is installed (if you have conda but not mamba installed you can run ```conda install -n base -c conda-forge mamba```). If you have neither, download and install miniforge following the instructions here: [https://github.com/conda-forge/miniforge](https://github.com/conda-forge/miniforge).

2. Create a virtual environment for the project with: ```mamba create -n SLSC_SWOT``` and activate your environment with ```conda activate SLSC_SWOT```

Using a package manager is benefitial because it:
- Allows you to install packages in an isolated environment, preventing clutter in your base Python environment with packages needed only for specific projects.
- Manages dependencies (as some packages rely on others) and resolves version conflicts (since some packages are only compatible with specific versions of others) for you.
- Keeps your system organized.

### Using environment.yml
1. Copy the [environment.yml](https://github.com/carocamargo/SLSC_SWOT/blob/main/environment.yml) file in your working directory.
2. Create your environment
  If you have mamba:
  ```mamba env create -f environment.yml```
  If you have conda:
  ```conda env create -f environment.yml```
You can then skip the [python-set-up](#python-set-up))
4. Activate it:
```conda activate SLCS_SWOT```

## Python Set Up
Next, we'll install python packages needed for the tutorial:

**Required packages**
```
  - xarray  
  - jupyterlab
  - cartopy
  - matplotlib
  - cmocean
  - copernicusmarine
  - os
  - pandas
```

These packages are necessary if you want to download swot data yourself:
**Optional packages**
```
  - geopandas
  - shapely
  - ftplib
  - getpass
```

If using ```mamba```, the command line syntax to install the packages is:
```
## activate your environment if it is not already
mamba activate SLCS_SWOT

## install required dependencies
mamba install -c conda-forge jupyterlab cartopy matplotlib cmocean pandas
mamba install -c conda-forge xarray "zarr<3" fsspec

## Install copernicusmarine from PyPI
pip install copernicusmarine

## install optional dependencies
mamba install -c conda-forge geopandas shapely ftplib getpass
```

(This should also work if you replace ```mamba``` with ```conda```, but will take longer). Note the "```-c conda-forge```" flag tells the package manager to download the packages located from the conda-forge channel. 

> **Note:**
If you're using conda and the ```conda install ...``` / ```conda env update ...``` commands are taking a long time, you could try [updating the solver to "libmamba"](https://www.anaconda.com/blog/a-faster-conda-for-a-growing-community).
If this doesn't work, you could also try setting the channel priority to flexible, with ```conda config --set channel_priority flexible```.

## Mamba/conda issues work around
On my case, my base environment was inconsistent, and I was not able to install mamba. A work around was to create a new enviroment and install mamba:
```conda create -n mamba-env -c conda-forge mamba python=3.10```
and then use that environment to install things on my other one:
``` conda activate mamba-env```
Install packages
```mamba install -n SLSC_SWOT -c conda-forge jupyterlab cartopy matplotlib cmocean pandas```
``` mamba install -n SLSC_SWOT -c conda-forge xarray "zarr<3" fsspec```
Leave the mamba environment
``` conda deactivate ```
Enter SWOT environment:
```  conda activate SLSC_SWOT ```
Install marinecopernicus with pip:
```pip install copernicusmarine  ```
Launch Jupyter Lab:
```jupyter lab```
