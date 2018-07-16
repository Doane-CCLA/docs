[CADES](http://support.cades.ornl.gov/) → [User Documentation](../README.md) → [Linux](linux-intro.md) → [System Configuration](system-config.md)

# System Configuration

- #### hostname: displays the name of the computer

  ```bash
  hostname
  ```

  _It will show the current name of the machine._

  To change the hostname, please type `hostnamectl set-hostname <new_name>`, and for additional configuration, the file is located at `/etc/hostname`.

- #### dmidecode: gives information about the hardware and detects if it is a virtual machine

  ```bash
  dmidecode
  ```

  _The information includes manufacturer, model, serial number, asset tags, CPU sockets, PCI slots, DIMM slots, and other I/O port info detected by the BIOS._

- #### uname: displays system information about the Linux environment

  ```bash
  uname -v
  ```

  _It will show you the version of the Linux kernel you are running._

  If you want to know the hardware platform, such as x86_64 or 32-bits, please run `uname -i`. If you need more details about the software, please run `uname -a`.

- #### free: check the used and available space of physical memory and swap memory

  ```bash
  free -g
  ```

  _It will display the size of the memory in GB (Gigabytes)._

  If you want to display the total line of the memory resource used, please run `free -t` or do `cat /proc/meminfo`.

- #### lscpu: shows CPU architecture information

  ```bash
  lscpu
  ```

  _It will show the vendor of the CPU, as well as the GHz, cores per socket, etc._

  You can view the information of your system CPU by viewing the content of the `/proc/cpuinfo`.

- #### top: shows statistical data related to the performance of a system and is updated every 5 seconds

  ```bash
  top
  ```

  _It will display a real-time view of the performance data of all running processes in a system._

  To sort by the use of CPU, type `P`, or if you want to sort by the use of memory, please type `M`, and `u` to view processes owned by a specific user. Press `q` to quit.

- #### iostat: lists CPU utilization, device utilization, and network file system utilization considered since the last reboot

  ```bash
  iostat -C
  ```

  _It will display to columns: **NAME** and **Comments** in the `/tmp/data_tab.txt` file._

  It will break the CPU utilization into user processes, system processes, I/O wait, and idle time.

- #### uptime: gives you the time for which the system has been up (or running)

  ```bash
  uptime
  ```

  _It will display the current time, how long the system has been running, users currently logged on, and the system load averages for the past 1, 5, and 15 minutes_.
