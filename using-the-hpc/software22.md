# Software

DEFAULT SHELL

The default shell on the CCLA cluster is bash. However, CCLA supports the following shells:

* `bash`
* `tcsh`
* `csh`
* `ksh`

USING MODULES  
The modules software package allows you to dynamically modify your user environment by using pre-written module files.

Each module file contains the information needed to configure the shell for an application. After the modules software package is initialized, the environment can be modified on a per-module basis using the module command, which interprets a module file. Typically, a module file instructs the module command to alter or set shell environment variables such as PATH or MANPATH. Module files can be shared by many users on a system, and users can have their own personal collection to supplement and/or replace the shared module files. As a user, you can add and remove module files from your current shell environment. The environment changes performed by a module file are viewed by using the module command. More information on modules are found by running man module.

To access ARM specific softwares in your environment, add following to your `.bashrc`

```text
export MODULEPATH=/software/user_tools/current/cades-arm/modulefiles:$MODULEPATH
```

SUMMARY OF MODULE COMMANDS

| Command | Description |
| --- | --- |
| module list | Lists modules currently located in user's environment |
| module avail | Lists all available modules on a system in condensed format |
| module avail -l | Lists all available modules on a system in long format |
| module display | Shows environment changes that will be made by loading a given module |
| module load | Loads a module |
| module unload | Unloads a module |
| module help | Shows help for a module |
| module swap | Swaps a currently loaded module for an unloaded module |

## Available Software

Additional software may be installed within the cluster, as required. To check list of available software run command `module avail`.

| Module | Description |
| --- | --- |
| ADI | ARM Data Integrator, ADI, is an open source framework that automates the process of retrieving and preparing data for analysis, simplifies the design and creation of output data products produced by the analysis, and provides a modular, flexible software development architecture for implementing algorithms. |
| PE-gnu PE-intel PE-nag PE-pgi: | This module sets up the Intel Programming Environment \(PE\). |
| tensorflow/0.11-cpu tensorflow/0.11-gpu: | Tensoflow is a ML engine developed by Google. |
| R/3.3.2 | R is a programming language and software environment for statistical computing and graphics. |
| theano/0.9-conda | Theano is a python library to support ML. |
| caffe/1.0-conda | Caffe is a python library to support ML. |
| ncl | NCL is an interpreted language designed specifically for scientific data analysis and visualization. |
| cuda/8.0 | CUDA is a parallel computing platform that enables GPU for general purpose processing. |
| keras/2.0.2-conda | keras is a python library to support ML. |
| cdo | CDO is a collection of command line Operators to manipulate and analyse Climate and NWP model Data. |
| nco | NCO The NCO toolkit manipulates and analyzes data stored in netCDF-accessible formats, including DAP, HDF4, and HDF5. |
| ATLAS | ATLAS is an optimized BLAS library with limited LAPACK routines. |
| anaconda2 | Anaconda is an open source distribution of the Python and R programming languages for large-scale data processing, predictive analytics, and scientific computing, that aims to simplify package management and deployment. |
| git | Git is a is a version control system primarily used for software development for tracking changes in computer files and coordinating work on those files among multiple people. |
| data\_wrapper/1.0.0 | The data wrapper provides a convenient wrapper around globus-url-copy. It simplifies the usage of globus-url-copy. |
| postgresql | PostgreSQL is an object-relational database management system. |
| netcdf/4.3.3.1 | NetCDF is a data model, library, and file format for storing and managing data. |

To see list of softwares loaded in your environment, run command `module list`

Some of the currently loaded modules are:

* gcc/5.3.0
* git/2.11.0
* python/2.7.12
* cuda/7.5
* hdf5-parallel/1.8.17
* netcdf/4.3.3.1

## Requesting New Software

To request a new software, please [contact the CCLA](../SUPPORT.md)
