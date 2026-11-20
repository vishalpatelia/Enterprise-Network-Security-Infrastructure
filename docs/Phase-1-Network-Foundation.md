# Phase 1 – Network Foundation

## 1. Project Overview

**Project:** Enterprise Network Security Infrastructure  
**Phase:** 1 – Network Foundation  
**Platform:** Cisco Packet Tracer

### Objective

To design and implement an enterprise network connecting a Head Office and two branch offices. The network uses VLAN segmentation, inter-VLAN routing, DHCP, and OSPF to provide structured network communication.

## 2. Network Architecture

The network consists of:

- Head Office router (HO-R)
- Head Office switch (HO-S)
- Branch A router and switch
- Branch B router and switch
- HR department VLAN
- Finance department VLAN
- DMZ VLAN
- Security Monitoring VLAN
- Syslog Server
- DMZ Web Server
- End-user PCs

## 3. VLAN Configuration

The Head Office switch uses the following VLANs:

| VLAN ID | VLAN Name | Network / Purpose |
|---|---|---|
| 10 | HR | 192.168.10.0/24 |
| 20 | FINANCE | 192.168.20.0/24 |
| 50 | DMZ | 192.168.50.0/24 |
| 60 | SECURITY-MONITORING | 192.168.60.0/24 |
| 999 | PARKING | Unused switch ports |

VLAN segmentation separates departments and infrastructure into different broadcast domains.

## 4. Inter-VLAN Routing

Router-on-a-stick configuration was implemented on HO-R using subinterfaces.

| Interface | IP Address | Purpose |
|---|---|---|
| G0/0.10 | 192.168.10.1/24 | HR gateway |
| G0/0.20 | 192.168.20.1/24 | Finance gateway |
| G0/0.50 | 192.168.50.1/24 | DMZ gateway |
| G0/0.60 | 192.168.60.1/24 | Security Monitoring gateway |

These subinterfaces provide Layer 3 connectivity for the VLANs.

## 5. DHCP Configuration

DHCP pools were configured on HO-R for the HR and Finance networks.

The router dynamically assigns IP addresses to client devices, reducing manual configuration.

Verification commands:

```text
show ip dhcp pool
show ip dhcp binding
```

## 6. Branch Connectivity and OSPF

The Head Office connects to two branch routers through point-to-point serial links.

### WAN and Branch Addressing

| Device | Interface | IP Address |
|---|---|---|
| HO-R | Serial0/3/0 | 10.0.0.1/30 |
| Branch A Router | Serial0/3/0 | 10.0.0.2/30 |
| HO-R | Serial0/3/1 | 10.0.0.5/30 |
| Branch B Router | Serial0/3/1 | 10.0.0.6/30 |
| Branch A Router | LAN interface | 192.168.30.1/24 |
| Branch B Router | LAN interface | 192.168.40.1/24 |

### OSPF Configuration Summary

- **Routing protocol:** Open Shortest Path First (OSPF)
- **Process ID:** 1
- **Area:** 0 (backbone area)

OSPF was configured to exchange routing information between the Head Office and branch offices.

### OSPF Verification

Command:

```text
show ip ospf neighbor
```

The recorded verification output showed these neighbor router IDs in the FULL state:

- Branch A neighbor: `192.168.30.1` – FULL state.
- Branch B neighbor: `192.168.40.1` – FULL state.

The FULL neighbor state confirms successful OSPF adjacency establishment with both branch routers.

## 7. Network Connectivity Testing

Connectivity was tested using ICMP ping commands. The documented tests include:

- HR client-to-default-gateway connectivity.
- Finance client-to-default-gateway connectivity.
- Head Office-to-branch connectivity.

The HR-to-Finance communication restriction is documented separately under Phase 3 ACL testing. Access to DMZ and monitoring networks should be described as verified only where corresponding test evidence is included.

## 8. Configuration Verification Commands

### Router

```text
show running-config
show ip interface brief
show ip dhcp pool
show ip dhcp binding
show ip ospf neighbor
show ip route
```

### Switch

```text
show vlan brief
show interfaces trunk
show interfaces status
show running-config
```

## 9. Phase 1 Outcome

The enterprise network foundation was implemented with:

- Department-based VLAN segmentation.
- Router-on-a-stick inter-VLAN routing.
- DHCP address assignment for HR and Finance clients.
- OSPF routing between Head Office and branch offices.
- Connectivity verification for the documented HR gateway, Finance gateway, and branch tests.

**Status:** Core Phase 1 configuration and the documented connectivity tests were completed in Cisco Packet Tracer.

## 10. Evidence Screenshots

The Phase 1 evidence is stored in `screenshots/Phase-1-Network-Foundation/`:

1. `P1-01-Enterprise-Topology.png`
2. `P1-02-VLAN-and-Trunk-Configuration.png`
3. `P1-03-Router-Interface-Configuration.png`
4. `P1-04-OSPF-and-Routing.png`
5. `P1-05-DHCP-Configuration.png`
6. `P1-06-HR-Gateway-Connectivity.png`
7. `P1-07-Finance-Gateway-Connectivity.png`
8. `P1-08-Branch-Connectivity.png`

---

**Next:** Phase 2 – Servers and Monitoring Documentation.
