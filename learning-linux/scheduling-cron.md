# Scheduling Tasks with cron

📝 **Note:** The majority of the following commands must be run by the superuser @root

## Part 1: Using the `crontab` Command

The `crontab` command is used to schedule commands to be executed periodically. It allows tasks to be automatically run in the background at regular intervals.

That means that you can use `crontab` to automatically create backups, synchronize files, schedule updates, and much more.

The main configuration file for cron is `/etc/crontab`. If you view the content of it, it will display:

```
# Example of job definition:
# .---------------- minute (0 - 59)
# | .------------- hour (0 - 23)
# | | .---------- day of month (1 - 31)
# | | | .------- month (1 - 12) OR jan,feb,mar,apr ...
# | | | | .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat
# | | | | |
# * * * * * user-name command to be executed
```

- #### List programmed tasks

  ```bash
  crontab -l
  ```

  _It will list the crontabs that are currently running on your environment, if you are a `root` user, you can list all the crons that the system has._

  If you have not set any jobs, it will display a message such as `crontab: no crontab for user`.

- #### Edit the list of cronjobs

  ```bash
  crontab -e
  ```

  _The option `e` let you edit a list of tasks. You can set some tasks using this format:_

  ```bash
  # Every hour, at the minute 37, a copy will take place
  37 * * * *  root  cp a /tmp/b

  # Every day at 5:23 compression will occur
  23 5 * * *  root  zip f1.zip f1

  #Every week on Sunday at 03:19 a copy will be made
  19 3 * * 0  root  scp hostname:/tmp/files .

  #Every month on day 6 at 00:23 minutes, a script will be run
  23 0 6 * *  root  ./script

  #run a cron job from a script for every Monday, Wednesday and Friday at 7:00 pm
  0 19 * * 1,3,5 nohup /home/user/script.sh > /tmp/script.log 2>&1
  ```

## Part 2: Using the `at` Command

Use `at` when you want to execute a command or multiple commands **once** at some future time.

```bash
at 4:55pm Friday
echo '5 p.m. meeting with Carol' | mail raithel
^D
Job c00ceb7fb.01 will be executed using /bin/sh
```

_The `at` command takes input up to the end-of-file character (`ctrl` `D` while at the beginning of a line). It reports the job number and informs you that it will use `/bin/sh` to execute the command. An email to raithel will be sent at 4:55pm on Friday with the Subject: '5 p.m. meeting with Carol'._

To program a script from `now`, you may add hours, minutes, or seconds with the `+` symbol, e.g.:

```bash
at now + 25 minutes
echo ^G > /dev/ttyp4
^D
Job c00ceb7fb.00 will be executed using /bin/sh
```

_This script will notify you with a beep in 25 minutes._

- To get a list of your pending at jobs, enter `atq`. If you are superuser, `atq` shows you the pending `at` jobs of all users.

- To delete a job, enter `atrm job_number` where `job_number` is the job number returned by `atq`. The superuser can also remove other user's jobs.
