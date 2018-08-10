# Docker Containers

📝 **Note:** If you are looking to eventually utilize Docker containers on an High Performance Computer (HPC), you may consider using [Singularity](singularity.md) instead, as it is designed to work in HPC systems.

## Background

[Docker](https://www.docker.com/) is a [container](https://en.wikipedia.org/wiki/Operating-system-level_virtualization) architecture and ecosystem.  A [linux.com article](https://www.linux.com/news/docker-shipping-container-linux-code) nicely summarizes Docker as follows:

>Docker is a tool that can package an application and its dependencies in a virtual container that can run on any Linux server. This helps enable flexibility and portability on where the application can run, whether on premises, public cloud, private cloud, bare metal, etc.

Containers have somewhat similar goals to a virtual machine (VM).  However, a Docker container is not a VM.  You are probably aware that VM's have some performance overhead compared to running things natively.  However, it is worth noting that the applications that run inside of Docker containers actually run *natively*. Your Docker containers share the kernel with their host operating system. So there is no double overhead in running a container inside our VM.  However, we still suffer some performance penalty by having virtualized in the first place.

Many of the applications you will be interested in deploying are already configured for very easy use with Docker.  You can find public repositories of many of your favorite applications set up on [Docker Hub](https://hub.docker.com/).



## First Steps

This tutorial uses an Ubuntu operating system.


## Install Docker

The official Docker documentation [provides a lot of useful information](https://docs.docker.com/engine/installation/linux/ubuntu/#install-using-the-repository) to this end.  Below we summarize only the steps outlined in that article.  If you wish to understand an individual step or if something goes wrong, please refer to the article.

Otherwise, run:

```bash
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo apt-key fingerprint 0EBFCD88

sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"

sudo apt-get update
sudo apt-get install -y docker docker.io
```

And if all is well, you should have Docker installed on your system.

## Run a Test Container

You can test that your setup is working correctly by running:

```bash
sudo docker pull hello-world
sudo docker run hello-world
```

If all goes well, you will have a small "hello world"-like output and return to your terminal, and should look something like this:

That's it!
