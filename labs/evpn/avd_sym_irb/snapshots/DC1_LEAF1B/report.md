# DC1_LEAF1B Commands Output

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
Management0     172.100.100.5/24     up         up              1500
```
## show lldp neighbors

```
Last table change time   : 0:05:57 ago
Number of table inserts  : 18
Number of table deletes  : 1
Number of table drops    : 0
Number of table age-outs : 1

Port          Neighbor Device ID       Neighbor Port ID    TTL
---------- ------------------------ ---------------------- ---
Et1           spine1                   Ethernet2           120
Et2           spine2                   Ethernet2           120
Et3           leaf1a                   Ethernet3           120
Et4           leaf1a                   Ethernet4           120
Et5           client1                  aac1.ab6c.9b5e      120
Et6           client2                  aac1.ab41.9f33      120
Ma0           client3                  0242.ac64.640c      120
Ma0           client1                  0242.ac64.640a      120
Ma0           client4                  0242.ac64.640d      120
Ma0           client2                  0242.ac64.640b      120
Ma0           l2leaf2b                 Management0         120
Ma0           spine1                   Management0         120
Ma0           l2leaf2a                 Management0         120
Ma0           spine2                   Management0         120
Ma0           svc2b                    Management0         120
Ma0           svc2a                    Management0         120
Ma0           leaf1a                   Management0         120
```
## show running-config

```
! Command: show running-config
! device: leaf1b (cEOSLab, EOS-4.30.5M-35156751.4305M (engineering build))
!
no aaa root
!
username admin privilege 15 role network-admin secret sha512 $6$82o4jK2SSBMidodE$5vjUsoIChwTFjUmeymWJsltf24lzUJ7VCbHzBr4jW4KEzhFIrQ1YdIv9glRBrwBLZncI1aqx/rpH1gcwKWbw7.
!
transceiver qsfp default-mode 4x10G
!
service routing protocols model multi-agent
!
hostname leaf1b
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
   ip address 172.100.100.5/24
   ipv6 address 2001:172:100:100::8/80
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
Serial number: 0466101459A7A5B66B8225EF03319AC2
Hardware MAC address: 001c.7329.426d
System MAC address: 001c.7329.426d

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
Free memory: 25221300 kB
```
