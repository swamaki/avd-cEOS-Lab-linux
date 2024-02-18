# DC1_L2_LEAF2A Commands Output

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
Management0     172.100.100.8/24     up         up              1500
```
## show lldp neighbors

```
Last table change time   : 0:05:53 ago
Number of table inserts  : 18
Number of table deletes  : 1
Number of table drops    : 0
Number of table age-outs : 1

Port          Neighbor Device ID       Neighbor Port ID    TTL
---------- ------------------------ ---------------------- ---
Et1           svc2a                    Ethernet5           120
Et2           svc2b                    Ethernet5           120
Et3           l2leaf2b                 Ethernet3           120
Et4           l2leaf2b                 Ethernet4           120
Et5           client3                  aac1.ab8e.cbbe      120
Et6           client4                  aac1.abdc.57cf      120
Ma0           client4                  0242.ac64.640d      120
Ma0           client1                  0242.ac64.640a      120
Ma0           client3                  0242.ac64.640c      120
Ma0           client2                  0242.ac64.640b      120
Ma0           spine1                   Management0         120
Ma0           l2leaf2b                 Management0         120
Ma0           leaf1b                   Management0         120
Ma0           spine2                   Management0         120
Ma0           svc2b                    Management0         120
Ma0           svc2a                    Management0         120
Ma0           leaf1a                   Management0         120
```
## show running-config

```
! Command: show running-config
! device: l2leaf2a (cEOSLab, EOS-4.30.5M-35156751.4305M (engineering build))
!
no aaa root
!
username admin privilege 15 role network-admin secret sha512 $6$s.SN.ir/h3DtZbCg$TTdlyzZgCmYmxtBP1mBN/IWG7griF2zcDlRUi1eIQcrxhdLYART7ke9h//TCc8CXAP/6H.CKftbcrFw/EZ9nM.
!
transceiver qsfp default-mode 4x10G
!
service routing protocols model multi-agent
!
hostname l2leaf2a
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
   ip address 172.100.100.8/24
   ipv6 address 2001:172:100:100::b/80
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
Serial number: D320A98C90903F69E935248A30BD4C6D
Hardware MAC address: 001c.73f8.4183
System MAC address: 001c.73f8.4183

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
Free memory: 25230208 kB
```
