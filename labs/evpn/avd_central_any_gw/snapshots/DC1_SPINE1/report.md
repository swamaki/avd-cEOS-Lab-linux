# DC1_SPINE1 Commands Output

## Table of Contents

- [show lldp neighbors](#show-lldp-neighbors)
- [show ip interface brief](#show-ip-interface-brief)
- [show interfaces description](#show-interfaces-description)
- [show version](#show-version)
- [show running-config](#show-running-config)
## show interfaces description

```
Interface                      Status         Protocol           Description
Et1                            up             up                 P2P_LINK_TO_DC1_LEAF1A_Ethernet1
Et2                            up             up                 P2P_LINK_TO_DC1_LEAF1B_Ethernet1
Et3                            up             up                 P2P_LINK_TO_DC1_LEAF2A_Ethernet1
Et4                            up             up                 P2P_LINK_TO_DC1_SVC1A_Ethernet1
Et5                            up             up                 P2P_LINK_TO_DC1_SVC1B_Ethernet1
Lo0                            up             up                 EVPN_Overlay_Peering
Ma0                            up             up                 oob_management
```
## show ip interface brief

```
Address
Interface       IP Address           Status     Protocol         MTU    Owner  
--------------- -------------------- ---------- ------------ ---------- -------
Ethernet1       172.31.255.0/31      up         up              9214           
Ethernet2       172.31.255.4/31      up         up              9214           
Ethernet3       172.31.255.8/31      up         up              9214           
Ethernet4       172.31.255.12/31     up         up              9214           
Ethernet5       172.31.255.16/31     up         up              9214           
Loopback0       192.168.255.1/32     up         up             65535           
Management0     172.100.100.2/24     up         up              1500
```
## show lldp neighbors

```
Last table change time   : 0:15:33 ago
Number of table inserts  : 15
Number of table deletes  : 0
Number of table drops    : 0
Number of table age-outs : 0

Port          Neighbor Device ID       Neighbor Port ID    TTL
---------- ------------------------ ---------------------- ---
Et1           DC1_LEAF1A               Ethernet1           120
Et2           leaf1b                   Ethernet1           120
Et3           DC1_LEAF2A               Ethernet1           120
Et4           DC1_SVC1A                Ethernet1           120
Et5           DC1_SVC1B                Ethernet1           120
Ma0           client2                  0242.ac64.640a      120
Ma0           client4                  0242.ac64.640c      120
Ma0           client1                  0242.ac64.6409      120
Ma0           leaf1b                   Management0         120
Ma0           DC1_SVC1A                Management0         120
Ma0           client3                  0242.ac64.640b      120
Ma0           DC1_LEAF2A               Management0         120
Ma0           DC1_SVC1B                Management0         120
Ma0           DC1_LEAF1A               Management0         120
Ma0           DC1_SPINE2               Management0         120
```
## show running-config

```
! Command: show running-config
! device: DC1-SPINE1 (cEOSLab, EOS-4.30.5M-35156751.4305M (engineering build))
!
no aaa root
!
username admin privilege 15 role network-admin secret sha512 $6$7GTxsrRjnwheeKfR$zhJ8qycVjAJz41rf5JRSfWIzp93IL5WL7sMS/Taz1yfShz.MAnoajCf7R2n1/EZW7PN5QA3Huayl0lVQesBYN1
!
vlan internal order ascending range 1006 1199
!
transceiver qsfp default-mode 4x10G
!
service routing protocols model multi-agent
!
hostname DC1_SPINE1
ip name-server vrf MGMT 1.1.1.1
ip name-server vrf MGMT 8.8.8.8
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
   description P2P_LINK_TO_DC1_LEAF1A_Ethernet1
   mtu 9214
   no switchport
   ip address 172.31.255.0/31
!
interface Ethernet2
   description P2P_LINK_TO_DC1_LEAF1B_Ethernet1
   mtu 9214
   no switchport
   ip address 172.31.255.4/31
!
interface Ethernet3
   description P2P_LINK_TO_DC1_LEAF2A_Ethernet1
   mtu 9214
   no switchport
   ip address 172.31.255.8/31
!
interface Ethernet4
   description P2P_LINK_TO_DC1_SVC1A_Ethernet1
   mtu 9214
   no switchport
   ip address 172.31.255.12/31
!
interface Ethernet5
   description P2P_LINK_TO_DC1_SVC1B_Ethernet1
   mtu 9214
   no switchport
   ip address 172.31.255.16/31
!
interface Loopback0
   description EVPN_Overlay_Peering
   ip address 192.168.255.1/32
!
interface Management0
   description oob_management
   vrf MGMT
   ip address 172.100.100.2/24
!
ip routing
no ip routing vrf MGMT
!
ip prefix-list PL-LOOPBACKS-EVPN-OVERLAY
   seq 10 permit 192.168.255.0/24 eq 32
!
ip route vrf MGMT 0.0.0.0/0 172.100.100.1
!
ntp server vrf MGMT time.google.com prefer iburst
!
route-map RM-CONN-2-BGP permit 10
   match ip address prefix-list PL-LOOPBACKS-EVPN-OVERLAY
!
router bfd
   multihop interval 300 min-rx 300 multiplier 3
!
router bgp 65001
   router-id 192.168.255.1
   no bgp default ipv4-unicast
   distance bgp 20 200 200
   maximum-paths 4 ecmp 4
   neighbor EVPN-OVERLAY-PEERS peer group
   neighbor EVPN-OVERLAY-PEERS next-hop-unchanged
   neighbor EVPN-OVERLAY-PEERS update-source Loopback0
   neighbor EVPN-OVERLAY-PEERS bfd
   neighbor EVPN-OVERLAY-PEERS ebgp-multihop 3
   neighbor EVPN-OVERLAY-PEERS password 7 q+VNViP5i4rVjW1cxFv2wA==
   neighbor EVPN-OVERLAY-PEERS send-community
   neighbor EVPN-OVERLAY-PEERS maximum-routes 0
   neighbor IPv4-UNDERLAY-PEERS peer group
   neighbor IPv4-UNDERLAY-PEERS password 7 AQQvKeimxJu+uGQ/yYvv9w==
   neighbor IPv4-UNDERLAY-PEERS send-community
   neighbor IPv4-UNDERLAY-PEERS maximum-routes 12000
   neighbor 172.31.255.1 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.31.255.1 remote-as 65101
   neighbor 172.31.255.1 description DC1_LEAF1A_Ethernet1
   neighbor 172.31.255.5 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.31.255.5 remote-as 65101
   neighbor 172.31.255.5 description DC1_LEAF1B_Ethernet1
   neighbor 172.31.255.9 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.31.255.9 remote-as 65102
   neighbor 172.31.255.9 description DC1_LEAF2A_Ethernet1
   neighbor 172.31.255.13 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.31.255.13 remote-as 65103
   neighbor 172.31.255.13 description DC1_SVC1A_Ethernet1
   neighbor 172.31.255.17 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.31.255.17 remote-as 65103
   neighbor 172.31.255.17 description DC1_SVC1B_Ethernet1
   neighbor 192.168.255.3 peer group EVPN-OVERLAY-PEERS
   neighbor 192.168.255.3 remote-as 65101
   neighbor 192.168.255.3 description DC1_LEAF1A
   neighbor 192.168.255.4 peer group EVPN-OVERLAY-PEERS
   neighbor 192.168.255.4 remote-as 65101
   neighbor 192.168.255.4 description DC1_LEAF1B
   neighbor 192.168.255.5 peer group EVPN-OVERLAY-PEERS
   neighbor 192.168.255.5 remote-as 65102
   neighbor 192.168.255.5 description DC1_LEAF2A
   neighbor 192.168.255.6 peer group EVPN-OVERLAY-PEERS
   neighbor 192.168.255.6 remote-as 65103
   neighbor 192.168.255.6 description DC1_SVC1A
   neighbor 192.168.255.7 peer group EVPN-OVERLAY-PEERS
   neighbor 192.168.255.7 remote-as 65103
   neighbor 192.168.255.7 description DC1_SVC1B
   redistribute connected route-map RM-CONN-2-BGP
   !
   address-family evpn
      neighbor EVPN-OVERLAY-PEERS activate
   !
   address-family ipv4
      no neighbor EVPN-OVERLAY-PEERS activate
      neighbor IPv4-UNDERLAY-PEERS activate
!
end
```
## show version

```
Arista cEOSLab
Hardware version: 
Serial number: BC41FC9A71CD93BC069912BF5C4EDBD4
Hardware MAC address: 001c.73fa.6e81
System MAC address: 001c.73fa.6e81

Software image version: 4.30.5M-35156751.4305M (engineering build)
Architecture: i686
Internal build version: 4.30.5M-35156751.4305M
Internal build ID: 10f74693-bb17-4752-b2b8-a0cd835c8624
Image format version: 1.0
Image optimization: None

cEOS tools version: (unknown)
Kernel version: 6.2.0-39-generic

Uptime: 36 minutes
Total memory: 63882152 kB
Free memory: 27953160 kB
```
