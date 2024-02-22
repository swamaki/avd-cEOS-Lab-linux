# DC1_FABRIC

## Table of Contents

- [Fabric Switches and Management IP](#fabric-switches-and-management-ip)
  - [Fabric Switches with inband Management IP](#fabric-switches-with-inband-management-ip)
- [Fabric Topology](#fabric-topology)
- [Fabric IP Allocation](#fabric-ip-allocation)
  - [Fabric Point-To-Point Links](#fabric-point-to-point-links)
  - [Point-To-Point Links Node Allocation](#point-to-point-links-node-allocation)
  - [Loopback Interfaces (BGP EVPN Peering)](#loopback-interfaces-bgp-evpn-peering)
  - [Loopback0 Interfaces Node Allocation](#loopback0-interfaces-node-allocation)
  - [VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)](#vtep-loopback-vxlan-tunnel-source-interfaces-vteps-only)
  - [VTEP Loopback Node allocation](#vtep-loopback-node-allocation)

## Fabric Switches and Management IP

| POD | Type | Node | Management IP | Platform | Provisioned in CloudVision | Serial Number |
| --- | ---- | ---- | ------------- | -------- | -------------------------- | ------------- |
| DC1_FABRIC | leaf | LEAF1A | 172.16.2.101/24 | cEOS-lab | Provisioned | - |
| DC1_FABRIC | leaf | LEAF1B | 172.16.2.102/24 | cEOS-lab | Provisioned | - |
| DC1_FABRIC | leaf | LEAF2A | 172.16.2.103/24 | 720XP | Provisioned | - |
| DC1_FABRIC | leaf | LEAF3A | 172.16.2.104/24 | cEOS-lab | Provisioned | - |
| DC1_FABRIC | leaf | LEAF3B | 172.16.2.105/24 | cEOS-lab | Provisioned | - |
| DC1_FABRIC | leaf | LEAF3C | 172.16.2.106/24 | cEOS-lab | Provisioned | - |
| DC1_FABRIC | leaf | LEAF3D | 172.16.2.107/24 | cEOS-lab | Provisioned | - |
| DC1_FABRIC | leaf | LEAF3E | 172.16.2.108/24 | cEOS-lab | Provisioned | - |
| DC1_FABRIC | l3spine | SPINE1 | 172.16.2.11/24 | vEOS-lab | Provisioned | - |
| DC1_FABRIC | l3spine | SPINE2 | 172.16.2.12/24 | vEOS-lab | Provisioned | - |

> Provision status is based on Ansible inventory declaration and do not represent real status from CloudVision.

### Fabric Switches with inband Management IP

| POD | Type | Node | Management IP | Inband Interface |
| --- | ---- | ---- | ------------- | ---------------- |
| DC1_FABRIC | leaf | LEAF1A | 10.10.10.6/24 | Vlan10 |
| DC1_FABRIC | leaf | LEAF1B | 10.10.10.7/24 | Vlan10 |
| DC1_FABRIC | leaf | LEAF2A | 10.10.10.8/24 | Vlan10 |
| DC1_FABRIC | leaf | LEAF3A | 10.10.10.9/24 | Vlan10 |
| DC1_FABRIC | leaf | LEAF3B | 10.10.10.10/24 | Vlan10 |
| DC1_FABRIC | leaf | LEAF3C | 10.10.10.11/24 | Vlan10 |
| DC1_FABRIC | leaf | LEAF3D | 10.10.10.12/24 | Vlan10 |
| DC1_FABRIC | leaf | LEAF3E | 10.10.10.13/24 | Vlan10 |

## Fabric Topology

| Type | Node | Node Interface | Peer Type | Peer Node | Peer Interface |
| ---- | ---- | -------------- | --------- | ----------| -------------- |
| leaf | LEAF1A | Ethernet1 | l3spine | SPINE1 | Ethernet1 |
| leaf | LEAF1A | Ethernet23 | mlag_peer | LEAF1B | Ethernet23 |
| leaf | LEAF1A | Ethernet24 | mlag_peer | LEAF1B | Ethernet24 |
| leaf | LEAF1B | Ethernet1 | l3spine | SPINE2 | Ethernet1 |
| leaf | LEAF2A | Ethernet1 | l3spine | SPINE1 | Ethernet2 |
| leaf | LEAF2A | Ethernet2 | l3spine | SPINE2 | Ethernet2 |
| leaf | LEAF3A | Ethernet1 | l3spine | SPINE1 | Ethernet3 |
| leaf | LEAF3A | Ethernet2 | l3spine | SPINE2 | Ethernet3 |
| leaf | LEAF3A | Ethernet3 | leaf | LEAF3C | Ethernet1 |
| leaf | LEAF3A | Ethernet4 | leaf | LEAF3D | Ethernet1 |
| leaf | LEAF3A | Ethernet5 | leaf | LEAF3E | Ethernet1 |
| leaf | LEAF3A | Ethernet23 | mlag_peer | LEAF3B | Ethernet23 |
| leaf | LEAF3A | Ethernet24 | mlag_peer | LEAF3B | Ethernet24 |
| leaf | LEAF3B | Ethernet1 | l3spine | SPINE1 | Ethernet4 |
| leaf | LEAF3B | Ethernet2 | l3spine | SPINE2 | Ethernet4 |
| leaf | LEAF3B | Ethernet3 | leaf | LEAF3C | Ethernet2 |
| leaf | LEAF3B | Ethernet4 | leaf | LEAF3D | Ethernet2 |
| leaf | LEAF3B | Ethernet5 | leaf | LEAF3E | Ethernet2 |
| l3spine | SPINE1 | Ethernet23 | mlag_peer | SPINE2 | Ethernet23 |
| l3spine | SPINE1 | Ethernet24 | mlag_peer | SPINE2 | Ethernet24 |

## Fabric IP Allocation

### Fabric Point-To-Point Links

| Uplink IPv4 Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ---------------- | ------------------- | ------------------ | ------------------ |

### Point-To-Point Links Node Allocation

| Node | Node Interface | Node IP Address | Peer Node | Peer Interface | Peer IP Address |
| ---- | -------------- | --------------- | --------- | -------------- | --------------- |

### Loopback Interfaces (BGP EVPN Peering)

| Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------- | ------------------- | ------------------ | ------------------ |
| 172.26.26.0/24 | 256 | 2 | 0.79 % |

### Loopback0 Interfaces Node Allocation

| POD | Node | Loopback0 |
| --- | ---- | --------- |
| DC1_FABRIC | SPINE1 | 172.26.26.1/32 |
| DC1_FABRIC | SPINE2 | 172.26.26.2/32 |

### VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)

| VTEP Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| --------------------- | ------------------- | ------------------ | ------------------ |

### VTEP Loopback Node allocation

| POD | Node | Loopback1 |
| --- | ---- | --------- |
