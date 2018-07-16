[CADES](http://support.cades.ornl.gov/) → [User Documentation](../README.md) → [Linux](linux-intro.md) → [Environment Customization](environment.md)

# Environment Variables

## Before Starting

Consider these important facts:

- Environment variables **are all upper case**.
- To use their values, precede the name with a `$`.

## Initializing Your Environment

Linux utilizes Bash as the default shell and when a session started it reads commands from `~/.bash_profile`.

Environment variables are set in the file `~/.bashrc`.

📝 **Note:** The files `~/.bash_profile` and `.bashrc` are hidden. To list hidden files, type `ls -a`.

## Know the Environment Variables

Here is a list of some common environment variables:

- `$HOME` - Path of your home directory
- `$PATH` - List of directories where the system checks for programs to run
- `$LD_LIBRARY_PATH` - List of directories where the system checks for shared libraries to load
- `$HOSTNAME` - The name of the host, e.g. `or-condos-login`.

📝 **Note:** See the values of all your environment variables by typing `env` on your terminal.

## Working with the Environment Variables

- Display the value of an environment variable using `echo`:

  ```bash
  echo $HOME
  /home/UID
  ```

- Modify the value of environment variables with `export`:

  ```bash
  export PATH=$PATH:/home/UID
  export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/home/UID/custom_lib_directory
  ```

- Set a value for environment variables:

  ```bash
  export OMP_NUM_THREADS=12
  ```

  _This command sets the value of the variable called OMP_NUM_THREADS (an OpenMP parameter) to 12._
