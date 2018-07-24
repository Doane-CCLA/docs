# HPC Software Configuration

In this section, we discuss the HPC Condos software configuration. Our software environment uses Linux environment [modules](how-to-use/modules.md) to perform this configuration. The software modules available to users also contain preconfigured [compiler toolchains](how-to-use/compilers.md), or programming environments which include parallel compiler wrappers and associated MPI stacks. There are also [workflow tools](how-to-use/workflows.md) that may help with your applications as well.

## Modules

The HPC software environment uses Linux environment modules to manage versions and dependencies of software packages. When you load a module, it sets the environment variables necessary for running your program.

A list of available software modules can be viewed by typing `module avail`.

**Modules: Local repository**<br>
By default the local repository is used as a source of software installations.

**Modules: CVMFS-based repository**<br>
A CVMFS (Cern Virtual File System)-based repository is available that has several software packages.

Additional information on HPC modules may be found [here](how-to-use/modules.md).

## Notes on Specific Software Usage

### Singularity Containers over MPI-IB
By default, Singularity does not use the InfiniBand libraries when doing message passing with MPI. In order to make sure Singularity uses the InfiniBand libraries while using MPI, perform the following step after loading the Singularity module:

```
source sourceme_for_mpioverib
```

Following the above step, the Singularity containers should use the InfiniBand libraries when running MPI applications.

### Visualizing Remote Data over SSH using Visit

Visit is a well-known visualization software package that is available on HPC. Visit may be configured by creating the profile of HPC Condo to visualize data from your local Visit client. In order to do so, follow the steps as shown below on your local Visit:

1. Start Visit and go to `Options` → `Host profiles`
2. Press `New Host` and populate the fields as described below
    - Host nickname: `cades`
    - Remote host name: `or-condo-login.ornl.gov`
    - Host name aliases: `or-condo-login#g`
    - Path to Visit installation: `/software/dev_tools/swtree/cs400_centos7.2_pe2016-08/visit/2.10.3/centos7.2_gnu5.3.0`
    - Username: `<your_ucams_id>`
5. Check the `Tunnel data ...` checkbox
6. Click on `Apply`
7. Now in the `file` → `open` menu, click on the dropdown (&#9662;) and select `cades`
8. Enter your password in the dialog box that opens
9. You should be able to see your data on the HPC file system which can be opened just as if it were local data
