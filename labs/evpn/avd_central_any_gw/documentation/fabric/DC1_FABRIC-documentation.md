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
| DC1_FABRIC | l3leaf | DC1_LEAF1A | 172.100.100.4/24 | cEOS-LAB | Provisioned | - |
| DC1_FABRIC | l3leaf | DC1_LEAF1B | 172.100.100.5/24 | cEOS-LAB | Provisioned | - |
| DC1_FABRIC | l3leaf | DC1_LEAF2A | 172.100.100.6/24 | cEOS-LAB | Provisioned | - |
| DC1_FABRIC | spine | DC1_SPINE1 | 172.100.100.2/24 | cEOS-LAB | Provisioned | - |
| DC1_FABRIC | spine | DC1_SPINE2 | 172.100.100.3/24 | cEOS-LAB | Provisioned | - |
| DC1_FABRIC | l3leaf | DC1_SVC1A | 172.100.100.7/24 | cEOS-LAB | Provisioned | - |
| DC1_FABRIC | l3leaf | DC1_SVC1B | 172.100.100.8/24 | cEOS-LAB | Provisioned | - |

> Provision status is based on Ansible inventory declaration and do not represent real status from CloudVision.

### Fabric Switches with inband Management IP

| POD | Type | Node | Management IP | Inband Interface |
| --- | ---- | ---- | ------------- | ---------------- |

## Fabric Topology

| Type | Node | Node Interface | Peer Type | Peer Node | Peer Interface |
| ---- | ---- | -------------- | --------- | ----------| -------------- |
| l3leaf | DC1_LEAF1A | Ethernet1 | spine | DC1_SPINE1 | Ethernet1 |
| l3leaf | DC1_LEAF1A | Ethernet2 | spine | DC1_SPINE2 | Ethernet1 |
| l3leaf | DC1_LEAF1A | Ethernet3 | mlag_peer | DC1_LEAF1B | Ethernet3 |
| l3leaf | DC1_LEAF1A | Ethernet4 | mlag_peer | DC1_LEAF1B | Ethernet4 |
| l3leaf | DC1_LEAF1B | Ethernet1 | spine | DC1_SPINE1 | Ethernet2 |
| l3leaf | DC1_LEAF1B | Ethernet2 | spine | DC1_SPINE2 | Ethernet2 |
| l3leaf | DC1_LEAF2A | Ethernet1 | spine | DC1_SPINE1 | Ethernet3 |
| l3leaf | DC1_LEAF2A | Ethernet2 | spine | DC1_SPINE2 | Ethernet3 |
| spine | DC1_SPINE1 | Ethernet4 | l3leaf | DC1_SVC1A | Ethernet1 |
| spine | DC1_SPINE1 | Ethernet5 | l3leaf | DC1_SVC1B | Ethernet1 |
| spine | DC1_SPINE2 | Ethernet4 | l3leaf | DC1_SVC1A | Ethernet2 |
| spine | DC1_SPINE2 | Ethernet5 | l3leaf | DC1_SVC1B | Ethernet2 |
| l3leaf | DC1_SVC1A | Ethernet3 | mlag_peer | DC1_SVC1B | Ethernet3 |
| l3leaf | DC1_SVC1A | Ethernet4 | mlag_peer | DC1_SVC1B | Ethernet4 |

## Fabric IP Allocation

### Fabric Point-To-Point Links

| Uplink IPv4 Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ---------------- | ------------------- | ------------------ | ------------------ |
| 172.31.255.0/24 | 256 | 20 | 7.82 % |

### Point-To-Point Links Node Allocation

| Node | Node Interface | Node IP Address | Peer Node | Peer Interface | Peer IP Address |
| ---- | -------------- | --------------- | --------- | -------------- | --------------- |
| DC1_LEAF1A | Ethernet1 | 172.31.255.1/31 | DC1_SPINE1 | Ethernet1 | 172.31.255.0/31 |
| DC1_LEAF1A | Ethernet2 | 172.31.255.3/31 | DC1_SPINE2 | Ethernet1 | 172.31.255.2/31 |
| DC1_LEAF1B | Ethernet1 | 172.31.255.5/31 | DC1_SPINE1 | Ethernet2 | 172.31.255.4/31 |
| DC1_LEAF1B | Ethernet2 | 172.31.255.7/31 | DC1_SPINE2 | Ethernet2 | 172.31.255.6/31 |
| DC1_LEAF2A | Ethernet1 | 172.31.255.9/31 | DC1_SPINE1 | Ethernet3 | 172.31.255.8/31 |
| DC1_LEAF2A | Ethernet2 | 172.31.255.11/31 | DC1_SPINE2 | Ethernet3 | 172.31.255.10/31 |
| DC1_SPINE1 | Ethernet4 | 172.31.255.12/31 | DC1_SVC1A | Ethernet1 | 172.31.255.13/31 |
| DC1_SPINE1 | Ethernet5 | 172.31.255.16/31 | DC1_SVC1B | Ethernet1 | 172.31.255.17/31 |
| DC1_SPINE2 | Ethernet4 | 172.31.255.14/31 | DC1_SVC1A | Ethernet2 | 172.31.255.15/31 |
| DC1_SPINE2 | Ethernet5 | 172.31.255.18/31 | DC1_SVC1B | Ethernet2 | 172.31.255.19/31 |

### Loopback Interfaces (BGP EVPN Peering)

| Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------- | ------------------- | ------------------ | ------------------ |
| 192.168.255.0/24 | 256 | 7 | 2.74 % |

### Loopback0 Interfaces Node Allocation

| POD | Node | Loopback0 |
| --- | ---- | --------- |
| DC1_FABRIC | DC1_LEAF1A | 192.168.255.3/32 |
| DC1_FABRIC | DC1_LEAF1B | 192.168.255.4/32 |
| DC1_FABRIC | DC1_LEAF2A | 192.168.255.5/32 |
| DC1_FABRIC | DC1_SPINE1 | 192.168.255.1/32 |
| DC1_FABRIC | DC1_SPINE2 | 192.168.255.2/32 |
| DC1_FABRIC | DC1_SVC1A | 192.168.255.6/32 |
| DC1_FABRIC | DC1_SVC1B | 192.168.255.7/32 |

### VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)

| VTEP Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| --------------------- | ------------------- | ------------------ | ------------------ |
| 192.168.254.0/24 | 256 | 5 | 1.96 % |

### VTEP Loopback Node allocation

| POD | Node | Loopback1 |
| --- | ---- | --------- |
| DC1_FABRIC | DC1_LEAF1A | 192.168.254.3/32 |
| DC1_FABRIC | DC1_LEAF1B | 192.168.254.3/32 |
| DC1_FABRIC | DC1_LEAF2A | 192.168.254.5/32 |
| DC1_FABRIC | DC1_SVC1A | 192.168.254.6/32 |
| DC1_FABRIC | DC1_SVC1B | 192.168.254.6/32 |
