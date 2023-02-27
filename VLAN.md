VLAN CISCO PACKET TRACER 4 PC 1 SWITCH 1 ROUTER

COPAS METHOD

SWITCH CONFIG

```
config terminal
vlan 10
name vlan1
vlan 20
name vlan2
```


SWITCH CONFIG
RANGE FOR 1 BY 1 FASTETHERNET

```
enable
config terminal
int fa0/1
switchport mode access
switchport access vlan 10
int fa0/2
switchport mode access
switchport access vlan 10
int fa0/3
switchport mode access
switchport access vlan 20
int fa0/4
switchport mode access
switchport access vlan 20
```



SWITCH CONFIG
RANGE FOR MULTIPLE FASTETHERNET

```
int range fa0/1-4
switchport mode access
```
SWITCH CONFIG
```
int fa 0/5
switchport mode trunk
```

ROUTER CONFIG
```
enable
config terminal

int fa0/0
no shutdown

int fa0/0.10
encapsulation dot1q 10
ip add 192.168.1.1 255.255.255.0

int fa0/0.20
encapsulation dot1q 20
ip add 192.168.2.1 255.255.255.0
```



MANUAL METHOD



Switch#config terminal
Switch(config)#vlan 10
Switch(config-vlan)#name SALES
Switch(config-vlan)#vlan 20
Switch(config-vlan)#name IT


Switch>enable
Switch#config terminal

Switch(config)#int fa0/1
Switch(config-if)#switchport mode access
Switch(config-if)#switchport access vlan 10

Switch(config-if)#int fa0/2
Switch(config-if)#switchport mode access
Switch(config-if)#switchport access vlan 10

Switch(config-if)#int fa0/3
Switch(config-if)#switchport mode access
Switch(config-if)#switchport access vlan 20

Switch(config-if)#int fa0/4
Switch(config-if)#switchport mode access
Switch(config-if)#switchport access vlan 20


Switch(config-if)#int range fa0/1-4
Switch(config-if-range)#switchport mode access


Switch(config)#int fa 0/5
Switch(config-if)#switchport mode trunk


SET STATIC IP FOR 4 PC

PC1   IP address 192.168.1.10   Subnet mask 255.255.255.0  Default gateway 192.168.1.1

PC2:  IP address 192.168.1.20  Subnet mask 255.255.255.0  Default gateway 192.168.1.1

PC3: IP address 192.168.2.10    Subnet mask 255.255.255.0  Default gateway 192.168.2.1

PC4: IP address  192.168.2.20  Subnet mask   255.255.255.0  Default gateway 192.168.2.1


To test connectivity between hosts in different VLANs:

Ping PC3 in VLAN 20 from PC1 in VLAN 10. Ping  here will definitely fail. Why? Because inter-VLAN routing is not yet enabled. Hope you can see how  we’ve used VLANs to place the hosts into two  
logical networks which can be viewed as separate broadcast domains.



Now, in order to allow the hosts in the two VLANs to communicate, we need to do something extra. And you can 
guess what. We’ll configure the router to permit  inter-VLAN communication. Let’s do that right away.

5. Configure inter-VLAN routing on the router

Router>enable
Router#config terminal

Router(config)#int fa0/0
Router(config-if)#no shutdown

Router(config-if)#int fa0/0.10
Router(config-subif)#encapsulation dot1q 10


Router(config-subif)#ip add 192.168.1.1 255.255.255.0
Router(config-subif)#

Router(config-subif)#int fa0/0.20
Router(config-subif)#encapsulation dot1q 20
Router(config-subif)#ip add 192.168.2.1 255.255.255.0


https://computernetworking747640215.wordpress.com/2018/07/05/vlan-configuration-on-a-cisco-switch-in-packet-tracer/
