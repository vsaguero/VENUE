# VENUS

Requirements: Ubuntu 16.04 installation (Desktop or Server), with internet (physical or virtual machine)

### ALTERNATIVE I 
(*Recommended for users who do not plan to develop their own applications*)

### ALTERNATIVE II 
(*Recommended for users who plan to develop their own applications*)
ns3 installation:
```shell
lxc launch ubuntu:16.04 ns3
lxc start ns3 
lxc exec ns3 bash
```
Inside the container
```shell
apt update
apt install python
apt install gcc 
apt install g++
```

Download ns3
```shell
mkdir ns3
cd ns3
wget https://www.nsnam.org/releases/ns-allinone-3.29.tar.bz2
tar xvjf ns-allinone-3.29.tar.bz2
cd ns-allinone-3.29
./build.py
cd ns-3.29
./waf configure --enable-tests
./tests.py
```
