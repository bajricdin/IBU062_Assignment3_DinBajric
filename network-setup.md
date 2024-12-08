Routers: 
    Router ISR4321
Switches:
    Switch 2960-24TT
End-Devices:
    PC-PT
    Laptop-PT
    Server-PT

Switch0:
    Default Gateaway: 168.90.0.1
    Subnet Mask: 255.255.0.0
    Devices Assigned: 
        PC0: 168.90.0.5
        PC1: 168.90.0.3
        PC3: 168.90.0.6
        Laptop0: 168.90.04
        Server0: 168.90.0.2
Switch1:
    Default Gateaway: 210.3.14.1
    Subnet Mask: 255.255.255.0
    Devices Assigned: 
        Server1: 210.3.14.2
        Server2: 210.3.14.3
        PC2: 210.3.14.4
        PC4: 210.3.14.5
        
Explanation of configuring DHCP:

enable - this command gives privileges for config commands

configure terminal - moves to configuration mode where you can make changes to the router 

interface FastEthernet0/0 - Access to first router which is connected to Switch0
ip address 168.90.0.1 255.255.0.0 - Assigns IP addres and subnet mask
no shutdown - activates interface
exit exits interface config mode

interface FastEthernet0/1 - Access to first router which is connected to Switch1
ip address 210.3.14.1 255.255.255.0 - Assigns IP addres and subnet mask
no shutdown
exit

ip dhcp pool Network1 - Creates a DHCP pool named "Network1"
network 168.90.0.0 255.255.0.0 - Specifies the network range and subnet mask
default-router 168.90.0.1 - Assigns the default gateway
exit - exits the DHCP config mode

ip dhcp pool Network2 - Creates a DHCP pool named "Network2"
network 210.3.14.0 255.255.255.0 - Specifies the network range and subnet mask
default-router 210.3.14.1
exit

ip dhcp excluded-address 168.90.0.1 - Prevents the specified IP Address from being assigned by DHCP
ip dhcp excluded-address 210.3.14.1

write memory - Permanently saves the config to the routers memory

show ip dhcp binding - Displays the list of IP Addresses assigned by DHCP