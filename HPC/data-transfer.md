

# CADES SHPC Data Transfer

## Scripts

We have provided two different methods to get data into the stratus cluster. The datastream_search tool allows access to datastreams that are too big or too old to be stored in the data center's fast storage. The adc_xfer tool allows users access to all the resources available in /data/archive and /data/datastream. For more information, see the table below:

| Data Transfer Scripts | Available Data Search Paths | Script Usage | Resource |
| ----- | ----- | ----- | ----- |
| datastream_search | NA: See script instructions | This program allows you to search and retrieve CADES datastreams. You can search for datastreams by site, data level, and instrument. Once you found your datastreams you can retrieve them with the -r flag. | HPSS Deep Archive |
| adc_xfer | /data/datastream <br> /data/project <br> /data/archive | This program allows you to move data between the ARM Data Center and the cluster. You can search for a path in the ADC using the -als flag or on the cluster using -cls. | ARM Data Center |

## Script Usage

Before you have access to these tools you need to export MODULEPATH (see documentation below). Then load the module data_wrapper/1.0.0 . Now you can use the data transfer scripts like a normal Linux program.

Transfer data from HPSS to CADES Lustre:

`datastream_search [-h] [-s YYYY-MM-DD] [-e YYYY-MM-DD] [-d DATASTREAM] [--site YYY] [--data_level XX] [--inst INSTRUMENT] [-r] [-v]`

The optional arguments and the descriptions are listed below:

| Optional Argument | Optional Argument | Argument Description |
| ----- | ----- | ----- |
| -h | --help | show this help message and exit |
| -s | --start | start date (Default: 1970-01-01) |
| -e | --end | end date (Default: today) |
| -d | --datastream | Get a specific datastream |
| | --site | filters by site |
| | --data-level | filter by data level |
| | --inst | filter by instrument |
| -r | --retrieve | retrieve files |
| -v | | verbose |

Transfer data from ADC to Stratus lustre:

`adc_xfer [-h] (-a ADC_SRC_PATH | -c CLUSTER_SRC_PATH | -als ) [--ops | --sci] DEST`

| Positional Arguments: | |
| --- | --- |
| DEST	| full path to destination |

The optional arguments and the descriptions are listed below:

| Optional Argument | Optional Argument | Argument Description |
| ----- | ----- | ----- |
| -h | --help | show this help message and exit |
| -a | | move file from ADC to cluster (See available Data Search Paths) |
| -c | | move file from cluster to ADC |
| -als | --arm-list | list a directory in ADC |
| --ops | | move to operational directory on warp |
| --sci | | move to science directory on warp |

## Data Retention, Purge, & Quotas

SUMMARY

The following table details quota, backup, purge, and retention information for each user-centric and project-centric storage area available at the CADES Cluster.

DATA STORAGE RESOURCES

| Area | Path | Type | Permissions | Quota | Backups | Purged | Retention |
| --- | --- | --- | --- | --- | --- | --- | --- |
| User Home | /home/$USER | NFS | User-controlled | 10 GB | No | No | NA |
| User Scratch | /lustre/or-hydra/cades-birthright/$USER | Lustre | 700 | TBD | No | No | TBD Days |
| Project Share | /lustre/or-hydra/cades-birthright/proj-share | Lustre | 770 | TBD | No | No | TBD Days |
| World Share | /lustre/or-hydra/cades-arm/world-share | Lustre | 775 | TBD | No | No | TBD Days |
| Local Scratch | /lustre/or-hydra/cades-birthright/scratch | Lustre | 770 | TBD | No | No | TBD Days |
