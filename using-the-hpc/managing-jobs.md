# Scheduling Jobs

HPC utilizes Torque/Moab to manage jobs that users submit to various queues on a computer system. Each queue represents a group of resources with attributes necessary for the queue's jobs. You can see the list of queues that HPC has by typing `qstat -q`. **batch** is the default queue.

📝 **Note:** Do not run jobs on the login nodes. All jobs launched from those nodes will be terminated without notice.

## Listing jobs

To list all jobs:

```bash
qstat
```

To refine the list of jobs to only those submitted by a user:

```bash
qstat -u username
```

To further refine the list of jobs, the following command will list jobs submitted by a user and which are running.

```bash
qstat -u username -s -r
```

To obtain the status of a job, run the following command using the job's ID number (this is provided at time of job submission).

```bash
qstat -f job_ID
```

You can also use `checkjob job_ID` to show the current status of the job.

## Submitting a job

To submit a job, use the `qsub` command, followed by the name of your submission file. A Job ID will be provided. You may want to make note of the ID for later use.

```bash
qsub your_script
```

## Deleting a job

📝 **Note:** Be aware that deleting a job cannot be undone. Double check the job ID before deleting a job.

Users can delete their jobs by typing the following command.

```bash
qdel job_ID
```

To delete all the jobs of a user:

```bash
qdel $(qselect -u username)
```

## Related Information

- [Execute a Job](../execute-a-job.md)
