# Packet-Tracer-Project-3---Inter-VLAN-Routing-with-VLANs

![Project 2 Screenshot](https://github.com/pinoechalle-lang/Packet-Tracer-Project-3---Inter-VLAN-Routing-with-VLANs/blob/main/Screenshot%202026-10-19%20165146.png?raw=true)

##### This project simulates small scale and enterprise networks where segmenting network into smaller portions is often practiced or observed to maximize network security, and to make the whole network efficient by giving each department, office, or group its own broadcast domain while maximizing the use of the switches.

## Requirements:
Working as a part-time student in a small BPO office with two departments, you are tasked by the senior IT admin to logically segment a switch in each department into different LANs. Your senior IT admin has given you a list of predefined VLAN names, port ranges, and IP subnets, and you are told to refer to the list. 

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

Commands:

```bash
show running-config
show ip interface brief
show interfaces <interface>

show vlan brief

show interfaces trunk
```

Explained:

- `show running-config`
  This command displays the full router or switch configuration. It is used to confirm that VLANs, trunk ports, IP addresses, and subinterfaces were configured correctly.

- `show ip interface brief`
  This command shows the status of all interfaces and their IP addresses. It verifies whether the interfaces are up/up, assigned the correct IPs, and operational.

- `show interfaces <interface>`
  This command displays detailed information about a specific interface, such as status, duplex, speed, and whether it is connected. In this project, it is used to check interfaces like:
  - `show interfaces g0/1`
  - `show interfaces g0/1.10`
  - `show interfaces g0/1.20`
  - `show interfaces g0/1.30`
  - `show interfaces g0/1.40`
  - `show interfaces g0/1.50`
  - `show interfaces g0/1.60`
  - `show interfaces g0/1.200`

- `show vlan brief`
  This command lists all VLANs that exist on the switch and shows which ports are assigned to each VLAN. It verifies that the required VLANs were created and assigned correctly.

- `show interfaces trunk`
  This command confirms whether trunk ports are enabled and which VLANs are allowed across the trunk links. It verifies that inter-switch communication is functioning properly.

Perform the following checks:

1. VLAN creation and assignment
- Use `show vlan brief` to confirm that VLANs 10, 20, 30, 40, 50, 60, 100, and 200 exist.
- Check that each access port is assigned to the correct VLAN.
- Confirm that unused ports are assigned to VLAN 800 and shut down.

2. Trunking configuration
- Use `show interfaces trunk` to confirm that the trunk links between switches and the router are active.
- Verify that all required VLANs are allowed on the trunk.
- Confirm that VLAN 100 is used as the native VLAN.

3. Router subinterface configuration
- Use `show running-config` to confirm each subinterface was created:
  - `g0/1.10`
  - `g0/1.20`
  - `g0/1.30`
  - `g0/1.40`
  - `g0/1.50`
  - `g0/1.60`
  - `g0/1.200`
- Confirm each subinterface has the correct VLAN encapsulation and IP address.

4. Interface and IP status
- Use `show ip interface brief` to verify the interfaces are active and have correct IP addresses.
- Use `show interfaces <interface>` to check port status and confirm the interface is operational.

5. Connectivity and Inter-VLAN routing
- Ping the default gateway of each VLAN to verify routing is working.
- Example:
  - `ping 192.168.10.254`
  - `ping 192.168.20.254`
  - `ping 192.168.30.254`
  - `ping 192.168.40.254`
  - `ping 192.168.50.254`
  - `ping 192.168.60.6`
  - `ping 192.168.200.254`
- Successful replies confirm that the VLAN interfaces and router configuration are correct and that inter-VLAN communication is functioning.

