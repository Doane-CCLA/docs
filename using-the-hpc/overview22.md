# Overview

## Contents

1. [System Overview](https://github.com/Doane-CCLA/docs/tree/6aa8e86be5b614a863272788de3d9c0182ee56c9/HPC/SHPC-1-overview.md)
2. [Cluster Policies](https://github.com/Doane-CCLA/docs/tree/6aa8e86be5b614a863272788de3d9c0182ee56c9/HPC/SHPC-2-cluster-policies.md)
3. [Accessing Stratus Cluster](https://github.com/Doane-CCLA/docs/tree/6aa8e86be5b614a863272788de3d9c0182ee56c9/HPC/SHPC-3-access.md)
   * [SSH access](https://github.com/Doane-CCLA/docs/tree/6aa8e86be5b614a863272788de3d9c0182ee56c9/HPC/SHPC-3-access.md#SSH_access)
4. [Data Storage Resources](https://github.com/Doane-CCLA/docs/tree/6aa8e86be5b614a863272788de3d9c0182ee56c9/HPC/SHPC-4-storage.md)
5. [Data Transfer](https://github.com/Doane-CCLA/docs/tree/6aa8e86be5b614a863272788de3d9c0182ee56c9/HPC/SHPC-5-data-transfer.md)
   * [Data Retention, Purge, & Quotas](https://github.com/Doane-CCLA/docs/tree/6aa8e86be5b614a863272788de3d9c0182ee56c9/HPC/SHPC-5-data-transfer.md#Retention)
6. [Software Environment](https://github.com/Doane-CCLA/docs/tree/6aa8e86be5b614a863272788de3d9c0182ee56c9/HPC/SHPC-6-software.md)
   * [Default Shell](https://github.com/Doane-CCLA/docs/tree/6aa8e86be5b614a863272788de3d9c0182ee56c9/HPC/SHPC-6-software.md#shell)
   * [Using Modules](https://github.com/Doane-CCLA/docs/tree/6aa8e86be5b614a863272788de3d9c0182ee56c9/HPC/SHPC-6-software.md#modules)
   * [Summary of Module Commands](https://github.com/Doane-CCLA/docs/tree/6aa8e86be5b614a863272788de3d9c0182ee56c9/HPC/SHPC-6-software.md#module_commands)
   * [Available Software](https://github.com/Doane-CCLA/docs/tree/6aa8e86be5b614a863272788de3d9c0182ee56c9/HPC/SHPC-6-software.md#software)
   * [Requesting new software](https://github.com/Doane-CCLA/docs/tree/6aa8e86be5b614a863272788de3d9c0182ee56c9/HPC/SHPC-6-software.md#requesting-software)
7. [Compiling Codes](https://github.com/Doane-CCLA/docs/tree/6aa8e86be5b614a863272788de3d9c0182ee56c9/HPC/SHPC-7-compiling-codes.md)
8. [Running Jobs](https://github.com/Doane-CCLA/docs/tree/6aa8e86be5b614a863272788de3d9c0182ee56c9/HPC/SHPC-8-jobs.md)
   * [Available queues](https://github.com/Doane-CCLA/docs/tree/6aa8e86be5b614a863272788de3d9c0182ee56c9/HPC/SHPC-8-jobs.md#queues)
   * [Scheduling batch jobs](https://github.com/Doane-CCLA/docs/tree/6aa8e86be5b614a863272788de3d9c0182ee56c9/HPC/SHPC-8-jobs.md#batch_jobs)

## System Overview

CCLA SHPC is a 1080-core computing cluster available to ARM investigators and users for ARM data analysis and visualization. The cluster consists of a 30-node Cray cluster with a total of 7.68 GB DDR4 memory per core. Each dual socket node consist of two Intel Xeon E5-2697V4 processors \(18 cores per processor, 36 cores per node\). It provides 57.6 TB fast Solid State Drive \(SSD\) storage and 100 TB parallel Lustre filesystem storage. It uses a high bandwidth Mellanox InfiniBand network. The system has two \(2\) external login nodes. Two of the system nodes also provides NVIDIA Kepler3 K80 \(GK210\) GB GPUs.

