# Phase 2 – Servers and Monitoring

## 1. Project Overview

**Project:** Enterprise Network Security Infrastructure  
**Phase:** 2 – Servers and Monitoring  
**Platform:** Cisco Packet Tracer

## 2. Objective

Implement the server and monitoring components of the enterprise lab. This phase configures a dedicated Security Monitoring VLAN, enables centralized Syslog collection, and deploys an HTTP/HTTPS web server in the DMZ.

## 3. Server and Network Addressing

| Component | VLAN / Network | Address / Details |
|---|---|---|
| Security Monitoring | VLAN 60 | `192.168.60.0/24` |
| Security Monitoring gateway | VLAN 60 | `192.168.60.1` |
| Syslog Server | VLAN 60 | `192.168.60.10/24` |
| Syslog Server default gateway | VLAN 60 | `192.168.60.1` |
| Syslog service | Syslog Server | Enabled; UDP port `514` configured as the router's remote logging destination |
| DMZ | VLAN 50 | `192.168.50.0/24` |
| DMZ gateway | VLAN 50 | `192.168.50.1` |
| DMZ Web Server | VLAN 50 | `192.168.50.10/24` |
| DMZ Web Server default gateway | VLAN 50 | `192.168.50.1` |

The Security Monitoring VLAN provides a separate network for centralized log collection. The DMZ VLAN hosts the web server separately from the HR and Finance user VLANs.

## 4. Syslog Server Configuration

The Syslog Server was configured with the following IPv4 settings:

- IP address: `192.168.60.10`
- Subnet mask: `255.255.255.0`
- Default gateway: `192.168.60.1`
- Syslog service: **On**

The Head Office router (HO-R) is configured to send remote log messages to `192.168.60.10` using UDP port `514`. The router's `show logging` output confirms that remote logging is enabled and the destination is reachable (`link up`).

The Syslog event list contains received messages from multiple network-device addresses, including `192.168.60.1`, `192.168.60.2`, `10.0.0.2`, and `10.0.0.6`. This demonstrates that device messages are being collected centrally.

## 5. DMZ Web Server Configuration

The DMZ Web Server was assigned these IPv4 settings:

- IP address: `192.168.50.10`
- Subnet mask: `255.255.255.0`
- Default gateway: `192.168.50.1`

The Packet Tracer server's HTTP and HTTPS services are both shown as **On**. The server's default web content is available to clients over HTTP.

## 6. Verification and Test Results

The following results are visible in the supplied Packet Tracer evidence:

| Test | Source / Destination | Observed result |
|---|---|---|
| Web access | Finance PC `192.168.20.21` → `http://192.168.50.10` | Web page loaded in the PC browser |
| ICMP connectivity | Finance PC `192.168.20.22` → `192.168.50.10` | 4 replies received; 0% packet loss |
| ICMP connectivity | HR PC `192.168.10.21` → `192.168.50.10` | 4 replies received; 0% packet loss |
| HR default gateway | HR PC `192.168.10.21` → `192.168.10.1` | 4 replies received; 0% packet loss |
| HR-to-Finance access check | HR PC `192.168.10.21` → Finance PC `192.168.20.21` | Destination host unreachable responses from `192.168.10.1`; this access-control result is documented in Phase 3 |

These tests show that the DMZ web server can be reached from the tested HR and Finance clients, while the displayed HR-to-Finance test is denied. The access-control policy and its explanation belong in Phase 3 – Network Security Hardening.

## 7. Evidence Screenshots

Place the verified screenshots in:

`screenshots/Phase-2-Servers-and-Monitoring/`

Use these filenames:

1. `P2-01-Router-Syslog-Configuration.png` – HO-R `show logging` output showing remote logging to `192.168.60.10` on UDP port `514`.
2. `P2-02-Syslog-Server-Event-Logs.png` – Syslog service event list showing received device messages.
3. `P2-03-Syslog-Server-IP-Configuration.png` – Syslog Server IP, subnet mask, and default gateway.
4. `P2-04-DMZ-Web-Server-IP-Configuration.png` – DMZ server IP `192.168.50.10/24` and gateway `192.168.50.1`.
5. `P2-05-DMZ-Web-Server-HTTP-Service.png` – HTTP and HTTPS services enabled.
6. `P2-06-Verify-DMZ-Web-Server-Access.png` – Finance PC browser displaying the web page at `http://192.168.50.10`.
7. `P2-07-DMZ-Web-Server-Connectivity-Test-Finance.png` – Finance PC ping showing 4/4 replies to `192.168.50.10`.
8. `P2-08-DMZ-Web-Server-Connectivity-Test-HR.png` – HR PC tests showing successful access to the DMZ server and HR gateway, plus the denied HR-to-Finance test.

Only use these screenshots with the matching descriptions. The HR-to-Finance denial is included as a cross-reference to Phase 3, not as a DMZ connectivity failure.

## 8. Phase 2 Outcome

The lab has a configured Syslog Server in VLAN 60 and a DMZ Web Server in VLAN 50. The supplied evidence shows remote log collection, enabled HTTP/HTTPS services, successful browser access to the DMZ web page, and successful ICMP connectivity from the tested HR and Finance clients to the DMZ server.

**Status:** Phase 2 server configuration and the listed Syslog and DMZ connectivity checks are evidenced by the supplied Packet Tracer screenshots.

---

**Next:** Phase 3 – Network Security Hardening.
