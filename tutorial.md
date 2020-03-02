## TUTORIAL: First interaction

This tutorial illustrates how to work with the VENUE platform.

First, it is required to download the [Virtual Machine](http://vm-images.netcom.it.uc3m.es/VENUE/) (VM) containing the VENUE installation. The VM runs an Ubuntu server 16.04 LTS that includes 1) [ns-3](https://www.nsnam.org/) discrete-event network simulator and 2) [LXD](https://linuxcontainers.org/lxd/) system container manager.

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

To start the ns-3 network type the following commands:

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
Please note that for the network to remain active, the process cannot be closed. From now on, any operation has to be performed on another terminal.

<li><h4>Fourth step: Check the connectivity between the LXCs</h4></li>

Finally, test the connectivity between the two UAVs. To do this, we're entering into the first container:
```console
imdea@venue:~$ lxc exec uav1 bash
root@uav1:~# ping 10.0.1.2 -c 5
64 bytes from 10.0.1.2: icmp_seq=1 ttl=64 time=1.68 ms
64 bytes from 10.0.1.2: icmp_seq=2 ttl=64 time=1.43 ms
64 bytes from 10.0.1.2: icmp_seq=3 ttl=64 time=2.43 ms
64 bytes from 10.0.1.2: icmp_seq=4 ttl=64 time=1.33 ms
64 bytes from 10.0.1.2: icmp_seq=5 ttl=64 time=3.31 ms
--- 10.0.1.2 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4008ms
rtt min/avg/max/mdev = 1.336/2.040/3.314/0.744 ms
````
If, after this guide, you still have any questions or need some advice to perform more complex experiments, do not hesitate to contact us at victor.sanchez@imdea.org

</ol>
