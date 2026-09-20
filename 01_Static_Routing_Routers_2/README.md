Static Routing Lab

Here we have 3 Routers: Router3, 4 and 5. Each router is connected to a single PC, and the routers are chained together to form the WAN links between them.

For R3 configuration

In CLI:

Enable
Configure terminal
Hostname R1

Interface fastEthernet 0/1
Ip address 10.0.0.1 255.255.255.252
No shutdown
Exit

Interface fastEthernet 0/0
Ip address 192.168.10.1 255.255.255.0
No shutdown
Exit
For R4 configuration

In CLI:

Enable
Configure terminal
Hostname R2

Interface fastEthernet 0/0
Ip address 10.0.0.2 255.255.255.252
No shutdown
Exit

Interface fastEthernet 1/0
Ip address 192.168.20.1 255.255.255.0
No shutdown
Exit

Interface fastEthernet 0/1
Ip address 10.0.0.5 255.255.255.252
No shutdown
Exit
For R5 configuration

In CLI:

Enable
Configure terminal
Hostname R3

Interface fastEthernet 0/0
Ip address 10.0.0.6 255.255.255.252
No shutdown
Exit

Interface fastEthernet 0/1
Ip address 192.168.30.1 255.255.255.0
No shutdown
Exit
Now we have to make static routes
For R3 Route
Config terminal
// here ip route <network address of destination> <subnet mask> <path>
Ip route 192.168.20.0 255.255.255.0 10.0.0.2
Ip route 192.168.30.0 255.255.255.0 10.0.0.2
End
For R4 Route
Ip route 192.168.30.0 255.255.255.0 10.0.0.6
Ip route 192.168.10.0 255.255.255.0 10.0.0.1
End
For R5 Route
Ip route 192.168.20.0 255.255.255.0 10.0.0.5
Ip route 192.168.10.0 255.255.255.0 10.0.0.5
End
Now we need to add IP address, subnet mask and default gateway on each PC

By going in Desktop > IP Configuration:

For PC3

Ip address: 192.168.10.2
Subnet mask: 255.255.255.0
Default gateway: 192.168.10.1

For PC4

Ip address: 192.168.20.2
Subnet mask: 255.255.255.0
Default gateway: 192.168.20.1

For PC5

Ip address: 192.168.30.2
Subnet mask: 255.255.255.0
Default gateway: 192.168.30.1
Now we can check basic connectivity tests

For any PC, check ping <ip address>

For PC3

Ping 192.168.10.1
Ping 192.168.20.2 or 192.168.30.2
Ping 10.0.0.1