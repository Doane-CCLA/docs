## Intro to CVMFS

Full documentation for the CernVM-File System (CVMFS) is available [here](https://cvmfs.readthedocs.io/en/stable/) which provides an introduction:

"The CernVM-File System (CernVM-FS) provides a scalable, reliable and low-maintenance software distribution service. It was developed to assist High Energy Physics (HEP) collaborations to deploy software on the worldwide- distributed computing infrastructure used to run data processing applications. CernVM-FS is implemented as a POSIX read-only file system in user space (a FUSE module). Files and directories are hosted on standard web servers and mounted in the universal namespace /cvmfs. Internally, CernVM-FS uses content-addressable storage and Merkle trees in order to maintain file data and meta-data. CernVM-FS uses outgoing HTTP connections only, thereby it avoids most of the firewall issues of other network file systems. It transfers data and meta-data on demand and verifies data integrity by cryptographic hashes.

By means of aggressive caching and reduction of latency, CernVM-FS focuses specifically on the software use case. Software usually comprises many small files that are frequently opened and read as a whole. Furthermore, the software use case includes frequent look-ups for files in multiple directories when search paths are examined.

CernVM-FS is actively used by small and large HEP collaborations. In many cases, it replaces package managers and shared software areas on cluster file systems as means to distribute the software used to process experiment data."

CVMFS might be thought of as a content distribution network for software which makes centrally managed and updated software repositories available across resources. This allows using the same software packages, toolchains, libraries and tools, across HPC institutes, private or public cloud environments and even desktop systems.

CVMFS integrates very will with container management systems, allowing the same software tree to be presented within containers or VMs without having to install (and maintain) the same packages into each, which may vary in versions or compilation options as well as creating container size bloat.

Software accessed via CVMFS is cached locally, thus providing runtime performance comparable to locally installed versions.


## CVMFS within CCLA

CCLA is providing initial access to cvmfs software repositories for evaluation in our SHPC environments.

Repositories for the Open Science Grid, and a (currently empty) internal CCLA repo are available on SPHC nodes.

CVMFS software repos may also be accessed by VMs running in CCLA OpenStack and ORNL desktop Linux systems. Instructions will be provided for these use cases, though CCLA support efforts will be focused on CVMFS within the SHPC environment.

### CVMFS Support

For assistance with cvmfs, please either email ccla@doane.edu or use the #cvmfs channel at https://cades.slack.com


### CVMS on SHPC Condos

The SHPC cluster login and compute nodes have cvmfs configured for the Open Science Grid repo and a new (as yet empty) cades.ornl.gov repo.

Other software repos (CERN, SLAC, FNAL, etc.) may be officially added in the future.

#### CVMFS Repos Available

The cades repos is hosted by ORNL which over time will be populated with the CCLA software tree.

The OSG repo contains software distributed and maintained by the Open Science Grid.

Directories under /cvmfs are automounted upon access. The cvmfs_config probe command will also cause them to be presented as well as verify availability:

On or-condo-login01:

```
-bash-4.2$ cvmfs_config probe
Probing /cvmfs/oasis.opensciencegrid.org... OK
Probing /cvmfs/rdlinux.ornl.gov... OK
Probing /cvmfs/cades.ornl.gov... OK

-bash-4.2$ ls /cvmfs/oasis.opensciencegrid.org/osg/
bin  modules  modules2  palms  projects  README.txt  sw  test_spack  update.details

-bash-4.2$ ls /cvmfs/cades.ornl.gov/
cades-ops  pgi
```

### OSG CVMFS Provided Modules and Tutorials

The Open Science Grid repo provides a nice software catalog and module wrapper to allow easily switching to their software tree.

This software repository is built and maintained by the OSG, and not CCLA. It is made available to users, though the software itself is not supported by CCLA.

Additional info:
https://support.opensciencegrid.org/support/solutions/articles/12000006683-switching-between-oasis-and-local-modules

On or-condo-login01
```
-bash-4.2$ source /cvmfs/oasis.opensciencegrid.org/osg/modules/lmod/current/init/bash

-bash-4.2$ module avail
----------------------- /cvmfs/oasis.opensciencegrid.org/osg/modules/modulefiles/Core -----------------------
   ANTS/1.9.4                       freetype/2.5.5             opencv/2.4.10
   ANTS/2.1.0                (D)    fsl/5.0.8                  opensees/6482
   Julia/0.6.0                      gamess/2013                opensim/3.3
   MUMmer/3.23                      gate/7.2                   orca/3.0.3
   OpenBUGS/3.2.3                   gcc/4.6.2                  orca/4.0.0                (D)
   OpenBUGS-3.2.3/3.2.3             gcc/4.6.4                  papi/5.3.2
   R/3.1.1                   (D)    gcc/4.8.1                  pari/2.7.5
   R/3.2.0                          gcc/4.9.2           (D)    pax/evan-testing
   R/3.2.1                          gcc/4.9.3                  pax/4.5.0
   R/3.2.2                          gcc/6.2.0                  pax/4.6.1
   R/3.3.1                          gd/2.1.1                   pax/4.9.1
   R/3.3.2                          gdal/2.0.0                 pax/4.11.0                (D)
   RAxML/8.2.9                      geant4/9.4p02              pbsuite/14.9.9
   RAxML-NG/0.5.0beta               geant4/10.02               pcre/8.35
   SeqGen/1.3.3                     geant4/10.3p01      (D)    pegasus/4.4.2-image_tools
   Shelx/2015                       geos/3.4.2                 pegasus/4.5.3
   SitePackage                      gfal/7.20                  pegasus/4.6.0dev
   SparseSuite/4.2.1                git/1.9.0                  pegasus/4.6.0cvs
   ViennaRNA/2.2                    glpk/4.54                  pegasus/4.6.0
   abyss/2.0.2                      gmp/6.0.0                  pegasus/4.6.1dev
   ant/1.9.4                        gnome_libs/1.0             pegasus/4.6.1
   apr/1.5.1                        gnuplot/4.6.5              pegasus/4.7.0
   aprutil/1.5.3                    graphviz/2.38.0            pegasus/4.7.1
   arc-lite/2015                    grass/6.4.4                pegasus/4.7.3
   atlas/3.10.1                     gromacs/4.6.5              pegasus/4.7.4
   atlas/3.10.2              (D)    gromacs/5.0.0       (D)    pegasus/4.8.0             (D)
   autodock/4.2.6                   gromacs/5.0.5.cuda         phenix/1.10
   bedtools/2.21                    gromacs/5.0.5              poppler/0.24.1            (D)
   binutils/2.26                    gromacs/5.1.2-cuda         poppler/0.32
   blasr/1.3.1                      gsl/1.16                   povray/3.7
   blast                            gsl/2.3             (D)    proj/4.9.1
   blender                          hdf5/1.8.9                 proot/2014
   boost/1.50.0                     hdf5/1.8.12-cxx11          protobuf/2.5
   boost/1.56                       hdf5/1.8.12                psi4/0.3.74
   boost/1.57.0                     hdf5/1.8.13-cxx11          psi4/1.1                  (D)
   boost/1.62.0-cxx11               hdf5/1.8.13         (D)    python/2.7                (D)
   boost/1.62.0              (D)    healpix/3.30               python/3.4
   bowtie/2.2.3                     hisat2/2.0.3-beta          python/3.5.2
   bowtie/2.2.9              (D)    hmmer/3.1                  qhull/2012.1
   bwa/0.7.12                       igraph/0.7.1               root/5.34-32-py34
   bwa/2014                  (D)    imagemagick/7.0.2          root/5.34-32
   bzip2/1.0.6                      intelMKL/11.3.0.109        root/6.06-02-py34         (D)
   canopy/1.4.1                     ipopt/3.12.6               rosetta/2015
   casino/2.13.211                  jasper/1.900.1             rosetta/2016-02
   cblosc/1.7.1                     java/7u71                  rosetta/2016-32           (D)
   ccp4/2015                        java/8u25                  ruby/2.1
   cctools/4.4.2                    java/8u131          (D)    rucio/1.6.6
   cctools/5.2.3                    jpeg/6b                    saga/2.2.0
   cctools/5.4.7                    jpeg/9a             (D)    samtools/0.1.17
   cctools/6.0.7             (D)    julia/0.6.0                samtools/1.3.1            (D)
   cdo/1.6.4                        lammps/2.0                 sca/10.1.6a
   cfitsio/3.37                     lammps/15May15      (D)    scons/2.3.4
   circos/0.68                      lapack/3.5.0               sdpa/7.3.8
   clhep/2.1.0.1                    lapack/3.6.1        (D)    serf/1.37
   clhep/2.2.0.8                    libXpm/3.5.10              settarg/5.6.2
   clhep/2.3.1.0                    libgfortran/4.4.7          shelx/2015
   clhep/2.3.1.1                    libtiff/4.0.4              shrimp/2.2.3
   clhep/2.3.4.4             (D)    llvm/3.6                   siesta/3.2
   cmake/3.0.1                      llvm/3.7                   simbody/3.5.3
   cmake/3.4.1                      llvm/3.8.0          (D)    snappy/1.1.3
   cmake/3.8.0               (D)    lmod/5.6.2                 sqlite/3.8.11.1
   connect-client/0.2.1             madgraph/2.1.2             sra/2.5.4
   connect-client/0.3.0             madgraph/2.2.2      (D)    sra/2.8.0                 (D)
   connect-client/0.4.0             matlab/2013b               stashcp/2.6
   connect-client/0.5.3      (D)    matlab/2014a               stashcp/4.3.0
   cp2k/2.5.1                       matlab/2014b               stashcp/4.3.1             (D)
   cpan/perl-5.10                   matlab/2015a               stringtie/1.1.2
   cufflinks/2.2.1                  matlab/2015b               stringtie/1.2.2           (D)
   curl/7.37.1                      matlab/2016a               subversion/1.8.10
   dakota/6.4.0                     matlab/2016b               sundials/2.5
   dmtcp/2.5.0                      matlab/2017a               swift/0.94.1
   ectools                          matlab/2017b        (D)    swift/0.96.2              (D)
   eemt/0.1                         mercurial/1.9.1            tassel/5.0
   eigen/3.2.10                     mixmodlib/3.1              tcl/8.6.2
   einstein/Payne-Gaposchkin        mono/4.2.1                 tcsh/6.20.00
   elastix/2015                     mothur/1.39.0              tophat/2.0.13
   entropy/2017.03.16               mpc/1.0.3                  tophat/2.1.1              (D)
   espresso/5.1                     mpfr/3.1.3                 transabyss/1.5.5
   espresso/5.2              (D)    mplayer/1.1                tutorial/1.0
   ete2/2.3.8                       mrbayes/3.2.2              uclust/2.22
   expat/2.1.0                      muscle/3.8.31              udunits/2.2.17
   ffmpeg/0.10.15                   mysql/5.1.73               unixodbc/2.3.2
   ffmpeg/2.5.2              (D)    namd/2.9                   valgrind/3.10
   fftw/3.3.4-gromacs               namd/2.10.cuda             vmd/1.9.1
   fftw/3.3.4                (D)    namd/2.10           (D)    wget/1.15
   fiji/2.0                         nco/4.3.0                  wxgtk/3.0.2
   fpc/2.6.4                        netcdf/4.2.0               xrootd/4.1.1
   freesurfer/5.1.0                 ngsTools/2017.03.16        xrootd/4.2.1              (D)
   freesurfer/5.3.0                 octave/3.8.1               xz/5.2.2
   freesurfer/6.0.0          (D)    openbabel/2.3.2            zlib/1.2.8
```

OSG Software tutorials are available with

```
-bash-4.2$ module load tutorial

-bash-4.2$ tutorial
  :)

-bash-4.2$ tutorial tensorflow-matmul
-bash-4.2$ less ./tutorial-tensorflow-matmul/README.md

```

Other OSG Module environment tools

```
-bash-4.2$ less /cvmfs/oasis.opensciencegrid.org/osg/sw/module-init.sh
-bash-4.2$ less /cvmfs/oasis.opensciencegrid.org/osg/sw/rhel/7/lmod/6.3/init/profile

View your current module environmentals:
-bash-4.2$ env | grep MODULE
```
