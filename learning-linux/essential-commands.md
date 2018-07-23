# Essential Commands

<!-- TOC depthFrom:2 depthTo:2 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Overview](#overview)
- [Common Shortcuts](#common-shortcuts)
- [Basic Commands](#basic-commands)
- [Pipe and Redirection](#pipe-and-redirection)

<!-- /TOC -->

## Overview

- Linux has a hierarchy of directories that lists contents of files in a tree-like format, starting from the file system root (`/`).

- Linux is _case-sensitive_, e.g. `Myfile`, `myfile`, `MYFILE`, and `MyFile` are four unique files.

- Linux does not require filename extensions such as `.doc`, `.exe`, and `.abc`. The `.` extension is simply part of the filename. Sometimes data files are named with extensions (.hdf, .cdf, .tar) for human readability, though this is optional.

- A file named with `.` at the beginning will be considered a hidden file.

- You can use the `<TAB>` key to autocomplete commands, paths, and environment variables. For example, you can type `cal` on your terminal followed by `<TAB>` to test this. If there is more than one option for the autocomplete to choose from, pressing `<TAB>` _twice_ will provide a list of all possible options based on what you have typed.

- The `up-arrow` will display the previous command you have typed and if you press the `down-arrow`, it will refer to the following command.

- The `history` command will show all of the previous commands you have entered during the last session(s).

## Common Shortcuts

macOS     | Windows    | Action
:-------- | :--------- | :----------------------------------------
`CMD`+`D` | `CTRL`+`D` | Exit a terminal, same as typing `exit`
`CMD`+`L` | `CTRL`+`L` | Clears the screen, same as typing `clear`
`CMD`+`C` | `CTRL`+`C` | Breaks/cancels an ongoing operation
`CMD`+`Z` | `CTRL`+`Z` | Pauses (stops) an ongoing operation
`CMD`+`N` | `CTRL`+`N` | Opens a new terminal

📝 **Note:** If you want to learn more shortcuts, please consult more documentation [here](shortcuts.md).

## Basic Commands

- #### pwd: Print Current Working Directory

  ```bash
  pwd
  /Users/x0y
  ```

  _The output of `pwd` in this case, is the home directory of the user x0y, which is shown with the complete path starting from root(`/`)_

- #### ls: List the contents of the current directory

  ```bash
  ls
  Documents/   Pictures/   Desktop/   Downloads/   document.txt
  ```

  _The output is a list of four directories (followed by a `/`) and one file. To see information about the contents in a list, type `ls -l`._

- #### cd: Change directory

  ```bash
  cd Documents
  ```

  _In this case, we are entering the "Documents" directory._

  If you want to go directly to your home directory (x0y), you can type `cd` without any specification of which directory.

  In the case of nested folders, you can jump one directory level upwards by typing `cd ..`

  **alias**: In case of deeply nested folders (/path/to/project/com/java/lang/morefiles) that might take more than 4 directory levels upwards, you can create an `alias`, for example, `alias ..2="cd ../.."` or `alias ..3="cd ../../.."` or `alias ..4="cd ../../../.."`. If you wish to make these aliases a permanent feature of your Bash environment, you may add the commands to the end of the `.bashrc` file. Edit the `.bashrc` file by opening it in your favorite text editor (it is located in your home directory). For example, type `vi .bashrc`.

- #### whoami: Shows the user ID as a name

  ```bash
  whoami
  x0y
  ```

  _This shows the username that is logged in to the current session of the machine._

  If you need additional information about the user, such as, to which groups they are a member, type `id`.

  If you want to see all the users that are logged in to the computer, you can type `w`.

- #### date: Display the date and time of the system

  ```bash
  date
  Wed Apr  4 09:06:30 EDT 2018
  ```

  _The date is shown in a complex format._ Use `date +%F` format if you want to do a [backup of a file including the date in the filename](scripts/backup.md).

  If you want to [calculate, in seconds, the duration of a program](scripts/seconds.md), you can use the `date +%s` command.

- #### cal: Display a calendar of the current month

  ```bash
  cal
  ```

  _This command displays the calendar of the current month of the year in which the command is executed._

  In case you need the whole year calendar of 2018, you may type `cal 2018` or set any other year you want to check.

  If you want to display any particular month of the year, you can type, for example, `cal March 2018`.

  To display the Eastern date of the current year, please type `ncal -o`.

- #### cat: Creates a single or multiple files, views the contents of a file, concatenates files, and redirects output into the terminal or into files

  ```bash
  cat /Users/x0y/myfile.txt
  hello world
  ```

  _In this case, we want to display the content of `myfile.txt` which is located inside the `x0y` directory._

  If we are positioned inside the `x0y` directory, all that is needed is `cat myfile.txt` to see its contents, which is "hello world".

  You can view the content of two files at the same time with the `cat file1.txt file2.txt`.

  In case you need the lines of a text numbered, please type `cat -n myfile.txt`.

- #### echo: Display a line of text or a string on standard output or into a file

  ```bash
  echo "Hi ORNL"
  Hi ORNL
  ```

  _In this example, the string `Hi ORNL` is shown because we send that message to the terminal._

  To view the value assigned to a variable, add `$` before the variable name:

  (e.g. `x=10; echo "The value of 'x' is: $x"`).

  If you need a new line `\n`, use the option `-e` (e.g. `echo -e "Hello \n world"`).

- #### touch: Create a new empty file

  ```bash
  touch myNEWfile
  ```

  _In this case, `myNEWfile` was created inside the directory in which you are positioned._

  You can create more than one file at the same time with by typing `touch file1 file2`.

  If you want to create lots of files that share a common string, e.g. `test1.txt`, `test2.txt`, `test3.txt`, and so on until 25, you can use `touch test{1..25}.txt`.

- #### mkdir: make directory

  ```bash
  mkdir myNEWdir
  ```

  _In this case, a new directory called `myNEWdir` is created in the current path._

  If you want to set the permission of the directory while you are creating the directory, you can do so by typing `mkdir -m a=rwx myNEWdir`. Here, the letters r, w, and x stand for read, write, and execute, respectively. For more information on file and directory permissions, see [here](permissions.md).

  If you want to create multiple directories at once, run `mkdir test1 test2 test3`.

  If you want to create several subdirectories at one time, type `mkdir -p /home/test/test1/test2/test3/test4`.

- #### cp: Copy files and directories

  ```bash
  cp /path/to/file_src /path/to/file_dest
  ```

  In this case the contents of `file_src` (source) will be copied to `file_dest` (destination) and both files will be present in both paths.

  If you need to copy more than one file into a directory, you can type `cp main.c def.h /Users/x0y/mydir/`.

  To copy all the files you have (in your current path) with the extension `.c` to a directory called `bak`, you can type `cp *.c bak`. The asterisk (`*`) is a wild-card character.

- #### mv: Move or rename the files or directories

  ```bash
  mv file1 Myfile1
  ```

  _The file called `file1` was renamed as `Myfile1`._

  If you want to move all of your C files to a subdirectory called `bak`, you can run `mv *.c bak`.

  If you want to create a backup when copying your `.txt` files into the `mybak` directory (to not overwrite existing files within `mybak`) use: `mv -bv *.txt /Users/x0y/mybak`.

- #### rm: Delete files or directories

  ```bash
  rm file1 Myfile1
  ```

  _The files called `file1` and `Myfile1` will be removed._

  For directories, the recursive option `-r` is needed, e.g. `rm -r modelOutput`.

- #### man: Display the manual of the Linux commands

  ```bash
  man sudo
  ```

  _A manual related to the `sudo` command is displayed explaining how the `sudo` command will grant you privileges to execute commands as the superuser does._

  For further information you can do `man man` to read more about `man`. To exit a manual page, type `q`.

## Pipe and Redirection

- #### |  Pipeline

  A _pipe_ is a form of redirection that sends the output of a program (written _before the pipe_) to another one (written _after the pipe_) for further processing.

  To make a pipe, put a vertical bar (`|`) on the command line between two commands.

  ```bash
  man pipe | cat > /tmp/myMAN.txt
  ```

  _The command `man pipe` will display the content of all the information about **pipe**, then **that content** will be processed by `cat` (taken as its **input**) and be redirected to the file `/tmp/myMAN.txt`. So, the **output**, the content of `myMAN.txt` will display the manual information about **pipe**._

- #### >  Redirecting output

  Commands can send and receive streams of data to and from files and devices.

  ```bash
  echo "Test report title" > /tmp/test.txt
  ```

  _"Test report title" will be written to the file `test.txt` located inside the `/tmp` directory._

  It is also possible to send all the content of `/tmp/hi.txt` to `/Users/x0y/hello`, by using `/tmp/hi.txt > /Users/x0y/hello`.

  `Mail -s "Subject" to-address@example.com < Filename` will email the content of `Filename`.

- #### >>  Appending (postpending) redirected output

  This command will append (postpend) information to where it is designated.

  ```bash
  echo "This report was done at $HOSTNAME at $(date+%F)">>/tmp/report.txt
  ```

  _The output of the first part of the command (before the `>>`) will be added at the **end** of the file `/tmp/report.txt`._
