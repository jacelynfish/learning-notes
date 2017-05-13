## Chap 9

#### Operation

Distance vecter routing protocols would: 

* Forward **entire** routing table
* **Periodically** or when the **topology network changes**
* **Directly connected** neighboring routers


###### routing table information:

* **distance**: total path cost
* **vector**: logical address of the first router on the path to each network contained in the table


##### Solution for routing loop

* Define maximum metic (usually hop count): when the hop count for a certian route in the routing table exceeds the maximum metric(usually 16), the packet is discarded by the router and the corresponding network is considered unreachable

* Split horizon: Routing updates sent to a particular neighbor router(B) by original router (A) should not contain information about routes that were learned from that neighbor B

  >  举例子：路由器A传给路由器B的路由表中，路由的via不能有B的，就是A不能把从B得知的路由又传给B

* Route poisoning: routing protocol will advertise infites-metric routes for a failed route, which makes it unreachable from the perspective of the router

* Triggered updates: when the router detects a topology change or a route fails, an update is sent immediately to ajacent routers rather than waiting on the update timer to expire

* Holddown timers

  ![holddown timer](./src_img/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202017-05-13%20%E4%B8%8B%E5%8D%884.34.07.png)

  suppose network 1 is down and the triggered updating message is sent to router B, which starts a holddown timer. While the holddown timer hasn't expired:

  1. new updating messages from **original router A** is sent indicating that network 1 is accessible again, B removes the holddown timer;

  2. new updating messages from **different router**(like C) with an **equal or even better** metric, the router B marks it as accessible and remove the timer;

  3. new updating messages from **different router**(like C) with a **poorer** metric, the update is **ignored**.

     > Ignoring an update with a poorer metric when a holddown timer is in effect allows more time for the knowledge of a disruptive change to propagate through the entire network.


#### Routing Information Protocol (RIP)

* Routing update message interval: 30 sec
* Metric: hop count
* holddown timer and split horizon (Noted: **no route poisoning!!!**)
* Its a **UDP** segment
* V2: classless routing protocol, multicasts routing updates using **224.0.0.9**


###### Default RIP timers:

* Update timer is 30 seconds.

* Invalid timer is 180 seconds.

  > It is used for routes that have not been heard from for the period of time that the invalid timer is set for. If the invalid timer expires, the route is considered invalid.

* Holddown timer is 180 seconds.

  > When a route goes down, the hold-down timer is started. While in hold down state, the router will keep sending updates about the route, and will keep forwarding packets via that route until the hold down expires.

* Flush timer is 240 seconds.

  > It restarts every time an update is received for a route from the router that it is learned from. The flush and invalid timers restart at the same time and run concurrently. When the flush timer expires for a route, the route is removed from the routing table. For RIP, the flush timer expires before the hold down timer can expire.


#### RIPv2 Configuration

```
Router(config)#router rip
Router(config-router)#version 2
Router(config-router)#network network-number
```

The *network-number* specified is the range of the network that you want to participate in the broadcast of the routing table information.

###### Verifying protocols:

```
Router#show ip protocol
```


#### IPv6 routing protocol: RIPng

* poison reverse and split horizon (Noted: **no holddown timer!!!**)
* Multicast routing updates through group: FF02::9
* UDP segments. Sent through port **521**

###### Configuration

Enable global ipv6 routing:

```
Router(config)#ipv6 unicast-routing
```

Enable IPv6 RIPng routing protocol:

```
Router(config)#ipv6 router rip name
```

> the *name* parameter is used later when configuring RIPng on participating interfaces

Inside the interface configurations:

```
Router(config-if)#ipv6 rip name enable
```

*Examples*:

![RIPng configuration](./src_img/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202017-05-13%20%E4%B8%8B%E5%8D%885.35.50.png)

```
Router1(config)#ipv6 unicast-routing 
Router1(config)#ipv6 router rip ripng 
Router1(config)#interface serial 0/0/0 
Router1(config-if)#ipv6 rip ripng enable 
Router1(config-if)#interface fastethernet 0/0 
Router1(config-if)# ipv6 rip ripng enable
```

