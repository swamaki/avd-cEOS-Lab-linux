# DC1_LEAF1A Commands Output

## Table of Contents

- [show lldp neighbors](#show-lldp-neighbors)
- [show ip interface brief](#show-ip-interface-brief)
- [show interfaces description](#show-interfaces-description)
- [show version](#show-version)
- [show running-config](#show-running-config)
## show interfaces description

```
Interface                      Status         Protocol           Description
Et1                            up             up                 P2P_LINK_TO_DC1_SPINE1_Ethernet1
Et2                            up             up                 P2P_LINK_TO_DC1_SPINE2_Ethernet1
Et3                            up             up                 MLAG_PEER_DC1_LEAF1B_Ethernet3
Et4                            up             up                 MLAG_PEER_DC1_LEAF1B_Ethernet4
Et5                            up             up                 server01_Eth1
Et6                            up             up                 server02_Eth1
Lo0                            up             up                 EVPN_Overlay_Peering
Lo1                            up             up                 VTEP_VXLAN_Tunnel_Source
Ma0                            up             up                 oob_management
Po3                            down           lowerlayerdown     MLAG_PEER_DC1_LEAF1B_Po3
Po5                            up             up                 server01_PortChannel5
Po6                            up             up                 server02_PortChannel6
Vl4093                         down           lowerlayerdown     MLAG_PEER_L3_PEERING
Vl4094                         up             up                 MLAG_PEER
Vx1                            up             up                 DC1_LEAF1A_VTEP
```
## show ip interface brief

```
Address
Interface      IP Address          Status    Protocol             MTU   Owner  
-------------- ------------------- --------- ----------------- -------- -------
Ethernet1      172.31.255.1/31     up        up                  9214          
Ethernet2      172.31.255.3/31     up        up                  9214          
Loopback0      192.168.255.3/32    up        up                 65535          
Loopback1      192.168.254.3/32    up        up                 65535          
Management0    172.100.100.4/24    up        up                  1500          
Vlan4093       10.255.251.0/31     down      lowerlayerdown      9214          
Vlan4094       10.255.252.0/31     up        up                  9214
```
## show lldp neighbors

```
Last table change time   : 0:15:33 ago
Number of table inserts  : 16
Number of table deletes  : 0
Number of table drops    : 0
Number of table age-outs : 0

Port          Neighbor Device ID       Neighbor Port ID    TTL
---------- ------------------------ ---------------------- ---
Et1           DC1_SPINE1               Ethernet1           120
Et2           DC1_SPINE2               Ethernet1           120
Et3           leaf1b                   Ethernet3           120
Et4           leaf1b                   Ethernet4           120
Et5           client1                  aac1.abbf.ab06      120
Et6           client2                  aac1.ab12.d1c3      120
Ma0           client3                  0242.ac64.640b      120
Ma0           client2                  0242.ac64.640a      120
Ma0           client4                  0242.ac64.640c      120
Ma0           client1                  0242.ac64.6409      120
Ma0           leaf1b                   Management0         120
Ma0           DC1_SVC1A                Management0         120
Ma0           DC1_SVC1B                Management0         120
Ma0           DC1_LEAF2A               Management0         120
Ma0           DC1_SPINE1               Management0         120
Ma0           DC1_SPINE2               Management0         120
```
## show running-config

```
! Command: show running-config
! device: DC1-LEAF1A (cEOSLab, EOS-4.30.5M-35156751.4305M (engineering build))
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
hostname DC1_LEAF1A
ip name-server vrf MGMT 1.1.1.1
ip name-server vrf MGMT 8.8.8.8
!
spanning-tree mode mstp
no spanning-tree vlan-id 4093-4094
spanning-tree mst 0 priority 4096
!
system l1
   unsupported speed action error
   unsupported error-correction action error
!
vlan 110
   name Tenant_A_OP_Zone_1
!
vlan 111
   name Tenant_A_OP_Zone_2
!
vlan 4093
   name LEAF_PEER_L3
   trunk group LEAF_PEER_L3
!
vlan 4094
   name MLAG_PEER
   trunk group MLAG
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
interface Port-Channel3
   description MLAG_PEER_DC1_LEAF1B_Po3
   switchport mode trunk
   switchport trunk group LEAF_PEER_L3
   switchport trunk group MLAG
!
interface Port-Channel5
   description server01_PortChannel5
   switchport trunk allowed vlan 110
   switchport mode trunk
   mlag 5
   spanning-tree portfast
!
interface Port-Channel6
   description server02_PortChannel6
   switchport trunk allowed vlan 111
   switchport mode trunk
   mlag 6
   spanning-tree portfast
!
interface Ethernet1
   description P2P_LINK_TO_DC1_SPINE1_Ethernet1
   mtu 9214
   no switchport
   ip address 172.31.255.1/31
!
interface Ethernet2
   description P2P_LINK_TO_DC1_SPINE2_Ethernet1
   mtu 9214
   no switchport
   ip address 172.31.255.3/31
!
interface Ethernet3
   description MLAG_PEER_DC1_LEAF1B_Ethernet3
   channel-group 3 mode active
!
interface Ethernet4
   description MLAG_PEER_DC1_LEAF1B_Ethernet4
   channel-group 3 mode active
!
interface Ethernet5
   description server01_Eth1
   channel-group 5 mode active
!
interface Ethernet6
   description server02_Eth1
   channel-group 6 mode active
!
interface Loopback0
   description EVPN_Overlay_Peering
   ip address 192.168.255.3/32
!
interface Loopback1
   description VTEP_VXLAN_Tunnel_Source
   ip address 192.168.254.3/32
!
interface Management0
   description oob_management
   vrf MGMT
   ip address 172.100.100.4/24
!
interface Vlan4093
   description MLAG_PEER_L3_PEERING
   mtu 9214
   ip address 10.255.251.0/31
!
interface Vlan4094
   description MLAG_PEER
   mtu 9214
   no autostate
   ip address 10.255.252.0/31
!
interface Vxlan1
   description DC1_LEAF1A_VTEP
   vxlan source-interface Loopback1
   vxlan udp-port 4789
   vxlan vlan 110 vni 10110
   vxlan vlan 111 vni 10111
!
ip routing
no ip routing vrf MGMT
!
ip prefix-list PL-LOOPBACKS-EVPN-OVERLAY
   seq 10 permit 192.168.255.0/24 eq 32
   seq 20 permit 192.168.254.0/24 eq 32
!
mlag configuration
   domain-id DC1_LEAF1
   local-interface Vlan4094
   peer-address 10.255.252.1
   peer-link Port-Channel3
   reload-delay mlag 300
   reload-delay non-mlag 330
!
ip route vrf MGMT 0.0.0.0/0 172.100.100.1
!
ntp server vrf MGMT time.google.com prefer iburst
!
route-map RM-CONN-2-BGP permit 10
   match ip address prefix-list PL-LOOPBACKS-EVPN-OVERLAY
!
route-map RM-MLAG-PEER-IN permit 10
   description Make routes learned over MLAG Peer-link less preferred on spines to ensure optimal routing
   set origin incomplete
!
router bfd
   multihop interval 300 min-rx 300 multiplier 3
!
router bgp 65101
   router-id 192.168.255.3
   no bgp default ipv4-unicast
   distance bgp 20 200 200
   maximum-paths 4 ecmp 4
   neighbor EVPN-OVERLAY-PEERS peer group
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
   neighbor MLAG-IPv4-UNDERLAY-PEER peer group
   neighbor MLAG-IPv4-UNDERLAY-PEER remote-as 65101
   neighbor MLAG-IPv4-UNDERLAY-PEER next-hop-self
   neighbor MLAG-IPv4-UNDERLAY-PEER description DC1_LEAF1B
   neighbor MLAG-IPv4-UNDERLAY-PEER route-map RM-MLAG-PEER-IN in
   neighbor MLAG-IPv4-UNDERLAY-PEER password 7 vnEaG8gMeQf3d3cN6PktXQ==
   neighbor MLAG-IPv4-UNDERLAY-PEER send-community
   neighbor MLAG-IPv4-UNDERLAY-PEER maximum-routes 12000
   neighbor 10.255.251.1 peer group MLAG-IPv4-UNDERLAY-PEER
   neighbor 10.255.251.1 description DC1_LEAF1B
   neighbor 172.31.255.0 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.31.255.0 remote-as 65001
   neighbor 172.31.255.0 description DC1_SPINE1_Ethernet1
   neighbor 172.31.255.2 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.31.255.2 remote-as 65001
   neighbor 172.31.255.2 description DC1_SPINE2_Ethernet1
   neighbor 192.168.255.1 peer group EVPN-OVERLAY-PEERS
   neighbor 192.168.255.1 remote-as 65001
   neighbor 192.168.255.1 description DC1_SPINE1
   neighbor 192.168.255.2 peer group EVPN-OVERLAY-PEERS
   neighbor 192.168.255.2 remote-as 65001
   neighbor 192.168.255.2 description DC1_SPINE2
   redistribute connected route-map RM-CONN-2-BGP
   !
   vlan 110
      rd 192.168.255.3:10110
      route-target both 10110:10110
      redistribute learned
   !
   vlan 111
      rd 192.168.255.3:10111
      route-target both 10111:10111
      redistribute learned
   !
   address-family evpn
      neighbor EVPN-OVERLAY-PEERS activate
   !
   address-family ipv4
      no neighbor EVPN-OVERLAY-PEERS activate
      neighbor IPv4-UNDERLAY-PEERS activate
      neighbor MLAG-IPv4-UNDERLAY-PEER activate
!
end
```
## show version

```
Arista cEOSLab
Hardware version: 
Serial number: 76DA4B62E8D5C46C4785E01484073CD3
Hardware MAC address: 001c.7345.f94c
System MAC address: 001c.7345.f94c

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
Free memory: 27993136 kB
```