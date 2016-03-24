#Wireless Networks Group Project

## What's going on?
This repositiory contains the configuration files for each cisco device
used in the project.

The project will be completed in a number of stages, each improving on the last.
This page contains a topology diagram of the network for the current stage, and
a list of checkpoints for the stage.


## Topology
![](http://uploads.jonne.io/topology_001.svg)


## Stage 1

##### All Devices
---
+ Basic config
+ Enable secret `ithurtswhenIP`
+ Interfaces configured
+ Local user `LANDownUnder` with password `ithurtswhenIP`
+ SSHv2 enabled, telnet disabled

##### All switches in `HQ`
---
+ Vlans 190, 191, 192, 199 and 999 added
+ All unused switchports set to blackhole VLAN (999) and shutdown
+ Only Vlans 190, 191, 192 and 199 allowed on trunks

##### All Access Points
---
+ Get addresses via DHCP
+ Discover and join controller via option 43

##### HQ_SW1
---
+ Ports Fa0/10-14 as access ports on vlan 199
+ Static default route to `HQ_ROUTER`
+ Acting as DHCP server for networks 172.16.190.0/24, 172.16.191.0/24, 172.16.192.0/24 and 172.16.199.0/24 (exclude address .1 - .29)


##### HQ_ROUTER
---
+ Static route to `BR1_ROUTER`
+ Acting as NTP server
+ 

##### BR1_ROUTER
---
+ Acting as DHCP server for network 172.16.198.0/24 (exluded addresses .1 - .29)
+ Static route to `HQ_ROUTER`

##### HQ_WLC01
---
+ SSIDs `GUEST`, `STAFF` and `STUDENT`
+ `GUEST` traffic on VLAN 190.
+ `STAFF` traffic on VLAN 191.
+ `STUDENT` traffic on VLAN 192.


