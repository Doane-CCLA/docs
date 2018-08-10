# HPC Software Configuration

In this section, we discuss the HPC Condos software configuration. Our software environment uses Linux environment [modules](modules.md) to perform this configuration. The software modules available to users also contain preconfigured [compiler toolchains](compilers.md), or programming environments which include parallel compiler wrappers and associated MPI stacks. There are also [workflow tools](workflows.md) that may help with your applications as well.

## Modules

The HPC software environment uses Linux environment modules to manage versions and dependencies of software packages. When you load a module, it sets the environment variables necessary for running your program.

A list of available software modules can be viewed by typing `module avail`.

**Modules: Local repository**<br>
By default the local repository is used as a source of software installations.

**Modules: CVMFS-based repository**<br>
A CVMFS (Cern Virtual File System)-based repository is available that has several software packages.

Additional information on HPC modules may be found [here](modules.md).

## Notes on Specific Software Usage

### Singularity Containers over MPI-IB
By default, Singularity does not use the InfiniBand libraries when doing message passing with MPI. In order to make sure Singularity uses the InfiniBand libraries while using MPI, perform the following step after loading the Singularity module:

```
source sourceme_for_mpioverib
```

Following the above step, the Singularity containers should use the InfiniBand libraries when running MPI applications.
