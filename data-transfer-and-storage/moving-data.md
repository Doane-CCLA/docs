[CADES](http://support.cades.ornl.gov/) &rarr; [User Documentation](../README.md) &rarr; [Moving Data](moving-data.md)

# Moving Data

CADES Data Transfer Nodes (DTNs) allow for speedy movement of large data sets into and out of ORNL's network. There are several transfer tool/protocol options to choose from to fit your needs.

1. [Globus](globus-overview.md) has a web interface or command line tools that you can use to transfer data between your personal endpoints or securely share access to your data. *This is the preferred method of transfer for CADES.*
2. Secure copy (scp) via the command line to and from storage locations, including local computers.
    ```
    scp username@remote-host1.gov:/path/to/directory/example.txt username@remote-host2.gov:/path/to/directory/
    ```
3. Secure (or SSH) file transfer protocol (SFTP) can be used to transfer files between two remote storage locations (similar to scp) but also allows the user to list directories and see content. You can use SFTP as long as you have SSH access to that host.
    ```
    sftp username@remote_hostname_or_IP
    ```
4. [Graphical clients (SFTP)](graphical-sftp.md) will allow you to use a graphical user interface with drag-and-drop capabilities. CADES maintains documentation for CyberDuck and WinSCP.

    > For Linux users, there is no clear recommendation for SFTP clients. No one free client supports all of CADES storage services and behaves consistently. However, [Cloud Explorer](http://cloud-explorer.org/) supports all of CADES services and _typically_ behaves predictably on Linux systems. See [here](https://www.linux-toys.com/archives/945) for a how-to guide using CloudExplorer and Scality.

5. [rsync](https://rsync.samba.org/) or [rclone](https://rclone.org/) (supports s3) are other command line utilities that may suit your data transfer needs. At this time, CADES does not offer support for these tools.

<!-- TODO should include why you should choose one over the other -->
