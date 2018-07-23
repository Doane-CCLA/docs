[CADES](http://support.cades.ornl.gov/) &rarr; [User Documentation](../../README.md) &rarr; [SHPC Condo User Guide](../overview.md)  &rarr; [Software](../software.md)  &rarr; [Bash Environment Customization](bash-env.md)  &rarr; [GNU Compiler](#)

# Customizing Your Environment: GNU Compiler

Locate your prompt in your home directory by executing `cd`.

You can add the following content to the `/home/username/.bash_profile`:

```
export PATH=/opt/torque/bin:/opt/torque/sbin:/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin
export LD_LIBRARY_PATH=

# Uncomment the following line if you don't like systemctl's auto-paging feature:
# export SYSTEMD_PAGER=

# R package by Anthony Walker
export PATH=/home/alp/src/R-3.2.5:/home/alp/R/bin:$PATH
export R_LIBS_USER=/home/alp/bin/Rlibs

# the following are with gcc-5.3.0, openmpi-1.10.3 (default)
module unload PE-intel
module unload PE-pgi
module load PE-gnu/1.0

module load boost/1.61.0
module load cmake/3.6.1
module load zlib/1.2.8

# parallel-enabled hdf5 with openmpi-1.10.3/gcc5.3.0
module load hdf5-parallel/1.8.17

export HDF5_PATH=/software/dev_tools/swtree/cs400_centos7.2_pe2016-08/hdf5-parallel/1.8.17/centos7.2_gnu5.3.0
export PATH=$HDF5_PATH/bin:$PATH
export LD_LIBRARY_PATH=$HDF5_PATH/lib:$LD_LIBRARY_PATH


# needs blas-lapack
module load mkl/2017
BLASLAPACK_LIBDIR=/software/dev_tools/swtree/cs400_centos7.2_pe2016-08/mkl/2017/centos7.2_gnu5.3.0/lib

# parallel-enabled hdf5 with openmpi-1.10.3/intel2016
module load hdf5-parallel/1.8.17

export HDF5_PATH=/software/dev_tools/swtree/cs400_centos7.2_pe2016-08/hdf5-parallel/1.8.17/centos7.2_gnu5.3.0
export PATH=$HDF5_PATH/bin:$PATH
export LD_LIBRARY_PATH=$HDF5_PATH/lib:$LD_LIBRARY_PATH

# netcdf built with openmpi-1.10.3/gnu and support of hdf5 (i.e. netcdf-4)
#module load netcdf-hdf5parallel/4.3.3.1
#export NETCDF_PATH=/software/dev_tools/swtree/cs400_centos7.2_pe2016-08/netcdf-hdf5parallel/4.3.3.1/centos7.2_gnu5.3.0

export PATH=$NETCDF_PATH/bin:$PATH
export LD_LIBRARY_PATH=$NETCDF_PATH/lib:$LD_LIBRARY_PATH
```
