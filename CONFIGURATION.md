# Enterprise Network Configuration

> This file contains only the device configurations for the project.

## Internal Switch (Cisco 2950)

```cisco
enable
configure terminal

vlan 10
 name ADMIN
vlan 20
 name OFFICE
vlan 30
 name LAB

interface range fa0/1-5
 switchport mode access
 switchport access vlan 10
 switchport port-security
 switchport port-security maximum 1
 switchport port-security violation shutdown
 no shutdown

interface range fa0/6-10
 switchport mode access
 switchport access vlan 20
 switchport port-security
 switchport port-security maximum 1
 switchport port-security violation shutdown
 no shutdown

interface range fa0/11-15
 switchport mode access
 switchport access vlan 30
 switchport port-security
 switchport port-security maximum 1
 switchport port-security violation shutdown
 no shutdown

interface fa0/24
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30
 no shutdown

interface range fa0/16-23
 shutdown

end
write memory
```

## DMZ Switch

```cisco
enable
configure terminal
vlan 20
 name DMZ

interface range fa0/1-5
 switchport mode access
 switchport access vlan 20
 no shutdown

interface fa0/24
 switchport mode access
 switchport access vlan 20
 no shutdown

end
write memory
```

## Router (Cisco 2811)

```cisco
enable
configure terminal

interface fa0/0.10
 encapsulation dot1Q 10
 ip address 10.0.10.1 255.255.255.0

interface fa0/0.20
 encapsulation dot1Q 20
 ip address 10.0.20.1 255.255.255.0

interface fa0/0.30
 encapsulation dot1Q 30
 ip address 10.0.30.1 255.255.255.0

interface fa0/1
 ip address 192.168.2.254 255.255.255.0
 no shutdown

ip route 0.0.0.0 0.0.0.0 192.168.2.1

end
write memory
```

## Cisco ASA 5506-X

```cisco
enable
configure terminal

interface g1/1
 nameif inside
 security-level 100
 ip address 192.168.2.1 255.255.255.0

interface g1/2
 nameif outside
 security-level 0
 ip address 192.168.1.2 255.255.255.0

interface g1/3
 nameif dmz
 security-level 50
 ip address 192.168.20.1 255.255.255.0

object network INSIDE_NET
 subnet 10.0.0.0 255.0.0.0
 nat (inside,outside) dynamic interface

write memory
```
