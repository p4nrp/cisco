PC GROUP 1 192.168.1.0   PC GROUP 2   192.168.2.0    PC GROUP 3   192.168.3.0
   


ROUTER GROUP 1 172.16.1.0 ROUTER GROUP 2  172.16.2.0     ROUTER GROUP 3   172.16.3.0
         

-[GAMBAR TOPOLOGY](https://ibb.co/c1Dq7b1)


ADD IP ROUTER GROUP 1
IP GATEWAY FROM PC GROUP 1
```
en
conf t 
int gig0/0
ip add 192.168.1.1 255.255.255.0
no sh
int gig0/2
ip add 172.16.1.1 255.255.255.252
no sh
int gig0/1
ip add 172.16.3.2 255.255.255.252
no sh
```
ip route
```
ex
ip route 192.168.2.0 255.255.255.0 172.16.1.2
ip route 192.168.3.0 255.255.255.0 172.16.3.1
```
ADD IP ROUTER
IP GATEWAY FROM PC GROUP 2
```
en
conf t 
int gig0/2
ip add 192.168.2.1 255.255.255.0
no sh
int gig0/1
ip add 172.16.1.2 255.255.255.252
no sh
int gig0/0
ip add 172.16.2.2 255.255.255.252
no sh
```
ip route
```
ex
ip route 192.168.1.0 255.255.255.0 172.16.1.1
ip route 192.168.3.0 255.255.255.0 172.16.2.1
```

ADD IP ROUTER
IP GATEWAY FROM PC GROUP 3

```
en
conf t
int gig0/2
ip add 192.168.3.1 255.255.255.0
no sh
int gig0/0
ip add 172.16.3.1 255.255.255.252
no sh
int gig0/1
ip add 172.16.2.1 255.255.255.252
no sh
```
ip route
```
ex
ip route 192.168.1.0 255.255.255.0 172.16.3.2
ip route 192.168.2.0 255.255.255.0 172.16.2.2
```








