# Configuration Vlan_Ospf_Bgp


<p align="center">
  <img height="auto" width="auto" src="https://i.imgur.com/N9KAUN8.png">
</p>


* [Set a Topology](https://github.com/p4nrp/cisco/blob/main/vlan_ospf_bgp.md#1-set-a-topology)
* [Configuration](https://github.com/p4nrp/cisco/blob/main/vlan_ospf_bgp.md#2-configuration)



### 1. Set a Topology

<p align="center">
  <img height="auto" width="auto" src="https://i.imgur.com/2FEy9ox.png">
</p>

### 2. Configuration

config switch1 VLAN 10,20,30 (add new VLAN)
<p align="center">
  <img height="auto" width="auto" src="https://i.imgur.com/yQfFa9H.jpeg">
</p>

```
en
conf t
vlan 10 
name VLAN10
vlan 20
name VLAN20
vlan 30
name VLAN30
ex
```
```
int range fa0/2-3
sw mod acc
sw acc vlan 10
spanning-tree portfast
int range fa0/4-5
sw mod acc
sw acc vlan 20
spanning-tree portfast
int range fa0/6-7
sw mod acc
sw acc vlan 30
spanning-tree portfast
ex
int fa0/1
sw mod trunk
ex
```
Config Router 1 alokasi ip vlan, router, and dhcp
```
en 
conf t
int fa0/0
no sh
```
```
int fa0/0.10
encapsulation dot1q 10
ip address 192.168.1.1 255.255.255.0
ex
int fa0/0.20
encapsulation dot1q 20
ip address 192.168.2.1 255.255.255.0
int fa0/0.30
encapsulation dot1q 30
ip address 192.168.3.1 255.255.255.0
ex
```
```
ip dhcp pool VLAN10
network 192.168.1.0 255.255.255.0
default-router 192.168.1.1
dns-server 8.8.8.8
ex
ip dhcp pool VLAN20
network 192.168.2.0 255.255.255.0
default-router 192.168.2.1
dns-server 8.8.8.8
ex
ip dhcp pool VLAN30
network 192.168.3.0 255.255.255.0
default-router 192.168.3.1
dns-server 8.8.8.8
ex
```
Config ip Router 1 to router 2
```
int fa0/1
no sh
ip address 10.10.10.1 255.255.255.252
ex
```
config switch2 VLAN 40,50,60 (add new VLAN)
```
en
conf t
vlan 40 
name VLAN40
vlan 50
name VLAN50
vlan 60
name VLAN60
ex
```
```
int range fa0/2-3
sw mod acc
sw acc vlan 40
spanning-tree portfast
int range fa0/4-5
sw mod acc
sw acc vlan 50
spanning-tree portfast
int range fa0/6-7
sw mod acc
sw acc vlan 60
spanning-tree portfast
ex
int fa0/1
sw mod trunk
ex
```
Config Router 3 alokasi ip vlan, router, and dhcp
```
en 
conf t
int fa0/1
no sh
```
```
int fa0/1.40
encapsulation dot1q 40
ip address 192.168.4.1 255.255.255.0
ex
int fa0/1.50
encapsulation dot1q 50
ip address 192.168.5.1 255.255.255.0
int fa0/1.60
encapsulation dot1q 60
ip address 192.168.6.1 255.255.255.0
ex
```
```
ip dhcp pool VLAN40
network 192.168.4.0 255.255.255.0
default-router 192.168.4.1
dns-server 8.8.8.8
ex
ip dhcp pool VLAN50
network 192.168.5.0 255.255.255.0
default-router 192.168.5.1
dns-server 8.8.8.8
ex
ip dhcp pool VLAN60
network 192.168.6.0 255.255.255.0
default-router 192.168.6.1
dns-server 8.8.8.8
ex
```
Config add ip Router 3 to router 2
```
int fa0/0
no sh
ip address 20.20.20.2 255.255.255.252
ex
```
Config add ip Router 2 to router 1
```
en
conf t
int fa0/0
no sh
ip address 10.10.10.2 255.255.255.252
ex
```
Config add ip Router 2 to router 3
```
int fa0/1
no sh
ip address 20.20.20.1 255.255.255.252
ex
```
Config router 1 bgp
```
router bgp 100
neighbor 10.10.10.2 remote-as 200
network 192.168.1.0 mask 255.255.255.0
network 192.168.2.0 mask 255.255.255.0
network 192.168.3.0 mask 255.255.255.0
network 10.10.10.0 mask 255.255.255.252
ex
```
Config router3 ospf
```
router ospf 1
network 20.20.20.0 0.0.0.3 area 0
network 192.168.4.0 0.0.0.255 area 0
network 192.168.5.0 0.0.0.255 area 0
network 192.168.6.0 0.0.0.255 area 0
ex
```
Config Router2
```
router ospf 1
network 20.20.20.0 0.0.0.3 area 0
ex
```
```
router bgp 200
neighbor 10.10.10.1 remote-as 100
network 10.10.10.0 mask 255.255.255.252
ex
```
```
router ospf 1
redistribute bgp 200 subnets
ex
```
```
router bgp 200
redistribute ospf 1
```
### 3. Check
```
en
conf t
do sh ip route
```
