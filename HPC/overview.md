

# CADES Scalable High-Performance Computing Guide

## Contents
1. [System Overview](SHPC-1-overview.md)
-  [Cluster Policies](SHPC-2-cluster-policies.md)
-  [Accessing Stratus Cluster](SHPC-3-access.md)
    -  [SSH access](SHPC-3-access.md#SSH_access)
-  [Data Storage Resources](SHPC-4-storage.md)
-  [Data Transfer](SHPC-5-data-transfer.md)
    - [Data Retention, Purge, & Quotas](SHPC-5-data-transfer.md#Retention)
-  [Software Environment](SHPC-6-software.md)
    -  [Default Shell](SHPC-6-software.md#shell)
    -  [Using Modules](SHPC-6-software.md#modules)
    -  [Summary of Module Commands](SHPC-6-software.md#module_commands)
    -  [Available Software](SHPC-6-software.md#software)
    -  [Requesting new software](SHPC-6-software.md#requesting-software)
-  [Compiling Codes](SHPC-7-compiling-codes.md)
-  [Running Jobs](SHPC-8-jobs.md)
    -  [Available queues](SHPC-8-jobs.md#queues)
    -  [Scheduling batch jobs](SHPC-8-jobs.md#batch_jobs)


## System Overview

CADES SHPC is a 1080-core computing cluster available to ARM investigators and users for ARM data analysis and visualization. The cluster consists of a 30-node Cray cluster with a total of 7.68 GB DDR4 memory per core. Each dual socket node consist of two Intel Xeon E5-2697V4 processors (18 cores per processor, 36 cores per node). It provides 57.6 TB fast Solid State Drive (SSD) storage and 100 TB parallel Lustre filesystem storage. It uses a high bandwidth Mellanox InfiniBand network. The system has two (2) external login nodes. Two of the system nodes also provides NVIDIA Kepler3 K80 (GK210) GB GPUs.
