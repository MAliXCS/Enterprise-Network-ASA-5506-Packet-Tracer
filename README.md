# Enterprise Network — Cisco ASA 5506-X + VLANs + DMZ

> A complete Cisco Packet Tracer enterprise network lab featuring VLAN segmentation, router-on-a-stick inter-VLAN routing, DHCP, Cisco ASA 5506-X firewall security zones, NAT, DMZ servers, DNS, ICMP inspection, and end-to-end verification.

![Network Architecture]

## Overview

This project demonstrates a segmented enterprise network architecture built in Cisco Packet Tracer:

- **3 internal VLANs:** ADMIN, OFFICE, and LAB
- **Inter-VLAN routing** using a Cisco 2811 router
- **DHCP services** for all internal VLANs
- **Cisco ASA 5506-X firewall** with Inside, DMZ, and Outside security zones
- **5 DMZ servers:** Web, Application, Database, Mail, and Backup
- **Dynamic NAT** for internal users accessing the simulated Internet
- **NAT exemption** between internal networks and the DMZ
- **DNS and HTTP/HTTPS services**
- **ICMP inspection and connectivity testing**
- **Port security and unused-port shutdown on switches**

## Architecture

```text
                    ┌──────────────────────┐
                    │   Internet Server    │
                    │    192.168.1.10      │
                    └──────────┬───────────┘
                               │
                    ┌──────────▼───────────┐
                    │    ASA 5506-X        │
                    │  Outside: 192.168.1.2│
                    │  Inside: 192.168.2.1 │
                    │  DMZ: 192.168.20.1   │
                    └──────┬─────────┬─────┘
                           │         │
                    ┌──────▼───┐ ┌───▼──────────────┐
                    │ Router   │ │   DMZ Switch     │
                    │ 2811     │ │ 5 Server Network │
                    └──────┬───┘ └──────────────────┘
                           │
                    ┌──────▼───────────┐
                    │ Internal Switch  │
                    │ VLAN 10/20/30    │
                    └──────────────────┘
```

## IP Addressing

| Segment | Network | Gateway |
|---|---|---|
| ADMIN / VLAN 10 | `10.0.10.0/24` | `10.0.10.1` |
| OFFICE / VLAN 20 | `10.0.20.0/24` | `10.0.20.1` |
| LAB / VLAN 30 | `10.0.30.0/24` | `10.0.30.1` |
| Firewall Inside | `192.168.2.0/24` | `192.168.2.1` |
| DMZ | `192.168.20.0/24` | `192.168.20.1` |
| Outside | `192.168.1.0/24` | `192.168.1.2` |

## DMZ Servers

| Server | Role | Address |
|---|---|---|
| Server 1 | Primary Web Server | `192.168.20.10` |
| Server 2 | Application Server | `192.168.20.11` |
| Server 3 | Database Server | `192.168.20.12` |
| Server 4 | Mail Server | `192.168.20.13` |
| Server 5 | Backup Server | `192.168.20.14` |

## Repository Structure

```text
Enterprise-Network-ASA-5506-Packet-Tracer/
├── README.md
├── LICENSE
├── .gitignore
├── configurations/
│   ├── switch-config.txt
│   ├── dmz-switch-config.txt
│   ├── router-config.txt
│   ├── asa-firewall-config.txt
│   └── icmp-inspection.txt
├── documentation/
│   ├── COMPLETE_CONFIGURATION_GUIDE.md
│   └── verification-commands.txt
└── images/
    └── network-diagram.png
```

## Quick Start

1. Open the Packet Tracer topology.
2. Configure the internal switch using `configurations/switch-config.txt`.
3. Configure the DMZ switch using `configurations/dmz-switch-config.txt`.
4. Configure the Cisco 2811 router using `configurations/router-config.txt`.
5. Configure the ASA firewall using `configurations/asa-firewall-config.txt`.
6. Configure the DMZ and Internet servers according to the complete guide.
7. Run the verification commands in `documentation/verification-commands.txt`.

## Verification Checklist

- [ ] VLANs are created and assigned correctly
- [ ] Trunk link is operational
- [ ] Internal clients receive DHCP addresses
- [ ] Inter-VLAN routing works
- [ ] Router can reach the ASA inside interface
- [ ] ASA can reach the Internet simulation server
- [ ] Internal users can access the DMZ
- [ ] Dynamic NAT works for Internet access
- [ ] DNS resolution works
- [ ] HTTP/HTTPS services are reachable
- [ ] ICMP inspection works
- [ ] End-to-end connectivity is verified

## Security Notes

This repository is intended for **educational lab and Cisco Packet Tracer use**. The configuration includes intentionally permissive ICMP rules for testing and a sample administrative credential in the original lab configuration. For production use, replace all sample credentials, restrict management access, apply least-privilege ACLs, and review all firewall policies.

## Author

**Muhammad Ali / MAliXCS**

Network Engineering • Cybersecurity • Cisco • Linux

**Repository:** `Enterprise-Network-ASA-5506-Packet-Tracer`

---
*Network Lab Version 1.0 • July 2026*
