##Final review problem set
>   Mostly router and routing protocol related problems.
>   Source: [https://ccnav6.com/ccna-2-final-exam-answers-2017-routing-switching-essentials.html](https://ccnav6.com/ccna-2-final-exam-answers-2017-routing-switching-essentials.html)



4. _In what situation would a Layer 2 switch have an IP address configured?_

   * when the Layer 2 switch is using a routed port
   * **when the Layer 2 switch needs to be remotely managed**
   * when the Layer 2 switch is the default gateway of user traffic
   * when the Layer 2 switch needs to forward user traffic to another device

   ​

5. _Compared with dynamic routes, what are two advantages of using static routes on a router? (Choose two.)_

   * They ~~automatically switch~~ the path to the destination network when the topology changes
   * **They Improve network security**
   * They take less time to ~~converge~~ when the network topology changes
   * **They use fewer router resources**
   * They improve the efficiency of ~~discovering neighboring networks~~.

   ​

6. _A network administrator adds the default-information originate command to the configuration of a router that uses RIP as the routing protocol. What will result from adding this command?_

   * The router will only forward packets that originate on directly connected networks.
   * **The router will propagate a static default route in its RIP updates, if one is present**
   * The router will be reset to the default factory information
   * The router will not forward routing information that is learned from other routers

   ​



13. _What network prefix and prefix-length combination is used to create a default static route that will match any IPv6 destination?:_
    * /128
    * FFFF:/128
    * ::1/64
    * **::/0**

    ​



17. _Which statement is correct about Ethernet switch frame forwarding decisions?_

    * **Unicast frames are always forwarded regardless of the destination MAC address**
    * Frame forwarding decisions are based on MAC address and port mappings in the CAM table
    * Cut-through frame forwarding ensures that invalid frames are always dropped
    * Only frames with a broadcast destination address are forwarded out all active switch ports

    ​

18. _Which type of static route is configured with a **greater administrative distance** to provide a backup route to a route learned from a dynamic routing protocol_

    * **floating static route **
    * default static route
    * summary static route
    * standard static route

    ​



24. A network engineer is interested in obtaining specific information relevant to the operation of both distribution and access layer Cisco devices. Which command provides common information relevant to both types of devices?
    * show port-security
    * **show ip interface**
    * show ip protocols
    * show mac-address-tables
    * how cdp neighbors

    ​



63.  _Which statement describes a route that has been learned **dynamically**?_
    * **It is automatically updated and maintained by routing protocols.**
    * It is unaffected by changes in the topology of the network.
    * It has an administrative distance of 1.
    * It is identified by the prefix C in the routing table.

    ​



![img](https://ccnav6.com/wp-content/uploads/2016/02/i209416v1n1_209416.png)

64. _Refer to the exhibit. How did the router obtain the last route that is shown?_
    * The ip route command was used.
    * The ipv6 route command was used.
    * **Another router in the same organization provided the default route by using a dynamic routing protocol.\***
    * The ip address interface configuration mode command was used in addition to the network routing protocol configuration mode command.

    ​



65. _Which statement is correct about IPv6 routing?_
    * IPv6 routing is enabled ~~by default~~ on Cisco routers.
    * IPv6 only supports the ~~OSPF and EIGRP~~ routing protocols.
    * IPv6 routes appear in the ~~same routing table~~ as IPv4 routes.
    * **IPv6 uses the link-local address of neighbors as the next-hop address for dynamic routes.\***

    ​



66. _Refer to the exhibit. Which type of route is 172.16.0.0/16?_
    ![img](https://ccnav6.com/wp-content/uploads/2016/02/i211955v1n2_211955.png)

    - child route
    - ultimate route
    - default route
    - **level 1 parent route\***

    ​

67. _Which two factors are important when deciding which interior gateway routing protocol to use? (Choose two.)_

    - **scalability\***
    - ISP selection
    - **speed of convergence\***
    - the autonomous system that is used
    - campus backbone architecture

    ​

68. _Refer to the exhibit. Which type of IPv6 static route is configured in the exhibit?_
    ![d](https://ccnav6.com/wp-content/uploads/2017/02/2017-02-18_154301.jpg)

    - directly attached static route
    - **recursive static route\***
    - fully specified static route
    - floating static route

    ​

69. _A router has used the OSPF protocol to learn a route to the 172.16.32.0/19 network. Which command will implement a backup floating static route to this network?_

    - ip route 172.16.0.0 255.255.240.0 S0/0/0 200
    - **ip route 172.16.32.0 255.255.224.0 S0/0/0 200\***
    - ip route 172.16.0.0 255.255.224.0 S0/0/0 100
    - ip route 172.16.32.0 255.255.0.0 S0/0/0 100

    ​

70. Which summary IPv6 static route statement can be configured to summarize only the routes to networks 2001:db8:::cafe::/58 through 2001:db8:cafe:c0::/58?

    - ipv6 route 2001:db8:cafe::/62 S0/0/0
    - ipv6 route 2001:db8:cafe::/54 S0/0/0
    - **ipv6 route 2001:db8:cafe::/56 S0/0/0\***
    - ipv6 route 2001:db8:cafe::/60 S0/0/0



72. _Which statement is true about the difference between OSPFv2 and OSPFv3?_

    - OSPFv3 routers use a different metric than OSPFv2 routers use.
    - OSPFv3 routers use a 128 bit router ID instead of a 32 bit ID.
    - OSPFv3 routers do not need to elect a DR on multiaccess segments.
    - **OSPFv3 routers do not need to have matching subnets to form neighbor adjacencies.\***

    ​

73. _What happens immediately after two OSPF routers have exchanged hello packets and have formed a neighbor adjacency?_

    - They exchange DBD packets in order to advertise parameters such as hello and dead intervals.
    - They negotiate the election process if they are on a multiaccess network.
    - They request more information about their databases.
    - **They exchange abbreviated lists of their LSDBs.\***

    ​



75. _Which three pieces of information does a link-state routing protocol use initially as link-state information for locally connected links? (Choose three.)_

    - **the link router interface IP address and subnet mask\***
    - **the type of network link\***
    - the link next-hop IP address
    - the link bandwidth
    - **the cost of that link\***

    ​

76. _Which three requirements are necessary for two OSPFv2 routers to form an adjacency? (Choose three.)_

    - **The two routers must include the inter-router link network in an OSPFv2 network command.\***
    - The OSPFv2 process is enabled on the interface by entering the ospf ~~process~~ area-id command.
    - **The OSPF hello or dead timers on each router must match.\***
    - The OSPFv2 process ID must be the same on each router.\**
    - **The link interface subnet masks must match.\***
    - The link interface on each router must be configured with a link-local address.

    ​



93. _Which command will create a static route on R2 in order to reach PC B?_
    ![img](https://ccnav6.com/wp-content/uploads/2016/02/i246203v1n1_2107451.png)

    - R2(config)# ip route 172.16.2.1 255.255.255.0 172.16.3.1
    - R2(config)# ip route 172.16.2.0 255.255.255.0 172.16.2.254
    - **R2(config)# ip route 172.16.2.0 255.255.255.0 172.16.3.1\***
    - R2(config)# ip route 172.16.3.0 255.255.255.0 172.16.2.254

    ​

94. _Refer to the exhibit. How many broadcast and collision domains exist in the topology?_
    ![img](https://ccnav6.com/wp-content/uploads/2016/02/i214792v1n1_5.png)

    - 10 broadcast domains and 5 collision domains
    - **5 broadcast domains and 10 collision domains\***
    - 5 broadcast domains and 11 collision domains
    - 16 broadcast domains and 11 collision domains



101.

1. **Fill in the blank.** In IPv6, all routes are level **__1__\*** ultimate routes.
2. **Fill in the blank.**Static routes are configured by the use of the **__ip route__\*** global configuration command.
3. **Fill in the blank.** The OSPF Type 1 packet is the **__Hello__ \***packet.
4. **Fill in the blank.**The default administrative distance for a static route is **__1__\*** .





![img](https://ccnav6.com/wp-content/uploads/2017/02/15-final-ccna2.png)

153. _Refer to the exhibit. R1 was configured with the static route command ip route 209.165.200.224 255.255.255.226 S0/0/0 and consequently users on network 172.16.0.0/16 are unable to reach resources on the Internet. How should this static route be changed to allow user traffic from the LAN to reach the Internet?_
     * Add an administrative distance of 254.
     * **Change the destination network and mask to 0.0.0.0 0.0.0.0\***
     * Change the exit interface to S0/0/1.
     * Add the next-hop neighbor address of 209.165.200.226.




![img](https://ccnav6.com/wp-content/uploads/2017/02/57-final-ccna2.png)

163. _Refer to the exhibit.What summary static address would be configured on R1 to advertise to R3?_
     * 192.168.0.0/24
     * 192.168.0.0/23
     * **192.168.0.0/22\***
     * 192.168.0.0/21

     ​


171. _An OSPF router has three directly connected networks; 172.16.0.0/16, 172.16.1.0/16, and 172.16.2.0/16. Which OSPF network command would advertise **only the 172.16.1.0 network to neighbors**_
     * **router(config-router)# network 172.16.1.0 0.0.255.255 area 0\***
     * router(config-router)# network 172.16.0.0 0.0.15.255 area 0
     * router(config-router)# network 172.16.1.0 255.255.255.0 area 0
     * router(config-router)# network 172.16.1.0 0.0.0.0 area 0

     ​



179. _To enable RIP routing for a specific subnet, the configuration command network 192.168.5.64 was entered by the network administrator. What address, if any, appears in the running configuration file to identify this network?_  ????
     * 192.168.5.64
     * **192.168.5.0\***
     * 192.168.0.0
     * No address is displayed.

     ​

180. _Which two statements are true about half-duplex and full-duplex communications? (Choose two.)_
     * **Full duplex offers 100 percent potential use of the bandwidth.\***
     * Half duplex has only one channel.
     * All modern NICs support both half-duplex and full-duplex communication.
     * **Full duplex allows both ends to transmit and receive simultaneously.\*** Full duplex increases the effective bandwidth.

     ​



188. _What is the effect of issuing the passive-interface default command on a router that is configured for OSPF?_
     * Routers that share a link and use the same routing protocol
     * **It prevents OSPF messages from being sent out any OSPF-enabled interface.\***
     * All of above
     * Routers that share a link and use the same routing protocol

     ​

189. _A network administrator is implementing a distance vector routing protocol between neighbors on the network. In the context of distance vector protocols, what is a neighbor?_
     * routers that are reachable over a TCP session
     * **routers that share a link and use the same routing protocol\***
     * routers that reside in the same area
     * routers that exchange LSAs

     ​



full operating system –> flash
limited operating system –> ROM
routing table –> RAM
startup configuration file –> NVRAM



200. _Which three addresses could be used as the destination address for OSPFv3 messages? (Choose three.)_
     * **FF02::5\***
     * **FF02::6\***
     * FF02::A
     * 2001:db8:cafe::1
     * FF02::1:2
     * **FE80::1\***