# Moving Data

CCLA Data Transfer Nodes (DTNs) allow for speedy movement of large data sets into and out of the network. There are several transfer tool/protocol options to choose from to fit your needs.

1. [Globus](globus-overview.md) has a web interface or command line tools that you can use to transfer data between your personal endpoints or securely share access to your data. *This is the preferred method of transfer for the CCLA.*
2. Secure copy (scp) via the command line to and from storage locations, including local computers.
    ```
    scp username@remote-host1.edu:/path/to/directory/example.txt username@remote-host2.edu:/path/to/directory/
    ```
3. Secure (or SSH) file transfer protocol (SFTP) can be used to transfer files between two remote storage locations (similar to scp) but also allows the user to list directories and see content. You can use SFTP as long as you have SSH access to that host.
    ```
    sftp username@remote_hostname_or_IP
    ```
4. [Graphical clients (SFTP)](graphical-sftp.md) will allow you to use a graphical user interface with drag-and-drop capabilities. CCLA maintains documentation for CyberDuck and WinSCP.

    > For Linux users, there is no clear recommendation for SFTP clients. No one free client supports all of CCLA storage services and behaves consistently. However, [Cloud Explorer](http://cloud-explorer.org/) supports all of CCLA services and _typically_ behaves predictably on Linux systems. See [here](https://www.linux-toys.com/archives/945) for a how-to guide using CloudExplorer and Scality.

5. [rsync](https://rsync.samba.org/) or [rclone](https://rclone.org/) (supports s3) are other command line utilities that may suit your data transfer needs. At this time, CCLA does not offer support for these tools.

<!-- TODO should include why you should choose one over the other -->
