# Execute a Job: _C++ Example_

The tutorial assumes you have already worked through the [Execute a Job Tutorial](../execute-a-job.md). Therefore, the instructions here are abbreviated but will follow the same format so you may easily consult the extended tutorial.

**Table of Contents**

<!-- TOC depthFrom:2 depthTo:3 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Step 1: Access Your Allocation](#step-1-access-your-allocation)
- [Step 2: Create a PBS Script](#step-2-create-a-pbs-script)
	- [Example PBS Script](#example-pbs-script)
	- [PBS Procedure](#pbs-procedure)
- [Step 3: Compile the C++ Program from Source](#step-3-compile-the-c-program-from-source)
	- [MPI Hello World Source Code](#mpi-hello-world-source-code)
	- [C++ Procedure](#c-procedure)
- [Step 4: Run the Job](#step-4-run-the-job)

<!-- /TOC -->

📝 **Note:** Do not execute jobs on the login nodes; only use the login nodes to access your compute nodes. Processor-intensive, memory-intensive, or otherwise disruptive processes running on login nodes will be killed without warning.

## Step 1: Access Your Allocation

If you need to request an allocation, see [instructions here](../request-access.md).

1. Open a Bash terminal (or PuTTY for Windows users).
2. Execute `ssh username@hostname`.
3. When prompted, enter your password.

## Step 2: Create a PBS Script

### Example PBS Script

Here is an example PBS script for running a batch job on a HPC allocation.

```bash
#!/bin/bash

#PBS -N mpi_hello_world_cpp
#PBS -M your_email@example.com
#PBS -l nodes=1:ppn=16
#PBS -l walltime=0:00:6:0
#PBS -W group_list=group_name
#PBS -A group
#PBS -l qos=burst
#PBS -V

module purge
module load PE-gnu
module list
cd $PBS_O_WORKDIR
pwd
mpirun hello_world_cpp
```


### PBS Procedure

1. From the login node, change your working directory to the desired file system. We are going to use our Lustre allocation for this example. _If Lustre storage is not available, you may complete this tutorial from within your home directory on NFS._

  ```bash
  cd /lustre/group/username
  ```

2. Use Vi to create and edit your PBS script.

  ```bash
  vi hello_world_cpp.pbs
  ```

3. Create your PBS script within Vi or paste the contents of your PBS script into Vi.
4. Save your file and return to the Bash shell.


## Step 3: Compile the C++ Program from Source

### MPI Hello World Source Code

```c++
#include<iostream>
#include "mpi.h"

using namespace std;
#include "mpi.h"

int main(int argc, char *argv[])
{
    int id, p, name_len;
    char processor_name[MPI_MAX_PROCESSOR_NAME];     
    MPI::Init(argc, argv);
    p = MPI::COMM_WORLD.Get_size();
    id = MPI::COMM_WORLD.Get_rank();
    MPI_Get_processor_name(processor_name, &name_len);
    cout<<" Processor " << processor_name<<" ID="<<id<< " Hello world\n";
    MPI::Finalize();
return 0;
}
```

### C++ Procedure

1. Ensure that you are still in your working directory (`/lustre/group/username`) using `pwd`.
2. Use Vi (`vi`) to create your C++ source file within your working directory.
4. Save your file and return to the Bash shell.
5. Load the MPI compiler using the PE-gnu module.

  ```bash
  module load PE-gnu
  ```

5. Compile the C++ source into a binary executable file.

  ```bash
  mpic++ -o hello_world_cpp hello_world.cpp
  ```

7. Use `ls -al` to verify the presence of the `hello_world_cpp` binary in your working directory.


## Step 4: Run the Job

1. Before proceeding, ensure that you are still in your working directory (using `pwd`) and that you still have the PE-gnu module loaded (using `module list`).

  - We need to be in the same path/directory as our PBS script and our C++ binary. Use `ls -al` to confirm their presence.
  - PE-gnu also loads OpenMPI, GCC, and XALT. Use `module list` to confirm their presence. If necessary, use `module load PE-gnu` to reload the module(s).

2. Use `qsub` to schedule your batch job in the queue.

  ```bash
  qsub hello_world_cpp.pbs
  ```

  This command will automatically queue your job using Torque and produce a six-digit job number (shown below).<br>

  ```bash
  143295.node
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
  more mpi_hello_world_cpp.o143295
  ```

  Your output should look something like this (_the output is truncated._):

  ```bash
  Processor node ID=9  Hello world
  Processor node ID=4  Hello world
  Processor node ID=0  Hello world
  Processor node ID=1  Hello world
  Processor node ID=3  Hello world
  Processor node ID=5  Hello world
  Processor node ID=2  Hello world
  Processor node ID=6  Hello world
  Processor node ID=7  Hello world
  Processor node ID=8  Hello world
  .
  .
  .
  ```

4. Download your results (using the `scp` command or an SFTP client) or move them to persistent storage. See our [moving data](../../../data-transfer-storage/moving-data.md) section for help.

#### Additional Examples
- [Working with C](../execute-a-job.md)
- [Working with Fortran](fortran.md)
- [Working with Python](python.md)
- [Working with Makefiles](makefile.md)
