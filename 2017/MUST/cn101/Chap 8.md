## Chap 8

#### Routing process

**Enabled**: router will forward the packet to the appropriate port according to the routingtable.

**Disabled**: router will drop the message if it's not destined to one of the routerinterfaces.

> A routing table is created after the routing process is enabled on the router

Enabling the routing process on the router:

IPv4

```
Router(config)#ip routing
```

IPv6

```
Router(config)#ipv6 unicast-routing
```



#### Network types

**connected network**: A router for a connected network is added automatically when a router interface is configure with an IP address and subnet mask of this network. This interface becomes part of that network.

**remote network**: remote networks must be configured manually by the administrator or acquired dynamically via a routing protocol.

![networks](./src_img/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202017-05-13%20%E4%B8%8B%E5%8D%881.57.06.png)



#### Routing table

fields of routing table:

* Protocol type (C, E, S, R, I...)

* Destination network

* Routing metrics 

  > The lower the value of metrics is more desirable

* Next-hop address (the address of directly connected router)

* Outbound interface

> The route of directly connected network has **no next-hop address** because there's no intermediate layer 3 device between the router and that network.

Routers use routing protocols to build and maintain the routing tables.

Routers communicate with one another to maintain their routing table through the transimission of **routing update messages**



#### Static routing

**Stub network**: point-to-point connection, only single network connection and no need for routing updates

Static route configuration:

```
Router(config)#ip route ip-address subnet-mask 
						{next-hop-ip-address | outgoing interface}
						[administrative distance]
```

Administrative distance (from 0 to 255): the higher the administrative distance, the lower the trustworthiness rating.

**Default administrative distance**:

* Next-hop address: 1
* Outgoing interface: 0

> static routes always have a lower administrative distance



###### Verify static route configuration

```
Router#show ip route
Router#show running-config
```

###### Static default route:

```
Router(config)#ip route 0.0.0.0 0.0.0.0 
						{next-hop-ip-address | outgoing interface}
						[administrative distance]
```

###### Dynamic default route:

```
Router(config)#ip default-network network-address
```

![static default route configuration](./src_img/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202017-05-13%20%E4%B8%8B%E5%8D%882.44.20.png)

```
Branch(config)#ip route 0.0.0.0 0.0.0.0 172.16.1.1
Gateway(config)#ip route 0.0.0.0 0.0.0.0 s0/1
Central(config)#ip default-network 200.200.200.0
```



#### Dynamic routing

**Routing protocol**: a communication tool used between routers that allows one router to share routes information with other routers. Routers thus use this information to build and maintain their own routing tables.

* RIP
* OSPF
* EIGRP

**Routed protocol**: it provides enough information in its network layer address to allow a packet to be forwarded from one host to another based on the addressing scheme. (IP, etc)

Two basic functions:

1. Timely distribution of routing update messages
2. maintenance of a routing table



Determining the best route:

Same routing protocol, different routes: **metrics**

Different routing protocols or static/dynamic routing: **administrative distance** (for example a static route always has lower administrative distances than what is learned from dynamic routing)



##### Metrics

* Hop count
* Bandwidth 
* Delay
* Load
* Reliability
* Cost

##### Administrative distance

![dynamic routing:AD](./src_img/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202017-05-13%20%E4%B8%8B%E5%8D%882.58.30.png)



#### Routing algorithms

types:

* Distance vector: algs: **Bellman-Ford**, example: **RIP**

  > Periodic, entire routing table, directly connected neighboring routers, no exact topology

* Link-state: algs: **Dijkstras SJF**, example: **OSPF**

  > full topology

* Balanced-Hybrid: example: **EIGRP**



#### Routing protocol config

```
Router(config)#router routing-protocol {options}
Router(config-router)#network network-number [wildcard-mask]
```

`options` parameter varies with routing protocols. IGRP and EIGPR require an autonomous system number. OSPF requires a process ID. RIP does not require either.

the `netwok` command specifies a directly-connected network.