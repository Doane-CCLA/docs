# Storage

The HPC provides an array of data storage platforms, each designed with a particular purpose in mind. Storage areas are broadly divided into two categories: those intended for user data and those intended for project data. Within each of the two categories, we provide different sub-areas, each with an intended purpose:

Storage Area  | Path                                                 | Purpose
------------- | ---------------------------------------------------- | ------------------------------------------
User Home     | /home/$USER                                          | Long-term data for routine access
User Scratch  | /export/$USER                                  | Short-term project data for fast, batch-job access that is not shared

#### USER HOME

Home directories for each user are NFS-mounted on all HPC systems and are intended to store long-term, frequently-accessed user data. User Home areas are not backed up. This file system does not generally provide the input/output (I/O) performance required by most compute jobs, and is not available to compute jobs on most larger systems. If a file system associated with your User Home directory is nearing capacity, HPC Support may contact you to request that you reduce the size of your Member home directory.
#### USER EXPORT

Users can temporarly store compputational data in /export, and it is available to all compute nodes. Because of the scratch nature of the file system, it is not backed up and files are subject to purged on a regular basis. Files should not be retained in this file system for long, but rather should be migrated to personal archive space as soon as the files are not actively being used. If a file system associated with your User Export directory is nearing capacity, HPC Support may contact you to request that you reduce the size of your Member export directory.

