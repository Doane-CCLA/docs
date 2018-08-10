# Execute a Job: _Python Example_

The tutorial assumes you have already worked through the [Execute a Job Tutorial](../execute-a-job.md). Therefore, the instructions here are abbreviated but will follow the same format so you may easily consult the extended tutorial.

**Table of Contents**

<!-- TOC depthFrom:2 depthTo:3 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Step 1: Access Your Allocation](#step-1-access-your-allocation)
- [Step 2: Create a PBS Script](#step-2-create-a-pbs-script)
	- [Example PBS Script](#example-pbs-script)
	- [PBS Procedure](#pbs-procedure)
- [Step 3: Create a Python Program](#step-3-create-a-python-program)
	- [MPI Hello World Code](#mpi-hello-world-code)
	- [Python Procedure](#python-procedure)
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

Here is an example PBS script for running a batch job on a HPC Condo allocation.

```bash
#!/bin/bash

#PBS -N mpi_hello_world_py
#PBS -M your_email@example.com
#PBS -l nodes=1:ppn=16
#PBS -l walltime=0:00:6:0
#PBS -W group_list=group_name
#PBS -A group
#PBS -l qos=burst
#PBS -V

module purge
module load python/3.6.1
module list
cd $PBS_O_WORKDIR
pwd
mpirun python hello_world.py
```


### PBS Procedure

1. From the login node, change your working directory to the desired file system. We are going to use our Lustre allocation for this example. _If Lustre storage is not available, you may complete this tutorial from within your home directory on NFS._

  ```bash
  cd /lustre/group/username
  ```

2. Use Vi to create and edit your PBS script.

  ```bash
  vi hello_world_py.pbs
  ```

3. Create your PBS script within Vi or paste the contents of your PBS script into Vi.
4. Save your file and return to the Bash shell.


## Step 3: Create a Python Program

### MPI Hello World Code

```python
#!/usr/bin/env python

import sys
from mpi4py import MPI

size = MPI.COMM_WORLD.Get_size()
rank = MPI.COMM_WORLD.Get_rank()
name = MPI.Get_processor_name()

print("Hello, World! I am process ",rank," of ",size," on ",name)
```

### Python Procedure

1. Ensure that you are still in your working directory (`/lustre/group/username`) using `pwd`.
2. Use Vi (`vi`) to create your C++ source file within your working directory.

  ```bash
  vi hello_world.py
  ```

3. Paste the hello world C++ code into Vi.
4. Save your file and return to the Bash shell.

_Python does not need to be compiled._


## Step 4: Run the Job

1. Before proceeding, ensure that you are still in your working directory (using `pwd`) and that you still have the python/3.6.1 module loaded (using `module list`).

  - We need to be in the same path/directory as our PBS script and our Python script. Use `ls -al` to confirm their presence.

2. Use `qsub` to schedule your batch job in the queue.

  ```bash
  qsub hello_world_py.pbs
  ```

  This command will automatically queue your job using Torque and produce a six-digit job number (shown below).<br>

  ```bash
  143295.or-node-pbs01
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
  more mpi_hello_world_py.o143295
  ```

  Your output should look something like this (_the output is truncated._):

  ```bash
  Hello, World! I am process  11  of  20  on  compute_node
  Hello, World! I am process  13  of  20  on  compute_node
  Hello, World! I am process  12  of  20  on  compute_node
  Hello, World! I am process  0   of  20  on  compute_node
  Hello, World! I am process  15  of  20  on  compute_node
  Hello, World! I am process  19  of  20  on  compute_node
  Hello, World! I am process  7   of  20  on  compute_node
  Hello, World! I am process  16  of  20  on  compute_node
  Hello, World! I am process  3   of  20  on  compute_node
  Hello, World! I am process  9   of  20  on  compute_node
  .
  .
  .
  ```

4. Download your results (using the `scp` command or an SFTP client) or move them to persistent storage. See our [moving data](../../../data-transfer-storage/moving-data.md) section for help.

#### Additional Examples
- [Working with C](../execute-a-job.md)
- [Working with C++](cpp.md)
- [Working with Fortran](fortran.md)
- [Working with Makefiles](makefile.md)
