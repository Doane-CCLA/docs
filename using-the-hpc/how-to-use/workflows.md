# Running Scientific Computational Workflows

## Overview

Workflows offer benefits of automation and efficient orchestration (eg. data parallel execution) of multi-stage computation. Furthermore, they are powerful reproducibility and portability tools for science and engineering applications.

Typically, a workflow is written in a high level language that is offered and understood by a workflow management software or simply a workflow tool.

## Workflow tools available on Condos

We currently offer support for the following workflow tools on SHPC:

1. Nextflow
1. Makeflow
1. Swift

A brief description about each of the aforementioned workflow tools is provided below:

**Nextflow**   
[Nextflow](https://www.nextflow.io/docs/latest/index.html) is a favored workflow tool among Singularity container users. Similarly, it is popular among users from the Biosciences domain.

**Makeflow**   
The [Makeflow](http://ccl.cse.nd.edu/software/makeflow/) workflow system uses a Makefile like language to define workflows that may be deployed and executed over clusters and clouds.

**Swift**   
[Swift](http://swift-lang.org/Swift-T/index.php) uses a C-like syntax to define workflows. Swift is capable of stitching computational steps defined in the workflow as a true HPC workflow that uses the Message Passing Paradigm of parallel computation using the MPI libraries and its own load balancer.

> &#128221; **Note:** While Nextflow and Makeflow require additional configuration if you wish to run them on compute nodes, Swift can run directly on compute nodes by simply plugging it into a job definition script just like any other MPI application.

## Example Workflows

### Hello World
#### Nextflow
```bash
#!/usr/bin/env nextflow

params.str = 'Hello world!'

process splitLetters {

    output:
    file 'chunk_*' into letters mode flatten

    """
    printf '${params.str}' | split -b 6 - chunk_
    """
}

process convertToUpper {

    input:
    file x from letters

    output:
    stdout result

    """
    cat $x | tr '[a-z]' '[A-Z]'
    """
}

result.subscribe {
    println it.trim()
}
```
Save the above code in a file, eg. `hello.nf`. To run the workflow on open condo login node, do the following:
```bash
$ module purge
$ module load PE-gnu
$ module load java/1.8.0_131
$ module load nextflow
$ nextflow run hello.nf
```

You should see output similar to the following:

```
N E X T F L O W  ~  version 0.27.6
Launching `nextflow_example.nf` [insane_meucci] - revision: 5319db7b93
[warm up] executor > local
[f9/cb98ba] Submitted process > splitLetters
[94/6ed3f3] Submitted process > convertToUpper (1)
[cb/506a85] Submitted process > convertToUpper (2)
HELLO
WORLD!
```

#### Makeflow
A "Hello World" in Makeflow would look something like so:
```bash
ECHO=/bin/echo

hello.txt:
	$ECHO 'Hello World!' > hello.txt

```
Save the above code in a file, say `hello.mkf` and run it on the open condo like so:

```bash
$ module load PE-gnu
$ module load cctools/6.2.7
$ makeflow hello.mkf
```
If all goes well, the output should look like so:
```
parsing hello.mkf...
local resources: 32 cores, 128833 MB memory, 6893119 MB disk
max running local jobs: 32
checking hello.mkf for consistency...
hello.mkf has 1 rules.
recovering from log file hello.mkf.makeflowlog...
makeflow: hello.txt is reported as existing, but does not exist.
starting workflow....
submitting job: /bin/echo ''Hello World!'' > hello.txt
submitted job 123822
job 123822 completed
nothing left to do.
```
And you should see a new file called `hello.txt` in your current working directory.

#### Swift
A Swift Hello World workflow looks like so:

```c
import io;

printf("Hello world");
```

Swift uses two steps to workflow execution: compile and run.

Load the swift module on condo like so:
```
$ module purge
$ module load PE-gnu
$ module load java/1.8.0_131 mpich/3.2
$ module load swift
```

Compile and run the workflow like so:
```
$ stc hello.swift
```
The above step will produce a TCL file called `hello.tic`. Run the TCL file like so:
```
turbine -n 2 hello.tic
```

If all goes well, you should see the following output:

```
Hello world
```

### General remarks
1. Note that the above workflows will run on login nodes. In order for them to run over compute nodes, more configuration is needed.
-  Note that `Nextflow` expects absolute paths for data and executables since it works in its own temp directory. Please adjust the paths to where you choose to run the workflow.

### Where to go from here?
* Use the [Crystal Workflow](condo-crystal-workflow.md) with these workflow tools.
* Come talk to us at CADES if you think one or more of your applications will benefit with the help of the aforementioned workflow tools.
