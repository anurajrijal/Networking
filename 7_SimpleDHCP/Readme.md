For DHCP
config terminal
ip dhcp pool<name>,
ip dhcp pool Lan
network 192.168.10.0 255.255.255.0
default router 192.168.10.1
dns server 8.8.8.8
domain LAB.com
exit


To block certain ip address for static
ip dhcp excluded-address 192.168.10.1 192.168.10.100 