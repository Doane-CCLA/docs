# Execute a Job on Doane's HPC Onyx

The tutorial below shows you how to run Wes Kendall's basic "hello world" program, written in C, using the message passing interface (MPI) to scale across the HPC compute nodes [[1]](#works-cited). This tutorial is intended for users who are new to the HPC environment and leverages a Slurm batch (sbatch) script and a C source code.

Additional examples can be found in [C++](examples/cpp.md), [Fortran](examples/fortran.md) or [Python](examples/python.md) sections.

**Table of Contents**

<!-- TOC depthFrom:2 depthTo:3 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Step 1: Access the Onyx HPC](#step-1-access-the-onyx-hpc)
- [Step 2: Create an sbatch Script](#step-2-create-a-sbatch-script)
	- [Example sbatch Script](#example-sbatch-script)
	- [sbatch Script Breakdown](#sbatch-script-breakdown)
	- [sbatch Procedure](#sbatch-procedure)
- [Step 3: Compile the C Program from Source](#step-3-compile-the-c-program-from-source)
	- [MPI Hello World Source Code](#mpi-hello-world-source-code)
	- [C Procedure](#c-procedure)
- [Step 4: Run the Job](#step-4-run-the-job)

<!-- /TOC -->

📝 **Note:** Do not execute jobs on the login nodes; only use the login nodes to access your compute nodes. Processor-intensive, memory-intensive, or otherwise disruptive processes running on login nodes will be killed without warning.

## Step 1: Access the Onyx HPC

1. Open a Bash terminal (or PuTTY for Windows users).
2. Execute `ssh doaneusername@onyx.doane.edu`.
3. If promted by a security message, type `yes` to continue connection.
4. When prompted, enter your password.

Once you have connected to the head node, you can proceed to Step 2 and begin assembling your sbatch script.

## Step 2: Create an sbatch Script

Below is the sbatch script we are using to run an MPI "hello world" program as a batch job. sbatch scripts use variables to specify things like the number of nodes and cores used to execute your job, estimated walltime for your job, and which compute resources to use (e.g., GPU _vs._ CPU). The sections below feature an example sbatch script for HPC resources, show you how to create and save your own sbatch script, and show you how store the sbatch script on an HPC file system.

Consult the [official Slurm documentation](https://slurm.schedmd.com/sbatch.html) for a complete list of sbatch variables.

### Example sbatch Script

Here is an example sbatch script for running a batch job on Onyx. We break down each command in the section below.

```bash
#!/bin/bash
#SBATCH -n 16
#SBATCH -o test_%A.out
#SBATCH --mail-user $CHANGE_TO_YOUR_EMAIL
#SBATCH --mail-type ALL

module purge
module load gnu
module load openmpi
module list
srun --ntasks=${SLURM_NTASKS} --mpi=openmpi hello_world_c
```

### sbatch Script Breakdown

Here, we break down the essential elements of the above PBS script.

- `#!/bin/bash`: sets the script type
- `#SBATCH -n 8`: sets the number of processors that you want to use to run your job; use -N to specify nodes instead of processors
- `#SBATCH -o test_%A.out`: sets the name of the output file; here `%A` will be replaced by slurm with the job number; 
- `#SBATCH --mail-user $CHANGE_TO_YOUR_EMAIL`: add your email address if you would like your job's status to be emailed to you
- `#SBATCH --mail-type ALL`: specifies which job status changes you want to be notified about; options include: NONE, BEGIN, END, FAIL, REQUEUE, ALL
- `module purge`: clears any modules currently loaded that might result in a conflict
- `module load gnu`: loads the gnu module, which loads GCC
- `module load openmpi`: loads the openmpi module
- `module list`: confirms the modules that were loaded.
- `srun --ntasks=${SLURM_NTASKS} --mpi=openmpi hello_world_c`: Slurm calls OpenMPI to run our `hello_world_c` binary with the number of processors we specified earlier.


### sbatch Procedure

Now that we have covered the basics of a sbatch script in the context of an HPC, we will now talk about actually creating and using the script on Onyx.

When creating and editing your sbatch script, we will be working on the head node using the text editor, nano. 

1. From the login node, change your working directory to your home directory. 
  ```bash
  cd
  ```

2. Use nano to create and edit your sbatch script.

  ```bash
  nano hello_world_c.job
  ```

3. Write your sbatch script within nano or paste the contents of your sbatch script into nano.
  - Copy sbacth script from this page
  - Hit Control/Command + p key to paste into nano from Windows/MacOS
  
4. When finished, hit `^X` (control + x key) to exit.
5. Enter `Y` to save your changes, and press `Return` to save your file and return to the Bash shell.

With the sbatch script in place, you can now move on to compiling your hello world C code in Step 3.

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

When creating and editing your `hello_world.c` source code, we will be working on the head node using the text editor, nano. 

1. Ensure that you are still in your working directory (`/home/username`) using `pwd`.
2. Use nano (`nano`) to create your C source file within your working directory.

  ```bash
  nano hello-world.c
  ```

3. Paste the hello world C code into nano.

  - Copy C code from this page
  - Hit Control/Command + p key to paste into nano from Windows/MacOS

4. When finished, hit `^X` (control + x key) to exit.
5. Enter `Y` to save your changes, and press `Return` to save your file and return to the Bash shell.<br>
  You now have a C source file that you can compile.
6. Load the MPI compiler using the gnu module.

  ```bash
  module load gnu
  ```

7. Compile the C source into a binary executable file.

  ```bash
  mpicc -o hello_world_c hello_world.c
  ```

8. Use `ls -al` to verify the presence of the `hello_world_c` binary in your working directory.

With the C code compiled into a binary (`hello_world_c`), we can now schedule and run the job on our compute nodes.

## Step 4: Run the Job

1. Before proceeding, ensure that you are still in your working directory (using `pwd`) and that you still have the gnu module loaded (using `module list`).

  - We need to be in the same path/directory as our sbatch script and our C binary. Use `ls -al` to confirm their presence.
  
2. Use `sbatch` to schedule your batch job in the queue.

  ```bash
  sbatch hello_world_c.job
  ```

  This command will automatically queue your job using Slurm and produce a job number.

  You can check the status of your job at any time with the `squeue` command.

  ```bash
  squeue <jobnumber>
  ```

  You can also stop your job at any time with the `scancel` command.

  ```bash
  scancel <jobnumber>
  ```

3. View your results.<br>
  Once your job completes, slurm will produce an output/data file. This output/data file, unless otherwise specified in the sbatch script, are placed in the same path as your binary.<br>
  The file (`test_<jobnumber>.out`) contains the results of the binary you just executed.<br>
  Replace "myscript" with the name of your script and "&lt;jobnumber&gt;" with your job number.<br>
  You can view the contents of these files using the `more` command followed by the file name.<br>

  ```bash
  more test_<jobnumber>.out
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
