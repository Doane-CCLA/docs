# Singularity

_Written for software version 2.5.2._

Singularity is a virtualization tool that allows users to containerize workflows, applications, and environments to allow for portability, customization, and reproducibility. Additionally, Singularity is integrated with the Message Passage Interface (MPI) to be used in High Performance Computing (HPC) systems as well as CCLA OpenStack Virtual Machines (VMs) which enables a seamless workflow environment. Lastly, you may also utilize Docker containers with Singularity!

Note: These instructions are adapted from the [official Singularity documentation](https://www.sylabs.io/docs/).

## Prerequisites

- A command line environment in Ubuntu or CentOS.
- Software dependencies (these may be numerous):
  - Ubuntu
      ```bash
      sudo apt-get update && \
      sudo apt-get install \
      python \
      dh-autoreconf \
      build-essential \
      libarchive-dev
      ```
  - CentOS
      ```bash
      sudo yum update && \
      sudo yum groupinstall 'Development Tools' && \
      sudo yum install \
      libarchive-devel \
      squashfs-tools
      ```

## Singularity Installation

The most up-to-date version is housed in a GitHub repository. The software is installed from the source. Use Git to clone the repository and run the following commands.

```bash
git clone https://github.com/singularityware/singularity.git
cd singularity
./autogen.sh
./configure --prefix=/usr/local --sysconfdir=/etc
make
sudo make install
```

## Building a Container using an Existing Container

The following command executes the `build` command, specifies the path and name of the container (`lolcow.simg`), and provides the location of the container on the [Singularity Hub](https://www.singularity-hub.org/) (`shub://GodloveD/lolcow`).

```bash
singularity build lolcow.simg shub://GodloveD/lolcow
```

## Interacting with Containers

There are three primary ways to interact with a Singularity container.

1. Run: Creates an ephemeral container that runs a predefined script

    `singularity run lolcow.simg` or `./lolcow.simg`

2. Shell: Supplies a command line prompt to interface with the container

    `singularity shell lolcow.simg`

3. Execute: Sends a command into the container and provides output

    `singularity exec lolcow.simg`

<hr>

Congratulations! You have successfully deployed a Singularity container!

As some next steps, navigate to the [official Singularity documentation](https://www.sylabs.io/docs/) to learn more about the [Singularity Hub](https://www.singularity-hub.org/), [Docker Hub](https://hub.docker.com/) and [building a container from scratch](https://www.sylabs.io/guides/2.5.1/user-guide/build_a_container.html).
