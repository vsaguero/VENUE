## TUTORIAL: First interaction

This tutorial illustrates how to work with the VENUE platform.

First, it is required to download the [Virtual Machine](www.google.es) (VM) containing the VENUE installation. The VM runs an Ubuntu server 16.04 LTS that includes 1) [ns-3](https://www.nsnam.org/) discrete-event network simulator and 2) [LXD](https://linuxcontainers.org/lxd/) system container manager.

<ol>
  <li><h4>First step: Start the VM</h4></li>
  
  The first step is to start the VM. Its credentials are:

  ```
     login: imdea
     password: imdea
  ```
  Once the machine has been started, it can be accessed using ssh. The VM has two interfaces, first one in bridge mode connected to a physical interface of the host (which should allow entering through ssh); and an interface in NAT mode which gives internet connectivity enabling quick installation and configuration of new software.

<li><h4>Second step: Start the Linux Containers</h4></li>

By default, the two LXD containers of this experiment are started. To check their status, use the following command:

```console
imdea@venue:~$ lxc list
+------+---------+------+------+------------+-----------+
| NAME |  STATE  | IPV4 | IPV6 |    TYPE    | SNAPSHOTS |
+------+---------+------+------+------------+-----------+
| uav1 | STOPPED |      |      | PERSISTENT | 0         |
+------+---------+------+------+------------+-----------+
| uav2 | STOPPED |      |      | PERSISTENT | 0         |
+------+---------+------+------+------------+-----------+
```

In case the output is not similar to the previous output, it is advised to start the containers using LXD commands.

<li><h4>Third step: Start the ns-3 wireless emulated network</h4></li>
<li><h4>Fourth step: Check the connectivity between the LXCs</h4></li>
</ol>
