[CADES](http://support.cades.ornl.gov/) → [User Documentation](../README.md) → [SHPC Condo User Guide](overview.md) → [Software](software.md)

# SHPC Condo Software Configuration

In this section, we discuss the SHPC Condos software configuration. Our software environment uses Linux environment [modules](software/modules.md) to perform this configuration. The software modules available to users also contain preconfigured [compiler toolchains](software/compilers.md), or programming environments which include parallel compiler wrappers and associated MPI stacks. There are also [workflow tools](software/workflows.md) that may help with your applications as well.

## Job Scheduler

SHPC utilizes Torque/Moab as a resource manager to schedule jobs, where Moab is used as an external scheduler for the PBS resource management system including job queues and the compute resources.

📝 The job scheduler supports a maximum walltime of 48 hours. If you need more time to run a job, please [contact us](../../SUPPORT.md).

## Modules

SHPC has more than one hundred software packages installed. Our software environment uses Linux (CentOS 7.x) environment modules to manage versions and dependencies of software packages. When you load a module, it sets the environment variables necessary for running your program.

A list of available software modules can be viewed by typing `module avail`.

**Modules: Local repository**<br>
By default the local repository is used as a source of software installations. To list available modules, type `module avail`. To load a module, use `module load module_name`. Similarly, unload modules by typing `module unload module_name`.

**Modules: CVMFS-based repository**<br>
A CVMFS (Cern Virtual File System)-based repository is available for use that has several software packages available for use. To use the CVMFS-based repository run the following commands from your login node:

```bash
source /software/dev_tools/swtree/cs400/modulefiles/switch-modules.sh
```

```bash
switch_modules oasis
```

After entering the above commands the new repository should be active and the command below will list the software available for use:

```bash
module avail
```

Similarly `switch_modules local` will bring back the local modules to use.

Additional information on SHPC modules may be found [here](software/modules.md).

## Compiler ToolChains

Depending on the application/code you are working on, you might choose a specific compiler to achieve the best performance of your programs. Compiler toolchains such as GNU, Intel, PGI and NAG are already installed to work with other libraries. [See here](software/compilers.md) for more information on SHPC compilers

## Workflow Tools

Workflow tools orchestrate multi-stage computations. Several [workflow tools](software/workflows.md) are available on SHPC.

## Notes on Specific Software Usage

### Singularity Containers over MPI-IB
By default, singularity does not use the InfiniBand libraries when doing message passing with MPI. In order to make sure Singularity uses the InfiniBand libraries while using MPI, perform the following step after loading the Singularity module:

```
source sourceme_for_mpioverib
```

Following the above step, the Singularity containers should use the InfiniBand libraries when running MPI applications.

### Visualizing Remote Data over SSH using Visit

Visit is a well-known visualization software package that is available on SHPC. Visit may be configured by creating the profile of SHPC Condo to visualize data from your local Visit client. In order to do so, follow the steps as shown below on your local Visit:

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
9. You should be able to see your data on the SHPC file system which can be opened just as if it were local data
