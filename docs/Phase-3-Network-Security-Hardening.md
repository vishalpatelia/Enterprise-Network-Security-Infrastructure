# Phase 3 – Network Security Hardening

## 1. Project Overview

**Project:** Enterprise Network Security and SOC Lab
**Phase:** 3 – Network Security Hardening
**Platform:** Cisco Packet Tracer

### Objective

To strengthen the enterprise network by implementing Layer 2 and Layer 3 security controls. These controls help prevent unauthorized device connections, restrict unwanted network traffic, and secure network device management.

## 2. Switch Port Security

Port security was configured on switch access ports to control which devices can connect to the network.

### Security Features

- Maximum MAC address limits configured on selected access ports.
- Sticky MAC address learning.
- Violation detection.
- Shutdown violation mode on the protected ports shown in the evidence.

The example below is specifically for Fa0/8, where the maximum MAC address limit is 1.

### Configuration Example

```text
interface fa0/8
switchport mode access
switchport access vlan 60
switchport port-security
switchport port-security maximum 1
switchport port-security mac-address sticky
switchport port-security violation shutdown
```

### Verification Commands

```text
show port-security
show port-security address
show port-security interface fa0/8
```

### Security Benefit

Port security helps prevent unauthorized devices from using protected switch access ports.

## 3. Secure Remote Management Using SSH

SSH was configured to provide encrypted remote management access to network devices instead of using insecure Telnet.

### Security Features

- SSH version 2.
- Local user authentication.
- RSA key generation.
- VTY access restricted to SSH.

### Verification Commands

```text
show ip ssh
show running-config
```

Check the VTY configuration for:

```text
transport input ssh
login local
```

### Security Benefit

SSH protects remote management sessions by encrypting communication between the administrator and network device.

## 4. Unused Switch Port Shutdown

Unused switch ports were disabled and assigned to the parking VLAN (VLAN 999).

### Security Purpose

- Prevent unauthorized connections through unused ports.
- Reduce unnecessary access points.
- Keep unused interfaces separated from production VLANs.

### Verification Command

```text
show interfaces status
```

Unused interfaces should show a disabled status.

## 5. Access Control Lists (ACLs)

An extended ACL named `HR-RESTRICT-FINANCE` was implemented on HO-R to restrict communication from the HR network to the Finance network.

### ACL Policy

| Source Network       | Destination Network       | Action |
| -------------------- | ------------------------- | ------ |
| HR – 192.168.10.0/24 | Finance – 192.168.20.0/24 | Deny   |
| Other traffic        | Other destinations        | Permit |

### ACL Configuration

```text
ip access-list extended HR-RESTRICT-FINANCE
deny ip 192.168.10.0 0.0.0.255 192.168.20.0 0.0.0.255
permit ip any any
```

The ACL was applied inbound on the HR router subinterface.

### Verification Commands

```text
show access-lists
show running-config
```

To verify where the ACL is applied, inspect the HR router subinterface configuration and confirm the inbound access-group statement is present.

### Traffic Testing

From an HR PC, test connectivity to a Finance PC:

```text
ping 192.168.20.21
```

Expected result: traffic is blocked by the ACL.

The ACL match counter provides additional evidence that the deny rule was triggered.

### Security Benefit

ACLs enforce network access policies by controlling which source and destination networks can communicate.

## 6. Trunk Port Security

The Head Office switch trunk was configured to carry only the required VLANs.

### Security Settings

| Setting       | Value          |
| ------------- | -------------- |
| Trunk port    | Fa0/5          |
| Native VLAN   | 999            |
| Allowed VLANs | 10, 20, 50, 60 |

### Verification Command

```text
show interfaces trunk
```

Verify that the trunk is operational and that only the required VLANs are allowed.

### Security Benefit

Restricting allowed VLANs reduces unnecessary VLAN traffic across trunk links.

## 7. Security Verification Checklist

- [ ] Port security enabled on selected access ports.
- [ ] Maximum MAC address limit configured.
- [ ] Sticky MAC learning configured.
- [ ] Shutdown violation mode configured.
- [ ] SSH version 2 enabled.
- [ ] Local authentication configured.
- [ ] VTY access restricted to SSH.
- [ ] Unused switch ports disabled.
- [ ] Unused ports assigned to VLAN 999.
- [ ] HR-to-Finance ACL configured.
- [ ] ACL traffic restriction tested.
- [ ] Trunk native VLAN configured as 999.
- [ ] Only required VLANs allowed on the trunk.

## 8. Phase 3 Outcome

Network security hardening controls were implemented to improve access control, secure management, and traffic restriction.

The phase demonstrates:

- Layer 2 access protection using port security.
- Secure device management using SSH.
- Reduction of unauthorized access through unused ports.
- Layer 3 traffic filtering using extended ACLs.
- Restricted VLAN propagation across trunk links.

**Status:** Security controls configured and tested in the Cisco Packet Tracer lab. The supplied screenshots document port-security settings, SSH status, unused-port shutdown, ACL configuration and traffic testing, and trunk restrictions. Before publishing, redact sensitive values from the SSH configuration screenshot. If the ACL application command is not visible in the evidence, add a screenshot showing the ACL applied inbound on the HR router subinterface.

## 9. Evidence Screenshots

Save the evidence in `screenshots/Phase-3-Network-Security-Hardening/`:

1. `P3-01-Port-Security-Configuration.png`
2. `P3-02-SSH-Secure-Management.png`
3. `P3-03-Unused-Ports-Disabled.png`
4. `P3-04-ACL-Configuration.png`
5. `P3-05-ACL-Denied-Traffic-Test.png`
6. `P3-06-Trunk-Security.png`

---

**Next:** Phase 4 – Incident Detection and Response Documentation.
