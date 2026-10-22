# Packet-Tracer-Project-3---Inter-VLAN-Routing-with-VLANs

![Project 2 Screenshot](https://github.com/pinoechalle-lang/Packet-Tracer-Project-3---Inter-VLAN-Routing-with-VLANs/blob/main/Screenshot%202026-10-19%20165146.png?raw=true)

#### Working as a part-time student in a small BPO office with two departments, you are tasked by the senior IT admin to logically segment a switch in each department into different LANs. You must trunk the switches to another switch that is directly connected to the company router, then enable communication between those different LANs to allow people in Department A and B to communicate with one another virtually. Additionally, all the switches must be configured to be remotely accessed by another IT employee working in both departments. The senior IT admin gave you a list of tables to follow.

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
### Switch - VLAN Interface Assignments

#### Switch A (SW-A)
| Interface(s) | Role |
|---------|------|
| F0/1 | Trunk to SW-B |
| F0/10-F0/14 | Access ports for VLANs 10, 20, 30 |
| F0/2-9, F0/15-24 | Shutdown |
| VLAN 200 | Remote Management (192.168.200.1) |


#### Switch B (SW-B)
| Interface(s) | Role |
|---------|------|
| G0/1 | Trunk to Router 1 |
| F0/1 | Trunk to SW-A |
| F0/3 | Trunk to SW-C |
| G0/2, F0/2, F0/4-24 | Shutdown |
| VLAN 200 | Remote Management (192.168.200.2) |

#### Switch C (SW-C)
| Interface(s) | Role |
|---------|------|
| F0/3 | Trunk to SW-B |
| F0/10-F0/14 | Access ports for VLANs 10, 40, 50/60 |
| F0/1-2, F0/4-9, F0/15-24 | Shutdown |
| VLAN 200 | Remote Management (192.168.200.3) |

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

---

### Verification


```bash
show running-config
show interfaces

show vlan brief
show trunk 
```

Verifying if the network was configured correctly is extremely important, especially in complex set-ups such as these.

#### Perform the following checks:

A. VLAN verification
- On each switch, the command show vlan brief was used to confirm that VLANs 10, 20, 30, 40, 50, 60, 100, and 200 were created and active.

- The access ports assigned to each VLAN were checked to confirm that the correct interfaces were in the correct VLANs.

B. Trunk verification
- On the switches, the command show interfaces trunk was used to verify that the trunk links were up.

- It was confirmed that the trunk ports carried the required VLANs and used VLAN 100 as the native VLAN.

C. Router verification
- On the router, the command show running-config was used to confirm the presence of the subinterfaces for VLANs 10, 20, 30, 40, 50, 60, and 200.

- The command show interfaces g0/1.10, show interfaces g0/1.20, etc., was used to confirm that each subinterface had the correct IP address and was operational.

D. Connectivity verification
- Ping the default gateway from any given VLAN to ensure that the default gateway is reachable.
- Ping a PC from the same VLAN.
- Ping a PC in a different VLAN to ensure that Inter-VLAN is working as intended.



