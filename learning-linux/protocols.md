[CADES](http://support.cades.ornl.gov/) → [User Documentation](../README.md) → [Linux](linux-intro.md) → [Protocols](protocols.md)

# Protocols

Protocols are a set of rules or standards that define the communication between devices on a network.

<!-- TOC depthFrom:2 depthTo:2 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Generalities of a Service](#generalities-of-a-service)
- [The `ssh` Protocol](#the-ssh-protocol)
- [The `scp` Protocol](#the-scp-protocol)
- [The `nfs` Protocol](#the-nfs-protocol)

<!-- /TOC -->

## Generalities of a Service

A process is a running program at a particular instant of time.

The process refers to an opening of a Web Browser or any other visible program or action for the user, but this term also includes programs that are running in the background waiting to be called by the system. Those programs can be services that offer remote connection, sending of mail, or translation of IPs into readable URLs.

These services are identified by a number of ports defined by the [Assigned Numbers RFC](https://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml).

The configuration of services is in `/etc/services` and includes the name, the port that defines the service, and which transport protocol is used (UDP or TCP) for each one.

## The `ssh` Protocol

This protocol enables secure connection to the SSH server on a remote machine.

- #### Installation of the package

  By default, in **CentOS 7**, the SSH package comes installed, but if not, please run:

  ```bash
  yum install openssh openssh-server openssh-clients openssl-libs
  ```

  _It installs the openssh package to enable SSH as a server and as a client._

  If you need additional information about **yum commands**, you can visit this [link](https://www.centos.org/docs/5/html/5.1/Deployment_Guide/s1-yum-useful-commands.htm).

- #### The default configuration file

  The default configuration file and settings for the SSHD daemon is in `/etc/ssh/sshd_config`.

  ```bash
  cp /etc/ssh/sshd_config /etc/ssh/sshd_config.ori
  ```

  _This creates a copy of the original configuration file in order to prevent damage or mistakes during a custom configuration._

  Then, you can customize the configuration in the `/etc/ssh/ssh_config` file with these options:

  ```bash
  Port 22
    PermitRootLogin without-password
    PermitRootLogin yes
    PasswordAuthentication yes
    ForwardAgent yes
    ForwardX11 yes
  ```

  Furthermore, to have the ability to run the protocol with the name of the servers such as `ssh server_name`, create a file `~/.ssh/config`, and customize it with:

  ```bash
  Host shortcut_name
    HostName 0.1.2.3
    Port 22
    User x0y
    ServerAliveInterval 120
    IdentityFile ~/.ssh/my_key.pem
  ```

  Then, you will be able to enter the server called `shortcut_name` with SSH by using:

  ```bash
  ssh shortcut_name
  ```

- #### Restart the SSHD service

  Once you make the configuration changes, you can save and close the file. For the changes to take effect, you should restart the SSH daemon.

  ```bash
  systemctl restart sshd.service
  ```

  _This command is used in case the SSHD service is `enabled`. To check the current status of the service, please read more about the [status of a service](services.md)._

- #### Generate an SSH Key

  To secure the transmission of information, SSH employs different types of data manipulation techniques that include forms of asymmetrical encryption such as an SSH key.

  ```bash
  ssh-keygen
  ```

  _Press `Enter` to accept the default location and filename which is `~/.ssh/id_rsa`. Then press `Enter`, then `Enter` again to not set a passphrase when prompted._

  Make sure the SSH key was successfully created by checking the encrypted content at `~/.ssh/id_rsa.pub`.

  This file must have the [permission 600](file-permissions.md). To check it please run `ls -AhlF ~/.ssh`.

  Finally, to copy the SSH key to a server, please run `ssh-copy-id -i ~/.ssh/id_rsa.pub user@server`

## The `scp` Protocol

This protocol allows files to be copied to, from, or between different hosts. It uses SSH for data transfer and provides the same authentication and same level of security as SSH.

- #### Copy the file `remote_file.txt` from a remote host to the local host

```bash
scp x0y@remotehost.ornl.gov:remote_file.txt /some/local/directory
```

- #### Copy the file `local_file.txt` from the local host to a remote host directory

  ```bash
  scp local_file.txt x0y@remotehost.ornl.gov:/some/remote/directory
  ```

- #### Copy the directory `local_directory` from the local host to a remote host's directory `remote_directory`

  ```bash
  scp -r local_directory x0y@remotehost.ornl:/some/remote/directory/remote_directory
  ```

- #### Copy the file `fr1.txt` from remote host `rh1.ornl.gov` to remote host `rh2.ornl.gov`

  ```bash
  scp x0y@rh1.ornl.gov:/some/remote/directory/fr1.txt x0y@rh2.ornl.gov:/some/remote/directory/
  ```

- #### Copy multiple files from a local directory to a remote host home directory

  ```bash
  scp one_file.txt another_file.txt x0y@remotehost.ornl.gov:
  ```


## The `nfs` Protocol

To set up `NFS mounts`, we will need at least two Linux/Unix machines. Here we will be using two servers.

- **NFS Server**: ornlserver.org with IP-192.168.0.100
- **NFS Client**: ornlclient.org with IP-192.168.0.101

### NFS Server

- #### **Configure export directory**

  For sharing a directory with NFS, we need to make an entry in the `/etc/exports` configuration file. Let's create a new directory named `nfsshare` in the `/` partition of the server.

  Then, we need to make an entry in `/etc/exports` and restart the services to make our directory shareable in the network.

  ```bash
  mkdir /nfsshare

  vi /etc/exports
  /nfsshare 192.168.0.101(rw,sync,no_root_squash)

  service autofs restart
  ```

  _It displays a directory in the `/` partition named "nfsshare" which is being shared with client IP "192.168.0.101" with read and write privileges. You can also use the hostname of a server._

### NFS Client

- #### Mount a shared directory on an NSF client

  To mount a directory in our server to access it locally, we need to find out what shares are available on the remote server or NFS Server with `showmount`.

  ```bash
  showmount -e 192.168.0.100
  Export list for 192.168.0.100:
  /nfsshare 192.168.0.101
  ```

  _This command shows that a directory named `nfsshare` is available at "192.168.0.100" to share with your server._

- #### To mount a shared NFS directory permanently, we can use following `mount` command:

  ```bash
  vi /etc/fstab
  192.168.0.100:/nfsshare /mnt  nfs defaults 0 0

  service autofs restart
  ```

  _With `vi /etc/fstab`, we are setting the `IP:name_directory` to be mounted, and it will be mounted on `/mnt`. You can verify it with `mount | grep nfs`._
