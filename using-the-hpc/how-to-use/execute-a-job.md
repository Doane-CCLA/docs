# Execute a Job on Your SHCP Condo Allocation

The tutorial below shows you how to run Wes Kendall's basic "hello world" program, written in C, using the message passing interface (MPI) to scale across the HPC Condo compute nodes [[1]](#works-cited). This tutorial is intended for users who are new to the HPC Condo environment and leverages a portable batch system (PBS) script and a C source code.

Additional examples can be found in [C++](examples/cpp.md), [Fortran](examples/fortran.md) or [Python](examples/python.md) sections.

**Table of Contents**

<!-- TOC depthFrom:2 depthTo:3 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Step 1: Access Your Allocation](#step-1-access-your-allocation)
- [Step 2: Create a PBS Script](#step-2-create-a-pbs-script)
	- [Example PBS Script](#example-pbs-script)
	- [PBS Script Breakdown](#pbs-script-breakdown)
	- [PBS Procedure](#pbs-procedure)
- [Step 3: Compile the C Program from Source](#step-3-compile-the-c-program-from-source)
	- [MPI Hello World Source Code](#mpi-hello-world-source-code)
	- [C Procedure](#c-procedure)
- [Step 4: Run the Job](#step-4-run-the-job)

<!-- /TOC -->

📝 **Note:** Do not execute jobs on the login nodes; only use the login nodes to access your compute nodes. Processor-intensive, memory-intensive, or otherwise disruptive processes running on login nodes will be killed without warning.

## Step 1: Access Your Allocation

Open and Moderate protection zones each have their own login node. Choose the login node for your protection zone. For this tutorial, we will be using the Open protection zone. If you need to request an allocation, see [instructions here](request-access.md).

📝 **Note:** The Open protection zone can be accessed either using either XCAMS or UCAMS credentials. However, the Moderate protection zone requires an ORNL UCAMS ID.

1. Open a Bash terminal (or PuTTY for Windows users).
2. Execute `ssh username@hostname`.
3. When prompted, enter your password.

Once you have connected to the login node, you can proceed to Step 2 and begin assembling your PBS script.

## Step 2: Create a PBS Script

Below is the PBS script we are using to run an MPI "hello world" program as a batch job. PBS scripts use variables to specify things like the number of nodes and cores used to execute your job, estimated walltime for your job, and which compute resources to use (e.g., GPU _vs._ CPU). The sections below feature an example PBS script for HPC resources, show you how to create and save your own PBS script, and show you how store the PBS script on an HPC file system.

Consult the [official Torque documentation](http://docs.adaptivecomputing.com/torque/4-0-2/Content/topics/commands/qsub.htm) for a complete list of PBS variables.

### Example PBS Script

Here is an example PBS script for running a batch job on a HPC Condo allocation. We break down each command in the section below.

```bash
#!/bin/bash

#PBS -N mpi_hello_world_c
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
mpirun hello_world_c
```

### PBS Script Breakdown

Here, we break down the essential elements of the above PBS script.

- `#!/bin/bash`: sets the script type
- `#PBS -N mpi_hello_world_c`: sets the job name; your output files will share this name
- `#PBS -M your_email@example.com`: add your email address if you would like errors to be emailed to you
- `#PBS -l nodes=1:ppn=16`: sets the number of nodes and processors per node that you want to use to run your job; in this case, we're using one node and 16 cores per node.
- `#PBS -l walltime=0:00:6:0`: tells PBS the anticipated runtime for your job, where `walltime=HH:MM:S`
- `#PBS -W group_list=group_name`: specifies your LDAP group; the full list of HPC Condo LDAP groups is [here](request-access.md#HPC-condo-groups)
- `#PBS -A group`: specifies your account type; list of account types is found [here](request-access.md#HPC-condo-groups)
- `#PBS -l qos=burst`: sets the quality of service (QOS) to <kbd>burst</kbd> or <kbd>std</kbd>
    - Burst jobs allow a user to leverage more nodes/cores/GPUs than may be in their formal allocation. However, in exchange for this "resource burst" flexibility, your burst job may be preempted if the rightful owner of those resources needs them to complete his or her own jobs.
    - In most cases, a user will simply run a job with the QOS set to <kbd>std</kbd>.
- `module purge`: clears any modules currently loaded that might result in a conflict
- `module load PE-gnu`: loads the PE-gnu module, which loads OpenMPI, GCC, and XALT
- `module list`: confirms the modules that were loaded.
- `cd $PBS_O_WORKDIR`: sets the working path
    - In this example, our binary will be launched from the same directory as our PBS script. The results from the binary will also be placed here.
- `pwd`: confirms current working directory
- `mpirun hello_world_c`: calls MPI to run our `hello_world_c` binary


### PBS Procedure

Now that we have covered the basics of a PBS script in the context of an HPC Condo, we will now talk about actually creating and using the script on your allocation.

When creating and editing your PBS script, we will be working on the login node (from Lustre storage) using the text editor, Vi. _If Lustre storage is not available, you may complete this tutorial from within your home directory on NFS._

1. From the login node, change your working directory to the desired file system. We are going to use our Lustre allocation for this example.

  ```bash
  cd /lustre/group/username
  ```

2. Use Vi to create and edit your PBS script.

  ```bash
  vi hello_world_c.pbs
  ```

3. Write your PBS script within Vi or paste the contents of your PBS script into Vi.

  - Hit `Esc` on your keyboard to exit the input mode.
  - Enter `:set paste` into Vi's command line, and press `Return` to enter paste mode.
  - Paste the PBS code into Vi.
  -
4. When finished, hit `Esc` on your keyboard to exit the input mode.
5. Enter `:x!` into Vi's command line, and press `Return` to save your file and return to the Bash shell.

With the PBS script in place, you can now move on to compiling your hello world C code in Step 3.

## Step 3: Compile the C Program from Source

Below is Wes Kendall's simple "hello world" C program that utilizes MPI to run the job in parallel [[1]](#works-cited). We will need to compile this source code on one of the compute nodes.

### MPI Hello World Source Code

```c
#include <mpi.h>
#include <stdio.h>

int main(int argc, char** argv) {
    // Initialize the MPI environment.
    MPI_Init(NULL, NULL);
    // Get the number of processes.
    int world_size;
    MPI_Comm_size(MPI_COMM_WORLD, &world_size);
    // Get the rank of the process.
    int world_rank;
    MPI_Comm_rank(MPI_COMM_WORLD, &world_rank);
    // Get the name of the processor.
    char processor_name[MPI_MAX_PROCESSOR_NAME];
    int name_len;
    MPI_Get_processor_name(processor_name, &name_len);
    // Print off a hello world message.
    printf("Hello world from processor %s, rank %d"
           " out of %d processors\n",
           processor_name, world_rank, world_size);
    // Finalize the MPI environment.
    MPI_Finalize();
}
```


### C Procedure

When creating and editing your `hello_world.c` source code, we will be working on the login node (from Lustre storage) using the text editor, Vi. _If Lustre storage is not available, you may complete this tutorial from within your home directory on NFS._

1. Ensure that you are still in your working directory (`/lustre/group/username`) using `pwd`.
2. Use Vi (`vi`) to create your C source file within your working directory.

  ```bash
  vi hello-world.c
  ```

3. Paste the hello world C code into Vi.

  - Hit `Esc` on your keyboard to exit the input mode.
  - Enter `:set paste` into Vi's command line, and press `Return` to enter paste mode.
  - Paste the C code into Vi.

4. When finished, hit `Esc` on your keyboard to exit the paste/input mode.
5. Enter `:x!` into Vi's command line, and press `Return` to save your file and return to the Bash shell.<br>
  You now have a C source file that you can compile.
6. Load the MPI compiler using the PE-gnu module.

  ```bash
  module load PE-gnu
  ```

7. Compile the C source into a binary executable file.

  ```bash
  mpicc -o hello_world_c hello_world.c
  ```

8. Use `ls -al` to verify the presence of the `hello_world_c` binary in your working directory.

With the C code compiled into a binary (`hello_world_c`), we can now schedule and run the job on our compute nodes.

## Step 4: Run the Job

1. Before proceeding, ensure that you are still in your working directory (using `pwd`) and that you still have the PE-gnu module loaded (using `module list`).

  - We need to be in the same path/directory as our PBS script and our C binary. Use `ls -al` to confirm their presence.
  - PE-gnu also loads OpenMPI, GCC, and XALT. Use `module list` to confirm their presence. If necessary, use `module load PE-gnu` to reload the module(s).

2. Use `qsub` to schedule your batch job in the queue.

  ```bash
  qsub hello_world_c.pbs
  ```

  This command will automatically queue your job using Torque and produce a six-digit job number (shown below).

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
  Once your job completes, Torque will produce two output/data files. These output/data files, unless otherwise specified in the PBS script, are placed in the same path as your binary.<br>
  One file (`myscript.o<jobnumber>`) contains the results of the binary you just executed, and the other (`myscript.e<jobnumber>`) contains any errors that occurred during execution.<br>
  Replace "myscript" with the name of your script and "&lt;jobnumber&gt;" with your job number.<br>
  You can view the contents of these files using the `more` command followed by the file name.<br>

  ```bash
  more mpi_hello_world_c.o143295
  ```

  Your output should look something like this, with one line per processor core (16 in this case):

  ```bash
    Hello world from processor node_name, rank 3 out of 16 processors
    Hello world from processor node_name, rank 4 out of 16 processors
    Hello world from processor node_name, rank 6 out of 16 processors
    Hello world from processor node_name, rank 11 out of 16 processors
    Hello world from processor node_name, rank 7 out of 16 processors
    Hello world from processor node_name, rank 14 out of 16 processors
    Hello world from processor node_name, rank 2 out of 16 processors
    Hello world from processor node_name, rank 5 out of 16 processors
    Hello world from processor node_name, rank 8 out of 16 processors
    Hello world from processor node_name, rank 9 out of 16 processors
    Hello world from processor node_name, rank 10 out of 16 processors
    Hello world from processor node_name, rank 12 out of 16 processors
    Hello world from processor node_name, rank 13 out of 16 processors
    Hello world from processor node_name, rank 15 out of 16 processors
    Hello world from processor node_name, rank 0 out of 16 processors
    Hello world from processor node_name, rank 1 out of 16 processors
  ```

4. Download your results (using the `scp` command or an SFTP client) or move them to persistent storage. See our [moving data](../../data-transfer-storage/moving-data.md) section for help.

#### Works Cited

1. Wes Kendall, "MPI Hello World," _MPI Tutorial_, accessed June 14, 2017, <http://mpitutorial.com/tutorials/mpi-hello-world/>.

#### Additional Examples
- [Working with C++](examples/cpp.md)
- [Working with Fortran](examples/fortran.md)
- [Working with Python](examples/python.md)
- [Working with Makefiles](examples/makefile.md)
