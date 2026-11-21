# Enterprise Network Security Infrastructure

## Project Overview

This project demonstrates the design, implementation, configuration, and security hardening of a multi-site enterprise network using **Cisco Packet Tracer**.

The simulated infrastructure consists of a Head Office and two branch offices. It demonstrates enterprise networking concepts, VLAN segmentation, inter-VLAN routing, dynamic routing, server infrastructure, centralized monitoring, network security controls, and incident detection and response.

The implementation is documented in four phases and provides a practical foundation for further cybersecurity and cloud security projects.

## Project Objectives

- Design a multi-site enterprise network.
- Implement VLAN segmentation and inter-VLAN routing.
- Configure DHCP and dynamic routing using OSPF.
- Establish connectivity between Head Office and branch offices.
- Configure DMZ and centralized Syslog monitoring.
- Implement secure remote administration using SSH.
- Apply switch port security and access-control policies.
- Secure unused switch ports and trunk interfaces.
- Simulate and detect an unauthorized-device incident.
- Demonstrate incident containment, recovery, and connectivity verification.

## Technologies and Tools

| Technology | Purpose |
|---|---|
| Cisco Packet Tracer | Network design and simulation |
| Cisco IOS CLI | Router and switch configuration |
| VLAN | Network segmentation |
| IEEE 802.1Q | VLAN trunking |
| DHCP | Automatic IP address allocation |
| OSPF | Dynamic routing |
| SSH v2 | Secure remote administration |
| Port Security | Unauthorized-device restriction |
| Access Control Lists | Traffic access restrictions |
| Syslog | Centralized event monitoring |

## Network Architecture

The simulated enterprise network includes:

- Head Office
- Branch A
- Branch B
- HR department
- Finance department
- DMZ network
- Security Monitoring network

### VLAN and IP Addressing Plan

| VLAN | Name | Network | Default Gateway |
|---|---|---|---|
| 10 | HR | 192.168.10.0/24 | 192.168.10.1 |
| 20 | FINANCE | 192.168.20.0/24 | 192.168.20.1 |
| 50 | DMZ | 192.168.50.0/24 | 192.168.50.1 |
| 60 | SECURITY-MONITORING | 192.168.60.0/24 | 192.168.60.1 |
| 999 | PARKING | Layer 2 | Not applicable |

### Branch Network Addressing

| Location | Network | Router Gateway | Switch Management IP |
|---|---|---|---|
| Branch A | 192.168.30.0/24 | 192.168.30.1 | 192.168.30.2 |
| Branch B | 192.168.40.0/24 | 192.168.40.1 | 192.168.40.2 |

### WAN Routing

OSPF Process 1, Area 0, provides dynamic routing between the Head Office and branch routers.

| Device | Serial Interface | IP Address |
|---|---|---|
| HO-R | Serial0/3/0 | 10.0.0.1/30 |
| Branch A Router | Serial0/3/0 | 10.0.0.2/30 |
| HO-R | Serial0/3/1 | 10.0.0.5/30 |
| Branch B Router | Serial0/3/1 | 10.0.0.6/30 |

## Project Implementation – Four Phases

### Phase 1 – Network Foundation

**Objective:** Design and configure the enterprise network infrastructure.

Implemented:
- Enterprise network topology.
- VLAN creation and assignment.
- 802.1Q trunk configuration.
- Router-on-a-stick inter-VLAN routing.
- DHCP configuration for Head Office departments.
- OSPF dynamic routing.
- Branch network connectivity.
- End-to-end connectivity testing.

**Documentation:** [Phase 1 – Network Foundation](docs/Phase-1-Network-Foundation.md)

**Evidence:** [Phase 1 Screenshots](screenshots/Phase-1-Network-Foundation/)

### Phase 2 – Servers and Monitoring

**Objective:** Configure server infrastructure and centralized network monitoring.

Implemented:
- DMZ network in VLAN 50.
- Security Monitoring network in VLAN 60.
- Syslog Server at 192.168.60.10.
- Syslog service configuration.
- Router and switch Syslog forwarding.
- Centralized event monitoring.

**Documentation:** [Phase 2 – Servers and Monitoring](docs/Phase-2-Servers-and-Monitoring.md)

**Evidence:** [Phase 2 Screenshots](screenshots/Phase-2-Servers-and-Monitoring/)

### Phase 3 – Network Security Hardening

**Objective:** Improve network security and restrict unauthorized access.

Implemented:
- SSH version 2 remote administration.
- Switch port security.
- Sticky MAC address learning.
- Unused port shutdown.
- VLAN 999 parking VLAN.
- Trunk security and allowed VLAN restrictions.
- HR-to-Finance access restriction using an ACL.
- Security policy testing.

**Documentation:** [Phase 3 – Network Security Hardening](docs/Phase-3-Network-Security-Hardening.md)

**Evidence:** [Phase 3 Screenshots](screenshots/Phase-3-Network-Security-Hardening/)

### Phase 4 – Incident Detection and Response

**Objective:** Demonstrate unauthorized-device detection and incident response.

Implemented:
- Authorized endpoint baseline.
- Unauthorized-device connection test.
- Port-security violation detection on HO-S Fa0/8.
- Automatic port shutdown.
- Syslog incident monitoring.
- Authorized endpoint reconnection.
- Port recovery.
- Post-incident connectivity verification.

**Incident Result:** The switch detected an unauthorized MAC address, placed Fa0/8 into a secure-shutdown state, and recorded a violation count of 1. The authorized endpoint was reconnected, and connectivity was successfully restored.

**Documentation:** [Phase 4 – Incident Detection and Response](docs/Phase-4-Incident-Detection-and-Response.md)

**Evidence:** [Phase 4 Screenshots](screenshots/Phase-4-Incident-Detection-and-Response/)

## Reviewed Device Configurations

The repository contains reviewed configuration files for six network devices. Sensitive password hashes have been redacted from the public versions.

| Device | Configuration |
|---|---|
| Head Office Router | [HO-R.txt](configurations/HO-R.txt) |
| Head Office Switch | [HO-S.txt](configurations/HO-S.txt) |
| Branch A Router | [Branch-A-Router.txt](configurations/Branch-A-Router.txt) |
| Branch A Switch | [Branch-A-Switch.txt](configurations/Branch-A-Switch.txt) |
| Branch B Router | [Branch-B-Router.txt](configurations/Branch-B-Router.txt) |
| Branch B Switch | [Branch-B-Switch.txt](configurations/Branch-B-Switch.txt) |

[View all device configurations](configurations/)

## Testing and Verification

The project includes testing and evidence for:

- VLAN and trunk configuration.
- Inter-VLAN communication.
- DHCP address allocation.
- OSPF neighbor relationships and route propagation.
- Branch connectivity.
- SSH configuration.
- Port-security enforcement.
- ACL traffic restriction.
- Syslog event monitoring.
- Unauthorized-device detection.
- Port recovery and connectivity restoration.

## Repository Structure

```text
Enterprise-Network-Security-Infrastructure/
│
├── README.md
│
├── docs/
│   ├── Phase-1-Network-Foundation.md
│   ├── Phase-2-Servers-and-Monitoring.md
│   ├── Phase-3-Network-Security-Hardening.md
│   └── Phase-4-Incident-Detection-and-Response.md
│
├── screenshots/
│   ├── Phase-1-Network-Foundation/
│   ├── Phase-2-Servers-and-Monitoring/
│   ├── Phase-3-Network-Security-Hardening/
│   └── Phase-4-Incident-Detection-and-Response/
│
└── configurations/
    ├── README.md
    ├── HO-R.txt
    ├── HO-S.txt
    ├── Branch-A-Router.txt
    ├── Branch-A-Switch.txt
    ├── Branch-B-Router.txt
    └── Branch-B-Switch.txt
```

## Learning Outcomes

Through this project, I developed practical experience in:

- Enterprise network design and implementation.
- VLAN segmentation and inter-VLAN routing.
- Cisco router and switch configuration.
- Dynamic routing using OSPF.
- Network troubleshooting and connectivity verification.
- Network access control and security hardening.
- Centralized Syslog monitoring.
- Basic security incident detection and response.

## Future Improvements

Planned extensions to the project include:

- Network traffic analysis using Wireshark.
- Vulnerability assessment.
- Authorized penetration-testing exercises.
- IDS/IPS implementation.
- SIEM and SOC monitoring.
- AWS cloud security.
- Network and security automation.

## Project Scope and Disclaimer

This project was developed and tested in Cisco Packet Tracer. Security incidents and network behavior described here are simulated laboratory exercises, not production-network events.

The public configuration files have sensitive password hashes redacted. Credentials and private keys should never be committed to a public repository.

---

**Project:** Enterprise Network Security Infrastructure  
**Implementation:** Phases 1–4  
**Platform:** Cisco Packet Tracer  
**Focus:** Enterprise Networking, Network Security, Monitoring, and Incident Response
