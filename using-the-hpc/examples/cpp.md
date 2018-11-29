# Execute a Job: _C++ Example_

The tutorial assumes you have already worked through the [Execute a Job Tutorial](../execute-a-job.md). Therefore, the instructions here are abbreviated but will follow the same format so you may easily consult the extended tutorial.

**Table of Contents**

<!-- TOC depthFrom:2 depthTo:3 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Step 1: Access the Onyx HPC](#step-1-access-the-onyx-hpc)
- [Step 2: Create an sbatch Script](#step-2-create-a-sbatch-script)
	- [Example sbatch Script](#example-sbatch-script)
	- [sbatch Procedure](#sbatch-procedure)
- [Step 3: Compile the C++ Program from Source](#step-3-compile-the-c-program-from-source)
	- [MPI Hello World Source Code](#mpi-hello-world-source-code)
	- [C++ Procedure](#c-procedure)
- [Step 4: Run the Job](#step-4-run-the-job)

<!-- /TOC -->

📝 **Note:** Do not execute jobs on the login nodes; only use the login nodes to access your compute nodes. Processor-intensive, memory-intensive, or otherwise disruptive processes running on login nodes will be killed without warning.

## Step 1: Access the Onyx HPC

If you need to request an allocation, see [instructions here](../request-access.md).

1. Open a Bash terminal (or MobaXterm for Windows users).
2. Execute `ssh doaneusername@onyx.doane.edu`.
3. When prompted, enter your password.

## Step 2: Create an sbatch Script

### Example sbatch Script

Here is an example sbatch script for running a batch job on a HPC allocation.

```bash
#!/bin/bash

#SBATCH -n 16
#SBATCH -o test_%A.out
#SBATCH --error test_%A.err
#SBATCH --mail-user $CHANGE_TO_YOUR_EMAIL
#SBATCH --mail-type ALL

module purge
module load gnu/5.4.0
module load openmpi
module list

srun hello.mpi
```


### sbatch Procedure

1. Use nano or Vim (we use Vim here) to create and edit your sbatch script.

  ```bash
  vim slurm_mpi_example.job
  ```

3. Create your sbatch script within Vim by typing ```i``` for ```insert``` mode or paste the contents of your sbatch script into Vim.
4. Save your file by typing ```:wq!``` and return to the Bash shell.


## Step 3: Compile the C++ Program from Source

### MPI Hello World Source Code

```c++
/*
  "Hello World" MPI Test Program
*/
#include <assert.h>
#include <stdio.h>
#include <string.h>
#include <mpi.h>

int main(int argc, char **argv)
{
    char buf[256];
    int my_rank, num_procs;

    /* Initialize the infrastructure necessary for communication */
    MPI_Init(&argc, &argv);

    /* Identify this process */
    MPI_Comm_rank(MPI_COMM_WORLD, &my_rank);

    /* Find out how many total processes are active */
    MPI_Comm_size(MPI_COMM_WORLD, &num_procs);

    /* Until this point, all programs have been doing exactly the same.
       Here, we check the rank to distinguish the roles of the programs */
    if (my_rank == 0) {
        int other_rank;
        printf("We have %i processes.\n", num_procs);

        /* Send messages to all other processes */
        for (other_rank = 1; other_rank < num_procs; other_rank++)
        {
            sprintf(buf, "Hello %i!", other_rank);
            MPI_Send(buf, sizeof(buf), MPI_CHAR, other_rank,
                     0, MPI_COMM_WORLD);
        }

        /* Receive messages from all other process */
        for (other_rank = 1; other_rank < num_procs; other_rank++)
        {
            MPI_Recv(buf, sizeof(buf), MPI_CHAR, other_rank,
                     0, MPI_COMM_WORLD, MPI_STATUS_IGNORE);
            printf("%s\n", buf);
        }

    } else {

        /* Receive message from process #0 */
        MPI_Recv(buf, sizeof(buf), MPI_CHAR, 0,
                 0, MPI_COMM_WORLD, MPI_STATUS_IGNORE);
        assert(memcmp(buf, "Hello ", 6) == 0),

        /* Send message to process #0 */
        sprintf(buf, "Process %i reporting for duty.", my_rank);
        MPI_Send(buf, sizeof(buf), MPI_CHAR, 0,
                 0, MPI_COMM_WORLD);

    }

    /* Tear down the communication infrastructure */
    MPI_Finalize();
    return 0;
}
```

### C++ Procedure

1. Use Vim (`vim wiki_mpi_example.c`) to create your C++ source file.
2. Save your file and return to the Bash shell.
3. Load the MPI compiler using the openmpi module.

  ```bash
  module load openmpi
  ```

5. Compile the C++ source into a binary executable file.

  ```bash
  mpicc wiki_mpi_example.c -o hello.mpi
  ```

7. Use `ls -al` to verify the presence of the `hello.mpi` binary in your working directory.


## Step 4: Run the Job

1. Before proceeding, ensure that you are still in your working directory (using `pwd`) and that you still have the openmpi module loaded (using `module list`).

  - We need to be in the same path/directory as our sbatch script and our C++ binary. Use `ls -al` to confirm their presence.

2. Use `sbatch` to schedule your batch job in the queue.

  ```bash
  sbatch slurm_mpi_example.job
  ```

  This command will automatically queue your job using slurm and produce a job number.
  You can check the status of your job at any time with the `squeue` command.

  ```bash
  squeue --job <jobnumber>
  ```

  You can also stop your job at any time with the `scancel` command.

  ```bash
  scancel --job <jobnumber>
  ```

3. View your results.<br>
  You can view the contents of these files using the `more` command followed by the file name.<br>

  ```bash
  more test_<jobnumber>.out
  ```

  Your output should look something like this:

  ```bash
  Currently Loaded Modules:
  1) gnu/5.4.0   2) openmpi/1.10.7

 
   We have 16 processes.
   Process 1 reporting for duty.
   Process 2 reporting for duty.
   Process 3 reporting for duty.
   Process 4 reporting for duty.
   Process 5 reporting for duty.
   Process 6 reporting for duty.
   Process 7 reporting for duty.
   Process 8 reporting for duty.
   Process 9 reporting for duty.
   Process 10 reporting for duty.
   Process 11 reporting for duty.
   Process 12 reporting for duty.
   Process 13 reporting for duty.
   Process 14 reporting for duty.
   Process 15 reporting for duty.

  ```

4. Download your results (using the `scp` command or an SFTP client) or move them to persistent storage. See our [moving data](../../../data-transfer-storage/moving-data.md) section for help.

#### Additional Examples
- [Working with C](../execute-a-job.md)
- [Working with Fortran](fortran.md)
- [Working with Python](python.md)
- [Working with Makefiles](makefile.md)
