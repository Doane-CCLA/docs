# Execute a Job: _Fortran Example_

The tutorial assumes you have already worked through the [Execute a Job Tutorial](../execute-a-job.md). Therefore, the instructions here are abbreviated but will follow the same format so you may easily consult the extended tutorial.

**Table of Contents**

<!-- TOC depthFrom:2 depthTo:3 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Step 1: Access Your Allocation](#step-1-access-your-allocation)
- [Step 2: Create a PBS Script](#step-2-create-a-pbs-script)
	- [Example PBS Script](#example-pbs-script)
	- [PBS Procedure](#pbs-procedure)
- [Step 3: Compile the Fortran Program from Source](#step-3-compile-the-fortran-program-from-source)
	- [MPI Hello World Source Code](#mpi-hello-world-source-code)
	- [Fortran Procedure](#fortran-procedure)
- [Step 4: Run the Job](#step-4-run-the-job)

<!-- /TOC -->

📝 **Note:** Do not execute jobs on the login nodes; only use the login nodes to access your compute nodes. Processor-intensive, memory-intensive, or otherwise disruptive processes running on login nodes will be killed without warning.

## Step 1: Access Your Allocation

If you need to request an allocation, see [instructions here](../request-access.md).

1. Open a Bash terminal (or PuTTY for Windows users).
2. Execute `ssh username@or-condo-login.ornl.gov`.

  - Replace "username" with your XCAMS or UCAMS ID.

3. When prompted, enter your XCAMS or UCAMS password.


## Step 2: Create a PBS Script

### Example PBS Script

Here is an example PBS script for running a batch job on a HPC Condo allocation.

```bash
#!/bin/bash

#PBS -N mpi_hello_world_f
#PBS -M your_email@ornl.gov
#PBS -l nodes=1:ppn=16
#PBS -l walltime=0:00:6:0
#PBS -W group_list=cades-birthright
#PBS -A birthright
#PBS -l qos=burst
#PBS -V

module purge
module load PE-gnu
module list
cd $PBS_O_WORKDIR
pwd
mpirun hello_world_f
```


### PBS Procedure

1. From the login node, change your working directory to the desired file system. We are going to use our Lustre allocation for this example. _If Lustre storage is not available, you may complete this tutorial from within your home directory on NFS._

  ```bash
  cd /lustre/or-hydra/cades-birthright/username
  ```

  Replace "username" with your UCAMS/XCAMS user ID.

2. Use Vi to create and edit your PBS script.

  ```bash
  vi hello_world_f.pbs
  ```

3. Create your PBS script within Vi or paste the contents of your PBS script into Vi.
4. Save your file and return to the Bash shell.


## Step 3: Compile the Fortran Program from Source

### MPI Hello World Source Code

```fortran
program helloworld
use mpi
integer ierr, numprocs, procid

call MPI_INIT(ierr)

call MPI_COMM_RANK(MPI_COMM_WORLD, procid, ierr)
call MPI_COMM_SIZE(MPI_COMM_WORLD, numprocs, ierr)

print *, "Hello world! I am process ", procid, "out of", numprocs, "!"

call MPI_FINALIZE(ierr)

stop
end
```

### Fortran Procedure

1. Ensure that you are still in your working directory (`/lustre/or-hydra/cades-birthright/username`) using `pwd`.
2. Use Vi (`vi`) to create your Fortran source file within your working directory.

  ```bash
  vi hello_world.f90
  ```
4. Save your file and return to the Bash shell.
5. Load the MPI compiler using the PE-gnu module.

  ```bash
  module load PE-gnu
  ```

6. Compile the Fortran source into a binary executable file.

  ```bash
  mpifort -o hello_world_f hello_world.f90
  ```

7. Use `ls -al` to verify the presence of the `hello_world_f` binary in your working directory.


## Step 4: Run the Job

1. Before proceeding, ensure that you are still in your working directory (using `pwd`) and that you still have the PE-gnu module loaded (using `module list`).

  - We need to be in the same path/directory as our PBS script and our Fortran binary. Use `ls -al` to confirm their presence.
  - PE-gnu also loads OpenMPI, GCC, and XALT. Use `module list` to confirm their presence. If necessary, use `module load PE-gnu` to reload the module(s).

2. Use `qsub` to schedule your batch job in the queue.

  ```bash
  qsub hello_world_f.pbs
  ```

  This command will automatically queue your job using Torque and produce a six-digit job number (shown below).<br>

  ```bash
  143295.or-condo-pbs01
  ```

  You can check the status of your job at any time with the `checkjob` command.

  ```bash
  checkjob 143295
  ```

  You can also stop your job at any time with the `qdel` command.

  ```bash
  qdel 143295
  ```

3. View your results.<br>
  You can view the contents of these files using the `more` command followed by the file name.<br>

  ```bash
  more mpi_hello_world_f.o143295
  ```

  Your output should look something like this (_the output is truncated._):

  ```bash
  Hello world! I am process            3 out of          20 !
  Hello world! I am process            0 out of          20 !
  Hello world! I am process            1 out of          20 !
  Hello world! I am process            7 out of          20 !
  Hello world! I am process            8 out of          20 !
  Hello world! I am process            2 out of          20 !
  Hello world! I am process            6 out of          20 !
  Hello world! I am process           11 out of          20 !
  .
  .
  .
  ```

4. Download your results (using the `scp` command or an SFTP client) or move them to persistent storage. See our [moving data](../../../data-transfer-storage/moving-data.md) section for help.

#### Additional Examples
- [Working with C](../execute-a-job.md)
- [Working with C++](cpp.md)
- [Working with Python](python.md)
- [Working with Makefiles](makefile.md)
