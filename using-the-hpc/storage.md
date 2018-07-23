[CADES](http://support.cades.ornl.gov/) → [User Documentation](../README.md) → [SHPC Condo User Guide](overview.md) → [Storage Configuration](storage.md)

# SHPC Condo Storage Configuration

## Lustre

[Lustre](http://wiki.lustre.org) is an on-premises, high performance, parallel file system that utilize technologies such as key, value, and set of attributes to compute data in the following environments:

**Open Lustre**:

- 1.7 PB of temporary computational storage

  _Your **temporary local storage** is located at_:`/lustre/or-hydra/group/username`

  Replace `group` with _[your group name](condos/how-to-use/request-access.md)_, and `username` with _your XCAMS/UCAMS_ ID.

**Moderate Lustre**:

- 400 TB of temporary computational storage

  _Your **temporary local storage** is located at_: `/lustre/hydra/group/username`

  Replace `group` with _[your group name](condos/how-to-use/request-access.md)_, and `username` with _your XCAMS/UCAMS_ ID.

📝 **Note:** All data is automatically purged every 2 weeks.

## NFS

[NFS (Network File System)](https://www.tldp.org/HOWTO/NFS-HOWTO/index.html) is a service that allows shared directories and files with others over a network. Home, software, and project directories have been set up on NFS and _are permanently available through the network_.

**Open NFS**:

- Each user is automatically given 20 GB of permanent NFS storage.

**Moderate NFS**:

- Each user is automatically given 20 GB of permanent NFS storage.

📝 **Note**: If your needs differ from what is listed here, be sure to [contact us](../../SUPPORT.md) to discuss options.
