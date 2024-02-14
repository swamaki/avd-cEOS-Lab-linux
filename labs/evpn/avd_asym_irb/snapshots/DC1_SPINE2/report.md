# DC1_SPINE2 Commands Output

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
Ma0                            up             up
```
## show ip interface brief

```
Address
Interface       IP Address           Status     Protocol         MTU    Owner  
--------------- -------------------- ---------- ------------- --------- -------
Management0     172.100.100.3/24     up         up              1500
```
## show lldp neighbors

```
Last table change time   : 0:06:30 ago
Number of table inserts  : 13
Number of table deletes  : 0
Number of table drops    : 0
Number of table age-outs : 0

Port          Neighbor Device ID       Neighbor Port ID    TTL
---------- ------------------------ ---------------------- ---
Et1           leaf1a                   Ethernet2           120
Et2           leaf1b                   Ethernet2           120
Et3           leaf2a                   Ethernet2           120
Et4           leaf2b                   Ethernet2           120
Ma0           client2                  0242.ac64.6409      120
Ma0           client4                  0242.ac64.640b      120
Ma0           client1                  0242.ac64.6408      120
Ma0           client3                  0242.ac64.640a      120
Ma0           leaf2b                   Management0         120
Ma0           leaf1a                   Management0         120
Ma0           spine1                   Management0         120
Ma0           leaf1b                   Management0         120
Ma0           leaf2a                   Management0         120
```
## show running-config

```
! Command: show running-config
! device: spine2 (cEOSLab, EOS-4.30.5M-35156751.4305M (engineering build))
!
no aaa root
!
username admin privilege 15 role network-admin secret sha512 $6$qPcg9KPcBGsLVy4B$HDvjyp0lZyR5cdgM4LH737H3hv32/qXWGS1QMEkyoXJjBJGnw.brpgRV6WuRejXW1ujYbTcaOh1k8Co6glEer0
!
transceiver qsfp default-mode 4x10G
!
service routing protocols model multi-agent
!
hostname spine2
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
interface Management0
   description oob_management
   vrf MGMT
   ip address 172.100.100.3/24
   ipv6 address 2001:172:100:100::5/80
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
Serial number: 10B699E89D8FF3D469CD29B16E0DA7B3
Hardware MAC address: 001c.73ad.1d08
System MAC address: 001c.73ad.1d08

Software image version: 4.30.5M-35156751.4305M (engineering build)
Architecture: i686
Internal build version: 4.30.5M-35156751.4305M
Internal build ID: 10f74693-bb17-4752-b2b8-a0cd835c8624
Image format version: 1.0
Image optimization: None

cEOS tools version: (unknown)
Kernel version: 6.2.0-39-generic

Uptime: 9 minutes
Total memory: 63882152 kB
Free memory: 54488264 kB
```
