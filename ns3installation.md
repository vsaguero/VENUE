ns3 installation:

lxc launch ubuntu:16.04 ns3
lxc start ns3 
lxc exec ns3 bash

Inside the container

apt update
apt install python
apt install gcc 
apt install g++

Download ns3
mkdir ns3
cd ns3
wget 
tar
cd ns3
./build.py
cd ns3
./waf configure --enable-tests
./tests.py

