# Execute a Job: _Makefile Example_

The tutorial assumes you have already worked through the [Execute a Job Tutorial](../execute-a-job.md). Therefore, the instructions here are abbreviated but will follow the same format so you may easily consult the extended tutorial.

On this page, we will use a Makefile to automate the compiling of the C, C++, and Fortran programs. In our PBS script, we will send a command to the Makefile which will compile codes prior to submitting the job to MPI.

**Table of Contents**

<!-- TOC depthFrom:2 depthTo:3 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Step 1: Access Your Allocation](#step-1-access-your-allocation)
- [Step 2: Create a PBS Script](#step-2-create-a-pbs-script)
	- [Example PBS Script](#example-pbs-script)
	- [PBS Procedure](#pbs-procedure)
- [Step 3: Create the Makefile](#step-3-create-the-makefile)
	- [Makefile Code](#makefile-code)
	- [Makefile Procedure](#makefile-procedure)
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

#PBS -N mpi_hello_world_make
#PBS -M your_email@example.com
#PBS -l nodes=1:ppn=16
#PBS -l walltime=0:00:6:0
#PBS -W group_list=group_name
#PBS -A group
#PBS -l qos=burst
#PBS -V

module purge
module load PE-gnu
module load python
module list
cd $PBS_O_WORKDIR
pwd

make all

echo "=================================="
echo "Output of the MPI and C program"
echo "=================================="

mpirun hello_world_c

echo "=================================="
echo "Output of the MPI and C++ program"
echo "==================================="

mpirun hello_world_cpp

echo "====================================="
echo "Output of the MPI and Fortran program"
echo "====================================="

mpirun hello_world_f

echo "====================================="
echo "Output of the MPI and Python program"
echo "====================================="

mpirun python hello_world.py

echo "============================="
echo "Successful!!!... End of File"
echo "============================="

```


### PBS Procedure

1. From the login node, change your working directory to the desired file system. We are going to use our Lustre allocation for this example. _If Lustre storage is not available, you may complete this tutorial from within your home directory on NFS._

  ```bash
  cd /lustre/group/username
  ```

2. Use Vi to create and edit your PBS script.

  ```bash
  vi hello_world_make.pbs
  ```

3. Create your PBS script within Vi or paste the contents of your PBS script into Vi.
4. Save your file and return to the Bash shell.


## Step 3: Create the Makefile

A makefile contains instructions for Make software to automate the build of programs and source codes.

### Makefile Code

This file must be located in the same path as the other source programs.

```make
CC = mpicc
CXX = mpic++
FC = mpifort

OPTFLAGS = -O3
CFLAGS = $(OPTFLAGS) -g
CXXFLAGS = $(OPTFLAGS) -g
FFLAGS = $(OPTFLAGS) -g

all:hello_world_c hello_world_cpp hello_world_f

hello_world_c: hello_world.c
		$(CC) $(CFLAGS) -o hello_world_c hello_world.c

hello_world_cpp: hello_world.cpp
		$(CXX) $(CXXFLAGS) -o hello_world_cpp hello_world.cpp

hello_world_f: hello_world.f90
		$(FC)  $(FFLAGS) -o hello_world_f hello_world.f90

clean:
		rm hello_world_*
```

📝 **Note:** Indentations in a Makefile must be a `Tab` and not `spaces`.

### Makefile Procedure

1. Ensure that you are still in your working directory (`/lustre/group/username`) using `pwd`.
2. Use Vi (`vi`) to create your Makefile within your working directory.

  ```bash
  vi Makefile
  ```

3. Paste the hello world Makefile code into Vi.
4. Save your file and return to the Bash shell.

_If you have been following along the CADES tutorials in order, you will already have compiled programs for C, C++, and Fortran. However, if you did not already have compiled codes, the Makefile we have created here would compile all of them when we run our PBS script. In the `hello_world_make.pbs` file, there is a line that says `make all`. This command will run the contents of our Makefile, which will compile the C, C++, and Fortran programs prior to running the job._

## Step 4: Run the Job

1. Before proceeding, ensure that you are still in your working directory (using `pwd`) and that you still have the PE-gnu and python/3.6.1 modules loaded (using `module list`).

  - We need to be in the same path/directory as our PBS script and our Makefile. Use `ls -al` to confirm their presence.

2. Use `qsub` to schedule your batch job in the queue.

  ```bash
  qsub hello_world_make.pbs
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
  more mpi_hello_world_make.o143295
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
- [Working with C++](cpp.md)
- [Working with Fortran](fortran.md)
- [Working with Python](python.md)
