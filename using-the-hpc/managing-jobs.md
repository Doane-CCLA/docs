# Scheduling Jobs

HPC utilizes Slurm to manage jobs that users submit to various queues on a computer system. Each queue represents a group of resources with attributes necessary for the queue's jobs. Doane's Onyx HPC only has one queue to worry about.

📝 **Note:** Do not run jobs on the head node. All jobs launched from this node will be terminated without notice.

## Listing jobs

To list all jobs:

```bash
squeue
```

To refine the list of jobs to only those submitted by a user:

```bash
squeue -u username
```

To obtain the status of a job, run the following command using the job's ID number (this is provided at time of job submission).

```bash
squeue <jobnumber>
```

## Submitting a job

To submit a job, use the `sbatch` command, followed by the name of your submission file. A Job ID will be provided. You may want to make note of the ID for later use.

```bash
sbatch your_script
```

## Deleting a job

📝 **Note:** Be aware that deleting a job cannot be undone. Double check the job ID before deleting a job.

Users can delete their jobs by typing the following command.

```bash
scancel <jobnumber>
```

## Related Information

- [Execute a Job](../execute-a-job.md)
