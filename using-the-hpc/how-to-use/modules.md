# Modules

Modules are a utility which allow users to load and manage applications and their versions. The modules of software packages allow you to dynamically modify your user environment by using “modulefiles.”
Each modulefile contains the information needed to configure the shell for an application. After the module software package is initialized, the environment can be modified on a per-module basis using the module command, which interprets modulefiles. Typically, modulefiles instruct the module command to change or set shell environment variables such as `PATH`, `MANPATH`, and others. The modulefiles can be shared by many users on a system.

📝 **Note:** Some modules cannot be used simultaneously, such as an Intel compiler and a GNU compiler ([information on compilers](compilers.md)). If you attempt to _load_ a module that is incompatible with a currently-loaded module, you will be prompted of the conflict. To avoid the error, you may have to _unload_ or _switch_ modules.

## Summary of Module Commands

Command         | Description
:-------------- | :-------------
`module list`   | Lists modules currently loaded in a user's environment. <br>A module is considered loaded when its associated modulefile has been executed <br>and the user's environment contains the changes from the modulefile.
`module avail`  | Lists all available modules on a system.
`module show`   | Shows environment changes that will be made by loading a given module.
`module load`   | Loads a module.
`module unload` | Unloads a module.
`module help`   | Shows help for a module.
`module swap`   | Swaps a currently loaded module for an unloaded module.


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

- [Environment Customization](condos/software/environment.md)
