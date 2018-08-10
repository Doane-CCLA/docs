# Modules

Modules are a utility which allow users to load and manage applications and their versions. The modules of software packages allow you to dynamically modify your user environment by using “modulefiles.”
Each modulefile contains the information needed to configure the shell for an application. After the module software package is initialized, the environment can be modified on a per-module basis using the module command, which interprets modulefiles. Typically, modulefiles instruct the module command to change or set shell environment variables such as `PATH`, `MANPATH`, and others. The modulefiles can be shared by many users on a system.

📝 **Note:** Some modules cannot be used simultaneously, such as an Intel compiler and a GNU compiler ([information on compilers](compilers.md)). If you attempt to _load_ a module that is incompatible with a currently-loaded module, you will be prompted of the conflict. To avoid the error, you may have to _unload_ or _switch_ modules.

#### Summary of Module Commands

Command         | Description
--------------- | -----------------------------------------------------
module list     | Lists modules currently located in user's environment
module avail    | Lists all available modules on a system in condensed format
module avail -l | Lists all available modules on a system in long format
module display  | Shows environment changes that will be made by loading a given module
module load     | Loads a module
module unload   | Unloads a module
module help     | Shows help for a module
module swap     | Swaps a currently loaded module for an unloaded module



**Modules: Local repository**<br>
By default the local repository is used as a source of software installations. To list available modules, type `module avail`. To load a module, use `module load module_name`. Similarly, unload modules by typing `module unload module_name`.

**Modules: CVMFS-based repository**<br>
A CVMFS (Cern Virtual File System)-based repository is available for use that has several software packages available for use. To use the CVMFS-based repository run the following commands from your login node:

```bash
source /software/dev_tools/swtree/cs400/modulefiles/switch-modules.sh
```

```bash
switch_modules oasis
```

After entering the above commands the new repository should be active and the command below will list the software available for use:

```bash
module avail
```

Similarly `switch_modules local` will bring back the local modules to use.



## Available Modules

To see a list of available modules, type

```bash
module avail
```

📝 **Note:** If you need a module that is not available, please [contact us](../../SUPPORT.md).

You can check for the existence of a module and its versions using `module avail <module-name>`.

```bash
$ module avail cuda

----------------- /software/dev_tools/swtree/cs400/modulefiles -----------------
cuda/6.5          cuda/7.5(default)       cuda/8.0
```

## Working with Modules

When you load a module, your environment is modified to use a specific software package. To load a module:

```bash
module load vmd
```

To verify your module has loaded, you can type `module list`.

To display information about the attributes of the module such as the size of the module, the compiler or the source from which the module was created, etc., use the following command:

```bash
module display your_module
```

## Removing and Switching Modules

Unloading a module will avoid conflict and/or messages of failure due to different versions or dependencies.

```bash
module unload PE-gnu/1.0
```

Switching between different module versions can accomplish the task of having to load, unload and load modules in multiple steps. In the following example, `cuda/7.5` is currently loaded. After running the command, `cuda/7.5` is _unloaded_ and `cuda/8.0` is _loaded_.

```bash
module switch cuda/7.5 cuda/8.0
```

You can unload all the modules on your environment, by executing the module purge command:

```bash
module purge
```

### Related Information

- [Environment Customization](environment.md)
- [CVMFS Modules](cvmfs-modules.md)
