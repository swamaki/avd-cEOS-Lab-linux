# DC1_SVC2A Commands Output

## Table of Contents

- [show lldp neighbors](#show-lldp-neighbors)
- [show ip interface brief](#show-ip-interface-brief)
- [show interfaces description](#show-interfaces-description)
- [show version](#show-version)
- [show running-config](#show-running-config)
## show interfaces description

```
Interface                      Status         Protocol           Description
Et1                            up             up                 
Et2                            up             up                 
Et3                            up             up                 
Et4                            up             up                 
Et5                            up             up                 
Et6                            up             up                 
Ma0                            up             up
```
## show ip interface brief

```
Address
Interface       IP Address           Status     Protocol         MTU    Owner  
--------------- -------------------- ---------- ------------- --------- -------
Management0     172.100.100.6/24     up         up              1500
```
## show lldp neighbors

```
Last table change time   : 0:07:21 ago
Number of table inserts  : 17
Number of table deletes  : 0
Number of table drops    : 0
Number of table age-outs : 0

Port          Neighbor Device ID       Neighbor Port ID    TTL
---------- ------------------------ ---------------------- ---
Et1           spine1                   Ethernet3           120
Et2           spine2                   Ethernet3           120
Et3           svc2b                    Ethernet3           120
Et4           svc2b                    Ethernet4           120
Et5           l2leaf2a                 Ethernet1           120
Et6           l2leaf2b                 Ethernet1           120
Ma0           l2leaf2a                 Management0         120
Ma0           client1                  0242.ac64.640a      120
Ma0           client3                  0242.ac64.640c      120
Ma0           client4                  0242.ac64.640d      120
Ma0           client2                  0242.ac64.640b      120
Ma0           spine1                   Management0         120
Ma0           l2leaf2b                 Management0         120
Ma0           leaf1b                   Management0         120
Ma0           spine2                   Management0         120
Ma0           svc2b                    Management0         120
Ma0           leaf1a                   Management0         120
```
## show running-config

```
! Command: show running-config
! device: svc2a (cEOSLab, EOS-4.30.5M-35156751.4305M (engineering build))
!
no aaa root
!
username admin privilege 15 role network-admin secret sha512 $6$pskabn0lEuUEI7o6$3gCrSUyoGpIarnl5lBTxUWDttwADiGHYb7e/DSzluIK0PQxqYev6MC0IYWTp1QgGNjki9MI3z2BRPORpb8/d6/
!
transceiver qsfp default-mode 4x10G
!
service routing protocols model multi-agent
!
hostname svc2a
!
spanning-tree mode mstp
!
system l1
   unsupported speed action error
   unsupported error-correction action error
!
vrf instance MGMT
!
management api http-commands
   protocol https ssl profile eAPI
   no shutdown
   !
   vrf MGMT
      no shutdown
!
management security
   ssl profile eAPI
      cipher-list HIGH:!eNULL:!aNULL:!MD5:!ADH:!ANULL
      certificate eAPI.crt key eAPI.key
!
interface Ethernet1
!
interface Ethernet2
!
interface Ethernet3
!
interface Ethernet4
!
interface Ethernet5
!
interface Ethernet6
!
interface Management0
   description oob_management
   vrf MGMT
   ip address 172.100.100.6/24
   ipv6 address 2001:172:100:100::6/80
!
no ip routing
no ip routing vrf MGMT
!
ip route vrf MGMT 0.0.0.0/0 172.100.100.1
!
ipv6 route vrf MGMT ::/0 2001:172:100:100::1
!
end
```
## show version

```
Arista cEOSLab
Hardware version: 
Serial number: AFFF3AF89FBEA33189DEACB4CC69CBF2
Hardware MAC address: 001c.731f.af67
System MAC address: 001c.731f.af67

Software image version: 4.30.5M-35156751.4305M (engineering build)
Architecture: i686
Internal build version: 4.30.5M-35156751.4305M
Internal build ID: 10f74693-bb17-4752-b2b8-a0cd835c8624
Image format version: 1.0
Image optimization: None

cEOS tools version: (unknown)
Kernel version: 6.2.0-39-generic

Uptime: 10 minutes
Total memory: 63882152 kB
Free memory: 25217836 kB
```
