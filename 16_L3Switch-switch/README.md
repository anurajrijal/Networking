devices are:
L2-SW0

enable
configure terminal

hostname L2-SW0

vlan 10
 name Users
exit

interface fa0/2
 switchport mode access
 switchport access vlan 10
 no shutdown
exit

interface fa0/1
 switchport mode trunk
 no shutdown
exit

end
write memory

L3-SW0

enable
configure terminal

hostname L3-SW0
ip routing

vlan 10
 name Users
exit

interface vlan 10
 ip address 192.168.10.1 255.255.255.240
 no shutdown
exit

interface gi1/0/3
 switchport mode trunk
 no shutdown
exit

interface range gi0/1 - 2
 no switchport
 channel-group 1 mode desirable
 no shutdown
exit

interface port-channel 1
 no switchport
 ip address 10.0.255.1 255.255.255.252
 no shutdown
exit

ip route 192.168.20.0 255.255.255.240 10.0.255.2

end
write memory

L3-SW1

enable
configure terminal

hostname L3-SW1
ip routing

vlan 20
 name Users
exit

interface vlan 20
 ip address 192.168.20.1 255.255.255.240
 no shutdown
exit

interface gi1/0/3
 switchport mode trunk
 no shutdown
exit

interface range gi0/1 - 2
 no switchport
 channel-group 1 mode desirable
 no shutdown
exit

interface port-channel 1
 no switchport
 ip address 10.0.255.2 255.255.255.252
 no shutdown
exit

ip route 192.168.10.0 255.255.255.240 10.0.255.1

end
write memory

L2-SW1

enable
configure terminal

hostname L2-SW1

vlan 20
 name RIGHT-LAN
exit

interface fa0/2
 switchport mode access
 switchport access vlan 20
 spanning-tree portfast
 no shutdown
exit

interface fa0/1
 switchport mode trunk
 no shutdown
exit

end
write memory