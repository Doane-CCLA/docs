# Running Jobs

AVAILABLE QUEUES:

| Queue | QOS | Max Walltime | Priority | Description |
| --- | --- | --- | --- | --- |
| Batch | burst |  |  | Burst queue allows for use of resources beyond ARM Stratus system |
| high\_mem | devel | 4 hours | high | Queue for use of CPU nodes |
|  | std | 48 hours | lower |  |
|  | long | 2 weeks | lowest |  |
| arm-prod |  | 6 hours | highest | Standing reservation for production jobs. Allows for use of up to 15 nodes between 12:00AM - 6:00AM daily. \(Use of this queue requires approval from ARM management\). |

## Example Submission Scripts:

BURST QUEUE

```text
#PBS -N jobname
#PBS -A arm-burst
#PBS -q batch
#PBS -W group_list=cades-user
#PBS -l qos=burst
#PBS -l nodes=16:ppn=16
#PBS -l walltime=1:00:00
```

STANDARD CPU QUEUE:

```text
#PBS -N jobname
#PBS -A arm
#PBS -q high_mem
#PBS -W group_list=cades-arm
#PBS -l qos=std
#PBS -l nodes=16:ppn=16
#PBS -l walltime=1:00:00
```

GPU QUEUE:

```text
#PBS -N jobname
#PBS -A arm
#PBS -q gpu_ssd
#PBS -W group_list=cades-arm
#PBS -l qos=std
#PBS -l nodes=2:ppn=16
#PBS -l walltime=1:00:00
```

## ARM Production Queue:

ARM production queue \(arm-prod\) has been specifically designed for daily production jobs. 15 nodes on Stratus queue is placed in a reservation every day during period of 12:00AM - 6:00AM to provide dedicated and guaranteed resources for critical operational jobs.

Details of the standing reservations can be checked using command `showres`.

```text
#PBS -N jobname
#PBS -A arm
#PBS -q high_mem
#PBS -x=FLAGS:ADVRES:arm-prod.5700
#PBS -W group_list=cades-arm
#PBS -l qos=std
#PBS -l nodes=16:ppn=16
#PBS -l walltime=1:00:00
```

## Scheduling Batch Jobs

Batch scripts, or job submission scripts, are the mechanism by which a user submits and configures a job for execution. A batch script is simply a shell script which contains:

* Commands that can be interpreted by batch scheduling software \(e.g. PBS\)
* Commands that can be interpreted by a shell

The batch script is submitted to the batch scheduler where it is parsed. Based on the parsed data, the batch scheduler places the script in the scheduler queue as a batch job. Once the batch job makes its way through the queue, the script will be executed on a service node within the set of allocated computational resources.

 **Sections of a Batch Script** - Batch scripts are parsed into the following three sections:

1. The Interpreter Line: The first line of a script can be used to specify the script’s interpreter. This line is optional. If not used, the submitter's default shell will be used. The line uses the "hash-bang-shell" syntax: `#!/path/to/shell`
2. The Scheduler Options Section: The batch scheduler options are preceded by \#PBS, making them appear as comments to a shell. PBS will look for `#PBS` options in a batch script from the script’s first line through the first non-comment line. A comment line begins with `#`. `#PBS` options entered after the first non-comment line will not be read by PBS.
3. The Executable Commands Section: The shell commands follow the last \#PBS option and represent the main content of the batch job. If any \#PBS lines follow executable statements, they will be ignored as comments.

The execution section of a script will be interpreted by a shell and can contain multiple lines of executable invocations, shell commands, and comments. When the job's queue wait time is finished, commands within this section will be executed on a service node \(sometimes called a "head node"\) from the set of the job's allocated resources. Under normal circumstances, the batch job will exit the queue after the last line of the script is executed.

## An Example Batch Script:

```text
#!/bin/bash
#PBS -A arm
#PBS -N kazsacr0reproc
#PBS -l nodes=16:ppn=8
#PBS -l walltime=4:00:00
#PBS -W group_list=cades-arm
#PBS -q high_mem
#PBS -j oe
#PBS -m abe
#PBS -M email@address
#PBS -V
#PBS -o o.log
#PBS -e e.log
#PBS -S /bin/bash
```

The following table summarizes frequently-used options to PBS:

| Option | Use | Description |
| --- | --- | --- |
| -A | \#PBS -A | Causes the job time to be charged to ???. The account string, e.g. arm, is typically composed of the three letters followed by three digits and optionally followed by a subproject identifier, The utility showproj can be used to list your valid assigned project ID\(s\). This option is required by all jobs. |
| -l | \#PBS -l nodes= | Maximum number of compute nodes. Jobs cannot request partial nodes. |
|  | \#PBS -l ppn= | Processors per nodes. |
|  | \#PBS -l walltime= | maximum wall-clock time, is in the format HH:MM:SS. |
|  | \#PBS -l partition= | Allocates resources on specified partition. |
| -o | \#PBS -o | Writes standard output to ??? instead of .o$PBS\_JOBID, $PBS\_JOBID is an environment variable created by PBS that contains the PBS job identifier. |
| -e | \#PBS -e | Writes standard error to ??? instead .e$PBS\_JOBID |
| -j | \#PBS -j {oe, eo} | Combines standard output and standard error into the standard error file \(eo\) or the standard out file \(oe\). |
| -m | \#PBS -m a | Sends email to the submitter when the job aborts. |
|  | \#PBS -m b | Sends email to the submitter when the job begins. |
|  | \#PBS -m e | Sends email to the submitter when the job ends. |
| -M | \#PBS -M | Specifies email address to use for -m options. |
| -N | \#PBS -N | Sets the job name to ??? instead of the name of the job script. |
| -S | \#PBS -S | Sets the shell to interpret the job script. |
| -q | \#PBS -q | Directs the job to the specified queue. This option is not required to run in the default queue on any given system. |
| -V | \#PBS -V | Exports all environment variables from the submitting shell into the batch job shell. Not recommended because the login nodes differ from the service nodes, using the `-V` option is not recommended. Users should create the needed environment within the batch job. |
| -X | \#PBS -X | Enables X11 forwarding. The `-X` PBS option should be used to tunnel a GUI from an interactive batch job. |

To submit job to the queue:

`qsub job_submission_script`

To check status of the jobs in the queue:

`qstat -u username`

PBS sets multiple environment variables at submission time. The following PBS variables are useful within batch scripts:

| Variable | Description |
| --- | --- |
| $PBS\_O\_WORKDIR | The directory from which the batch job was submitted. By default, a new job starts in your home directory. |
| $PBS\_JOBID | The job's full identifier. A common use for PBS\_JOBID is to append the job's ID to the standard output and error files. |
| $PBS\_NUM\_NODES | The number of nodes requested. |
| $PBS\_JOBNAME | The job name supplied by the user. |
| $PBS\_NODEFILE | The name of the file containing the list of nodes assigned to the job. Used sometimes on non-Cray clusters. |

