[Uploading Enterprise_Configuration_Guide.md…]()
# Cisco ASA 5506-X Enterprise Network Configuration Guide

> Comprehensive configuration reference with explanations, purposes, alternatives, and Packet Tracer considerations.

# Table of Contents
1. Introduction
2. Network Overview
3. Internal Switch Configuration
4. DMZ Switch Configuration
5. Router Configuration
6. Cisco ASA Firewall Configuration
7. Server Configuration
8. Verification
9. Packet Tracer Bugs
10. Best Practices

---

# Introduction

This project demonstrates a complete enterprise network built in Cisco Packet Tracer using VLANs, Router-on-a-Stick, DHCP, Cisco ASA 5506-X Firewall, NAT, DMZ, DNS, and multiple servers.

---

# Internal Switch Configuration

## Purpose

Separates departments into VLANs to improve security, reduce broadcast traffic, and simplify administration.

## Why VLANs?

- Better security
- Smaller broadcast domains
- Easier management
- Scalable enterprise design

## Alternative Approaches

- Flat Layer-2 network
- Private VLANs
- Software Defined Networking (SDN)

## Example Configuration

```cisco
vlan 10
 name ADMIN

interface range fa0/1-5
 switchport mode access
 switchport access vlan 10
 switchport port-security
 switchport port-security maximum 1
 switchport port-security violation shutdown
```

### Command Explanation

- **vlan 10** — Creates VLAN ID 10.
- **name ADMIN** — Assigns a descriptive name.
- **switchport mode access** — Makes the interface an access port.
- **switchport access vlan 10** — Assigns the interface to VLAN 10.
- **switchport port-security** — Restricts unauthorized devices.

---

# Router Configuration

## Purpose

Provides inter-VLAN routing and DHCP services.

## Why Router-on-a-Stick?

A single physical interface can route traffic for multiple VLANs using 802.1Q tagging.

### Alternatives

- Layer-3 Switch
- Multiple physical router interfaces

---

# Cisco ASA Firewall

## Purpose

Protects the internal network using security zones, NAT, ACLs, and traffic inspection.

### Security Levels

| Zone | Level |
|------|------:|
| Inside | 100 |
| DMZ | 50 |
| Outside | 0 |

### Why NAT?

- Conserves public IP addresses
- Hides internal addressing
- Enables Internet connectivity

### Alternatives

- Static NAT
- Policy NAT
- Twice NAT

---

# Packet Tracer Bugs (Detailed)

## 1. HTTP Timeout through ASA

### Symptoms
HTTP requests fail even when the configuration is correct.

### Cause
Packet Tracer has incomplete ASA HTTP simulation.

### Workaround
- Test using Simulation Mode.
- Verify with ping.
- Check NAT translations.
- Accept as a simulator limitation.

---

## 2. Interface Up/Down

### Cause

- Cable disconnected
- Device powered off
- Interface shutdown

### Fix

```cisco
interface g1/1
 no shutdown
```

---

## 3. DHCP Not Working

### Symptoms

Clients receive APIPA (169.254.x.x).

### Causes

- Missing DHCP pool
- Incorrect VLAN
- Router interface down

### Verification

```cisco
show ip dhcp binding
show ip interface brief
```

---

## 4. DNS Resolution Failure

### Causes

- DNS service disabled
- Wrong DNS address
- Firewall blocking UDP/53

### Verification

```cisco
ping google.com
```

---

## 5. NAT Translations Missing

### Causes

- No generated traffic
- Incorrect NAT object
- ACL blocking packets

Verification:

```cisco
show xlate
show nat
```

---

# Verification Commands

```cisco
show vlan brief
show interfaces trunk
show ip route
show running-config
show access-list
show nat
show xlate
```

---

# Best Practices

- Disable unused ports.
- Use strong passwords.
- Apply ACLs using least privilege.
- Separate public servers into a DMZ.
- Verify configurations before deployment.
- Save configurations using `write memory`.
