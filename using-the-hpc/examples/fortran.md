# Execute a Job: _Fortran Example_

The tutorial assumes you have already worked through the [Execute a Job Tutorial](../execute-a-job.md). Therefore, the instructions here are abbreviated but will follow the same format so you may easily consult the extended tutorial.

**Table of Contents**

<!-- TOC depthFrom:2 depthTo:3 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Step 1: Access the Onyx HPC](#step-1-access-the-onyx-hpc)
- [Step 2: Create an sbatch Script](#step-2-create-a-sbatch-script)
	- [Example sbatch Script](#example-sbatch-script)
	- [sbatch Procedure](#sbatch-procedure)
- [Step 3: Compile the Fortran Program from Source](#step-3-compile-the-fortran-program-from-source)
	- [MPI Hello World Source Code](#mpi-hello-world-source-code)
	- [Fortran Procedure](#fortran-procedure)
- [Step 4: Run the Job](#step-4-run-the-job)

<!-- /TOC -->

📝 **Note:** Do not execute jobs on the login nodes; only use the login nodes to access your compute nodes. Processor-intensive, memory-intensive, or otherwise disruptive processes running on login nodes will be killed without warning.

## Step 1: Access the Onyx HPC

1. Open a Bash terminal (or MobaXterm for Windows users).
2. Execute `ssh doaneusername@onyx.doane.edu`.
3. When prompted, enter your password.


## Step 2: Create an sbatch Script

### Example sbatch Script

Here is an example sbatch script for running a batch job on an HPC like Onyx.
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
mpirun hello_world_f
```

### sbatch Procedure

1. Use nano or Vim (we use Vim here) to create and edit your sbatch script.

  ```bash
  vim slurm_f90_example.job
  ```

2. Create your sbatch script within Vim by typing ```i``` for ```insert``` mode or paste the contents of your sbatch script into Vim.
3. Save your file by typing ```:wq!``` and return to the Bash shell.


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

1. Use Vim (`vim`) to create your Fortran source file.

  ```bash
  vim hello_world.f90
  ```
2. Save your file and return to the Bash shell.
3. Load the MPI compiler using the openmpi module.

  ```bash
  module load openmpi
  ```

4. Compile the Fortran source into a binary executable file.

  ```bash
  mpifort -o hello_world_f hello_world.f90
  ```

5. Use `ls -al` to verify the presence of the `hello_world_f` binary in your working directory.


## Step 4: Run the Job

1. Before proceeding, ensure that you are still in your working directory (using `pwd`) and that you still have the PE-gnu module loaded (using `module list`).

  - We need to be in the same path/directory as our sbatch script and our Fortran binary. Use `ls -al` to confirm their presence.

2. Use `sbatch` to schedule your batch job in the queue.

  ```bash
  sbatch slurm_f90_example.job
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
  You can view the contents of these files using the `less` command followed by the file name.<br>

  ```bash
  less test_<jobnumber>.out
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
