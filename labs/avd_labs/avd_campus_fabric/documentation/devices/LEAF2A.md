# LEAF2A

## Table of Contents

- [Management](#management)
  - [Management Interfaces](#management-interfaces)
  - [IP Name Servers](#ip-name-servers)
  - [NTP](#ntp)
  - [Management API HTTP](#management-api-http)
- [Authentication](#authentication)
  - [Local Users](#local-users)
  - [AAA Authorization](#aaa-authorization)
- [Spanning Tree](#spanning-tree)
  - [Spanning Tree Summary](#spanning-tree-summary)
  - [Spanning Tree Device Configuration](#spanning-tree-device-configuration)
- [Internal VLAN Allocation Policy](#internal-vlan-allocation-policy)
  - [Internal VLAN Allocation Policy Summary](#internal-vlan-allocation-policy-summary)
  - [Internal VLAN Allocation Policy Device Configuration](#internal-vlan-allocation-policy-device-configuration)
- [VLANs](#vlans)
  - [VLANs Summary](#vlans-summary)
  - [VLANs Device Configuration](#vlans-device-configuration)
- [Interfaces](#interfaces)
  - [Ethernet Interfaces](#ethernet-interfaces)
  - [Port-Channel Interfaces](#port-channel-interfaces)
  - [VLAN Interfaces](#vlan-interfaces)
- [Routing](#routing)
  - [Service Routing Protocols Model](#service-routing-protocols-model)
  - [IP Routing](#ip-routing)
  - [IPv6 Routing](#ipv6-routing)
  - [Static Routes](#static-routes)
- [Multicast](#multicast)
  - [IP IGMP Snooping](#ip-igmp-snooping)
- [802.1X Port Security](#8021x-port-security)
  - [802.1X Summary](#8021x-summary)
- [VRF Instances](#vrf-instances)
  - [VRF Instances Summary](#vrf-instances-summary)
  - [VRF Instances Device Configuration](#vrf-instances-device-configuration)

## Management

### Management Interfaces

#### Management Interfaces Summary

##### IPv4

| Management Interface | description | Type | VRF | IP Address | Gateway |
| -------------------- | ----------- | ---- | --- | ---------- | ------- |
| Management0 | oob_management | oob | MGMT | 172.16.2.103/24 | 172.16.2.1 |

##### IPv6

| Management Interface | description | Type | VRF | IPv6 Address | IPv6 Gateway |
| -------------------- | ----------- | ---- | --- | ------------ | ------------ |
| Management0 | oob_management | oob | MGMT | - | - |

#### Management Interfaces Device Configuration

```eos
!
interface Management0
   description oob_management
   no shutdown
   vrf MGMT
   ip address 172.16.2.103/24
```

### IP Name Servers

#### IP Name Servers Summary

| Name Server | VRF | Priority |
| ----------- | --- | -------- |
| 1.1.1.1 | MGMT | - |
| 8.8.8.8 | MGMT | - |

#### IP Name Servers Device Configuration

```eos
ip name-server vrf MGMT 1.1.1.1
ip name-server vrf MGMT 8.8.8.8
```

### NTP

#### NTP Summary

##### NTP Servers

| Server | VRF | Preferred | Burst | iBurst | Version | Min Poll | Max Poll | Local-interface | Key |
| ------ | --- | --------- | ----- | ------ | ------- | -------- | -------- | --------------- | --- |
| time.google.com | MGMT | True | - | True | - | - | - | - | - |

#### NTP Device Configuration

```eos
!
ntp server vrf MGMT time.google.com prefer iburst
```

### Management API HTTP

#### Management API HTTP Summary

| HTTP | HTTPS | Default Services |
| ---- | ----- | ---------------- |
| False | True | - |

#### Management API VRF Access

| VRF Name | IPv4 ACL | IPv6 ACL |
| -------- | -------- | -------- |
| MGMT | - | - |

#### Management API HTTP Device Configuration

```eos
!
management api http-commands
   protocol https
   no shutdown
   !
   vrf MGMT
      no shutdown
```

## Authentication

### Local Users

#### Local Users Summary

| User | Privilege | Role | Disabled | Shell |
| ---- | --------- | ---- | -------- | ----- |
| admin | 15 | network-admin | False | - |
| ansible | 15 | network-admin | False | - |

#### Local Users Device Configuration

```eos
!
username admin privilege 15 role network-admin nopassword
username ansible privilege 15 role network-admin secret sha512 <removed>
```

### AAA Authorization

#### AAA Authorization Summary

| Type | User Stores |
| ---- | ----------- |
| Exec | local |

Authorization for configuration commands is disabled.

#### AAA Authorization Device Configuration

```eos
aaa authorization exec default local
!
```

## Spanning Tree

### Spanning Tree Summary

STP mode: **mstp**

#### MSTP Instance and Priority

| Instance(s) | Priority |
| -------- | -------- |
| 0 | 16384 |

### Spanning Tree Device Configuration

```eos
!
spanning-tree mode mstp
spanning-tree mst 0 priority 16384
```

## Internal VLAN Allocation Policy

### Internal VLAN Allocation Policy Summary

| Policy Allocation | Range Beginning | Range Ending |
| ------------------| --------------- | ------------ |
| ascending | 1006 | 1199 |

### Internal VLAN Allocation Policy Device Configuration

```eos
!
vlan internal order ascending range 1006 1199
```

## VLANs

### VLANs Summary

| VLAN ID | Name | Trunk Groups |
| ------- | ---- | ------------ |
| 10 | INBAND_MGMT | - |
| 210 | IDF2-Data | - |
| 220 | IDF2-Voice | - |
| 230 | IDF2-Guest | - |

### VLANs Device Configuration

```eos
!
vlan 10
   name INBAND_MGMT
!
vlan 210
   name IDF2-Data
!
vlan 220
   name IDF2-Voice
!
vlan 230
   name IDF2-Guest
```

## Interfaces

### Ethernet Interfaces

#### Ethernet Interfaces Summary

##### L2

| Interface | Description | Mode | VLANs | Native VLAN | Trunk Group | Channel-Group |
| --------- | ----------- | ---- | ----- | ----------- | ----------- | ------------- |
| Ethernet1 | SPINE1_Ethernet2 | *trunk | *10,210,220,230 | *- | *- | 1 |
| Ethernet2 | SPINE2_Ethernet2 | *trunk | *10,210,220,230 | *- | *- | 1 |
| Ethernet6 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet7 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet8 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet9 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet10 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet11 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet12 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet13 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet14 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet15 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet16 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet17 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet18 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet19 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet20 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet21 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet22 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |

*Inherited from Port-Channel Interface

##### Phone Interfaces

| Interface | Mode | Native VLAN | Phone VLAN | Phone VLAN Mode |
| --------- | ---- | ----------- | ---------- | --------------- |
| Ethernet6 | trunk phone | 210 | 220 | untagged |
| Ethernet7 | trunk phone | 210 | 220 | untagged |
| Ethernet8 | trunk phone | 210 | 220 | untagged |
| Ethernet9 | trunk phone | 210 | 220 | untagged |
| Ethernet10 | trunk phone | 210 | 220 | untagged |
| Ethernet11 | trunk phone | 210 | 220 | untagged |
| Ethernet12 | trunk phone | 210 | 220 | untagged |
| Ethernet13 | trunk phone | 210 | 220 | untagged |
| Ethernet14 | trunk phone | 210 | 220 | untagged |
| Ethernet15 | trunk phone | 210 | 220 | untagged |
| Ethernet16 | trunk phone | 210 | 220 | untagged |
| Ethernet17 | trunk phone | 210 | 220 | untagged |
| Ethernet18 | trunk phone | 210 | 220 | untagged |
| Ethernet19 | trunk phone | 210 | 220 | untagged |
| Ethernet20 | trunk phone | 210 | 220 | untagged |
| Ethernet21 | trunk phone | 210 | 220 | untagged |
| Ethernet22 | trunk phone | 210 | 220 | untagged |

#### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet1
   description SPINE1_Ethernet2
   no shutdown
   channel-group 1 mode active
!
interface Ethernet2
   description SPINE2_Ethernet2
   no shutdown
   channel-group 1 mode active
!
interface Ethernet6
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
   dot1x reauthentication
   dot1x port-control auto
   dot1x host-mode multi-host authenticated
   dot1x mac based authentication
   dot1x timeout tx-period 3
   dot1x timeout reauth-period server
   dot1x reauthorization request limit 3
   spanning-tree portfast
   spanning-tree bpduguard enable
!
interface Ethernet7
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
   dot1x reauthentication
   dot1x port-control auto
   dot1x host-mode multi-host authenticated
   dot1x mac based authentication
   dot1x timeout tx-period 3
   dot1x timeout reauth-period server
   dot1x reauthorization request limit 3
   spanning-tree portfast
   spanning-tree bpduguard enable
!
interface Ethernet8
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
   dot1x reauthentication
   dot1x port-control auto
   dot1x host-mode multi-host authenticated
   dot1x mac based authentication
   dot1x timeout tx-period 3
   dot1x timeout reauth-period server
   dot1x reauthorization request limit 3
   spanning-tree portfast
   spanning-tree bpduguard enable
!
interface Ethernet9
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
   dot1x reauthentication
   dot1x port-control auto
   dot1x host-mode multi-host authenticated
   dot1x mac based authentication
   dot1x timeout tx-period 3
   dot1x timeout reauth-period server
   dot1x reauthorization request limit 3
   spanning-tree portfast
   spanning-tree bpduguard enable
!
interface Ethernet10
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
   dot1x reauthentication
   dot1x port-control auto
   dot1x host-mode multi-host authenticated
   dot1x mac based authentication
   dot1x timeout tx-period 3
   dot1x timeout reauth-period server
   dot1x reauthorization request limit 3
   spanning-tree portfast
   spanning-tree bpduguard enable
!
interface Ethernet11
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
   dot1x reauthentication
   dot1x port-control auto
   dot1x host-mode multi-host authenticated
   dot1x mac based authentication
   dot1x timeout tx-period 3
   dot1x timeout reauth-period server
   dot1x reauthorization request limit 3
   spanning-tree portfast
   spanning-tree bpduguard enable
!
interface Ethernet12
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
   dot1x reauthentication
   dot1x port-control auto
   dot1x host-mode multi-host authenticated
   dot1x mac based authentication
   dot1x timeout tx-period 3
   dot1x timeout reauth-period server
   dot1x reauthorization request limit 3
   spanning-tree portfast
   spanning-tree bpduguard enable
!
interface Ethernet13
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
   dot1x reauthentication
   dot1x port-control auto
   dot1x host-mode multi-host authenticated
   dot1x mac based authentication
   dot1x timeout tx-period 3
   dot1x timeout reauth-period server
   dot1x reauthorization request limit 3
   spanning-tree portfast
   spanning-tree bpduguard enable
!
interface Ethernet14
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
   dot1x reauthentication
   dot1x port-control auto
   dot1x host-mode multi-host authenticated
   dot1x mac based authentication
   dot1x timeout tx-period 3
   dot1x timeout reauth-period server
   dot1x reauthorization request limit 3
   spanning-tree portfast
   spanning-tree bpduguard enable
!
interface Ethernet15
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
   dot1x reauthentication
   dot1x port-control auto
   dot1x host-mode multi-host authenticated
   dot1x mac based authentication
   dot1x timeout tx-period 3
   dot1x timeout reauth-period server
   dot1x reauthorization request limit 3
   spanning-tree portfast
   spanning-tree bpduguard enable
!
interface Ethernet16
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
   dot1x reauthentication
   dot1x port-control auto
   dot1x host-mode multi-host authenticated
   dot1x mac based authentication
   dot1x timeout tx-period 3
   dot1x timeout reauth-period server
   dot1x reauthorization request limit 3
   spanning-tree portfast
   spanning-tree bpduguard enable
!
interface Ethernet17
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
   dot1x reauthentication
   dot1x port-control auto
   dot1x host-mode multi-host authenticated
   dot1x mac based authentication
   dot1x timeout tx-period 3
   dot1x timeout reauth-period server
   dot1x reauthorization request limit 3
   spanning-tree portfast
   spanning-tree bpduguard enable
!
interface Ethernet18
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
   dot1x reauthentication
   dot1x port-control auto
   dot1x host-mode multi-host authenticated
   dot1x mac based authentication
   dot1x timeout tx-period 3
   dot1x timeout reauth-period server
   dot1x reauthorization request limit 3
   spanning-tree portfast
   spanning-tree bpduguard enable
!
interface Ethernet19
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
   dot1x reauthentication
   dot1x port-control auto
   dot1x host-mode multi-host authenticated
   dot1x mac based authentication
   dot1x timeout tx-period 3
   dot1x timeout reauth-period server
   dot1x reauthorization request limit 3
   spanning-tree portfast
   spanning-tree bpduguard enable
!
interface Ethernet20
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
   dot1x reauthentication
   dot1x port-control auto
   dot1x host-mode multi-host authenticated
   dot1x mac based authentication
   dot1x timeout tx-period 3
   dot1x timeout reauth-period server
   dot1x reauthorization request limit 3
   spanning-tree portfast
   spanning-tree bpduguard enable
!
interface Ethernet21
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
   dot1x reauthentication
   dot1x port-control auto
   dot1x host-mode multi-host authenticated
   dot1x mac based authentication
   dot1x timeout tx-period 3
   dot1x timeout reauth-period server
   dot1x reauthorization request limit 3
   spanning-tree portfast
   spanning-tree bpduguard enable
!
interface Ethernet22
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
   dot1x reauthentication
   dot1x port-control auto
   dot1x host-mode multi-host authenticated
   dot1x mac based authentication
   dot1x timeout tx-period 3
   dot1x timeout reauth-period server
   dot1x reauthorization request limit 3
   spanning-tree portfast
   spanning-tree bpduguard enable
```

### Port-Channel Interfaces

#### Port-Channel Interfaces Summary

##### L2

| Interface | Description | Type | Mode | VLANs | Native VLAN | Trunk Group | LACP Fallback Timeout | LACP Fallback Mode | MLAG ID | EVPN ESI |
| --------- | ----------- | ---- | ---- | ----- | ----------- | ------------| --------------------- | ------------------ | ------- | -------- |
| Port-Channel1 | SPINES_Po2 | switched | trunk | 10,210,220,230 | - | - | - | - | - | - |

#### Port-Channel Interfaces Device Configuration

```eos
!
interface Port-Channel1
   description SPINES_Po2
   no shutdown
   switchport
   switchport trunk allowed vlan 10,210,220,230
   switchport mode trunk
```

### VLAN Interfaces

#### VLAN Interfaces Summary

| Interface | Description | VRF |  MTU | Shutdown |
| --------- | ----------- | --- | ---- | -------- |
| Vlan10 | Inband Management | default | 1500 | False |

##### IPv4

| Interface | VRF | IP Address | IP Address Virtual | IP Router Virtual Address | VRRP | ACL In | ACL Out |
| --------- | --- | ---------- | ------------------ | ------------------------- | ---- | ------ | ------- |
| Vlan10 |  default  |  10.10.10.8/24  |  -  |  -  |  -  |  -  |  -  |

#### VLAN Interfaces Device Configuration

```eos
!
interface Vlan10
   description Inband Management
   no shutdown
   mtu 1500
   ip address 10.10.10.8/24
```

## Routing

### Service Routing Protocols Model

Multi agent routing protocol model enabled

```eos
!
service routing protocols model multi-agent
```

### IP Routing

#### IP Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | False |
| MGMT | False |

#### IP Routing Device Configuration

```eos
no ip routing vrf MGMT
```

### IPv6 Routing

#### IPv6 Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | False |
| MGMT | false |

### Static Routes

#### Static Routes Summary

| VRF | Destination Prefix | Next Hop IP | Exit interface | Administrative Distance | Tag | Route Name | Metric |
| --- | ------------------ | ----------- | -------------- | ----------------------- | --- | ---------- | ------ |
| MGMT | 0.0.0.0/0 | 172.16.2.1 | - | 1 | - | - | - |
| default | 0.0.0.0/0 | 10.10.10.1 | - | 1 | - | - | - |

#### Static Routes Device Configuration

```eos
!
ip route vrf MGMT 0.0.0.0/0 172.16.2.1
ip route 0.0.0.0/0 10.10.10.1
```

## Multicast

### IP IGMP Snooping

#### IP IGMP Snooping Summary

| IGMP Snooping | Fast Leave | Interface Restart Query | Proxy | Restart Query Interval | Robustness Variable |
| ------------- | ---------- | ----------------------- | ----- | ---------------------- | ------------------- |
| Enabled | - | - | - | - | - |

#### IP IGMP Snooping Device Configuration

```eos
```

## 802.1X Port Security

### 802.1X Summary

#### 802.1X Interfaces

| Interface | PAE Mode | State | Phone Force Authorized | Reauthentication | Auth Failure Action | Host Mode | Mac Based Auth | Eapol |
| --------- | -------- | ------| ---------------------- | ---------------- | ------------------- | --------- | -------------- | ------ |
| Ethernet6 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet7 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet8 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet9 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet10 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet11 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet12 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet13 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet14 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet15 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet16 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet17 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet18 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet19 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet20 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet21 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet22 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |

## VRF Instances

### VRF Instances Summary

| VRF Name | IP Routing |
| -------- | ---------- |
| MGMT | disabled |

### VRF Instances Device Configuration

```eos
!
vrf instance MGMT
```
