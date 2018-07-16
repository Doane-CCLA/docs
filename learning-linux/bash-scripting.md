[CADES](http://support.cades.ornl.gov/) → [User Documentation](../README.md) → [Linux](linux-intro.md) → [Bash Scripting](bash-scripting.md)

# Bash Scripting

## Considerations

- It is crucial that the first line of the Bash script begins with the header `#!/bin/bash`.

- The extension of a file which represents a script should be `.sh`.

- Comments in Bash begin with `#` and run to the end of the line:

  ```bash
  echo Hello, World. # prints out "Hello, World."
  ```

- To execute a script, you must be sure your file has the permission to be executed `chmod +x your_script.sh`. Click [here](file-permissions.md) to see more about permissions.

- If you are located in the same PATH were you created the script, you execute your script by running `./your_script.sh`.

## Conditionals (Decision Control Structure)

Use conditionals to specify different courses of action to be taken. In this case, we have three possibilities to check a number in a range of other values:

```bash
#!/bin/bash
#Setting a value to output
output=99
#Determine an action based on the output's value
if [ $output -eq 100 ]   #if the output is equal to 100
then
  echo "The calculation reaches 100%"
else
  if [ $output -gt 100 ]   #if the output is greater than 100
  then
    echo "The calculation is greater than 100%"
  else     #only option is that the output is less than 100
  echo "The calculation is less than 100%"
  fi
```

Read more examples about [if conditionals](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_07_01.html).

## Loops (Repetitive tasks)

In a loop, commands will continue to run repeatedly until a task is executed for all elements. One useful command for loop calculations is `for`. Here is an example of printing numbers from 1 to 9:

```bash
#!/bin/bash
#Printing numbers from 1 to 9
for i in {1..9}; do echo $i; done
```

If you want to have all the numbers in the same line, add the `-n` option. If you want to add 4 units, use double parentheses in the operation:

```bash
#!/bin/bash
#Numbers from 1 to 9
#Add four units in the same line
for i in {1..9}; do echo -n "$((i+4))  " ;  done
```

- Click [here](https://www.tldp.org/LDP/abs/html/loops1.html) to see more examples.

## Working with files (combining conditionals with Bash commands)

Check the existence of a file to determine the size of the file as well the quantity of words:

```bash    
#!/bin/bash
#Clear the terminal
tput clear

#Request the name of the file to be evaluated
printf "Enter the absolute path of the file, e.g. /home/x0y/your_file\n"
read FILE

#Evaluate the file
if [ -e $FILE ]
then
    printf "The $FILE has a size of $(du -h $FILE | awk '{print $1}') and it contains $(wc -w $FILE | awk '{print $1}') words.\n"
else
    printf "File not found, keep trying..."
fi
```

📝 It is important to indent the code in the `if` block with 4 spaces. Also include 1 space between the _contents_ of the brackets (`[` and `]`) and the brackets themselves.

## Working with filesystems (combining conditionals with Bash commands)

Send an email if disk usage in the system has reached 90% or more:

```bash
#!/bin/bash
#Run 'df -H' first to check filesystems and usage
#Then filter with `grep` to not consider Filesystem, tmpfs, nor cdrom using the options `-vE`
#Take only columns 5 and 1 with 'awk' and keep that output using `while read` to do an action
df -H | grep -vE '^Filesystem|tmpfs|cdrom' | awk '{ print $5 " " $1 }' | while read output;
do
#Print the output with 'echo', and assign to `usep` only the first column of output, taking out '%'
  echo $output
  usep=$(echo $output | awk '{ print $1}' | cut -d'%' -f1  )
#Partition is only going to take the names of your filesystems
  partition=$(echo $output | awk '{ print $2 }' )
#if the value of `usep` is greater than or equal to 90 then you will print a message and send an email to alert
  if [ $usep -ge 90 ]; then
    echo "Running out of space \"$partition ($usep%)\" on $(hostname) as on $(date)" |
     mail -s "Alert: Almost out of disk space $usep%" username@example.com
  fi
done
```

_You can learn more about Bash scripting by taking a look at this [tutorial](http://www.tldp.org/LDP/abs/html/)._
