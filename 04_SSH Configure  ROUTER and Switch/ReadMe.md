Static Routing + SSH Configuration Lab

Two routers (R1, R2) each connected to a LAN switch (SW1, SW2), with static routing between the two LANs and SSH enabled for remote management on all four devices.

**_IP Address Plan_**
Device Interfaces
Device Interface IP Address Mask Gateway
R1 LAN 192.168.1.1 /24 —
R1 R1–R2 10.1.1.1 /30 —
R2 R2–R1 10.1.1.2 /30 —
R2 LAN 192.168.2.1 /24 —
SW1 VLAN 1 192.168.1.10 /24 192.168.1.1
SW2 VLAN 1 192.168.2.10 /24 192.168.2.1

**_PC IP Addressing_**
PC IP Address Mask Gateway
PC1 192.168.1.11 255.255.255.0 192.168.1.1
PC2 192.168.1.12 255.255.255.0 192.168.1.1
PC3 192.168.2.11 255.255.255.0 192.168.2.1
PC4 192.168.2.12 255.255.255.0 192.168.2.1

**_Notes on Key Commands_**

transport input ssh — Configures a device's VTY (Virtual Terminal) lines to accept only SSH connections for remote management, blocking Telnet.
ip ssh version 2 — Forces the device to use SSH version 2 specifically.
ip default-gateway 192.168.1.1 — Sets the gateway a Layer 2 switch uses to reach networks outside its own VLAN, for management traffic.
crypto key generate rsa modulus 2048 — Generates the RSA key pair SSH needs. 2048 bits is the industry-standard size, balancing strong security with acceptable processing performance.
description Management IP (under an interface) — Documents the purpose of the interface; the ip address command is what actually assigns the network identity.

**\*R1 Configuration**
enable
configure terminal
hostname R1

**LAN interface**

interface gigabitEthernet 0/0
description LAN-interface
ip address 192.168.1.1 255.255.255.0
no shutdown
exit

**Link to R2**

interface gigabitEthernet 0/1
description R1-R2
ip address 10.1.1.1 255.255.255.252
no shutdown
exit

Static route to R2's LAN

ip route 192.168.2.0 255.255.255.0 10.1.1.2

**SSH configuration\***

ip domain-name ccna.local
username admin privilege 15 secret cisco
crypto key generate rsa modulus 2048
ip ssh version 2
line vty 0 15
login local
transport input ssh
exit
end
write memory

**_R2 Configuration_**
enable
configure terminal
hostname R2

**LAN interface**

interface gigabitEthernet 0/0
description LAN-interface
ip address 192.168.2.1 255.255.255.0
no shutdown
exit

**Link to R1**

interface gigabitEthernet 0/1
description R2 to R1
ip address 10.1.1.2 255.255.255.252
no shutdown
exit

Static route to R1's LAN

ip route 192.168.1.0 255.255.255.0 10.1.1.1

**S**SH configuration\*\*

ip domain-name ccna.local
username admin privilege 15 secret cisco
crypto key generate rsa modulus 2048
ip ssh version 2
line vty 0 15
login local
transport input ssh
exit
end
write memory

**_SW1 Configuration_**
enable
configure terminal
hostname SW1

interface vlan 1
description Management IP
ip address 192.168.1.10 255.255.255.0
no shutdown
exit

ip default-gateway 192.168.1.1

**SSH configuration**

ip domain-name ccna.local
username admin privilege 15 secret cisco
crypto key generate rsa modulus 2048
ip ssh version 2
line vty 0 15
login local
transport input ssh
exit
end
write memory

**_SW2 Configuration_**
enable
configure terminal
hostname SW2

interface vlan 1
description Management IP
ip address 192.168.2.10 255.255.255.0
no shutdown
exit

ip default-gateway 192.168.2.1

**SSH configuration**

ip domain-name ccna.local
username admin privilege 15 secret cisco
crypto key generate rsa modulus 2048
ip ssh version 2
line vty 0 15
login local
transport input ssh
exit
end
write memory

**_Troubleshooting Commands_**

R1

show ip interface brief
show ip route
show running-config
show ip ssh
show users

R2

show ip interface brief
show ip route
show ip ssh

SW1 / SW2

show ip interface brief
show vlan brief
show ip ssh
show running-config
