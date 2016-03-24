#Wireless Networks Group Project

## What's going on?
This repositiory contains the configuration files for each cisco device
used in the project.

The project will be completed in a number of stages, each improving on the last.
This page contains a topology diagram of the network for the current stage, and
a list of checkpoints for the stage.


## Topology
![](http://uploads.jonne.io/topology_001.svg)

## Important things
---
#### Networks
+ `172.16.199.0/24` (**VLAN 199**) HQ Management (for SSH and stuff)
+ `172.16.198.0/24` BR1
+ `172.16.197.0/24` (**VLAN 197**) HQ AP Management
+ `172.16.196.0/30` Link between HQ and BR1
+ `172.16.193.0/24` (**VLAN 193**) User data in HQ
+ `172.16.192.0/24` (**VLAN 192**) Traffic from `G190-STUDENT`
+ `172.16.191.0/24` (**VLAN 191**) Traffic from `G190-STAFF`
+ `172.16.190.0/24` (**VLAN 190**) Traffic from `G190-GUEST`


## Stage 1

##### All Devices
---
+ Basic config
+ Enable secret `ithurtswhenIP`
+ Interfaces configured
+ Local user `LANDownUnder` with password `ithurtswhenIP`
+ SSHv2 enabled, telnet disabled
+ Domain `landownunder` (for SSH)

##### All switches in `HQ`
---
+ Vlans 190, 191, 192, 193, 197, 199 and 999 added
+ All unused switchports set to blackhole VLAN (999) and shutdown
+ Only Vlans 190, 191, 192, 193, 197 and 199 allowed on trunks

##### All Access Points
---
+ Get addresses via DHCP
+ Discover and join controller via option 43

##### HQ_SW1
---
+ Ports Fa0/10-14 as access ports on vlan 199
+ Static default route to `HQ_ROUTER`
+ Acting as DHCP server for networks 172.16.190.0/24, 172.16.191.0/24, 172.16.192.0/24 and 172.16.199.0/24 (exclude address .1 - .29)
+ OSPF


##### HQ_ROUTER
---
+ Static route to `BR1_ROUTER`
+ Acting as NTP server
+ OSPF

##### BR1_ROUTER
---
+ Acting as DHCP server for network 172.16.198.0/24 (exluded addresses .1 - .29)
+ Static route to `HQ_ROUTER`
+ OSPF

##### HQ_WLC01
---
+ SSIDs `G190-GUEST`, `G190-STAFF` and `G190-STUDENT`
+ `G190-GUEST` traffic on VLAN 190.
+ `G190-STAFF` traffic on VLAN 191.
+ `G190-STUDENT` traffic on VLAN 192.


