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

In this experiment, it is necessary to use two containers. To check their status, use the following command:

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

By default, the LXCs do not start since they need a specific configuration. To properly configure the environment use the following script (this script also provides some configuration needed to start the ns-3 network explained in the next section.):

```console
imdea@venue:~$ sudo sh environment.sh static 2
```

Now, everything is ready to start the containers:
```console
imdea@venue:~$ lxc start uav1
imdea@venue:~$ lxc start uav2
```

After that, the containers should be working, and their state should be running.

```console
imdea@venue:~$ lxc list
+------+---------+--------------------------------+-----------------------------------------------+------------+-----------+
| NAME |  STATE  |              IPV4              |                     IPV6                      |    TYPE    | SNAPSHOTS |
+------+---------+--------------------------------+-----------------------------------------------+------------+-----------+
| uav1 | RUNNING | 10.236.55.141 (eth0)           | fdd2:3294:121f:350f:216:3eff:fe54:1366 (eth0) | PERSISTENT | 0         |
|      |         | 10.0.1.1 (eth1)                |                                               |            |           |
+------+---------+--------------------------------+-----------------------------------------------+------------+-----------+
| uav2 | RUNNING | 10.236.55.133 (eth0)           | fdd2:3294:121f:350f:216:3eff:fee5:a042 (eth0) | PERSISTENT | 0         |
|      |         | 10.0.1.2 (eth1)                |                                               |            |           |
+------+---------+--------------------------------+-----------------------------------------------+------------+-----------+
```
Similar to the VM, each container has two network interfaces. eth0 interface is configured in NAT mode to provide internet connectivity and being able to install any tool for future experiments. The eth1 interface is statically configured and will be used to connect the containers through the network created using ns-3.

<li><h4>Third step: Start the ns-3 wireless emulated network</h4></li>

```console
imdea@venue:~$ cd ns3/
imdea@venue:~/ns3$ cd ns-3-allinone/
imdea@venue:~/ns3/ns-3-allinone$ cd ns-3.30/
imdea@venue:~/ns3/ns-3-allinone/ns-3.30$ sudo ./waf --run scratch/helloworld
[sudo] password for imdea:
Waf: Entering directory `/home/imdea/ns3/ns-3-allinone/ns-3.30/build'
Waf: Leaving directory `/home/imdea/ns3/ns-3-allinone/ns-3.30/build'
Build commands will be stored in build/compile_commands.json
'build' finished successfully (1.669s)
```

<li><h4>Fourth step: Check the connectivity between the LXCs</h4></li>
</ol>
