# Packet-Tracer-Project-3---Inter-VLAN-Routing-with-VLANs

![Project 2 Screenshot](https://github.com/pinoechalle-lang/Packet-Tracer-Project-3---Inter-VLAN-Routing-with-VLANs/blob/main/Screenshot%202026-10-19%20165146.png?raw=true)

#### Working as a part-time student in a small BPO office with two departments, you are tasked by the senior IT admin to logically segment the switch in each department into different LANs. You must trunk the switches to another switch that is directly connected to the company router, then enable communication between those different LANs to allow people in Department A and B to communicate with one another virtually.

## Requirements:

### VLANs (Identical across three Switches):


| VLAN | Name | Subnet |
|-------------|-----------|------------|
| VLAN 10 | Guest | 192.168.10.0 /24 | 
| VLAN 20 | Reception | 192.168.20.0 /24 | 
| VLAN 30 | Staff/Maintenance | 192.168.30.0 /24 | 
| VLAN 40 | Security | 192.168.40.0 /24 | 
| VLAN 50 | Office | 192.168.50.0 /24 | 
| VLAN 60 | Voice | 192.168.60.0 /24 | 
| VLAN 100 | Native | 192.168.100.0 /24 | 
| VLAN 200 | Remote_Management | 192.168.200.0 /24 |
| VLAN 800 | UNUSED-SHUTDOWN | |

---
### Switch - VLAN Port Assignments

| Switch | Port(s) | Role |
|--------|---------|------|
| SW-A | F0/1 | Trunk to SW-B |
| SW-A | F0/10-F0/14 | Access ports for VLANs 10, 20, 30 |
| SW-A | F0/2-9, F0/15-24 | Shutdown |
| SW-C | F0/3 | Trunk to SW-B |
| SW-C | F0/10-F0/14 | Access ports for VLANs 10, 40, 50/60 |
| SW-C | F0/1-2, F0/4-9, F0/15-24 | Shutdown |
| SW-B | G0/1 | Trunk to Router 1 |
| SW-B | F0/1 | Trunk to SW-A |
| SW-B | F0/3 | Trunk to SW-C |
| SW-B | G0/2, F0/2, F0/4-24 | Shutdown |

---
### Router: VLAN Default Gateway

| VLAN | Interface | Default Gateway | Subnet Mask |
|-------------|-----------|------------|-------------|
| VLAN 10 | G0/1.10 | 192.168.10.254 | 255.255.255.0 | 
| VLAN 20 | G0/1.20 | 192.168.20.254 | 255.255.255.0 | 
| VLAN 30 | G0/1.30 | 192.168.30.254 | 255.255.255.0 | 
| VLAN 40 | G0/1.40 | 192.168.40.254 | 255.255.255.0 | 
| VLAN 50 | G0/1.50 | 192.168.50.254 | 255.255.255.0 | 
| VLAN 60 | G0/1.60 | 192.168.60.6 | 255.255.255.248 | 
| VLAN 100 | G0/1.100 | 192.168.100.254 | 255.255.255.0 | 
| VLAN 200 | G0/1.200 | 192.168.200.254 | 255.255.255.0 | 
