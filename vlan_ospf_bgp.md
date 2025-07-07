# Configuration Vlan_Ospf_Bgp


<p align="center">
  <img height="auto" width="auto" src="https://i.imgur.com/N9KAUN8.png">
</p>


* [Set a Topology](https://github.com/p4nrp/cisco/blob/main/vlan_ospf_bgp.md#1-set-a-topology)
* [Configuration](https://github.com/p4nrp/cisco/blob/main/vlan_ospf_bgp.md#2-configuration)
* [Start Your Validator](https://github.com/p4nrp/testnet/blob/main/elixirfinance.md#3-start-your-validator)
* [Usefull Command](https://github.com/p4nrp/testnet/blob/main/elixirfinance.md#usefull-commands)


### 1. Set a Topology

<p align="center">
  <img height="auto" width="auto" src="https://i.imgur.com/2FEy9ox.png">
</p>

### 2. Configuration

config switch1 VLAN 10,20,30
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
```





