# Execute a Job on Doane's HPC Onyx

The tutorial below shows you how to run a basic job on Doane's Onyx supercomputer. This tutorial is intended for users who are new to the HPC environment and leverages a Slurm batch (sbatch) script.

Additional examples can be found in [C++](examples/cpp.md), [Fortran](examples/fortran.md) or [Python](examples/python.md) sections.

**Table of Contents**

<!-- TOC depthFrom:2 depthTo:3 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Step 1: Access the Onyx HPC](#step-1-access-the-onyx-hpc)
- [Step 2: Create an sbatch Script](#step-2-create-a-sbatch-script)
	- [Example sbatch Script](#example-sbatch-script)
	- [sbatch Script Breakdown](#sbatch-script-breakdown)
	- [sbatch Procedure](#sbatch-procedure)
- [Step 3: Run the Job](#step-3-run-the-job)

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

srun -l hostname

module avail
module purge
module load gnu
module load openmpi
module list
mpirun -np 16 hostname
```

### sbatch Script Breakdown

Here, we break down the essential elements of the above PBS script.

- `#!/bin/bash`: sets the script type
- `#SBATCH -n 8`: sets the number of processors that you want to use to run your job; use -N to specify nodes instead of processors
- `#SBATCH -o test_%A.out`: sets the name of the output file; here `%A` will be replaced by slurm with the job number; 
- `#SBATCH --mail-user $CHANGE_TO_YOUR_EMAIL`: add your email address if you would like your job's status to be emailed to you
- `#SBATCH --mail-type ALL`: specifies which job status changes you want to be notified about; options include: NONE, BEGIN, END, FAIL, REQUEUE, ALL
- `srun -l hostname`: Run a parallel job on cluster managed by Slurm, in this case run `hostname` in parallel with `-l` prepending task numbers to lines of output stdout/err.
- `module avail`: Lists the currently available software modules.
- `module purge`: Clears any modules currently loaded that might result in a conflict.
- `module load gnu`: Loads the gnu module.
- `module load openmpi`: Loads the openmpi module.
- `module list`: confirms the modules that were loaded.
- `mpirun -np 16 hostname`: Slurm calls OpenMPI to run our `hostname` with the number of processors we specified earlier.


### sbatch Procedure

Now that we have covered the basics of a sbatch script in the context of an HPC, we will now talk about actually creating and using the script on Onyx.

When creating and editing your sbatch script, we will be working on the head node using the text editor, nano. 

1. From the login node, change your working directory to your home directory. 
  ```bash
  cd
  ```

2. Use nano to create and edit your sbatch script.

  ```bash
  nano slurm_example.job
  ```

3. Write your sbatch script within nano or paste the contents of your sbatch script into nano.
  - Copy sbacth script from this page
  - Hit Control/Command + p key to paste into nano from Windows/MacOS
  
4. When finished, hit `^X` (control + x key) to exit.
5. Enter `Y` to save your changes, and press `Return` to save your file and return to the Bash shell.

With the sbatch script in place, you can now move on to running the script in Step 3.

## Step 3: Run the Job

1. Before proceeding, ensure that you are still in your working directory (using `pwd`).

  - We need to be in the same path/directory as our sbatch script. Use `ls -al` to confirm its presence.
  
2. Use `sbatch` to schedule your batch job in the queue.

  ```bash
  sbatch slurm_example.job
  ```

  This command will automatically queue your job using Slurm and produce a job number.

  You can check the status of your job at any time with the `squeue` command.

  ```bash
  squeue <jobnumber>
  ```
  `squeue <jobnumber>` is likely to not return any information, as this test job takees only a second to complete.

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


#### Additional Examples
- [Working with C++](examples/cpp.md)
- [Working with Fortran](examples/fortran.md)
- [Working with Python](examples/python.md)
- [Working with Makefiles](examples/makefile.md)
