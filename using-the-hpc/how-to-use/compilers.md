# Compiler Toolchains

HPC supports four _programming environment (PE)_ modules to easily switch between compilers. Each programming environment contains the full set of compatible compilers and libraries.<br>
These compilers are: [GNU Collection Compiler (GCC)](https://gcc.gnu.org), the [Intel compiler](https://software.intel.com/en-us/intel-compilers), [The Portland Group (PGI)](https://www.pgroup.com), and the [Numerical Algorithms Group (NAG)](https://www.nag.com/nag-compiler).

📝 **Note:** You cannot use more than one `PE-module` at the same time. For example, if you are working with GNU and then you decide to work with the Intel compiler, first unload the `PE-gnu` module and then load `PE-intel`.

## The GNU Compiler Suite

To load the GNU module:

```bash
module load PE-gnu
```

You can check which modules are loaded in your system by typing:

```bash
$ module list
Currently Loaded Modulefiles:
  1) gcc/5.3.0        2) openmpi/1.10.3   3) xalt/0.7.5       4) PE-gnu/1.0
```

To display information about the module, such as the size, the compiler, or the source from which the module was created, etc., use the following command:

```bash
$ module display PE-gnu
-------------------------------------------------------------------
/software/dev_tools/swtree/cs400/modulefiles/PE-gnu/1.0:

module-whatis     PE-gnu defines the environment needed to build

                 applications using GNU compiler suites on this system.
conflict     PE-gnu PE-intel PE-pgi
setenv         PE_NAME GNU
setenv         PE_CC mpicc
setenv         PE_CXX mpic++
setenv         PE_FORTRAN mpif90
prepend-path     PATH /software/dev_tools/swtree/cs400_centos7.2_pe2016-08/PE/1.0/noarch/bin
module         load xalt
-------------------------------------------------------------------
```

You can switch between the two versions of PE-gnu v1.0 and PE-gnu v2.0:

```bash
$ module switch PE-gnu/1.0 PE-gnu/2.0
$ module list
Currently Loaded Modulefiles:
  1) gcc/5.3.0       2) openmpi/2.1.1   3) PE-gnu/2.0      4) xalt/0.7.5
```

## The Intel Compiler Suite

📝 If you are working with another module, first you need to unload it.

```bash
module load PE-intel
```

You can see what the module provides with the commands `module list` and `module display`.

```bash
$ module list
Currently Loaded Modulefiles:
  1) intel/16.0.1     2) openmpi/1.10.3   3) xalt/0.7.5       4) PE-intel/1.0
```

```bash
module display PE-intel
-------------------------------------------------------------------
/software/dev_tools/swtree/cs400/modulefiles/PE-intel/1.0:

module-whatis     PE-intel defines the environment needed to build

                 applications using Intel compiler suites on this system.
conflict     PE-gnu PE-intel PE-pgi
setenv         PE_NAME INTEL
setenv         PE_CC mpicc
setenv         PE_CXX mpic++
setenv         PE_FORTRAN mpif90
prepend-path     PATH /software/dev_tools/swtree/cs400_centos7.2_pe2016-08/PE/1.0/noarch/bin
module         load xalt
-------------------------------------------------------------------
```

## The Portland Group Compiler Suite

📝 If you are working with another module, first you need to unload it.

```bash
module load PE-pgi
```

You can see what does the module provides with the commands `module list` and `module display`.

```bash
$ module list
Currently Loaded Modulefiles:
  1) pgi/15.7.0       2) openmpi/1.10.3   3) xalt/0.7.5       4) PE-pgi/1.0
```

```bash
$ module display PE-pgi
-------------------------------------------------------------------
/software/dev_tools/swtree/cs400/modulefiles/PE-pgi/1.0:

module-whatis     PE-pgi defines the environment needed to build

                 applications using PGI compiler suites on this system.
conflict     PE-gnu PE-intel PE-pgi
setenv         PE_NAME PGI
setenv         PE_CC mpicc
setenv         PE_CXX mpic++
setenv         PE_FORTRAN mpif90
prepend-path     PATH /software/dev_tools/swtree/cs400_centos7.2_pe2016-08/PE/1.0/noarch/bin
module         load xalt
-------------------------------------------------------------------
```

## The Numerical Algorithm Group Compiler Suite

📝 If you are working with another module, first you need to unload it.

```bash
module load PE-nag
```

You can see what the module provides with the commands `module list` and `module display`.

```bash
$ module list
Currently Loaded Modulefiles:
  1) nag/6.0      2) mpich/3.2    3) xalt/0.7.5   4) PE-nag/1.0
```

```bash
$ module display PE-nag
-------------------------------------------------------------------
/software/dev_tools/swtree/cs400/modulefiles/PE-nag/1.0:

module-whatis     PE-nag defines the environment needed to build

                 applications using NAG Fortran compiler on this system.
conflict     PE-gnu PE-intel PE-pgi
setenv         PE_NAME NAG
setenv         PE_CC mpicc
setenv         PE_CXX mpic++
setenv         PE_FORTRAN mpif90
prepend-path     PATH /software/dev_tools/swtree/cs400_centos7.2_pe2016-08/PE/1.0/noarch/bin
module         load xalt
-------------------------------------------------------------------
```

### Related Information

- [Environment Customization](condos/software/environment.md)
- [Modules](condos/software/modules.md)
