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

Download dockerfile from elixir finance
```
wget https://files.elixir.finance/Dockerfile
```

Edit file DockerFile with your address and your private key
```
nano DockerFile
```

Build DockerFile image
```
docker build . -f Dockerfile -t elixir-validator
```

### 3. Start Your Validator
Run the validator by executing the following docker command: 
```
docker run -it --name ev elixir-validator
```
Optionally, you can configure the the validator to automatically run at startup:
```
docker run -d --restart unless-stopped --name ev elixir-validator
```
Your validator should start up in 20 seconds and begin submitting order proposals to the network.


# Usefull commands
check docker available running
```
docker ps
```

check docker logs realtime run
```
docker logs -f machinename
```

Upgrading Node 
```
docker kill ev
docker rm ev
docker pull elixirprotocol/validator:testnet-2
docker build . -f Dockerfile -t elixir-validator
```




