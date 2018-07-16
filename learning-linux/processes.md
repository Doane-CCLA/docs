[CADES](http://support.cades.ornl.gov/) → [User Documentation](../README.md) → [Linux](linux-intro.md) → [Processes](processes.md)

# Linux Processes

Processes are tasks that the operating system carries out.

<!-- TOC depthFrom:2 depthTo:2 withLinks:1 updateOnSave:1 orderedList:0 -->

- [The `ps` Command](#the-ps-command)
- [Killing Processes](#killing-processes)
- [Prioritizing Processes](#prioritizing-processes)
- [Background Processes](#background-processes)

<!-- /TOC -->

## The `ps` Command

`ps` stands for [**process status**](https://www.tldp.org/LDP/tlk/kernel/processes.html) and shows the running processes on a system.

To invoke it, run `ps` and it will display the following information:

- **PID**: process ID which identifies the running process
- **TTY**: is the terminal type
- **TIME**: Total CPU usage
- **CMD**: the command or program that is running, including options

- #### List all current running processes in the machine

  ```bash
  ps -ef
  ```

  _The option `-e` will display all the processes, and the `-f` option will display in a full format listing._

- #### List the processes of a user

  ```bash
  ps -f -u <user>
  ```

  _It displays the process that belongs to **user**. When you have multiple usernames, separate them using a comma._

- #### Check the execution time of a process

  ```bash
  ps -eo comm,etime,user | grep httpd
  ```

  _It shows the command, time, and user(s) related to the "httpd" service. You can replace "httpd" with the service you are looking for._

- #### Find the top five running processes by memory usage

  ```bash
  ps -eo pmem,pid,cmd | sort -k 1 -nr | head -5
  ```

  _It displays the top five of the output, organized in three columns with the memory that a process is taking, process ID, and the command, sorted by memory usage._

- #### Display the processes in the form of a tree diagram

  ```bash
  pstree -np | less
  ```

  _The option `-p` shows process identification numbers (PIDs) and `-n` sorts its output in the order of the PIDs._

  If you want to see the process tree of any specific user, please run `pstree <user>`. Use your username instead of `<user>`.

- #### Determine how much memory process uses

  ```bash
  pmap 1232
  ```

  _It displays the memory usage map of a process 1232. If you need information for multiple processes, you can add the their PID separated by a space._

## Killing Processes

All processes in Linux respond to signals. Signals are an OS-level way of telling programs to terminate or modify their behavior.

- #### kill: sends the TERM signal to the process to ask the process to terminate and exit _smoothly_

  ```bash
  kill 1734
  ```

  _This terminates a process with a PID of 1734._

  If this fails, the stronger signal 9, called SIGKILL can help by doing `kill -9 1734`. To see all the options, run `kill -l`

  In case you cannot determine the number of the process, you can use the name of the program to make it stop: `kill -9 firefox`

- #### killall: if there are multiple instances of a particular command running, the command will terminate them all

  ```bash
  killall firefox
  ```

  _In this case `killall` is closing a current program(s) that is running a process called `firefox`._

## Prioritizing Processes

Linux schedules the process and allocates CPU time accordingly for each of them, but you can set the priority to get more CPU time by using the `nice` and `renice` commands.

The process scheduling priority has a **nice value** that ranges from **-20 to 19**. The highest priority will consume a lot of CPU and that is not nice, so we set it as -20. On the other hand, the least priority for a process is represented as nicer because it will not take much CPU resources, and a nice value of 19 then is set.

Only the root user can set a negative value. A nice value of a process can be seen in the column `NI` after you type `top` in your terminal.

- #### top: monitors processes and system resource usage on Linux

  ```bash
  top
  ```

  _It displays the main 30 processes on the system sorted by CPU utilization, memory usage, and routine. See more information [here](http://www.techoism.com/top-command-in-centosrhel/)._

  If you want to sort processes by CPU usage, you can do so with `top -o %CPU`.

  To see a list of processes of any user, use `top -u <user>`. Please remember to replace `<user>` with your username or `root`.

- #### nice: sets priority on new processes

  ```bash
  nice -n 10 apt-get upgrade
  ```

  _It sets a **positive 10** as a nice value that gives **less priority** to a process._

- #### renice: sets a priority on existing processes

  ```bash
  renice 10 -p 2187
  ```

  _It sets a priority of 10 to a process with an ID 2187. If its value was 0, you are lowering the priority._

  📝 **Note:** You can set the default nice value of a particular user or group in the `/etc/security/limits.conf` file, by using the syntax: `[username] [hard|soft] priority [nice value]`, e.g. `backupuser hard priority 1`.

## Background Processes

A background process executes independently of the shell, without user intervention, leaving the terminal free for other work.

This means that you do not have to wait for a command to finish in the terminal to run another one. For further information, please click [here](https://www.xaprb.com/blog/2008/08/01/how-to-leave-a-program-running-after-you-log-out/).

After using commands to run process in the background, you will immediately be returned to the shell, and you will see the shell prompt.

- #### &: include an ampersand at the end of the command you use to run the job

  ```bash
  ./myscript.py &
  ```

  _The file `./myscript.py` is forked and runs in a separate sub-shell as a job. A process's job number and its PID will be displayed and stored in a special variable `$!`. This can be seen later with `echo $!`._

- #### nohup: stands for no hang up and prevents termination of background processes after shell termination

  ```bash
  nohup ./myscript.py &
  ```

  _The output generated by `./myscript.py` will be saved in `nohup.out` in the current directory. If you logout, your process will not get killed._

  To run more scripts at the same and leave them to be finished in background, run `./script.py & ./script2.py & ./script3.py &`.

- #### screen: runs a background process on a remote server, and keeps it running despite a dropped connection

  ```bash
  screen
  ```

  _This creates a new session when you log into another server. A screen ID is displayed after running your command(s)._

  To create a screen session with a name, please run `screen -S name`. See more screen options on `man screen` or [here](http://dasunhegoda.com/unix-screen-command/263/).

  To detach from the screen session with `CTRL`+`A`+`D` or **if you are remotely logged in**, you can do it with `screen -d [SCREENID]`.

- #### jobs: once a process is forked, it can be seen in the jobs list

  ```bash
  jobs
    [1]+  Running                 ./myscript.py &
  ```

  _It displays the list of the current jobs that are running in the background; there is the script `./myscript.py` with the **job number:1**._

- #### bg: resumes suspended jobs in the current environment by running them as background jobs

  ```bash
  dd if=/dev/zero of=myfile bs=1K count=2048000
    ^Z
    [1]+ Stopped dd if=/dev/zero of=file bs=1K count=2048000
    bg %1
  ```

  _The number **1** is the ID of the job as viewed under a job suspended; then, to use it with `bg` it must be preceded with a `%`._

- #### fg: runs them in foreground and occupies the current terminal and waits for process to exit

  ```bash
  fg
  ```

  _Without any argument, `fg` runs the current job in foreground._

  To see the ID of the jobs that are running in the background to bring them to the foreground, please type `jobs`. Then type the ID preceded by a`%`, e.g. `fg %1`.

- #### disown: removes the process from the shell's job control, but leaves it connected to the terminal

  ```bash
  ./run_script.sh
    CTRL-Z
    [1]+  Stopped                 run_script.sh
    bg
    [1]+ run_script.sh &
    disown %1
  ```

  _The `./run_script.sh` file is executed, then this job is suspended by pressing `ctrl`+`Z`, followed by `bg` to make it run in the background. Then, by typing `disown %1`, the job won't get the SIGHUP signal to be shut down._

- #### sleep: tells Bash what time to run a command and delays execution to allow a process to start

  ```bash
  sleep 3h; mplayer game.mp3
  ```

  _This will wait three hours to play game.mp3._

  You might consider using `m` to set minutes, e.g.`sleep 10m ; your_script`, or `d`, for days. If you do not specify anything, the sleepy action will happen in seconds.

- #### wait: waits until the last background process is completed

  ```bash
  collect-job1.sh &
    collect-job2.sh &
    collect-job3.sh &
    wait
    process-job-output.sh
    wait
  ```

  _The three scripts of "collection" that are running in the background will finish before the `process-job-output` starts._

  `wait` ensures this process and asks to not exit the containing script until all the execution has finished.
