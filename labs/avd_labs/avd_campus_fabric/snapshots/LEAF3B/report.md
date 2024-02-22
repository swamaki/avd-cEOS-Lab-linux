# LEAF3B Commands Output

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
Et23                           up             up                 
Et24                           up             up                 
Ma0                            up             up
```
## show ip interface brief

```
Address
Interface       IP Address          Status      Protocol         MTU    Owner  
--------------- ------------------- ----------- ------------- --------- -------
Management0     172.16.2.105/24     up          up              1500
```
## show lldp neighbors

```
Last table change time   : 0:09:16 ago
Number of table inserts  : 17
Number of table deletes  : 0
Number of table drops    : 0
Number of table age-outs : 0

Port          Neighbor Device ID       Neighbor Port ID    TTL
---------- ------------------------ ---------------------- ---
Et1           spine1                   Ethernet4           120
Et2           spine2                   Ethernet4           120
Et3           leaf3c                   Ethernet2           120
Et4           leaf3d                   Ethernet2           120
Et5           leaf3e                   Ethernet2           120
Et23          leaf3a                   Ethernet23          120
Et24          leaf3a                   Ethernet24          120
Ma0           wan_core                 Management0         120
Ma0           leaf2a                   Management0         120
Ma0           leaf3d                   Management0         120
Ma0           leaf3c                   Management0         120
Ma0           leaf1b                   Management0         120
Ma0           leaf1a                   Management0         120
Ma0           spine1                   Management0         120
Ma0           spine2                   Management0         120
Ma0           leaf3a                   Management0         120
Ma0           leaf3e                   Management0         120
```
## show running-config

```
! Command: show running-config
! device: leaf3b (cEOSLab, EOS-4.30.5M-35156751.4305M (engineering build))
!
no aaa root
!
username admin privilege 15 role network-admin nopassword
username ansible privilege 15 role network-admin secret sha512 $6$nFVThdcfj0ARFsTV$lock/CQ/Pwxb4z/ha5qib26TUKKhGCZb1KSMH91nRAN1RGzGjsJxHk/qSzmeWzRY5AsXQ9uKxUnbqM6615Mm.0
!
transceiver qsfp default-mode 4x10G
!
service routing protocols model multi-agent
!
hostname leaf3b
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
interface Ethernet23
!
interface Ethernet24
!
interface Management0
   description oob_management
   vrf MGMT
   ip address 172.16.2.105/24
   ipv6 address 2001:172:16:2::2/80
!
no ip routing
no ip routing vrf MGMT
!
ip route vrf MGMT 0.0.0.0/0 172.16.2.1
!
ipv6 route vrf MGMT ::/0 2001:172:16:2::1
!
end
```
## show version

```
Arista cEOSLab
Hardware version: 
Serial number: 4944A49C00562EC8EEB008DD1A21E3B6
Hardware MAC address: 001c.7382.2c18
System MAC address: 001c.7382.2c18

Software image version: 4.30.5M-35156751.4305M (engineering build)
Architecture: i686
Internal build version: 4.30.5M-35156751.4305M
Internal build ID: 10f74693-bb17-4752-b2b8-a0cd835c8624
Image format version: 1.0
Image optimization: None

cEOS tools version: (unknown)
Kernel version: 6.5.0-18-generic

Uptime: 11 minutes
Total memory: 63881692 kB
Free memory: 51198832 kB
```
